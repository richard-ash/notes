---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2021-04-12-contentful-faster-full-text-search.md
  - agent-notes/raw/computer-science/databases/2022-11-06-complete-guide-full-text-search-postgres-ecto.md
compiled_at: 2026-10-22
model: claude-fable-5-1
confidence: high
---

# Postgres Full-Text Search

Postgres full-text search (FTS) is the built-in `tsvector`/`tsquery` machinery, usually backed by a GIN index, that lets a relational database answer "which rows contain these words" without a separate search engine. It is the first rung of the search ladder in [[postgres-for-everything]], and the long-document counterpart to [[postgres-trigram-search]], which handles short strings like names and slugs. Ullrich's own framing in the second source is that `ILIKE` and trigram similarity scan the whole text of every row, which is fine for a name column and too slow for a book summary; FTS replaces the text with a normalized keyword list and compares those instead.

The article draws on two sources that sit at opposite ends of the same system. Peter Ullrich's 2022 guide is the baseline: how to set FTS up from an Ecto migration, rank and highlight results, and handle several languages, with a benchmark. Farruco Sanjurjo's 2021 account of Contentful is what happens in production once the baseline exists: a query planner that could not see the search terms, and a denormalized search table that got *slower* until the query shape was changed to match it. Read the first half to build it and the second half to find out why it is slow.

## Building blocks

- **`tsvector`** is a sorted list of normalized lexemes with positions. Ullrich's example: `to_tsvector('english', 'Coding with Elixir makes for cleaner code')` yields `'cleaner':6 'code':1,7 'elixir':3 'make':4`. Five things happened: stop words (`with`, `for`) were dropped, words were stemmed to a lexeme (`coding` → `code`, `makes` → `make`), words sharing a lexeme were merged, the list was sorted, and each lexeme kept the positions it occupied in the source. The positions are what proximity ranking later consumes. Store the vector as a column so it is computed once at write time, not on every query; Contentful keeps a `text_value_searchable tsvector` beside every `text_value`.
- **`tsquery`** is the search-side expression: lexemes joined by `&`, `|`, `!`, `<->` (followed by), with parentheses for grouping. Postgres builds it from user input with one of four functions, compared below.
- **`@@`** is the match operator; **GIN** is the index that makes it fast. A GIN index maps each lexeme to a posting list of rows, so the cost of a term scales with how many rows contain it. GIN stores lexemes only, not positions or weights, which matters for ranking below.
- **Prefix match** appends `:*` to a lexeme (`house:*` matches houses, household, housework). This is how "left-anchored" search-as-you-type is done in FTS. On a GIN index it is a range scan over every key sharing the prefix, so a short prefix is expensive.
- **`ts_debug`** shows how the parser tokenizes a string and which lexemes survive the dictionary chain. Contentful uses it to drive input normalization.
- **Text-search configuration** (which parser and dictionaries apply) is part of the answer, not the query. `to_tsvector('english', …)` and `to_tsvector(…)` under a different `default_text_search_config` produce different vectors. `SELECT cfgname FROM pg_ts_config` lists what the instance has; Ullrich notes the `simple` configuration is the fallback for text of unknown language, at the cost of no stemming and a much larger vector. That detail returns several times below.

### The four query builders

| Function | What it does with the input | Safe for raw user input? |
|---|---|---|
| `to_tsquery` | Parses operators literally (`&`, `\|`, `!`, `<->`, parentheses) | No: malformed input raises a syntax error |
| `plainto_tsquery` | Ignores operators, ANDs every word | Yes, but no phrases or negation |
| `phraseto_tsquery` | Ignores operators, joins every word with `<->` (exact phrase, in order) | Yes, but only phrase search |
| `websearch_to_tsquery` (PG11+) | Google-style syntax: quoted phrases, `OR`, `-word`, implicit AND | Yes; never raises |

Ullrich's example of the last: `websearch_to_tsquery('"efficient search" or postgres and -java')` equals `to_tsquery('(efficient <-> search) | (postgres & !java)')`. His recommendation, which this article endorses, is to use `websearch_to_tsquery` for anything typed by a user. The point the guide leaves implicit is the first row of the table: `to_tsquery` on user input is not merely unsafe semantically, it is a 500 error waiting for an unbalanced parenthesis.

## The baseline: a weighted generated column under a GIN index

Ullrich's single-language setup, as an Ecto migration:

