---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2024-11-11-what-i-wish-someone-told-me-about-postgres.md
compiled_at: 2026-09-09
model: claude-fable-5-1
confidence: high
---

# Postgres Fundamentals

Hazel Bachrach's "What I Wish Someone Told Me About Postgres" is a working web developer's shortlist: the handful of things about Postgres that the 3,200-page manual makes hard to find and that most engineers otherwise learn from an outage. This article keeps her structure, adds the mechanisms and mitigations she leaves implicit, and notes what has changed since Postgres 17. The lock-queue section is the one to remember.

## Schema: normalize by default

Normalize unless you have a measured reason not to. The test for redundancy is the update problem: if a user's email lives on every `documents` row, changing it means touching hundreds of rows and risking inconsistency. Foreign keys exist so each fact lives in one place.

Denormalization is a read-performance trade, and Bachrach's bakery example (precomputing hours worked per employee) shows the shape that justifies it: the value is derived, expensive to recompute per read, and read far more often than it changes. The cost is always one of two things: inconsistency if the derived value drifts, or write complexity if you keep it in sync. Denormalizing *inside* Postgres (a column, a materialized view, a trigger-maintained aggregate) keeps that sync transactional; denormalizing into a cache does not. That distinction is the same one that makes [[postgres-for-everything]] attractive.

The maintainers' own list, the "Don't Do This" wiki page, covers the rest. Three items Bachrach highlights: use `text` for all strings (`varchar(n)` buys nothing in Postgres but a constraint you will later have to relax), use `timestamptz` for all timestamps, and name tables and columns in snake_case (unquoted identifiers are case-folded, so camelCase becomes a permanent quoting tax). One correction: Bachrach writes "timestampz / time with time zone." The wiki recommends `timestamptz` (timestamp *with* time zone) and explicitly warns against `timetz`, because a time of day without a date cannot be adjusted for DST.

## NULL means "unknown", not "nothing"

SQL uses three-valued logic. `NULL = NULL` is `NULL`, and so is almost any comparison with a NULL operand. `WHERE` keeps only rows whose condition is `true`, so `WHERE title != 'manager'` silently drops every row where title is NULL. The operators that treat NULL as an ordinary value are `IS NULL`, `IS NOT NULL`, `IS [NOT] DISTINCT FROM`, and `COALESCE` (first non-NULL argument).

Two consequences Bachrach does not spell out:

- `x NOT IN (subquery)` returns **no rows at all** if the subquery yields even one NULL, because `x <> NULL` is unknown for every x. Use `NOT EXISTS`.
- `UNIQUE` constraints treat NULLs as distinct from each other, so a unique column can hold any number of NULLs. Postgres 15 added `UNIQUE NULLS NOT DISTINCT` for when that is not what you want.

## psql is configurable

Five minutes, once:

- `export PAGER='less -S'` so wide rows truncate instead of wrapping.
- `~/.psqlrc` containing `\x auto` (expanded display only when the table is too wide) and `\pset null '[NULL]'` (make NULLs visible; the default renders them as empty strings, which is exactly wrong given the section above).
- `\d table`, `\d+`, `\e` (edit the current query in `$EDITOR`), `\h KEYWORD` (syntax with a docs link), `\?` for the rest.
- `\copy (select ...) to 'file.csv' CSV HEADER` writes to the *client's* filesystem and needs no elevated rights, unlike server-side `COPY`.
- `GROUP BY 1 ORDER BY 2` positional shorthands are fine interactively and hostile in committed code.

## Indexes: the planner decides, and it needs the right index

Postgres will not use an index just because it exists. The planner estimates from per-table statistics whether the index beats a sequential scan, and on a 100-row development table it usually does not, which is why "it's fast locally" proves nothing. `EXPLAIN` shows the plan; `EXPLAIN (ANALYZE, BUFFERS)` shows what actually happened; explain.depesz.com and the pganalyze guide help read the output. There are no index hints; `SET enable_seqscan = off` exists for diagnosis only.

Three rules from the article, with the mechanism behind each:

**Multicolumn index order matters.** An index on `(a, b)` serves `WHERE a = 1 AND b = 2` and `WHERE a = 1` well, but serves `WHERE b = 5` poorly, because the B-tree is keyed on `a` first and `b` values are scattered across every `a` subtree. If you filter on `b` alone, you need an index that leads with `b`. Lead with the column that is filtered most often or most selectively. (See the temporal note on skip scan below.)

**Prefix matching needs `text_pattern_ops`.** `WHERE path LIKE '/1/2/3/%'` cannot use a default B-tree index unless the database collation is `C`. Under any locale-aware collation, sort order is not byte-by-byte, so the planner cannot turn a prefix into an index range. `CREATE INDEX ... (path text_pattern_ops)` builds an index that compares bytewise. This is the anchored-prefix case only; for unanchored substring or fuzzy matching see [[postgres-trigram-search]].

**Always `CREATE INDEX CONCURRENTLY` in production.** Plain `CREATE INDEX` takes a `SHARE` lock that blocks every write to the table for the duration of the build.

## Locks form a queue, and the queue is what breaks apps

Table-level lock modes, weakest to strongest: `ACCESS SHARE` (SELECT), `ROW SHARE` (SELECT FOR UPDATE), `ROW EXCLUSIVE` (INSERT/UPDATE/DELETE), `SHARE UPDATE EXCLUSIVE` (CREATE INDEX CONCURRENTLY, VACUUM), `SHARE` (CREATE INDEX), `ACCESS EXCLUSIVE` (most forms of ALTER TABLE). Readers and writers never block each other. `ACCESS EXCLUSIVE` conflicts with everything, including a plain SELECT.

