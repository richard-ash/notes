# Computer Science > Databases

Database technologies, architectures, and paradigms — relational, vector, graph, and beyond.

## Articles
- [[amazon-dynamo]] — Amazon's 2007 always-writeable key-value store; consistent hashing, vector clocks, sloppy quorum, hinted handoff, plus implementation lessons from an Elixir port
- [[postgres-listen-notify]] — Postgres's built-in pub/sub; the global commit lock that serializes NOTIFY, and the buffer-batch-plus-fallback-poll pattern that takes it from ~2.9K to ~60K writes/sec
- [[postgres-trigram-search]] — efficient short-string search using pg_trgm with ILIKE and similarity on GIN indexes
- [[vector-databases]] — purpose-built databases for storing and searching high-dimensional embedding vectors
