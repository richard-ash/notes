---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2021-10-22-scaling-ecto-and-postgres.md
compiled_at: 2026-10-12
model: claude-fable-5-1
confidence: medium
---

# Postgres Scaling

How a Postgres-backed application grows past its first big table, told through Ecto. Tyler Hawkins's ElixirConf 2021 talk *Scaling Ecto and Postgres* comes out of Divvy, the Utah expense-management fintech he joined at launch, which went from roughly 50 to over 500 employees and from thousands of card transactions a month to thousands an hour in his three and a half years there. His running example is a `transactions` table (UUID primary key, amount in cents, merchant name, `card_id`, timestamps) that has grown to millions of rows, is skewed so that a few cards hold most of the transactions, and now takes up to 30 seconds to list a big customer's transactions where it once took under a second.

The talk is a ladder with four rungs. Each rung is cheap relative to the next and each is defeated by a specific failure to use its key:

| Rung | Fixes | Key you must always use | Fails when |
|---|---|---|---|
| Indexes | Read latency | The leading column(s) of a compound index | You index everything and writes slow down |
| Read replicas | Connection and read load | Routing reads to a replica Repo | You read your own write and get stale data |
| Table partitions | One disproportionately large table | The partition key in every `WHERE` | You omit it and the query becomes a union over every partition |
| Shards | A database that has outgrown one instance | The tenant boundary chosen up front | You query across shards, or picked the wrong boundary |

Hawkins's summary order: indexes first, replicas for request load, Ecto's own tools for query efficiency and consistency, partitions when one table has outgrown the rest, and shards only when nothing else is left. This article keeps that order, adds the Postgres and Ecto mechanics he gestures at from slides that the transcript does not show, and corrects two claims in the Q&A. It is the horizontal-scaling companion to [[postgres-fundamentals]] (indexes and locks on one instance) and the "when to leave" section of [[postgres-for-everything]].

## Why a big database is a problem even when disk is cheap

Hawkins names three constraints: storage, speed, and load. Cloud storage upgrades are a button press, so storage alone is rarely the limit. The real cost of row count is that everything that touches every row gets slower together: replication, backups, and above all restore. His test question is "if production crashes, is disaster recovery minutes, hours, or days?" That reframing matters because it is independent of query speed. A table can be well indexed and still make the database unrecoverable in an acceptable window. Partitioning and sharding both reduce the unit of recovery, which is a reason to reach for them that has nothing to do with latency.

## Rung 1: indexes that match the top queries

Ecto exposes Postgres's `CREATE INDEX CONCURRENTLY` as `create index(..., concurrently: true)`. Hawkins's case for it is the one in [[postgres-fundamentals]]: a plain index build takes a lock that blocks writes to the table for the whole build, and on a large table built in the middle of the day that is an outage. The costs he lists are correct: a concurrent build scans the table twice, takes longer, and competes for I/O with live queries. Two mechanics the talk omits:

- In an Ecto migration a concurrent index needs `@disable_ddl_transaction true` (Postgres refuses `CREATE INDEX CONCURRENTLY` inside a transaction) and, since Ecto SQL 3.x, `@disable_migration_lock true` so the migration does not hold the `schema_migrations` lock across a build that can take an hour. Omitting the first is a hard error; omitting the second serializes every other deploy behind the build.
- A concurrent build that fails leaves an `INVALID` index behind that is maintained on writes but never used for reads. `\d` shows it; drop it and retry.

The second half of the rung is restraint. Hawkins shows a migration that naively indexes all five columns of `transactions` and points out the trade: every insert now updates the row plus five B-trees, several of which (`updated_at` on an immutable transaction) will never be queried. At 20 or 30 indexed columns and millions of rows, he says, an update can take seconds to minutes. The fix is to list the actual top queries, which at Divvy are "by date range" and "by card", and build compound indexes that serve them: `(card_id, inserted_at)` rather than one index per column. Column order is load-bearing for the reason given in [[postgres-fundamentals]]: an index on `(card_id, amount)` is nearly useless for a query filtering on `amount` alone. Going from five indexes to two looks small; the point is the habit, because the write cost of indexes compounds with width.

For finding the top queries, Hawkins's Q&A answer is `EXPLAIN`, trial and error, and a query-level monitor (he names VividCortex, now SolarWinds DPM, and Datadog's database monitoring) that ranks queries by total time and call count. `pg_stat_statements` gives the same ranking for free. Ecto's telemetry events (`[:my_app, :repo, :query]`) carry query time and the query text, so the same ranking can be built in-app.

## Rung 2: read replicas