```elixir
execute """
  ALTER TABLE books
    ADD COLUMN searchable tsvector
    GENERATED ALWAYS AS (
      setweight(to_tsvector('english', coalesce(title, '')), 'A') ||
      setweight(to_tsvector('english', coalesce(summary, '')), 'B')
    ) STORED;
"""

execute "CREATE INDEX books_searchable_idx ON books USING gin(searchable);"
```

Three decisions are packed in here.

- **A `STORED` generated column** (PG12+) keeps the vector current on every insert or update of `title` or `summary` without triggers or application code. Generated columns must be built from `IMMUTABLE` expressions, which is why the two-argument `to_tsvector('english', …)` form is used; the one-argument form is only `STABLE` because it reads `default_text_search_config`. So the generated column pins the configuration *by construction*, which is exactly the discipline Contentful's `IMMUTABLE` function needs (Lesson 2 below).
- **`coalesce(col, '')`** because `to_tsvector(NULL)` is `NULL`, and `NULL || tsvector` is `NULL`, so one empty summary would silently make the whole row unsearchable.
- **`setweight(…, 'A')`** labels every lexeme from the title with weight A and every lexeme from the summary with weight B. The labels do nothing at match time; they are multipliers at rank time, defaulting to A = 1.0, B = 0.4, C = 0.2, D = 0.1 and overridable per call. This is how "a hit in the title beats a hit in the body" is expressed.

The query:

```elixir
from(b in Book,
  where: fragment("searchable @@ websearch_to_tsquery(?)", ^term),
  order_by: {:desc, fragment("ts_rank_cd(searchable, websearch_to_tsquery(?), 4)", ^term)}
)
```

Two corrections this article makes to the baseline as printed:

- **Pin the configuration on the query side too.** `websearch_to_tsquery(?)` with one argument uses the session's `default_text_search_config`. The stored column was built with `'english'`. If the two ever differ (a managed host whose default is `simple`, a session that set a different config), the query's lexemes will not be stemmed the way the column's were, and matches will fail silently rather than error. Write `websearch_to_tsquery('english', ?)`, mirroring the column.
- **The stored column is not optional if you rank.** Ullrich says the column can be dropped and the `setweight(…) || setweight(…)` expression used directly in both the index and the query. That is true for matching: an expression index serves `@@` fine. But `ts_rank_cd` needs the full vector with positions and weights, GIN does not store either, and so ranking has to fetch the vector per candidate row. With a stored column that is a heap read; without one it is a `to_tsvector` call on the original text for every matching row, which is the per-query recomputation the column exists to avoid.

### Verifying the index is used

Prefix the query with `EXPLAIN ANALYZE` and look for `Bitmap Heap Scan` on top of a `Bitmap Index Scan` of the GIN index. On a development table with a few hundred rows the planner will prefer a sequential scan because it is genuinely cheaper there; `SET enable_seqscan = OFF` forces the index for the check. The same test and the same caveat appear in [[postgres-trigram-search]] and in the 100-row-dev-table warning of [[postgres-fundamentals]].

## Ranking

`ts_rank` scores on term frequency and weight. `ts_rank_cd` (cover density) also scores on proximity: how close together the query's terms sit in the document, which is why it needs positions and cannot rank a vector produced by `strip()`. Ullrich's summary is that a document which mentions the terms often, close together, and in a heavily weighted section ranks highest.

The third argument is a normalization bitmask that discounts for document length, because a long book matches any term more often than a short essay by chance alone. The options are additive: 1 divides by 1 + log(length), 2 divides by length, 4 divides by the mean harmonic distance between matching extents (meaningful only for `ts_rank_cd`), 8 divides by the number of unique words, 16 by 1 + log(unique words), 32 maps the rank into 0..1 as rank/(rank + 1). Ullrich uses 4, which favours an essay with a few close matches over a long book with many scattered ones, and advises tuning both the bitmask and the weights against real data rather than trusting any default.

Ranking is the expensive half of a search query. Matching touches only the index; ranking must read the tsvector of every row the index returned, so a term that matches a hundred thousand rows costs a hundred thousand rank computations regardless of how many results are shown. Ullrich's mitigation is a `LIMIT`, and it is a partial one: `ORDER BY rank LIMIT 10` still ranks every match, since the sort needs every score to find the top ten, though the top-N heap sort is cheaper than a full sort and uses bounded memory. The real lever is to make the match selective first, which is the whole subject of Contentful's Lessons 1 and 2.

### Highlighting with `ts_headline`

