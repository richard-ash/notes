---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2021-04-12-contentful-faster-full-text-search.md
compiled_at: 2026-09-09
model: claude-fable-5-1
confidence: high
---

# Postgres Full-Text Search

Postgres full-text search (FTS) is the built-in `tsvector`/`tsquery` machinery, usually backed by a GIN index, that lets a relational database answer "which rows contain these words" without a separate search engine. It is the first rung of the search ladder in [[postgres-for-everything]], and the long-document counterpart to [[postgres-trigram-search]], which handles short strings like names and slugs.

This article is anchored on Farruco Sanjurjo's 2021 account of how Contentful cut the median latency of its FTS by 35%. The account matters less for the number than for the two failure modes it documents: a query planner that could not see the search terms, and a denormalized search table that got *slower* until the query shape was changed to match it. Both generalize well beyond Contentful.

## Building blocks

- **`tsvector`** is a sorted list of normalized lexemes (stemmed, lower-cased, stop-words removed) with positions. Store it as a column so it is computed once at write time, not on every query. Contentful keeps a `text_value_searchable tsvector` beside every `text_value`.
- **`tsquery`** is the search-side expression: lexemes joined by `&`, `|`, `!`, `<->`. Postgres builds it from user input with `to_tsquery`, `plainto_tsquery`, `phraseto_tsquery`, or (since PG11) `websearch_to_tsquery`.
- **`@@`** is the match operator; **GIN** is the index that makes it fast. A GIN index maps each lexeme to a posting list of rows, so the cost of a term scales with how many rows contain it.
- **Prefix match** appends `:*` to a lexeme (`house:*` matches houses, household, housework). This is how "left-anchored" search-as-you-type is done in FTS. On a GIN index it is a range scan over every key sharing the prefix, so a short prefix is expensive.
- **`ts_debug`** shows how the parser tokenizes a string and which lexemes survive the dictionary chain. Contentful uses it to drive input normalization.

The text-search *configuration* (which parser and dictionaries apply) is part of the answer, not the query: `to_tsvector('english', …)` and `to_tsvector(…)` under a different `default_text_search_config` produce different vectors. That detail returns below.

## Contentful's problem shape

Contentful stores content in entity-attribute-value style: an `entries` table plus an `entry_fields` table with one row per field per locale, text and non-text rows mixed together. Its search semantics are strict: return every entry where **all** terms appear, in **any** field, in **any** locale, with each term prefix-matched. That was expressed as one `EXISTS` subselect per term against `entry_fields`, each with its own `@@` condition.

The design is reasonable and it is also exactly the shape that exposes the two problems below.

## Lesson 1: prefix search needs your own input normalization

Sanjurjo's first point is that `plainto_tsquery` output cannot be blindly suffixed with `:*`. The parser splits `lo-master` into `lo` and `master`, `I'm` into `i` and `m`, `Q&A` into `q` and `a`. Suffixing those gives `lo:*` (matches local, low, long), `m:*`, and `a:*`, which is both semantically wrong and a performance disaster, because `a:*` touches the posting list of every lexeme starting with "a" and the database has to filter all of it.

Contentful's fix is a normalization step that inspects the `ts_debug` output and decides per lexeme whether a prefix wildcard is appropriate. `lo-master` becomes `lo-master:*` (the parser also emits the whole hyphenated token as one lexeme), while `Q&A` becomes `q & a` with no wildcard, so it only matches the single-letter lexemes exactly.

The transferable rule is that user input is a trust boundary for the planner as much as for security. Anything that can turn into a one- or two-character prefix wildcard needs to be caught before it reaches `@@`.

## Lesson 2: the planner has to be able to see the tsquery

The normalization logic was first written as an inline scalar subselect inside each `EXISTS`: `text_value_searchable @@ (SELECT … ts_debug … )`. It worked until a customer searched for a fifteen-word headline. The query took over ten seconds. The plan showed the planner had chosen to evaluate the subselect for the word **"and"** first, which matched roughly 840,000 rows that every later node then had to filter.

Sanjurjo's diagnosis: a scalar subselect is opaque at planning time. The planner does not know what tsquery it will produce, so it cannot consult the column's statistics to estimate how many rows each term will match. With fifteen equally unknown predicates it picks an order that is effectively arbitrary.

The fix moved normalization into a SQL function declared `IMMUTABLE PARALLEL SAFE`:

```sql
CREATE OR REPLACE FUNCTION cf_normalize_fts_input_string(text)
RETURNS tsquery AS $func$
  select /* normalize and return a tsquery */
