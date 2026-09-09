---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2023-10-02-postgres-as-a-cache.md
compiled_at: 2026-09-09
model: claude-fable-5-1
confidence: medium
---

# Postgres as a Cache

Using a Postgres table as the application cache instead of running Redis or Memcached. The recipe is one row of the [[postgres-for-everything]] replacement map, and Martin Heinz's 2023 article is the standard how-to for it: an `UNLOGGED` table keyed by text with a JSONB value and a timestamp, an expiry procedure scheduled by `pg_cron`, and optionally a `last_read` column for LRU eviction. Heinz's argument is the operational one — every extra service costs setup, monitoring, backups, and someone who understands it — and his claim is that Postgres meets each requirement a caching service is expected to meet. The claim holds for most of the checklist. Where it does not hold is the case where the cache exists to protect the database itself, and that is the case the article never separates out.

## The requirements checklist

Heinz lists what a cache must offer and maps each to a Postgres mechanism:

| Requirement | Mechanism | Notes |
|---|---|---|
| Key-value storage | A `key text` column with a unique constraint; `jsonb`, `text`, or `bytea` value | The `UNIQUE` constraint already builds a B-tree on `key`. Heinz's schema then adds a second explicit index on the same column, which is a pure duplicate that doubles write cost. Simpler still: make `key` the primary key and drop the `serial id`. |
| Fast writes | `CREATE UNLOGGED TABLE` — no write-ahead log | See below. |
| No persistence expected | Unlogged tables are truncated on crash recovery | Survives a clean restart, not an unclean one. |
| Expiration | A procedure that deletes rows older than a retention interval, called hourly by `pg_cron` | Correct as a garbage collector, insufficient as the correctness mechanism (below). |
| Eviction | Add `last_read`, update it on every read, purge least-recently-read rows | Heinz flags the cost and leaves the choice to the reader. The cost is larger than it looks (below). |
| Invalidation | "Overwrite data when it changes" | Listed but never shown. The Postgres idiom is `INSERT … ON CONFLICT (key) DO UPDATE SET value = EXCLUDED.value, inserted_at = now()`. |

## What `UNLOGGED` actually buys and costs

An unlogged table (available since 9.1) skips the write-ahead log, so inserts and updates avoid the WAL write and its fsync. That is where Heinz's "huge improvements in write performance" come from; the Crunchy Data article he defers to for numbers is the usual benchmark reference. Its indexes are unlogged too.

The trade-offs are exactly the ones a cache can tolerate, but they should be named precisely:

- **Truncated after any unclean shutdown**, not just a disk failure: an `immediate` shutdown, an OOM kill, or a container being stopped without a grace period all count. On the next start the table is empty. The application must treat every lookup as a possible miss, which it should anyway.
- **Empty on streaming replicas.** Replication carries the WAL, and there is none, so a standby cannot read the table. Heinz calls this "no distributed cache." More precisely: no *read-scaled* cache, and no cache survives a failover. A reader that hits the replica for everything else still has to go to the primary for cache lookups.
- **Convertible.** `ALTER TABLE cache SET LOGGED` (9.5+) turns it into an ordinary table at the cost of a full rewrite — relevant if a cache quietly becomes something the business depends on.

What `UNLOGGED` does not change is the read path. A hot cache table is served from `shared_buffers` like any other hot table, so reads are memory-speed once warm; the gap to Redis on reads is the client round-trip, protocol parsing, planning, and MVCC visibility checks, not disk.

## Corrections to the recipe

**The stale-read window.** Heinz purges expired rows on an hourly cron, which means a row past its TTL is still returned to readers for up to an hour. The fix costs nothing: put the TTL in the read query (`WHERE key = $1 AND inserted_at > now() - interval '1 hour'`) and let the cron job be a garbage collector rather than the thing that defines freshness. A per-row `expires_at` column is the natural generalisation — different keys get different lifetimes, which is how Redis's `EX` works — and the read predicate becomes `expires_at > now()`.

**The purge has no index to use.** The schema has no index on `inserted_at`, so every `DELETE … WHERE inserted_at < …` is a sequential scan. Fine while the cache is small; add a B-tree on the timestamp column once it is not.

