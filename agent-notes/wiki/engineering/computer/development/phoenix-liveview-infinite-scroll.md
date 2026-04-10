---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-09-phoenix-liveview-infinite-scroll.md
compiled_at: 2026-04-10
model: claude-opus-4-6
confidence: high
---

# Phoenix LiveView Infinite Scroll with Streams

A pattern for building fully-virtualized infinite scroll lists in Phoenix LiveView using `stream/3`, the `phx-viewport-top` / `phx-viewport-bottom` bindings, and zero custom JavaScript. The result is a DOM that stays constant in size regardless of how many items exist server-side, with bidirectional scrolling for free.

## The three primitives that make it work

1. **`stream/3`** — LiveView streams assign items to the socket without holding the data server-side after rendering. Only minimal metadata (stream inserts/deletes) is tracked between renders. Combined with `phx-update="stream"`, the client DOM is patched incrementally.
2. **`phx-viewport-top` / `phx-viewport-bottom`** — bindings on the stream container that fire when the first (respectively last) child enters the viewport. LiveView does the scroll detection internally — no IntersectionObserver, no scroll event listeners, no client JS.
3. **The stream `:limit` option** — passing `limit: n` to `stream/3` caps how many items live in the DOM. When new items are inserted, excess items on the opposite end are pruned automatically. The **sign of the limit** indicates which end to prune: negative limit prunes from the top (use when appending to bottom), positive limit prunes from the bottom (use when prepending to top).

## Canonical shape

The tutorial's core pattern (abbreviated):

```elixir
defp paginate_posts(socket, new_page) when new_page >= 1 do
  %{per_page: per_page, page: cur_page} = socket.assigns
  posts = Blog.list_posts(offset: (new_page - 1) * per_page, limit: per_page)

  {posts, at, limit} =
    if new_page >= cur_page do
      {posts, -1, per_page * 3 * -1}    # scrolling down: append, prune top
    else
      {Enum.reverse(posts), 0, per_page * 3}  # scrolling up: prepend (reversed), prune bottom
    end

  case posts do
    [] ->
      assign(socket, end_of_timeline?: at == -1)

    [_ | _] = posts ->
      socket
      |> assign(end_of_timeline?: false)
      |> assign(:page, new_page)
      |> stream(:posts, posts, at: at, limit: limit)
  end
end
```

With `per_page = 20` and `limit = per_page * 3`, at most 60 items exist in the DOM at any moment — a rolling window of three pages.

## Template details that matter

```heex
<ul
  id="posts"
  phx-update="stream"
  phx-viewport-top={@page > 1 && JS.push("prev-page", page_loading: true)}
  phx-viewport-bottom={!@end_of_timeline? && JS.push("next-page", page_loading: true)}
  class={[
    if(@end_of_timeline?, do: "pb-10", else: "pb-[calc(200vh)]"),
    if(@page == 1, do: "pt-10", else: "pt-[calc(200vh)]")
  ]}
>
  <li :for={{id, post} <- @streams.posts} id={id}>...</li>
</ul>
```

Two non-obvious tricks:

- **Conditional bindings.** `phx-viewport-top` is only attached when `@page > 1`; `phx-viewport-bottom` is only attached when the timeline hasn't ended. The bindings simply evaluate to `false` otherwise, so no event fires.
- **The `200vh` padding trick.** Above and below the list, the container gets 200vh of padding whenever it's "somewhere in the middle". That phantom space gives the user room to keep scrolling past the rendered window while the next batch loads, preventing an abrupt stop. At page 1 (no previous) or end-of-timeline (no next), the padding collapses to `pt-10`/`pb-10`.

## The `_overran` edge case

When the user grabs the scrollbar and yanks it — say, all the way to the top in one motion — the viewport blows past the boundary before LiveView can respond. The bindings send `"_overran" => true` in that case, and the handler should reset to page 1 (or the extreme) rather than decrementing by one:

```elixir
def handle_event("prev-page", %{"_overran" => true}, socket) do
  {:noreply, paginate_posts(socket, 1)}
end
```

Without this clause, fast scrolling would leave the user stuck because each `prev-page` event only steps back one page while the scroll position has already jumped several.

## `page_loading: true`

The `JS.push("next-page", page_loading: true)` option tells LiveView to toggle `phx-page-loading` on the document body while the event is in-flight. Pair with a fixed `.loading-indicator` styled to show only under that class, and you get a free "loading" bar without bespoke state.

## Why this is an interesting pattern

- **Server memory is O(window size), not O(total items).** Traditional assign-based pagination either accumulates all loaded items in socket state (memory grows with scroll distance) or drops them manually. Streams make the window bound automatic.
- **No client JS to maintain.** The same feature in a React/Vue app typically means an IntersectionObserver plus scroll-restoration logic plus debouncing. LiveView collapses all of it into three HTML attributes.
- **Bidirectional scrolling is symmetric.** Because `stream/3`'s `:at` and `:limit` accept both positive and negative values, the same function handles "scroll down to load newer" and "scroll up to load older" without a separate code path.

This fits the broader LiveView philosophy of pushing DOM mechanics (patching, pruning, scroll detection) onto the framework so application code stays in Elixir. It's a nice companion to [[computers-can-be-understood]]: a case where the abstraction is thin enough that understanding what `phx-viewport-bottom` actually does takes one paragraph, not a mental model of a whole client-side framework.

## Applicability

The tutorial frames this for a blog post listing, but the same shape works for any append-mostly list:

- Chat message history (load older on scroll up)
- Activity / notification feeds
- Log viewers
- Search results with lazy materialization

The pattern assumes **offset-based pagination is acceptable** for the underlying query. For very large tables where `OFFSET` becomes slow, swap `list_posts/1` for a cursor/keyset query (`WHERE inserted_at < $last_seen ORDER BY inserted_at DESC LIMIT $n`) — the LiveView side of the pattern is unchanged.

## Sources
- Full Stack Phoenix (2026). "Infinite Scroll in Phoenix LiveView." <https://fullstackphoenix.com/tutorials/infinite-scroll-in-phoenix-liveview> — [[2026-04-09-phoenix-liveview-infinite-scroll|local copy]]
