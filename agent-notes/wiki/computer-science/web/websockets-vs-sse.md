---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/web/2026-09-17-websockets-vs-sse.md
compiled_at: 2026-09-17
model: claude-fable-5-1
confidence: medium
---

# WebSockets vs. SSE (ordering and correctness)

The usual framing of the realtime-transport debate is latency and simplicity: Server-Sent Events plus ordinary Fetch requests reuse one multiplexed HTTP connection, so why hand-roll a protocol over a WebSocket? José Valim (creator of Elixir and a core Phoenix contributor) argues that framing misses the point. The question that should decide it is **how many independent streams can update the same piece of UI**, because every additional stream is an opportunity to render events out of order — and the usual fixes cost either latency or client complexity.

The piece responds to the top Hacker News comment on Andros's *HTML over WebSockets* article (Django LiveView), which recommended "just use SSE and Fetch" for most apps.

## The secondary arguments

Valim grants two conventional points for WebSockets and then explicitly demotes them:

- **Stateless requests repeat work.** Fetch reuses the TCP connection, but each request still decrypts the session, loads the user from database or cache, and so on. A WebSocket authenticates once and keeps the user in memory for the life of the connection.
- **Payload size.** LiveView sends diffs rather than HTML, which a request/response cycle can't easily do because there is no per-connection state to diff against.

## The race

An article has tags `erlang, clojure, javascript`. You add `elixir` via Fetch; simultaneously another user removes `javascript`, and that change reaches you over SSE. Both channels carry the *resulting tag list*.

The ordering everyone pictures: your add lands, then the delete lands, the SSE event carries `erlang, clojure, elixir`, and your UI agrees with the database.

The ordering that also happens, "thanks to the network, garbage-collectors, proxies, and other factors":

1. The delete commits first. Its server computes the snapshot `erlang, clojure` and queues it for SSE delivery.
2. Your add commits second. The database now holds `erlang, clojure, elixir`.
3. Your Fetch response arrives first: UI shows `erlang, clojure, elixir`. Correct.
4. The delayed SSE event arrives: UI is overwritten with `erlang, clojure`. Wrong — and it stays wrong.

The UI briefly flashes the right answer, then behaves as though your write never happened.

### "It's eventually consistent" is the wrong defence

Valim's sharpest point. Eventual consistency promises that *if updates stop, all replicas converge*. Here updates have stopped and the client has not converged; it stays stale until a refresh or an unrelated later event happens to repair it. That is not a weak consistency model, it is no consistency model.

A useful way to read this against [[amazon-dynamo]]: Dynamo earns the word "eventually" with machinery — vector clocks to detect causally unrelated versions, read repair and Merkle-tree anti-entropy to force convergence. The SSE + Fetch client has neither a way to detect that the snapshot it just received is older than the one it is showing, nor any background process that would correct it. Calling it eventually consistent borrows the label without paying for the mechanism.

### The cause is stream count, not SSE

Valim is careful here: a WebSocket *plus* Fetch, both delivering data to the same component, has the identical race. What a WebSocket offers is bidirectionality, which makes it practical to put reads and writes on **one** connection. Then the server-side process for that connection handles your event and the other user's broadcast sequentially, recomputes the tag list each time, and the single ordered channel guarantees the client sees results in the order they were produced.

## Fixes for multi-stream setups, and what each costs

| Approach | How it restores order | Cost |
|---|---|---|
| **Single delivery stream** — Fetch performs the write but returns no data; the client waits for its own update to come back over SSE | Only one channel ever renders | Latency: your own write goes client → server 1 → message bus → server 2 → SSE. Phoenix's long-poll transport works this way but drops a hop because nodes talk directly over Distributed Erlang |
| **Bidirectional connection** | Request and response share an ordered channel; no second server in the path | Need WebSocket infrastructure and a stateful connection process |
| **SSE as a doorbell** — push only "you have new data", client refetches | Every render comes from a fresh read | Extra requests and server load; client must queue fetches rather than run them concurrently (Valim links his earlier critique of Remix's concurrent submissions) and prioritise user interactions |
| **Reorder on the client** | Client sequences events itself | "Sounds much simpler than it actually is": no guarantee a create arrives before its delete, or that update order matches database order. Whole platforms (Electric) exist for this |

## Implications and connections

**The doorbell row is a pattern this wiki has seen before.** [[postgres-listen-notify]] reaches the same design from the database side: treat notifications as wake-up hints over a durable table, so that "a dropped or reordered notification costs you latency, not correctness, because the reader re-reads the table." That is exactly why the doorbell approach is safe — and it also explains what a well-behaved LiveView process should do when a PubSub broadcast arrives. A single connection only guarantees *delivery* order; if the broadcast itself carried a stale snapshot, a process that blindly rendered it would reproduce the bug over a WebSocket. "Recomputing updates", in Valim's phrase, is doing real work: the process re-derives state rather than trusting the payload.

**The race depends on shipping snapshots.** (Agent's observation, not Valim's.) In the tag example both channels carry the full list, so a late snapshot clobbers a newer one. Two cheaper mitigations exist for this specific shape: send operations (`+elixir`, `−javascript`) that commute, or stamp each snapshot with a monotonic version and discard anything older than what is on screen. Neither generalises — most operations don't commute, and versioning a single resource doesn't help with Valim's create-before-delete case across resources — but for a single-resource view they are far less than a sync platform. Valim's "harder than it sounds" is right about the general problem and somewhat overstated for the narrow one.

**Reorder-on-the-client, done seriously, is local-first.** The last row of the table is what [[local-first-architecture]] describes: Linear wrote its sync engine before anything else, precisely because ordering, optimistic mutation and reconciliation are a foundation rather than a feature. The two articles bracket the design space — LiveView keeps the state machine on the server and makes the client a thin ordered view of it; Linear moves the state machine into the browser and makes the server a sync target. SSE + Fetch with two data-bearing streams sits in the uncomfortable middle, with state on both sides and no protocol reconciling them.

**Read the closing pitch as a pitch.** Dashbit is Valim's own Elixir consultancy, and the conclusion that "Phoenix gives you the best bang for your buck" is unsurprising from that seat. The Distributed Erlang hop-saving is real but specific to the BEAM. The ordering argument stands independently of it and applies to any stack: count the streams that can write to a component, and if the answer is more than one, name the mechanism that orders them.

For what LiveView's single-connection model looks like in application code, see [[phoenix-liveview-infinite-scroll]] and [[phoenix-activity-feed-rendering]].

## Sources
- Valim, José (2026). "WebSockets vs. SSE should be about ordering and correctness." <https://dashbit.co/blog/websockets-vs-sse> — [[2026-09-17-websockets-vs-sse|local copy]]