**The trigger alternative is worse than Heinz admits.** He offers an `AFTER INSERT` trigger that runs the purge as a fallback for people who will not install `pg_cron`, and says he does not recommend it. The reason is worth spelling out: it runs that full-table delete on *every insert*, turning the cache's cheapest operation into its most expensive one, and under concurrent writers the deletes contend with each other. Since `pg_cron` is now an enable-it-yourself extension on essentially every managed host (RDS, Cloud SQL, Azure, Supabase, Neon), the fallback rarely needs to exist.

**LRU turns every read into a write.** Updating `last_read` on each hit means each cache read produces a dead tuple. Without WAL the cost is lower than on a logged table, and if `last_read` is unindexed and the page has room the update is HOT, but the dead tuples still accumulate and autovacuum still has to clear them. On a read-heavy cache — which is what caches are — this can generate more churn than the writes the cache was meant to absorb. Cheaper alternatives: rely on TTL to bound size (Heinz's own suggestion), or evict by `inserted_at` (FIFO), which needs no read-side write at all. High churn on cache and queue tables is also the exit condition [[postgres-for-everything]] identifies for leaving Postgres, so this is the knob to watch.

**Use `timestamptz`.** The schema uses bare `timestamp`, which stores wall-clock time with no zone. Nothing in the recipe breaks, but there is no reason to take the risk; [[postgres-fundamentals]] covers the general point.

**Invalidation can share the business transaction.** This is the win Heinz leaves implicit and the one the [[postgres-for-everything]] article makes the centrepiece: when the cache is a table, the upsert that refreshes or deletes a cache entry commits atomically with the write that made it stale. With Redis there is always a window between the database commit and the cache write, and it is the source of a whole class of "why did the user see old data for two seconds" bugs.

## What this cache is for — and what it cannot do

A cache table in the same Postgres instance **does not offload the database**. It saves recomputation: an expensive aggregate, a rendered fragment, a third-party API response, a rate-limit counter. If the bottleneck is the database's own CPU or I/O, caching into the same database moves load from one table to another and adds a lookup on top. Goedecke's rule in [[system-design]] — never cache something without first seriously trying to make it fast — applies with extra force here, because caching a slow query into the database it runs against is strictly worse than adding the index. Heinz's own list gets this backwards when it names "avoid slow database queries" as the main reason to cache; that is the one motivation his solution does not serve.

Putting the cache table in a *separate* Postgres instance restores the shielding property, but then there is a second service to run, which was the thing being avoided.

## Where it sits on the ladder

Three rungs, cheapest first:

1. **Process-local memory** — an in-process LRU, or ETS on the BEAM. Zero network, zero services, and correct whenever the cache does not need to be shared across nodes or survive a deploy.
2. **A Postgres table.** Shared across application nodes, survives deploys and clean restarts, transactional with the data it caches, and no new service. This is Heinz's rung, and it is the right default for a small team that already runs Postgres — the same reasoning as [[choose-boring-technology]].
3. **Redis / Memcached.** Sub-millisecond latency on a hot path, hundreds of thousands of operations per second, purpose-built structures (sorted sets, streams, pub/sub), tens of thousands of cheap client connections where Postgres has hundreds of expensive ones, and — the decisive one — a cache that lives *outside* the database it protects.

Move up a rung on measurement, not anticipation.

## Temporal notes

Heinz writes as though `pg_cron` requires an OS-level install and a custom Docker image. That was true for self-hosting in 2023 and still is, but the managed providers have since made it a one-statement enable, which removes the main reason anyone would reach for the trigger fallback. His suggestion of `hstore` as an alternative value type is legacy; JSONB has covered that ground since 9.4.

## Assessment

A single practitioner how-to with no benchmarks, from an author who says up front that benchmarks are out of scope. The mechanics are right and the operational argument is sound. The schema has a duplicate index, the expiry design serves stale rows for up to a purge interval, and the article does not distinguish "cache to save work" from "cache to protect the primary," which is the distinction that decides whether this technique replaces Redis or merely postpones it.

## Sources

- Heinz, Martin (2023). "You Don't Need a Dedicated Cache Service - PostgreSQL as a Cache." <https://martinheinz.dev/blog/105> — [[2023-10-02-postgres-as-a-cache|local copy]]
- Referenced: Crunchy Data. "PostgreSQL Unlogged Tables — Look Ma, No WAL!" <https://www.crunchydata.com/blog/postgresl-unlogged-tables>
- Referenced: PostgreSQL documentation, "Reliability and the Write-Ahead Log." <https://www.postgresql.org/docs/current/wal-intro.html>
