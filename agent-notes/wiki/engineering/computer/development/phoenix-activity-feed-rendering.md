---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-11-activity-feed-rendering-phoenix-liveview.md
compiled_at: 2026-04-29
model: claude-opus-4-7
confidence: high
---

# Phoenix Activity Feed Rendering

The UI half of an activity-feed system: how to render an event timeline in Phoenix LiveView using cursor-based pagination and streams. Pairs with [[ecto-activity-tracking]], which covers the data-capture half (Repo-override audit logging). The two together form FullStackPhoenix's two-part activity-feed tutorial.

## The pattern in three pieces

1. **A `to_feed/1` context function** that returns `{events, next_cursor}`. It accepts `limit`, `cursor`, `record`, and `users`/`user` filters, and preloads `actor → user` via a join so the template can render display names without N+1 queries.
2. **A LiveView that holds only the cursor in assigns** and pushes events into a stream. Mount loads page one; a `"load-more"` `handle_event` fetches the next page using the current cursor and appends it to the same stream.
3. **A function component** (`<.activity_feed events={...} cursor={...} />`) that owns rendering only. The parent LiveView still handles the `"load-more"` event and stream; the component is purely presentational.

## Why cursor pagination instead of offset

Activity feeds are **append-mostly at the top** — new events show up constantly while the user is scrolling. Offset pagination duplicates or skips rows in this scenario: if three new events arrive between page 1 and page 2, the user sees rows 17, 18, 19 of page 1 again as the first three rows of page 2. Cursor pagination is immune because the cursor is a value (the `inserted_at` of the last row seen), not a position.

The cursor itself is the `DateTime` of the last loaded event — passed directly to the query, not serialized to a string. The follow-up query is `WHERE inserted_at < ^cursor ORDER BY inserted_at DESC LIMIT n`, which hits the timestamp index and runs in constant time regardless of how many events are in the table. No `OFFSET`, no `COUNT(*)`, no degradation as the table grows to millions of rows.

A subtle wrinkle: the tutorial uses `inserted_at` alone as the cursor, which is **not strictly stable** under sub-second event bursts where multiple events share the same timestamp. The strict form is a composite cursor `(inserted_at, id)` with a tuple comparison: `WHERE (inserted_at, id) < (^cursor_ts, ^cursor_id)`. For an audit log where events come from human actions, single-column is fine; for high-throughput event streams, prefer the composite form.

## Cursor doubles as "has more?"

The handler returns `nil` as the cursor when fewer rows came back than the requested limit. The template uses that directly:

```heex
<button :if={@cursor} phx-click="load-more">Load more</button>
<div :if={is_nil(@cursor)}>No more activity.</div>
```

No separate `:end_of_feed?` boolean. This is a small but characteristic LiveView idiom: collapse two pieces of state into one when one already implies the other. Compare to the [[phoenix-liveview-infinite-scroll]] pattern, which does need a separate `end_of_timeline?` because viewport-driven loading happens in two directions.

## Stream, not assign

Streams matter here for the same reason they matter elsewhere: the events list is unbounded and append-only. If you held the events in a normal assign (`assign(socket, :events, events ++ new_events)`), socket memory would grow with every "load more" click — every event is held server-side until the LiveView process dies. With `stream/3`, the server holds only stream metadata (inserts/deletes) between renders; the rendered DOM is the source of truth for what the user sees.

For "load more" feeds, you typically don't pass `:limit` to `stream/3` because the user is the one bounding the window (they choose how many times to click). For viewport-driven infinite scroll, do pass `:limit` — see [[phoenix-liveview-infinite-scroll]].

## Scoping for free

Because the filter logic lives in `to_feed/1`, the same LiveView shape gives you three feed types by changing one keyword option at mount:

- **Global feed** — `to_feed(limit: 20)`
- **User feed** — `to_feed(limit: 20, user: current_user)` — pulls only events where this user was the actor
- **Record feed** — `to_feed(limit: 20, record: post)` — pulls all events about a specific struct, useful on detail pages

The record-scoped query hits the JSONB `data` field via the GIN index from the tracking-side migration, so it stays fast at scale.

## Component split — what goes where

The tutorial extracts a `<.activity_feed>` function component that takes `events` and `cursor` attrs. This is the right split: the component owns markup and helper functions (`action_verb/1`, `action_color/1`, `relative_time/1`); the parent LiveView owns events, cursor state, and the stream itself. The `phx-click="load-more"` button lives in the component but bubbles up to the parent's `handle_event/3`, because LiveView events are dispatched to the LiveView, not to the component.

The relative-time helper is a representative bit of "no-dependency Elixir" — five `cond` arms over `DateTime.diff/3` that produce "5m ago", "3h ago", "2d ago", or a full date for anything older than a week. No Timex, no humanize-time library.

## Where this fits in the LiveView pagination spectrum

There are three legitimate Phoenix patterns for "many items, one screen at a time":

| Pattern | UX | Pagination | DOM size | When to use |
|---|---|---|---|---|
| Click "Load more" | Explicit | Cursor or offset | Grows unbounded | Activity feeds, comments, mostly-read content |
| Viewport infinite scroll | Implicit | Cursor or offset | Bounded via `stream :limit` | Timelines, search results, chat |
| Numbered pages | Click | Offset | Bounded per page | Admin tables, structured browsing |

This article covers the first; [[phoenix-liveview-infinite-scroll]] covers the second.

## Sources

- FullStackPhoenix (2026). "Rendering an Activity Feed in Phoenix LiveView." <https://fullstackphoenix.com/tutorials/rendering-an-activity-feed-in-phoenix-liveview> — [[2026-04-11-activity-feed-rendering-phoenix-liveview|local copy]]
