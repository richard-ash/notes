# Computer Science > Databases

Database technologies, architectures, and paradigms — relational, vector, graph, and beyond.

## Articles
- [[amazon-dynamo]] — Amazon's 2007 always-writeable key-value store; consistent hashing, vector clocks, sloppy quorum, hinted handoff, plus implementation lessons from an Elixir port
- [[postgres-as-cache]] — Heinz's UNLOGGED-table cache (no WAL, truncated on crash, empty on replicas) with pg_cron expiry and upsert invalidation; the wiki's corrections (duplicate index, stale-read gap until the TTL moves into the read query, LRU last_read turning reads into writes) and the implication that a same-instance cache saves recomputation but cannot shield the primary
- [[postgres-for-everything]] — the "just use Postgres" default: FTS, JSONB, SKIP LOCKED queues, Timescale, pgvector, unlogged-table caches, ltree, Apache AGE; why fewer systems beats better systems, and when to leave
- [[postgres-full-text-search]] — Contentful's tsvector/GIN tuning: ts_debug-guided input normalization for prefix queries, an IMMUTABLE normalization function so the planner can see the tsquery and order per-term subselects by selectivity (10s → ~20ms), and a denormalized one-row-per-entry-per-locale search table
- [[postgres-fundamentals]] — Bachrach's practitioner shortlist: normalize by default, three-valued NULL, psql setup, planner-driven indexing (column order, text_pattern_ops), why a waiting ALTER TABLE queues every SELECT behind it and the lock_timeout fix, JSONB's missing statistics
- [[postgres-listen-notify]] — Postgres's built-in pub/sub; the global commit lock that serializes NOTIFY, and the buffer-batch-plus-fallback-poll pattern that takes it from ~2.9K to ~60K writes/sec
- [[postgres-trigram-search]] — efficient short-string search using pg_trgm with ILIKE and similarity on GIN indexes
- [[vector-databases]] — purpose-built databases for storing and searching high-dimensional embedding vectors
