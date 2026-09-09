---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2019-11-13-stop-mapping-stuff-in-your-middleware.md
compiled_at: 2026-09-09
model: claude-fable-5-1
confidence: medium
---

# SQL-side JSON serialization

**SQL-side serialization** is the practice of having the database emit the nested JSON (or XML) document a service returns, using the JSON aggregation operators every major RDBMS now ships, instead of loading rows into an object graph in the application tier and mapping that graph to JSON with a second library. Lukas Eder, author of jOOQ, made the case in a November 2019 rant provoked by a reddit thread about "fixing Hibernate." Its one-line thesis:

> Don't go mapping that stuff in the middleware if you're not consuming it in the middleware.

The article is polemical and Java-flavoured, but the observation underneath is stack-agnostic: most read endpoints are a projection of the schema into a tree, and SQL can produce trees.

## The problem it removes

Eder's inventory of what a "produce some JSON from the database" service conventionally requires: entities, DTOs, factories and factory builders; a debate about immutability and which annotation library (Lombok, AutoValue, Immutables) eases it; a JPA-versus-Hibernate-specific mapping decision; Jackson for the JSON step; then debugging the interactions between Jackson, JAXB, Lombok, and JPA annotations, and one or two N+1 query bugs. Every layer exists to bridge the same gap — SQL returns flat rows, the client wants a nested document — and every layer must change when the document's shape changes.

The mechanism behind the N+1 bugs is worth naming, because it is the reason the mapping layer keeps growing. An ORM materializes a parent row and lazily fetches each child collection on access, so rendering *n* parents with two nested collections costs 1 + n + n·m round-trips. The fixes (eager joins, batch fetching, entity graphs) each reintroduce a different problem: a single JOIN across two nested collections is a cartesian product that duplicates parent columns per child combination and has to be de-duplicated in memory. [[system-design]] states the general rule — when querying the database, query the database; JOIN rather than stitching in memory — and this article is that rule applied to the serialization step.

## The technique

Eder's example, against the Sakila sample database, wants actors → the categories they have appeared in → the films within each category. The SQL Server form, tidied:

```sql
SELECT a.first_name, a.last_name, (
    SELECT c.name, (
        SELECT title
        FROM film AS f
        JOIN film_category AS fc ON f.film_id = fc.film_id
        JOIN film_actor    AS fa ON fc.film_id = fa.film_id
        WHERE fc.category_id = c.category_id AND a.actor_id = fa.actor_id
        FOR JSON PATH
    ) AS films
    FROM category AS c
    JOIN film_category AS fc ON c.category_id = fc.category_id
    JOIN film_actor    AS fa ON fc.film_id = fa.film_id
    WHERE fa.actor_id = a.actor_id
    GROUP BY c.category_id, c.name
    FOR JSON PATH
) AS categories
FROM actor AS a
FOR JSON PATH, ROOT ('actors')
```

Three things make it work:

1. **Each nesting level is a correlated subquery, not a join.** The outer query produces one row per actor; the subquery in its SELECT list produces one array per actor. Because the nesting happens inside a scalar subquery, parent rows are never duplicated, so the cartesian-product problem does not arise.
2. **An aggregation operator turns the subquery's rows into one value.** `FOR JSON PATH` in SQL Server; `json_agg` and `json_build_object` in Postgres; `JSON_ARRAYAGG` and `JSON_OBJECT` in the SQL:2016 standard as implemented by Oracle, MySQL, and (since version 16) Postgres; `json_group_array` in SQLite.
3. **The document shape is the query shape.** Reordering, renaming, or adding a level is an edit to one statement. Switching to XML is a change of operator (`FOR XML PATH ('film'), TYPE`), and Eder notes XSLT can derive one format from the other if both are needed.

The result streams from driver to HTTP response as text. Any SQL API can carry it — JDBC, jOOQ, JdbcTemplate, MyBatis, a JPA native query — because nothing is being mapped; and if a particular API cannot express the query, Eder's answer is to put it in a view.

