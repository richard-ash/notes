---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-11-activity-tracking-phoenix-liveview.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: medium
---

# Ecto Activity Tracking

Automatic audit logging for Phoenix apps by overriding Ecto `Repo` operations. The pattern intercepts `insert/2`, `update/2`, and `delete/2` at the Repo level so that any schema implementing a `Trackable` protocol gets logged without modifying existing context functions.

## Architecture

The system has four components:

1. **Event storage** — two tables: `activity_actors` (one row per user, upserted on first tracked action) and `activity_events` (immutable append-only log with action, subject, and JSONB `data` field).
2. **Trackable protocol** — each schema opts in by implementing `allowed_actions/1` (which of `:insert`, `:update`, `:delete` to track) and `to_activity/1` (human-readable subject string for the feed).
3. **TrackedRepo macro** — `use MyApp.ActivityTracking.TrackedRepo` in the Repo module. It uses `defoverridable` to wrap the six Repo mutation functions (`insert`, `update`, `delete` and their bang variants), checking each result against the protocol.
4. **Process dictionary actor** — `put_actor/1` stores the current user ID in the process dictionary at request start (via a LiveView `on_mount` hook or controller plug). The Repo override reads it implicitly, avoiding the need to thread the user through every context call.

## Key design decisions

**Separate actor table.** Rather than putting `user_id` directly on events, an `activity_actors` table is upserted per user. This provides a single join point and makes multi-tenancy extensions (adding `account_id`) straightforward.

**JSONB `data` field with GIN index.** Events store a `record` key like `"Blog.Post:42"` — a normalized module path plus ID. The GIN index enables efficient queries like "all events for this specific record." The `record_key/1` helper strips the top-level app module and joins the rest.

**Immutable events.** The events table uses `timestamps(updated_at: false)` since events should never be modified after creation.

**Opt-out and override via Repo options.** Pass `track: false` to skip tracking, `track_subject: "custom text"` to override the subject, or `actor: user` to explicitly set the actor instead of using the process dictionary.

## Process dictionary trade-off

Using the process dictionary (`Process.put/get`) for the current actor is convenient — it avoids threading a `%User{}` through every context function. However, it only works within the same BEAM process. This is fine for LiveView (each LV connection is a process) and controller requests (each request is a process), but won't automatically work across process boundaries (e.g., a Task or GenServer spawned from a request). For those cases, pass the `:actor` option explicitly or use the `with_tracking/4` helper.

## Manual tracking

For operations that don't go through Repo directly (multi-step transactions, batch operations), a `with_tracking/4` block helper only records the event if the block returns `{:ok, struct}`:

```elixir
ActivityTracking.with_tracking(current_user, :insert, "batch import") do
  Blog.create_post(attrs)
end
```

## Related patterns

- [[phoenix-activity-feed-rendering]] — the companion (part two) tutorial: rendering the recorded events as a LiveView feed with cursor pagination and streams
- [[phoenix-liveview-infinite-scroll]] — alternative pagination/UX pattern (viewport-driven, offset-based) for the same kind of append-mostly list
- Ecto's `Repo` `defoverridable` pattern is similar to how [[software-migrations]] describes intercepting system boundaries for cross-cutting concerns

## Sources

- FullStackPhoenix (2026). "Activity Tracking in Phoenix LiveView." <https://fullstackphoenix.com/tutorials/activity-tracking-in-phoenix-liveview> — [[2026-04-11-activity-tracking-phoenix-liveview|local copy]]