$func$
LANGUAGE sql IMMUTABLE PARALLEL SAFE;
```

`IMMUTABLE` tells the planner it may evaluate the function once at plan time and substitute the resulting `tsquery` constant into the plan. Now the `@@` selectivity estimator sees a real query and can compare it against the most-common-lexeme statistics that `ANALYZE` collects for tsvector columns. The same fifteen-word search dropped to about 20 ms because the planner started with `biden:*`, roughly 1,500 rows, a 99% reduction in what the remaining nodes had to filter. `PARALLEL SAFE` is a separate flag that keeps the function from disqualifying the query from parallel plans.

The cost Sanjurjo names is planning time: every pre-evaluated function call is work done before execution starts, so a fifteen-term query plans slower than it used to. For a search endpoint that is a good trade; for a hot path with many short queries it might not be, and prepared statements do not help because the constant folding depends on the literal input.

Two points the article leaves implicit:

- **The `IMMUTABLE` label is only honest if the text-search configuration is pinned.** `to_tsquery(text)` is declared `STABLE` in Postgres precisely because its output depends on `default_text_search_config`; the two-argument `to_tsquery(regconfig, text)` form is `IMMUTABLE`. A normalization function that calls the one-argument form and is marked `IMMUTABLE` will constant-fold correctly until someone changes the session config, at which point cached plans and any expression index built on it silently disagree with fresh evaluations. Pass the config explicitly inside the function.
- **`STABLE` would probably have fixed the estimate, but not the plan.** The planner folds `STABLE` functions with constant arguments for estimation purposes only, so selectivity would likely have improved. `IMMUTABLE` goes further and inlines the constant into the index condition itself, which is what makes the plan visibly simpler in `EXPLAIN`.

This is the concrete form of the rule in [[postgres-fundamentals]]: the planner decides, and it can only decide well on inputs it can see. A scalar subselect, a `STABLE` function, or a parameter whose value arrives at execution time all hide information the statistics were collected to answer.

## Lesson 3: a narrower search table, but keep one predicate per term

The second change was structural. Contentful added an `entries_full_text_search` table with one row per (entry, locale) holding the concatenation of every text field's `tsvector`, GIN-indexed. The intent was to replace fifteen `EXISTS` subselects with one, matching a combined tsquery like `swiss:* & cows:*`.

It got slower in some cases. Sanjurjo's finding: for an AND-ed tsquery, Postgres performs one index scan per term and intersects the results, so the whole predicate runs as slowly as its **slowest** term. The frequent word that Lesson 2 had taught the planner to avoid was back, because inside a single `@@` there is nothing for the planner to reorder.

A likely mechanism the article does not spell out: GIN has had a "fast scan" optimization since Postgres 9.4 that can skip through a frequent term's posting list using a rare term's entries, but it does not apply to prefix (`:*`) keys, whose matches are collected into a bitmap and scanned in full. Contentful's every term is a prefix match, so the fused query got no benefit.

The resolution was to keep the new table but return to one `EXISTS` subselect per term against it. That hands ordering back to the planner, which by then had the statistics it needed. The narrower table then helped on its own terms: fewer rows per entry and no non-text rows mixed in means the index bitmap covers fewer heap pages, and the `Bitmap Heap Scan` that checks them does less I/O.

What the article omits is the write side. The concatenated row has to be rebuilt whenever any text field of an entry changes, so this is a denormalization with write amplification. It is the same trade [[postgres-fundamentals]] describes for derived aggregates: acceptable because the derived value is read far more than it changes, and safe because the rebuild happens in the same transaction as the field update, so the search table never lags the source. That in-transaction property is also the strongest argument in [[postgres-for-everything]] for keeping search inside the database rather than syncing to Elasticsearch.

## The general pattern

1. Precompute `tsvector` columns and index them with GIN. Never compute vectors per query.
2. Normalize user input yourself before it becomes a `tsquery`, and never let a short lexeme acquire a `:*`.
3. Make every value the planner must estimate a constant by plan time: `IMMUTABLE` functions with an explicit text-search configuration, no scalar subselects in index predicates.
4. Give the planner independent predicates it can reorder. One `EXISTS` per term costs more SQL and lets the cheapest term run first; one fused `&` query runs at the speed of the worst term.
5. Keep the searched table narrow. Rows that are not text should not share heap pages with rows that are.
6. Read `EXPLAIN (ANALYZE, BUFFERS)` for two things: which term the plan starts from, and how many rows that node returns. The 840,000-to-1,500 gap was the whole story.

## Temporal notes

Written against Postgres on AWS RDS in April 2021; nothing in the mechanics has changed through Postgres 18. What has changed is the next rung of the ladder: built-in FTS still has no BM25 ranking, and the extensions that add it, Timescale's `pg_textsearch` and ParadeDB's `pg_search`, did not exist or were not mature in 2021. For a team whose problem is relevance rather than latency, those are now the alternative to leaving Postgres. Contentful's current search architecture is not documented in this source and should not be inferred from it.

## Assessment

The narrative and the numbers (35% median improvement, 10 s to ~20 ms, ~840K versus ~1.5K rows) are Contentful's own and first-hand. The mechanism claims about `IMMUTABLE` versus `STABLE` folding, the configuration-pinning caveat, and the GIN fast-scan exclusion for prefix keys are this article's additions from the Postgres documentation and source; the fast-scan point in particular is a plausible explanation rather than something the source confirms. The article gives no p95/p99 figures, so the improvement's shape at the tail is unknown. For semantic rather than lexical search, see [[vector-databases]].

## Sources

- Sanjurjo, F. (2021). "Full-text search at Contentful got faster: How we did it." <https://www.contentful.com/blog/contentful-faster-full-text-search/> — [[2021-04-12-contentful-faster-full-text-search|local copy]]