Load is a separate constraint from table size. Hawkins's framing: even if every query is fast, too many simultaneous connections mean queries wait for a pool slot, and a few slow queries hog the pool for everyone. Streaming replicas carry the primary's WAL and serve read-only copies with slight lag.

Ecto's support is the pattern from the official "Replicas and dynamic repositories" guide, which Hawkins's slide reproduces: define one Repo module per replica, and a `replica/0` function on the primary Repo that returns one of them (he uses `Enum.random/1`; round-robin works equally). Call sites change from `Repo.all(query)` to `Repo.replica().all(query)` wherever no write follows. Each Repo module has its own connection pool, which is the mechanism that spreads load: you are not just moving queries to another machine, you are giving them a separate pool so a slow replica query cannot block a primary write.

The hazard is reading your own write. Hawkins's second example updates a merchant name and immediately reads it back through the replica, and gets the old name if replication lag exceeds the round trip. His advice is simply not to do that; the general version in [[system-design]] is to route reads to replicas except where there is genuine zero tolerance for lag, and to fill in the just-written value from the write's return value rather than re-reading it. Two further consequences:

- `UNLOGGED` tables are empty on replicas because they write no WAL, so a cache built the way [[postgres-as-cache]] describes is invisible through `Repo.replica()`.
- Long reads on a replica can be cancelled by replication conflicts (`max_standby_streaming_delay`), which bears on the streaming-export pattern below. `hot_standby_feedback` prevents the cancellation at the cost of letting the replica's open snapshot hold back vacuum on the primary.

Hawkins connects replicas to the BEAM: Phoenix makes concurrency cheap, so an app can fan reads out across replicas without ceremony. The same property is why connection-pool exhaustion arrives early on the BEAM; a LiveView app with thousands of processes needs a conscious pool budget per Repo.

## Rung 3: Ecto's own tools

Three Ecto features, each matched to a resource constraint.

**Batching, against query count.** N+1 is the failure mode: load a few card IDs, make two queries per card, fine; load 100 cards with thousands of transactions each, and "one piece of information" costs thousands of round trips. More queries means more connection time and more load, regardless of how fast each one is, and good indexes make N+1 worse by hiding it until the N grows. The fix is one query for all cards (`where: c.id in ^ids`) and one for all transactions, or a single join. Ecto's `Repo.preload/2` already batches this way (one `IN` query per association), and `preload:` inside a query joins instead. The mechanism by which ORMs manufacture N+1 is described in [[sql-json-serialization]].

**`Ecto.Multi`, against partial writes.** Hawkins is explicit that Multi does not make queries faster; it buys consistency. A Multi composes steps the way the pipe operator composes functions, each step receiving the results of earlier steps, and `Repo.transaction/1` runs the whole thing in one database transaction. Any step returning an error tuple rolls back everything before it. His example: rename a merchant, then compute per-merchant statistics; if the statistics step fails, the rename should not survive. The return shape is `{:ok, %{step => result}}` or `{:error, failed_step, reason, changes_so_far}`, which makes the failure site addressable in a `case`. The same guarantee is why [[postgres-for-everything]] favours in-Postgres queues and caches: writes that share the business transaction never need an outbox.

**`Repo.stream/2`, against memory.** A stream pulls rows in chunks (`max_rows`, default 500) instead of materialising the result. Divvy uses it for CSV export: rather than building a 100,000-row CSV in memory, chunks flow through NimbleCSV (which, Hawkins notes, prefers streams) and out through a chunked HTTP response. The caveat the talk does not state is that `Repo.stream` must run inside `Repo.transaction/1`, because Postgres implements it with a server-side cursor that lives only as long as the transaction. That has two costs: the transaction holds a snapshot for the entire export, so vacuum cannot reclaim dead tuples from that point until it finishes (the mechanism behind the idle-in-transaction warning in [[postgres-fundamentals]]), and on a replica the long snapshot is exactly what triggers conflict cancellation. Run big exports on a replica with `hot_standby_feedback`, or page with keyset pagination instead of a cursor.

Hawkins lists three more in passing: window functions for aggregates, `dynamic/2` fragments for conditional `WHERE` clauses in search and filter UIs, and `Ecto.Enum` to store integers while the code reads atoms, which also gives product a stable sort order for statuses.

## Rung 4: table partitioning

When a single table approaches a billion rows while the rest of the database (the `cards` table, in the example) stays slim, declarative partitioning splits that one table. Hawkins's image is a router table: the parent `transactions` has no rows of its own and directs each query to child tables by the partition key. Each child is a real table with its own storage and indexes, queryable directly if you want.