`ts_headline(config, text, tsquery, options)` returns a fragment of the original text with matches wrapped in `<b>` tags by default, or whatever `StartSel`/`StopSel` specify; `MinWords`/`MaxWords` bound the fragment length. Ullrich's Ecto version selects it with a `fragment` and a `CONCAT(title, ' ', summary)` document. One addition from the Postgres documentation: `ts_headline` runs on the *original text*, not the vector, so it is slow per row and must not be computed for every match. Put the match-and-rank query in a subselect with its `LIMIT`, and call `ts_headline` in the outer query on the ten rows that survive. As printed in the guide it headlines every matching book.

## Multi-language search

The baseline hard-codes `'english'`. Ullrich works through three ways to search text in several languages, and they differ on three axes: whether the language of each row must be known, whether adding a language needs a migration, and how much is stored.

### 1. Concatenate a vector per language

Generate one `STORED` column holding `to_tsvector('english', doc) || to_tsvector('spanish', doc) || to_tsvector('italian', doc)` and query it with one `@@` per language, OR-ed. This is the only strategy that works when neither the text's language nor the query's language is known. The costs are storage (every row carries every language's vector, though only one is meaningful), false positives across languages (Ullrich's example is `Zeitgeist` matching German rows when English ones were wanted), and a migration that rewrites the column and rebuilds the index, with the table locked, whenever a language is added. A side effect worth knowing: tsvector `||` offsets the right-hand positions past the left-hand ones, so each real occurrence appears three times at three distant positions. Frequency-based rank is inflated uniformly and ordering survives; proximity rank across the copies is noise.

### 2. One partial index per language

Add a `language` column and build, per supported language, a GIN expression index on `to_tsvector('<lang>', doc)` restricted by `WHERE language = '<lang>'`. There is no stored column, the indexes together are no bigger than one index over everything, and an empty partial index costs almost nothing, so one can be created up front for every configuration the instance supports. The row's language must be known; the query's need not be, since one can try the most common languages in turn.

### 3. One expression index with a dynamic configuration

Wrap the cast in an `IMMUTABLE` SQL function, `lang_to_regconfig(text) RETURNS regconfig`, and build a single GIN index on `to_tsvector(lang_to_regconfig(language), doc)`. The wrapper exists because index expressions must be immutable and the bare `language::regconfig` cast is not (name resolution depends on the search path), which is the same honesty question raised about Contentful's function in Lesson 2: the function is only truly immutable while the configuration names it resolves stay fixed. Querying must use the identical expression, `to_tsvector(lang_to_regconfig(language), …) @@ …`; Ullrich states the rule plainly and the next section is a demonstration of what breaks when it is not followed. No stored column, no migration to add a language, and no need to filter by language in the query.

### The Ecto `regconfig` cast

Postgrex cannot encode a parameter as `regconfig` (the guide cites Postgrex issue 502, open as of late 2022), so `websearch_to_tsquery(?, ?)` with a language parameter errors. The workaround is to bind it as text and let Postgres cast: `websearch_to_tsquery(?::text::regconfig, ?)`.

### The benchmark, and what the printed plan actually shows

Ullrich benchmarked the three strategies with Benchee on roughly 23,000 Gutenberg abstracts in four languages, searching German for one short sentence that matched one row:

| Strategy | Average | Relative |
|---|---|---|
| Concatenated vectors | 4.12 ms | 1× |
| Single dynamic-config index | 4.30 ms | 1.04× slower |
| Partial indexes | 366.62 ms | 88.93× slower |

His reading is that the first two are interchangeable, the "dumb" concatenation narrowly wins, and the partial-index strategy is an outlier because "Postgres spins up a worker to conduct the partial index search."

This article reads the plan differently. The `EXPLAIN ANALYZE` output Ullrich prints is a `Gather` over a `Parallel Seq Scan on books` with the `@@` condition in its `Filter` and 11,218 rows removed by that filter. That is a table scan; no index was used. The cause is visible in the same filter line: the query's expression is `to_tsvector((language)::regconfig, …)`, while the partial indexes were built on `to_tsvector('german', …)` with a literal configuration. Postgres matches an expression index only when the query's expression is structurally identical to the indexed one, and these are not, so the planner had no usable index and fell back to a parallel scan. The worker is a consequence of the sequential scan, not the source of the slowness. Strategy 2 as benchmarked therefore measures the cost of a mismatched query, not of partial indexes, and the "16.52 versus 3212.54" planner cost comparison in the guide is the same mismatch seen from the estimate side.

