---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2026-10-22-soft-deletes-with-ecto.md
compiled_at: 2026-10-22
model: claude-fable-5-1
confidence: high
---

# Soft Deletes

A soft delete marks a row as deleted instead of removing it, so the data survives for undo, audit, or reporting while the application stops showing it. The question is *where* that rule is enforced. José Valim's Dashbit post (August 2024, adapting Evil Martians' ["Soft deletion with PostgreSQL: but with logic on the database!"](https://evilmartians.com/chronicles/soft-deletion-with-postgresql-but-with-logic-on-the-database)) answers: in Postgres, with a rewrite rule and a view, so that Ecto code barely changes and nothing connected to the database can remove the row by accident.

## Application level vs database level

Valim's split:

- **Application level** — a `deleted_at` column, a context function that sets it, and a filter on every query. Fine for one or two resources. Its failure modes are structural: anyone can still call `Repo.delete` or `delete_all`, an `ON DELETE CASCADE` foreign key removes rows the application never touched, and every query has to remember the filter.
- **Database level** — warranted when soft deletion applies to several resources and matters (compliance, undo, audit). The guarantee holds for psql sessions, migrations, scripts, and cascades alike, because the database itself refuses to delete.

This is the same instinct as [[postgres-for-everything]]: put the invariant where every client has to pass through it. The vault's [[ecto-activity-tracking]] shows the Elixir-side alternative (overriding `Repo.delete` with `defoverridable`), which carries exactly the gaps Valim lists.

## The rule: rewrite DELETE into UPDATE

Add the column, then a [PostgreSQL rule](https://www.postgresql.org/docs/current/rules.html) in the same migration:

```elixir
add :deleted_at, :utc_datetime

execute """
        CREATE OR REPLACE RULE soft_deletion AS ON DELETE TO orders
        DO INSTEAD UPDATE orders SET deleted_at = NOW() WHERE id = OLD.id AND deleted_at IS NULL RETURNING OLD.*;
        """,
        "DROP RULE IF EXISTS soft_deletion ON orders;"
```

Rules are **query rewriting**, not triggers: the rewriter replaces the `DELETE` with the `UPDATE` before anything executes. That has consequences the post leaves implicit:

- It fires once per statement, not per row. `DELETE FROM orders WHERE total < 10` becomes a single `UPDATE` over the same matched rows, so bulk soft deletes stay one statement.
- No `DELETE` ever reaches the executor, so foreign-key actions (`ON DELETE CASCADE`, `SET NULL`) never fire. Children of a soft-deleted parent stay visible until you soft-delete them too. Evil Martians' original covers cascading the soft delete (rules on child tables, or a parent rule that also updates children); Valim points there rather than repeating it.
- `AND deleted_at IS NULL` makes repeat deletes no-ops, so `deleted_at` records the *first* deletion. `NOW()` is transaction start time.
- `RETURNING OLD.*` keeps `DELETE … RETURNING` working, which Ecto needs for any `:read_after_writes` field.

## The view: hide deleted rows by default

The rule stops deletion but `Repo.all(Order)` still returns deleted rows. Two more lines in the migration fix that:

```elixir
execute "CREATE OR REPLACE VIEW visible_orders AS SELECT * FROM orders WHERE deleted_at IS NULL",
        "DROP VIEW IF EXISTS visible_orders"
```

and the schema points at the view:

```elixir
schema "visible_orders" do
  ...
  field :deleted_at, :utc_datetime
  timestamps()
end
```

Now the default is safe and the exception is explicit. Ecto treats the **source** (table or view) and the **schema** (field types) as separate things, so the same schema reads the base table when you ask:

```elixir
Repo.all({"orders", MyApp.Order})

from o in {"orders", MyApp.Order},
  join: u in assoc(o, :users),
  where: o.total >= ^min_value
```

Type casting and parameterised queries work unchanged. Because the view is a single table with a plain `WHERE`, Postgres makes it automatically updatable: inserts, updates, and deletes go through `visible_orders` without naming the base table, and a delete through the view still lands on the rule.

**The operational tax Valim does not mention.** Postgres expands `SELECT *` when the view is *created*, not when it is queried. Every later migration that adds a column to `orders` must also re-run `CREATE OR REPLACE VIEW visible_orders …`, or the new Ecto field has no column behind it and every query on the schema fails. `CREATE OR REPLACE` can only append columns; dropping or reordering one means `DROP VIEW` and recreate, and `DROP COLUMN` on the base table is refused while the view depends on it. Budget for this in every schema change, or generate the view from a helper in the migration module.

## Caveats

- **`Repo.delete(order)` raises `Ecto.StaleEntryError`.** The rewritten statement reports zero rows affected, which Ecto reads as "this row no longer exists". From Ecto 3.12 (August 2024) you opt in: `Repo.delete(order, allow_stale: true)`. The same stale-entry mechanism applies to `Repo.update` of a row that has already been soft-deleted, since through the view it matches nothing. That is arguably the behaviour you want: deleted rows cannot be edited back into existence by accident.
- **`Repo.delete_all` always reports zero.** When the count matters, write the soft delete as `Repo.update_all` setting `deleted_at` yourself.
- **Indexes and constraints.** Unique indexes and check constraints usually should not apply to deleted rows (a deleted user's email or a deleted post's slug should be reusable). Postgres partial indexes `WHERE deleted_at IS NULL` do this, and Ecto's `unique_constraint/3` then needs the partial index's name. Performance indexes deserve the same thought: a partial index on the view's predicate serves queries through the view and stays smaller as deletions accumulate.
- **Cascades**, as above: nothing cascades until you make it.

## Hard-deleting anyway

Postgres can disable a rule, and because DDL is transactional, you can do it inside the transaction that performs the real delete:

```elixir
Repo.transaction(fn ->
  Repo.query!("ALTER TABLE orders DISABLE RULE soft_deletion")
  Repo.delete!(order)
  Repo.query!("ALTER TABLE orders ENABLE RULE soft_deletion")
end)
```

Valim wraps this as `Repo.disable_soft_deletion(tables, fun)`, which disables the rule on each table, runs `fun` in a `try … after` that re-enables them, and quotes table names after rejecting any containing `"`.

Two points worth stating plainly:

- **The transaction is the guarantee, not the `after`.** Disable and re-enable commit together, and a rollback restores the rule, so no other session ever observes the table with the rule off. The `after` is defensive; the transaction is what makes the escape hatch safe.
- **The escape hatch takes a heavy lock.** The `ALTER TABLE` docs note no weaker lock for `ENABLE`/`DISABLE RULE`, so it takes the default `ACCESS EXCLUSIVE`, which blocks even reads of `orders` until the transaction commits and, if it has to wait for a running query, queues every later query behind it (the lock-queue hazard in [[postgres-fundamentals]]). Keep the hard-delete transaction tiny, never wrap a slow job in it, and set `lock_timeout`. The real delete also fires the real cascades, which is often the point.

## Choosing a shape

Valim's closing advice, with the decision made explicit:

| Need | Shape |
|---|---|
| Deleted rows must keep participating in the same constraints and foreign keys as live rows | Rule + view (this article) |
| Deleted rows only need to be recoverable or auditable, across many resource types | Brandur's [`deleted_record` table](https://brandur.org/fragments/deleted-record-insert): a trigger copies a JSON snapshot of the row on delete, the row really goes away, and indexes, constraints, and cascades stay simple |
| One resource, low stakes | Application level, accepting the gaps above |

The rule-and-view approach pays its rent in migrations (the view tax) and in Ecto ergonomics (`allow_stale`, zero counts); the `deleted_record` approach pays in restore complexity, since a snapshot has to be reinserted against today's schema and constraints. The two techniques Valim demonstrates along the way, pointing one schema at several sources and reading "zero rows affected" as staleness, are useful well beyond soft deletes, for example in [[postgres-scaling]]'s per-replica and per-shard repos.

## Sources

- Valim, J. (2024). "Soft deletes with Ecto and PostgreSQL." Dashbit. <https://dashbit.co/blog/soft-deletes-with-ecto> — [[2026-10-22-soft-deletes-with-ecto|local copy]]