**Ecto support.** Ecto migrations have no partition DSL, but a migration is Elixir code: `execute("CREATE TABLE ... PARTITION BY RANGE (card_id)")` and `execute("CREATE TABLE transactions_1 PARTITION OF transactions FOR VALUES FROM (0) TO (100)")`. (`create table(:transactions, options: "PARTITION BY RANGE (inserted_at)")` also works for the parent.) Queries need no change; `Repo.all(from t in Transaction, where: t.card_id == ^id)` hits the parent and Postgres prunes. Hawkins's slide partitions by `card_id` in blocks of 100 and then by `inserted_at` range within that.

**Choosing partitions.** His operational advice is to count: `GROUP BY card_id` to find the ten cards that hold most of the data (ad-spend cards charged continuously, in a fintech), give each its own partition, and leave the long tail in the default partition. The payoff is isolation: a customer on their own partition is the only one who feels their own slowness. The limit is overhead per partition; thousands are fine if each holds real data, one per card is not.

**Time partitioning** fits when the product promise is "last 30 days are fast, older is cold storage". The benefit Hawkins does not mention is retention: dropping a partition is instant and produces no dead tuples, where `DELETE WHERE inserted_at < ...` on a billion-row table is a vacuum event. The cost is that Postgres never creates the next period's partition for you; a cron, a trigger, or the `pg_partman` extension has to create them ahead of time.

**The partition key is the whole bet.** Hawkins's `EXPLAIN` on 100,000 rows across 11 partitions:

| Query | Estimated cost | Rows scanned |
|---|---|---|
| Without `card_id` in the `WHERE` | 1,232 | ~4,500 |
| With `card_id` | 251 | 989 |

Without the key the plan is a sequential scan of every child, `Append`-ed together, which he correctly calls worse than not partitioning at all. With the key, the planner prunes to one child. The gap widens with row count. This is why he says partitioning every table is a mistake: each partitioned table imposes its key on every query that touches it. His answer to the analytics question in Q&A is that cross-partition queries with other selective predicates (a specific amount, say) are tolerable, but genuine analytics across customers belongs in a warehouse such as Snowflake, not in the OLTP database.

**Two corrections to the Q&A.**

1. Hawkins says you cannot partition an existing table in any released Postgres. In-place conversion is still unsupported, but the standard migration path is not a trigger-and-copy: create the partitioned parent, add a `CHECK` constraint on the old table matching the bounds you intend (so the attach skips its validation scan), then `ALTER TABLE parent ATTACH PARTITION old_table FOR VALUES ...`. The old table becomes one partition without copying, and new partitions are added alongside it. Copying is only needed if you want the old data redistributed.
2. He says a row that lands in the default partition will migrate if you later create a partition covering it. It will not. `CREATE TABLE ... PARTITION OF` for a range that overlaps rows already in the default partition fails with a constraint violation, and attaching a partition when a default exists scans the default to prove no rows conflict. The rows must be moved out by hand (insert into the new partition, delete from the default, in one transaction) before the new partition can exist. This is why time partitions are created ahead of their period, which Hawkins does recommend.

One Ecto-specific consequence worth stating: a partitioned table's primary key and every unique constraint must include the partition key. The example's UUID primary key becomes `(id, card_id)` once the table is partitioned by `card_id`, which changes the Ecto schema's `@primary_key`, every `Repo.get/2` call, and any foreign key from another table that referenced `transactions.id` alone.

## Rung 5: sharding

When partitioning one table is not enough, and the problem is the whole database, sharding splits the database into independent instances with a "core" or router that knows where each tenant lives. Hawkins is blunt that this is where complexity jumps: nothing is automatic, and "having a poor boundary line will cause more headache than help, and you'll probably hate whoever put shards into your infrastructure."

**Four questions before sharding**, his list:

1. Where is the boundary? Not `card_id`, even though the big table carries it, but a user or organization ID: the entity you never query across. The partition-key rule returns at database scale.
2. What is the least the core database needs to know? The router is the one component that does not scale horizontally, so it should hold the minimum (tenant → shard), and need not even be Postgres; Redis or Nebulex is enough.
3. How often must data be queried across shards? If often, the boundary is wrong. Go back to question 1.
4. How often must data move between shards? Adding a shard under a hash scheme forces a migration; have a rehearsed process.

**Routing strategies**, with his trade-offs:

- **Lookup table in the core.** Most flexible; the core holds tenant → shard and can move a tenant.
- **ID-embedded shard.** A prefix like `s1` on the UUID. Works, but every consumer must know the ID format.
- **Hash.** Even distribution, but adding a shard changes the function and forces mass migration. [[amazon-dynamo]] solves this for key-value stores with consistent hashing and virtual nodes; Hawkins does not mention it, and Postgres sharding does not get it for free.
- **Range on serial IDs.** Simple, incompatible with UUIDs, and worst for isolation: a single customer's rows spread across every shard, so "we need our data isolated" cannot be answered and "where is all their data?" may not be answerable either.

The lookup table plus a tenant boundary gives the payoff Hawkins values most: a customer who needs isolation gets their own shard, and once the code supports two shards, adding a tenth is routine. His scaling answer in Q&A: millions of rows in a wide table is where slowness starts without indexes, billions needs real optimization, and once sharded "every shard is as good as your biggest database would have been before", so growth is a matter of spinning up shards until you have hundreds and the money to solve that differently.

**Ecto mechanics.** The naive version is one Repo module per shard and call sites that say `Shard2.all(query)`, which pushes shard knowledge into every function. The better one is `Repo.put_dynamic_repo/1`: a plug or middleware resolves the current user's shard once per request and sets it as the process's default Repo, after which every `Repo.*` call in that process hits the right shard with no changes at the call sites. Dynamic repos are designed for exactly this: one Repo module started several times under different names (`Repo.start_link(name: :shard_1, ...)`) with one set of schemas and migrations, and each instance configured separately (different credentials per shard, as he notes). The caveat he closes on is that the setting is per process. A `Task` or GenServer spawned from the request does not inherit it and silently queries the default Repo. This is the same trap as the process-dictionary actor in [[ecto-activity-tracking]], and the same discipline applies: pass the shard explicitly across every process boundary.

Partitioning and sharding compose. Hawkins's example: shard by organization, and a big organization's `transactions` table may still need partitioning within its shard.

**Managed alternatives.** Asked about Citus, Aurora, and similar, Hawkins's position is that they trade control for convenience: they keep accepting inserts and manage distribution for you, but when you need to decide that one customer gets an isolated shard, the hand-rolled approach is what gives you that. This is a reasonable 2021 answer; see the temporal notes.

## Assessment

A practitioner's ladder, delivered from the experience of a fintech whose transaction volume grew three orders of magnitude, and valuable for its ordering and its recurring rule: every scaling mechanism has a key, and the mechanism fails the moment a query omits it. The Postgres content is mostly correct and the two Q&A slips are on edge cases. What the talk under-weights is the schema and code cost of partitioning (composite primary keys, foreign keys, Ecto schema changes), which is the usual reason teams stop at replicas and indexes for longer than the ladder suggests. Hawkins's own closing line is the right frame: Postgres and Ecto "aren't the solution for everything, but they go pretty far", which is the thesis of [[postgres-for-everything]] with the exit stairs drawn in.

## Temporal notes

Delivered October 2021 against Postgres 14, which had shipped three weeks earlier. Since then:

- Postgres 14 added `ALTER TABLE ... DETACH PARTITION CONCURRENTLY`, so retiring a time partition no longer takes an exclusive lock on the parent. Partition pruning and the planner's handling of thousands of partitions have improved through 15 to 18; the "too many partitions" ceiling is higher than in 2021, though the per-partition overhead has not gone away.
- `pg_partman` is now the standard answer to "Postgres won't create the next partition" and is available on RDS, Cloud SQL, and most managed hosts.
- Citus, the sharding extension Hawkins was asked about, went fully open source in 2022 and now runs as Azure Cosmos DB for PostgreSQL; the "third-party tools give you less control" trade is less lopsided than it was, since Citus supports tenant isolation to a dedicated node.
- Ecto 3.13 (2025) added `Repo.transact/2`, which runs a function in a transaction and commits or rolls back on `{:ok, _}` / `{:error, _}`, covering the simpler Multi use cases with plain `with` chains. `Ecto.Multi` remains the tool when you need the per-step failure site.
- Divvy itself had been acquired by Bill.com for roughly $2.5 billion in mid-2021, a few months before the talk.

## Sources

- Hawkins, Tyler (2021). "Scaling Ecto and Postgres." ElixirConf 2021. <https://www.youtube.com/watch?v=SHjAMcBwY_o> — [[2021-10-22-scaling-ecto-and-postgres|local copy]]
- Referenced: Ecto documentation. "Replicas and dynamic repositories." <https://hexdocs.pm/ecto/replicas-and-dynamic-repositories.html>
- Referenced: PostgreSQL documentation. "Table Partitioning." <https://www.postgresql.org/docs/current/ddl-partitioning.html>
