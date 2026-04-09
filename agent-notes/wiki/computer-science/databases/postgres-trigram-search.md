---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2022-10-16-efficient-name-search-postgres-ecto.md
compiled_at: 2026-04-09
model: claude-opus-4-6
confidence: high
---

# Postgres Trigram Search (pg_trgm)

Postgres ships with `pg_trgm`, an extension for trigram-based text matching that enables efficient **short-string search** (names, titles, slugs) without full-text search infrastructure. It powers two complementary query strategies: exact substring matching with `ILIKE` and fuzzy matching with `similarity`.

This is distinct from Postgres full-text search (FTS via `tsvector`/`tsquery`), which is designed for longer documents and natural-language ranking.

## Core mechanism: trigrams

A trigram is a group of three consecutive characters extracted from a string. Postgres pads the beginning and end with spaces:

```sql
SELECT show_trgm('Bert');
-- {"  b"," be","ber","ert","rt "}
```

All comparisons are case-insensitive at the trigram level. The `similarity` score between two strings is the ratio of shared trigrams to total distinct trigrams:

```
similarity = shared / (count_a + count_b - shared)
```

For example, `similarity('Bert', 'Berry') = 3 / (5 + 6 - 3) = 0.375`.

## GIN index setup

Both ILIKE and similarity queries benefit from the same GIN trigram index:

```elixir
execute "CREATE EXTENSION IF NOT EXISTS pg_trgm;"

execute """
  CREATE INDEX persons_name_gin_trgm_idx
    ON persons
    USING gin (name gin_trgm_ops);
"""
```

**Ecto gotcha:** The standard `create index(:table, [:col], using: "GIN")` macro produces a `varchar_ops` index that does *not* accelerate trigram queries. You must specify `gin_trgm_ops` explicitly, either via raw SQL or:

```elixir
create index(:persons, [~s("name" gin_trgm_ops)], using: "GIN")
```

Always verify with `EXPLAIN ANALYZE` that the plan shows `Bitmap Heap Scan` (indexed) rather than `Seq Scan`.

## Strategy 1: ILIKE (exact substring)

Returns rows where the column contains the search term as a substring. Case-insensitive.

```elixir
defp search(term) do
  term = "%#{term}%"
  from(p in Person, where: ilike(p.name, ^term))
  |> Repo.all()
end
```

With a GIN trigram index on 18k rows, this runs ~30x faster than a sequential scan. `ILIKE` is deterministic: `"Ber"` matches `Bert` and `Berry` but not `Bart`.

## Strategy 2: similarity (fuzzy)

Returns rows whose trigram overlap exceeds a threshold (default 0.3). Use the `%` shorthand operator to hit the GIN index:

```elixir
def search_similar(name) do
  from(p in Person,
    where: fragment("? % ?", ^name, p.name),
    order_by: {:desc, fragment("? % ?", ^name, p.name)}
  ) |> Repo.all()
end
```

Key rules for index usage:
- **Use the `%` operator**, not the `similarity()` function — the function form bypasses the index.
- For `<%` (word_similarity) and `<<%` (strict_word_similarity), the **search term must come first**: `WHERE ^term <% col`.
- The `%` operator uses a global threshold (`pg_trgm.similarity_threshold`, default 0.3). Configure per-connection in Ecto via `after_connect`:

```elixir
config :my_app, MyApp.Repo,
  after_connect: {Postgrex, :query!, ["SET pg_trgm.similarity_threshold = 0.4", []]}
```

## Strategy 3: ILIKE + similarity (recommended for production)

Filter with ILIKE for deterministic matching, then rank by similarity for relevance ordering. Both operations use the GIN index:

```elixir
def search(term) do
  ilike_term = "%#{term}%"
  from(p in Person,
    where: ilike(p.name, ^ilike_term),
    order_by: {:desc, fragment("? % ?", ^term, p.name)}
  ) |> Repo.all()
end
```

This avoids the threshold sensitivity of pure similarity queries while surfacing the best matches first. The tradeoff: it won't return fuzzy non-substring matches (e.g., `Ana` won't find `Anna`).

## Word similarity variants

Standard `similarity` compares against the **entire** string, penalizing long names. Two alternatives handle word boundaries:

| Operator | Function | Behavior | Shorthand |
|---|---|---|---|
| similarity | `similarity(a, b)` | Whole-string trigram overlap | `%` |
| word_similarity | `word_similarity(a, b)` | Best-matching **substring** of b | `<%` |
| strict_word_similarity | `strict_word_similarity(a, b)` | Best-matching **whole word** of b | `<<%` |

For multi-word names, `word_similarity` is usually the better choice. Example: `word_similarity('Bert', 'Dagobert Duck') = 0.6` vs `strict_word_similarity('Bert', 'Dagobert Duck') = 0.28` — word_similarity finds the substring `bert` inside `Dagobert`, while strict_word_similarity compares against the full word `Dagobert`.

## When to use what

- **Autocomplete / typeahead:** ILIKE with `term%` prefix matching (fastest, most predictable).
- **Name search with ranking:** ILIKE + similarity combo.
- **"Did you mean?" fuzzy search:** similarity with `%` operator.
- **Multi-word name fields:** `word_similarity` (`<%`) to avoid length bias.
- **Full document search:** Use [[vector-databases]] or Postgres FTS (`tsvector`/`tsquery`) instead — pg_trgm is not designed for long text.

## Sources

- Ullrich, P. (2022). "Efficient Name Search with Postgres and Ecto." <https://peterullrich.com/efficient-name-search-with-postgres-and-ecto> — [[2022-10-16-efficient-name-search-postgres-ecto|local copy]]