The failure Bachrach walks through:

1. A slow SELECT, say a years-old dashboard query that has gradually grown from milliseconds to minutes, is running against `users` and holds `ACCESS SHARE`.
2. A migration runs `ALTER TABLE users ADD COLUMN ...`. The ALTER itself would take milliseconds, but it requests `ACCESS EXCLUSIVE` and must wait for the SELECT to finish.
3. **Every subsequent SELECT on `users` now queues behind the waiting ALTER.** Postgres grants locks in request order so that a strong-lock requester cannot be starved by an endless stream of weak ones. The consequence is that a *waiting* DDL statement is a barrier. The app's hot path stalls, requests time out, the site serves 503s, and the cause is a fast migration plus one slow read.

The thing to internalize is that the ALTER's own duration is irrelevant. What matters is how long whatever it waits on holds its lock, and the fact that the wait itself blocks everyone who arrives after.

Long-running transactions produce the same problem at row level. Locks are held until COMMIT, so `BEGIN; UPDATE ... WHERE id = 2;` followed by a coffee break holds a row lock that blocks any other writer to that row until the session returns. ORMs that open transactions early, and humans in `psql`, both produce these "idle in transaction" sessions.

Mitigations the article gestures at but does not list:

- **`SET lock_timeout = '2s'`** before DDL. The ALTER gives up instead of becoming a barrier; wrap it in a retry loop. This single setting turns the scenario above from an outage into a retried migration.
- **`idle_in_transaction_session_timeout`** ends the coffee-break session automatically. **`statement_timeout`** ends the runaway dashboard query.
- **Split expensive DDL into cheap steps.** Add the column without a default, backfill in batches, then set the default. `ADD CONSTRAINT ... NOT VALID` followed by `VALIDATE CONSTRAINT`, which needs only `SHARE UPDATE EXCLUSIVE`. `CREATE INDEX CONCURRENTLY` then `ADD CONSTRAINT ... UNIQUE USING INDEX`.
- **Find the blocker** with `pg_stat_activity` and `pg_blocking_pids()`.
- **Lint migrations** so the rules are enforced rather than remembered: strong_migrations (Rails), excellent_migrations (Ecto), squawk (any SQL), or a staging tool like pgroll.

Which DDL rewrites the table: adding a column with a *volatile* default (`now()`, `gen_random_uuid()`), changing a column's type, and adding a unique constraint directly. Since Postgres 11, a *constant* default is a catalog-only change.

The [[postgres-listen-notify]] article describes a different lock with the same lesson: throughput and latency are set by how long a lock is held and how many requests queue behind it, not by how fast the work inside it runs.

## JSONB is a sharp knife

JSONB gives Postgres document-store capability without a second system, which is the case made in [[postgres-for-everything]]. Bachrach's three cautions:

1. **No statistics inside the document.** The planner keeps no stats on keys within a JSONB value, so selectivity estimates for `data->>'brand' = ...` are default guesses and plans can be badly wrong (Heap's example is a 2000x slowdown). The fix for hot keys is an expression index on `(data->>'brand')`, which also makes ANALYZE gather stats for that expression, or a stored generated column (Postgres 12+) that promotes the key to a real, typed, indexable column.
2. **No schema.** Key naming, value types, and enum-versus-boolean conventions are enforced nowhere. Reserve JSONB for genuinely variable shapes, document the expected keys, and use check constraints with `jsonb_typeof` where a little enforcement is worth it.
3. **Type awkwardness.** `data['brand'] = 'JanSport'` errors because the right-hand side must itself be valid JSON; write `'"JanSport"'` (quotes inside the literal) or extract text with `data->>'brand'`. JSON `null` is a value, distinct from SQL NULL: `'null'::jsonb = 'null'::jsonb` is true.

Use `jsonb`, never `json`: the latter stores raw text and cannot be GIN-indexed.

## Temporal notes

Written against Postgres 17 (November 2024). Postgres 18 (September 2025) is now current, and one change bears directly on the indexing section: **B-tree skip scan** lets an index on `(a, b)` serve `WHERE b = 5` by iterating internally over each distinct value of `a`. It helps when `a` has few distinct values and does nothing when `a` is high-cardinality, so the ordering rule still stands, with a narrower blast radius. Postgres 18's asynchronous I/O also shifts sequential-scan costs, which changes some planner decisions at the margin. Nothing in the locking or JSONB sections has changed.

## Assessment

A tutorial from a working web developer aimed at juniors, not a specialist's treatise. Every claim checks against the official docs; the value is selection, not novelty. The lock-queue mechanism is the one piece most engineers learn from a production incident, and it is the reason to read this before running any migration against a hot table.

## Sources

- Bachrach, Hazel (2024). "What I Wish Someone Told Me About Postgres." <https://challahscript.com/what_i_wish_someone_told_me_about_postgres> — [[2024-11-11-what-i-wish-someone-told-me-about-postgres|local copy]]
- Referenced: PostgreSQL Wiki. "Don't Do This." <https://wiki.postgresql.org/wiki/Don%27t_Do_This>
- Referenced: Xata. "Postgres migrations and exclusive locks." <https://xata.io/blog/migrations-and-exclusive-locks>
- Referenced: Heap. "When To Avoid JSONB In A PostgreSQL Schema." <https://www.heap.io/blog/when-to-avoid-jsonb-in-a-postgresql-schema>
