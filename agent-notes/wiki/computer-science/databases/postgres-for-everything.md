---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2024-02-14-postgresql-for-everything.md
compiled_at: 2026-09-09
model: claude-fable-5-1
confidence: medium
---

# Postgres for Everything

"Postgres for everything" (also "just use Postgres") is the position that a single PostgreSQL instance should be the default answer to most infrastructure needs — search, documents, queues, time series, caching, vectors, graphs — and that a dedicated system should be added only after Postgres demonstrably fails at the job. Raphael Bauer's essay is one of a genre (Stephan Schmidt's "Postgres for everything," Armin Ronacher's "SQL is Agile," DBOS's Postgres-as-substrate posts) and is useful less for any single technique than for the decision rule it advocates: **when a new requirement arrives, ask "can't Postgres do this?" before evaluating anything else.**

## Bauer's argument

Bauer, an interim CTO who has used Postgres since a 2003 bioinformatics project, locates its power in three properties:

1. **Rock-solid and old.** First release 1996; database bugs take decades of production exposure to shake out, and Postgres has had them. New features (JSONB, partitioning, CTEs) land without breaking old ones.
2. **Trivial to run anywhere.** Distro packages, Homebrew, Docker, Testcontainers for tests against a real database, and one-click managed offerings from every cloud. Broad support translates directly into less maintenance.
3. **It collapses the system count.** This is the real thesis. Every separate system is another thing to run, back up, monitor, secure, and — most costly — keep in sync with the primary data. A second search index, cache, or queue is a distributed-consistency problem you did not have before.

The third point is the one that survives scrutiny best, and it is an operational argument rather than a feature argument. Bauer's ColumbaDB anecdote is representative: MySQL plus Lucene/Solr would have worked, but two systems meant sync logic and two things to keep up; Postgres full-text search meant zero sync and one thing to keep up. "Simplicity" throughout the essay means *fewer moving parts*, not *less capable parts*.

## The replacement map

Bauer's catalogue, with the Postgres mechanism behind each claim and the practical caveats the essay leaves out:

| Would-be system | Postgres mechanism | Where the seams are |
|---|---|---|
| Elasticsearch / Solr | `tsvector`/`tsquery` with GIN indexes; `pg_textsearch` (BM25) or ParadeDB's `pg_search` (Tantivy-backed) when ranking or scale outgrows built-in FTS | Built-in ranking is weaker than BM25; the extensions are young relative to core Postgres and not universally available on managed hosts. For short-string matching see [[postgres-trigram-search]] instead. |
| MongoDB | JSONB columns with GIN indexes; Contentful, Instacart, and The Guardian are cited as production migrations | JSONB is, as Bachrach puts it, a sharp knife: schemaless columns forfeit constraints and make bad data easy. Use it for genuinely variable shapes, not as an excuse to skip modelling. |
| Kafka / RabbitMQ / SQS | A table plus `SELECT … FOR UPDATE SKIP LOCKED` for competing consumers; cursor-based reads for persistent-log semantics | Fine for job queues into the thousands of jobs per second; high churn needs vacuum attention. For low-latency wake-ups the companion primitive is [[postgres-listen-notify]], which has its own throughput ceiling. Kafka's real distinguishing features — partitioned ordered logs, replayable consumer groups, multi-team fan-out — are not what most teams reaching for Kafka need. |
| ClickHouse | TimescaleDB hypertables, compression, and continuous aggregates | Bauer runs an analytics product on it and vouches for it. ClickHouse still wins at columnar scan throughput on very wide, very large tables; Timescale gets you "nearly" there while keeping one system. |
| Dedicated vector DB | `pgvector` (HNSW/IVFFlat indexes), `pgvectorscale`, and `pgai` for in-database embedding calls | The live debate documented in [[vector-databases]]: extensions have largely closed the gap for workloads that fit on one machine and benefit from joining vectors against relational data. |
| Redis | `UNLOGGED` tables (no WAL, so much faster writes) plus a trigger or cron for expiry | Unlogged tables are truncated on crash and are not replicated to standbys, which is acceptable for a cache by definition. "As fast as Redis" is Bauer's claim, not a benchmark; Redis is in-memory and sub-millisecond, Postgres adds connection and MVCC overhead. Session stores on hot paths deserve a measurement. |
| Filesystem for small blobs | `bytea` columns holding Flatbuffers, deserialised client-side | A single client anecdote. Postgres's buffer cache and batched I/O beat many small file operations; it will not beat the filesystem for large objects. |
| Tree structures | `ltree` datatype with GiST indexes | Strictly better than recursive CTEs for hierarchical tags and paths — readable and fast. |
| Neo4j | Apache AGE, an ASF top-level project implementing openCypher inside Postgres, so graph queries and SQL combine in one statement | AGE lags Postgres major versions and is not offered by most managed providers. It answers "we have some graph queries," not "we are a graph company." |
| JSON-returning microservices | `json_agg`, `row_to_json`, `json_build_object` — the database emits the response shape directly | Lukas Eder's argument: mapping rows to objects in middleware is often pure overhead. Pushing it into SQL couples API shape to schema, which is a real cost when the API is public. |