### Postgres form

Most of this wiki's database material is Postgres ([[postgres-for-everything]], [[postgres-fundamentals]]), so the same query in Postgres idiom:

```sql
SELECT json_agg(json_build_object(
  'first_name', a.first_name,
  'last_name',  a.last_name,
  'categories', (
    SELECT json_agg(json_build_object(
      'name',  c.name,
      'films', (
        SELECT json_agg(json_build_object('title', f.title))
        FROM film f
        JOIN film_category fc ON fc.film_id = f.film_id
        JOIN film_actor    fa ON fa.film_id = f.film_id
        WHERE fc.category_id = c.category_id
          AND fa.actor_id    = a.actor_id
      )
    ))
    FROM category c
    WHERE EXISTS (
      SELECT 1
      FROM film_category fc
      JOIN film_actor fa ON fa.film_id = fc.film_id
      WHERE fc.category_id = c.category_id
        AND fa.actor_id    = a.actor_id
    )
  )
))
FROM actor a;
```

Two Postgres-specific notes. Use the `json_*` functions rather than `jsonb_*` for output: `json` preserves key order and skips the parse into binary form, which is wasted work for a value that will be sent as text and never queried — the advice in [[postgres-fundamentals]] to prefer `jsonb` is about *stored* documents. And `json_agg` over zero rows returns SQL NULL, not `[]`; wrap it in `coalesce(..., '[]'::json)` where the client expects an array.

## Eder's FAQ, condensed

The second half of the article is a list of objections with terse replies. The substantive ones:

- **"It doesn't fit our architecture."** Then fix the architecture. The dismissiveness hides a real claim: a DTO layer's purpose is to insulate the API from the schema, and Eder's position is that most services never cash in that insulation.
- **"SQL is bad."** No: it is a declarative 4GL over relational algebra, and the optimizer produces better plans than hand-written 3GL loops. Trusting the optimizer is the precondition for the whole approach.
- **"What about testing? Mocking is better."** Spin up the real database with Testcontainers, migrate the schema with Flyway or Liquibase, load sample data, write integration tests. "The more you mock away the database, the more you're writing your own database."
- **"What if we change RDBMS?"** It will not happen; if it does, rewriting five to ten JSON queries takes twenty minutes and will not be the biggest problem. Every dialect has an equivalent operator anyway.
- **"That's 1990s two-tier architecture."** So what — it took 5% of the time, and the other 95% goes to customers rather than to bikeshedding mapping technology.
- **"We've already spent person-years on our middleware."** Sunk cost. [[wrong-abstraction]] describes the same trap from the code side: an abstraction survives because of what was paid for it, not what it returns.
- **"We need abstraction over ingestion."** No: send JSON into the database and normalize it there with the inverse operators (`JSON_TABLE`, `json_to_recordset`, `OPENJSON`). "You don't *need* middleware abstraction and mapping, you just *want* it."

## Where the argument is strong, and where it stops

The argument is strongest for **read endpoints whose output is a pure projection of the schema**: list and detail views, reports, exports, anything a SELECT describes completely. There the object graph is a pass-through and every line of it is cost without benefit. It also holds for ingestion of documents that are stored, not reasoned about.

It needs qualification in several places the article does not address:

1. **When the middleware does consume the data.** Business rules, per-field authorization, computed fields that call other services, or anything that branches on the row all need the values in the application language. Eder's thesis is explicitly conditional on *not* consuming it in the middleware; the failure mode is reading it as "never build objects."
2. **CPU placement.** Serialization now runs on the database. Application servers scale horizontally and cheaply; a Postgres primary is the one box that does not. For a handful of expensive queries this is irrelevant; for a high-QPS API where JSON building dominates per-request cost, it moves work onto the scarcest resource. The counterweight is that the ORM approach makes the database do *more* work overall (N+1 round-trips, cartesian joins), so the JSON approach usually lowers total database load even while adding serialization. Measure rather than assume.
3. **Correlated subqueries execute per parent row.** Postgres runs a SELECT-list subquery as a SubPlan for each outer row; it does not decorrelate them into joins. With indexes on the correlating columns this is a fast nested loop and still a single round-trip, but for very large parent sets a `LATERAL` join with `GROUP BY`, or pre-aggregating each level in a CTE, plans better.
4. **Type information leaves the type system.** The query returns text. Typed clients — TypeScript, Swift, OpenAPI schemas — need the shape declared somewhere, and the database will not check that the query still matches it after a column rename. Integration tests against the real schema (Eder's own testing answer) catch this; jOOQ's later `MULTISET` operator (below) is the type-safe form.
5. **Coupling is relocated, not removed.** The API shape is now tied to the schema in one statement instead of five files. That is a large improvement in edit cost, but the caveat in [[postgres-for-everything]] stands: a *public*, versioned API will eventually need the schema to change under a response shape that cannot, and something has to absorb the difference — a view, or one query per API version.

The pattern composes with the other "let Postgres do it" techniques: the statement that aggregates the JSON can read the cache table in [[postgres-as-cache]] or rank hits from [[postgres-full-text-search]], and the response is built in the same transaction as the reads.

For Elixir readers: Ecto's `preload` solves the same nested-collection problem differently — one extra query per association using an `IN` list, so *n* parents with two levels cost three queries rather than 1 + n + n·m — and Phoenix's JSON views are exactly the "mapping in the middleware" Eder argues against. Ecto can express Eder's form directly with a `json_agg` `fragment` in a `select`, returning the document as a string.

## Temporal notes

The article is from November 2019 and reads as a contrarian rant. The intervening years have moved its position toward the mainstream.

- **jOOQ 3.14** (October 2020) shipped the `FOR JSON` / `FOR XML` emulation the article promises, and **jOOQ 3.15** (2021) added `MULTISET`, a type-safe nested-collection operator implemented by generating exactly these JSON/XML subqueries and deserializing the result into typed records — Eder's technique with caveat 4 above answered.
- **Postgres 16** (September 2023) added the SQL:2016 constructors (`JSON_OBJECT`, `JSON_ARRAY`, `JSON_ARRAYAGG`, `JSON_OBJECTAGG`); **Postgres 17** (September 2024) added `JSON_TABLE` for the ingestion direction. Eder's "there are also SQL standard JSON APIs as implemented in other RDBMS" now includes Postgres, though `json_agg` and `json_build_object` remain the common idiom.
- **Whole platforms are built on the thesis.** PostgREST's resource embedding, Supabase's API layer over it, and Hasura's GraphQL compiler each turn a nested request into one SQL statement whose leaves are `json_agg` subqueries. They are industrialised versions of the article's query, with the middleware reduced to a request-to-SQL translator.
- The provoking reddit thread was about Hibernate 5. Hibernate 6 (2022) improved the mapping story, but the structural argument — that the mapping layer is unnecessary when nothing consumes the objects — is unaffected.

## Sources

- Eder, Lukas (2019). "Stop Mapping Stuff in Your Middleware. Use SQL's XML or JSON Operators Instead." <https://blog.jooq.org/stop-mapping-stuff-in-your-middleware-use-sqls-xml-or-json-operators-instead/> — [[2019-11-13-stop-mapping-stuff-in-your-middleware|local copy]]
- Referenced: Eder, Lukas (2020). "Using SQL Server FOR XML and FOR JSON Syntax on Other RDBMS With jOOQ." <https://blog.jooq.org/using-sql-server-for-xml-and-for-json-syntax-on-other-rdbms-with-jooq/>
- Referenced: Eder's SQL optimizer talk linked from the article. <https://www.youtube.com/watch?v=wTPGW1PNy_Y>