The fix is the rule Ullrich himself gives for strategy 3. Either query with the same literal the index was built with (interpolate a whitelisted configuration name into the SQL rather than binding a parameter, since a bound `$1::regconfig` folds to a constant only in a custom plan), or build the partial indexes on `lang_to_regconfig(language)` too and keep the `WHERE language = …` predicate so each stays small. Done that way, strategy 2 should be at least as fast as strategy 3 on the same query, because each partial index is a fraction of the single index's size; it has not been re-measured here, so treat that as the expected outcome rather than a result.

## Contentful's problem shape

Contentful stores content in entity-attribute-value style: an `entries` table plus an `entry_fields` table with one row per field per locale, text and non-text rows mixed together. Its search semantics are strict: return every entry where **all** terms appear, in **any** field, in **any** locale, with each term prefix-matched. That was expressed as one `EXISTS` subselect per term against `entry_fields`, each with its own `@@` condition.

The design is reasonable and it is also exactly the shape that exposes the three problems below.

## Lesson 1: prefix search needs your own input normalization

Sanjurjo's first point is that `plainto_tsquery` output cannot be blindly suffixed with `:*`. The parser splits `lo-master` into `lo` and `master`, `I'm` into `i` and `m`, `Q&A` into `q` and `a`. Suffixing those gives `lo:*` (matches local, low, long), `m:*`, and `a:*`, which is both semantically wrong and a performance disaster, because `a:*` touches the posting list of every lexeme starting with "a" and the database has to filter all of it.

Contentful's fix is a normalization step that inspects the `ts_debug` output and decides per lexeme whether a prefix wildcard is appropriate. `lo-master` becomes `lo-master:*` (the parser also emits the whole hyphenated token as one lexeme), while `Q&A` becomes `q & a` with no wildcard, so it only matches the single-letter lexemes exactly.

The transferable rule is that user input is a trust boundary for the planner as much as for security. Anything that can turn into a one- or two-character prefix wildcard needs to be caught before it reaches `@@`. `websearch_to_tsquery` handles the syntax side of that boundary (no parse errors, no operator injection); it does nothing about the selectivity side, which is why Contentful needed its own layer on top.

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

- **The `IMMUTABLE` label is only honest if the text-search configuration is pinned.** `to_tsquery(text)` is declared `STABLE` in Postgres precisely because its output depends on `default_text_search_config`; the two-argument `to_tsquery(regconfig, text)` form is `IMMUTABLE`. A normalization function that calls the one-argument form and is marked `IMMUTABLE` will constant-fold correctly until someone changes the session config, at which point cached plans and any expression index built on it silently disagree with fresh evaluations. Pass the config explicitly inside the function. Ullrich's `STORED` generated column and his `lang_to_regconfig` wrapper are two more places the same discipline applies, one enforced by Postgres and one on trust.
- **`STABLE` would probably have fixed the estimate, but not the plan.** The planner folds `STABLE` functions with constant arguments for estimation purposes only, so selectivity would likely have improved. `IMMUTABLE` goes further and inlines the constant into the index condition itself, which is what makes the plan visibly simpler in `EXPLAIN`.

This is the concrete form of the rule in [[postgres-fundamentals]]: the planner decides, and it can only decide well on inputs it can see. A scalar subselect, a `STABLE` function, or a parameter whose value arrives at execution time all hide information the statistics were collected to answer.

## Lesson 3: a narrower search table, but keep one predicate per term

The second change was structural. Contentful added an `entries_full_text_search` table with one row per (entry, locale) holding the concatenation of every text field's `tsvector`, GIN-indexed. The intent was to replace fifteen `EXISTS` subselects with one, matching a combined tsquery like `swiss:* & cows:*`.

It got slower in some cases. Sanjurjo's finding: for an AND-ed tsquery, Postgres performs one index scan per term and intersects the results, so the whole predicate runs as slowly as its **slowest** term. The frequent word that Lesson 2 had taught the planner to avoid was back, because inside a single `@@` there is nothing for the planner to reorder.

A likely mechanism the article does not spell out: GIN has had a "fast scan" optimization since Postgres 9.4 that can skip through a frequent term's posting list using a rare term's entries, but it does not apply to prefix (`:*`) keys, whose matches are collected into a bitmap and scanned in full. Contentful's every term is a prefix match, so the fused query got no benefit.

The resolution was to keep the new table but return to one `EXISTS` subselect per term against it. That hands ordering back to the planner, which by then had the statistics it needed. The narrower table then helped on its own terms: fewer rows per entry and no non-text rows mixed in means the index bitmap covers fewer heap pages, and the `Bitmap Heap Scan` that checks them does less I/O.

What the article omits is the write side. The concatenated row has to be rebuilt whenever any text field of an entry changes, so this is a denormalization with write amplification. It is the same trade [[postgres-fundamentals]] describes for derived aggregates: acceptable because the derived value is read far more than it changes, and safe because the rebuild happens in the same transaction as the field update, so the search table never lags the source. That in-transaction property is also the strongest argument in [[postgres-for-everything]] for keeping search inside the database rather than syncing to Elasticsearch. Ullrich's `STORED` generated column is the one-table version of the same guarantee, with Postgres doing the rebuild.

## The general pattern

1. Precompute `tsvector` columns and index them with GIN. A `STORED` generated column is the cheapest way to keep them current; never compute vectors per query, and keep the column if you rank, because GIN holds no positions or weights.
2. Pin the text-search configuration everywhere a vector or query is built: in the generated column, in the query's `websearch_to_tsquery`, and inside any function marked `IMMUTABLE`.
3. Build queries from user input with `websearch_to_tsquery`, never `to_tsquery`. Then normalize further yourself if you use prefix matching, and never let a short lexeme acquire a `:*`.
4. Make every value the planner must estimate a constant by plan time: `IMMUTABLE` functions with an explicit configuration, no scalar subselects in index predicates.
5. Give the planner independent predicates it can reorder. One `EXISTS` per term costs more SQL and lets the cheapest term run first; one fused `&` query runs at the speed of the worst term.
6. Keep the searched table narrow. Rows that are not text should not share heap pages with rows that are.
7. Query with the exact expression the index was built on. An expression index that the query spells differently is a sequential scan with extra steps.
8. Rank and headline on as few rows as possible: selective match first, `ts_rank_cd` over the survivors, `ts_headline` only on the page being returned.
9. Read `EXPLAIN (ANALYZE, BUFFERS)` for three things: whether the top node is a `Bitmap Heap Scan` at all, which term the plan starts from, and how many rows that node returns. The 840,000-to-1,500 gap was the whole Contentful story; the `Parallel Seq Scan` was the whole benchmark story.

## Temporal notes

Sanjurjo wrote against Postgres on AWS RDS in April 2021 and Ullrich against Postgres 15 in November 2022. Nothing in the mechanics has changed through Postgres 18: `websearch_to_tsquery` (PG11) and `STORED` generated columns (PG12) were already available to both. The Postgrex `regconfig` limitation is reported as of the guide's date; check the issue before relying on the `::text::regconfig` workaround being still necessary. What has changed is the next rung of the ladder: built-in FTS still has no BM25 ranking, and the extensions that add it, Timescale's `pg_textsearch` and ParadeDB's `pg_search`, did not exist or were not mature when either source was written. For a team whose problem is relevance rather than latency, those are now the alternative to leaving Postgres. Contentful's current search architecture is not documented in this source and should not be inferred from it.

## Assessment

The Contentful narrative and numbers (35% median improvement, 10 s to ~20 ms, ~840K versus ~1.5K rows) are first-hand. Ullrich's setup code is standard and matches the Postgres documentation; his benchmark numbers are his own, on a small single-machine dataset with one query, and the partial-index figure should be discarded for the reason given above rather than taken as a property of the strategy. The mechanism claims about `IMMUTABLE` versus `STABLE` folding, the configuration-pinning caveat, the GIN fast-scan exclusion for prefix keys, the ranking-needs-the-stored-column point, the `LIMIT` qualification, and the re-reading of the benchmark plan are this article's additions from the Postgres documentation and the plan text itself; the fast-scan point in particular is a plausible explanation rather than something the source confirms. Neither source gives tail-latency figures. For semantic rather than lexical search, see [[vector-databases]]; for the indexing and Ecto mechanics around this, [[postgres-scaling]].

## Sources

- Sanjurjo, F. (2021). "Full-text search at Contentful got faster: How we did it." <https://www.contentful.com/blog/contentful-faster-full-text-search/> — [[2021-04-12-contentful-faster-full-text-search|local copy]]
- Ullrich, P. (2022). "The Complete Guide to Full-text Search with Postgres and Ecto." <https://peterullrich.com/complete-guide-to-full-text-search-with-postgres-and-ecto> — [[2022-11-06-complete-guide-full-text-search-postgres-ecto|local copy]]