Bauer's advice for every row is the same: **start with Postgres, migrate only on measured failure.** The queue and graph sections say it explicitly; the search section shows the full ladder — vanilla FTS, then an extension, then (implicitly) a dedicated system — and the point is that each rung keeps the data in one transactional place.

## Why it works: the innovation-token reading

The essay is an application of [[choose-boring-technology]]. McKinley's boring technology is technology whose failure modes are known, and Postgres is the canonical example. Adding Kafka spends an innovation token on a system whose failure modes your team will discover in production; adding a Postgres table spends nothing. Sean Goedecke's [[system-design]] essay makes the same move from the other direction: for scheduled jobs and large cached objects he recommends "using the idea without using the technology named after it," which in practice means a table with a `scheduled_at` column rather than Redis.

Two implications the essay leaves implicit:

**Transactions are the hidden win.** When the queue, the search index, and the cache are tables, enqueueing a job, updating the searchable document, and invalidating the cache can all happen in the same transaction as the business write. Every separate system reintroduces the outbox problem — the gap between "committed to the database" and "visible to the other system" — which is exactly the class of bug that is hard to reproduce and easy to ship.

**Extensions are not free innovation tokens.** Core Postgres is boring; ParadeDB, Apache AGE, and pg_textsearch are not. They are young, version-lagged, and sometimes unavailable on RDS or Cloud SQL. The honest version of the ladder is: vanilla Postgres is nearly free, a well-established extension (pg_trgm, TimescaleDB, pgvector) costs a fraction of a token, and a niche extension costs most of one — often still cheaper than a whole new system, but not zero, and the managed-hosting question should be asked before adopting.

## When to leave

Bauer does not enumerate the exit conditions, but the pattern across the map is consistent. Leave Postgres for a dedicated system when:

- The workload needs a **different storage engine**, not a different query: columnar scans over billions of rows, or a truly in-memory sub-millisecond store on a hot path.
- You need the **distributed semantics** the dedicated system was built for: Kafka's replayable partitioned log consumed by many independent teams, Elasticsearch's sharded cluster across a corpus that will not fit one node.
- Vacuum and bloat from **high-churn tables** (queues, caches) start competing with the primary workload — the usual signal that a queue has outgrown its host.

Until one of those is true, the operational cost of the extra system generally exceeds its capability benefit, which is the whole essay in one sentence.

## Temporal notes

The page carries a February 2024 publication date but has been revised since: the Hacker News thread it links, the BM25 extensions, the "Timescale / TigerData" naming (Timescale rebranded its company as TigerData in 2025), and the Apache AGE section all postdate the original. Treat it as a living document rather than a 2024 snapshot.

Two factual corrections. **pgvector is not a Timescale release.** It is Andrew Kane's open-source extension, dating from 2021; Timescale's own contributions are `pgvectorscale` (a faster index) and `pgai`. And **ElephantSQL is gone** — the managed provider Bauer lists announced its shutdown for January 2025.

## Assessment

A single opinionated practitioner essay, from someone who sells a Timescale-backed analytics product and has an interest in the "one system" story. The claims about capabilities are accurate; the claims about performance parity (Redis, the filesystem) are anecdotal and should be measured per workload. The essay's value is the default it sets, and the default is right for almost every team below hundreds of engineers: the marginal system is more expensive than it looks, and Postgres is more capable than it looks.

## Sources

- Bauer, Raphael A. (2024, revised 2026). "PostgreSQL for Everything." <https://www.raphaelbauer.com/posts/postgresql-everything/> — [[2024-02-14-postgresql-for-everything|local copy]]
- Referenced: Schmidt, Stephan. "Just Use Postgres for Everything." <https://www.amazingcto.com/postgres-for-everything/>
- Referenced: Crunchy Data. "Message Queuing Using Native PostgreSQL." <https://www.crunchydata.com/blog/message-queuing-using-native-postgresql>
- Referenced: The Guardian (2018). "Bye bye Mongo, Hello Postgres." <https://www.theguardian.com/info/2018/nov/30/bye-bye-mongo-hello-postgres>
