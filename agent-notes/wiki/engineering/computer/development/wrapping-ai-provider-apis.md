---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-27-req-is-all-you-need.md
compiled_at: 2026-06-04
model: claude-opus-4-7
confidence: medium
---

# Wrapping AI Provider APIs

Ben Reinhart argues that the popular category of "unified AI SDK" libraries — packages like the Vercel AI SDK, LangChain, LiteLLM, or his own (now-archived) [axflow](https://github.com/axflow/axflow/tree/main/packages/models) — is mostly unnecessary, and that hand-rolling a thin per-provider HTTP wrapper is the better default. The post is grounded in Elixir and uses [Req](https://hexdocs.pm/req) as the HTTP client, but the argument generalizes: AI providers are just HTTP APIs, and the only meaningful incidental complexity is parsing Server-Sent Events for streaming responses.

This is a recurring tension in AI tooling design. It connects to broader threads about commodity model layers ([[ai-lab-economics]], [[ai-eats-the-world]]) — if model APIs are converging toward commodity infrastructure, the value of an abstraction layer that papers over their differences is small and shrinking, since the differences themselves are a transient inefficiency.

## Reinhart's four arguments against unified SDKs

1. **Most projects don't actually need N providers interchangeably.** The "switchable backends" feature is theoretical for the majority of consumers.
2. **Provider documentation no longer maps 1:1 to your code.** You now have to learn two APIs — the provider's and the wrapper's — and translate between them when reading docs or debugging.
3. **Libraries introduce their own concepts and surface area** that you have to model in your head alongside the underlying API.
4. **You inherit the library's release cadence.** New provider features (prompt caching, computer use, files, extended thinking) ship when the wrapper maintainer gets to them, not when the provider ships them. Reinhart frames this as "you're at the mercy of the library."

The fourth point is the load-bearing one for fast-moving providers in 2026. Anthropic and OpenAI ship new capabilities roughly monthly; an abstraction that hides those differences either lags or leaks.

The argument is sympathetic to Anthropic's own [[claude-api]] guidance: write directly against the Messages API, take advantage of its first-class features (prompt caching, tool use, extended thinking) rather than reducing them to a lowest-common-denominator interface.

## The wrapper, in three pieces

Reinhart's recommended architecture is roughly 50 lines of Elixir per provider, plus an off-the-shelf SSE parser. The three pieces:

**1. Non-streaming endpoint** — a single `messages/1` function that wraps `Req.post/2` against the provider URL, sets the auth header, bumps the timeout (Req's 15s default is too low for AI calls — bump to 1+ minute), and returns `{:ok, body}` / `{:error, body}`. The request body is a plain map that mirrors the provider's JSON schema exactly. No translation layer; the caller writes `%{model: "claude-haiku-4-5", max_tokens: 8192, messages: [...]}` just as it appears in the docs.

**2. Streaming endpoint** — `stream_messages/1` adds three changes: `stream: true` in the body, `into: :self` in Req opts (to receive the response as a stream of messages to the calling process), and a pipeline that runs the body through `ServerSentEvents.decode_stream/1` (Reinhart's own [server_sent_events](https://github.com/benjreinhart/server_sent_events) library, written specifically to do nothing but parse SSE correctly per spec) followed by JSON-decoding each event's data field. Output is a lazy `Stream` the caller can `Enum.each` over.

**3. Cancellation** — the tricky bit. Streaming AI calls run for tens of seconds and users press stop. Reinhart shows two approaches:

  - *Cheap version:* return the cancel function alongside the stream: `{:ok, stream, cancel}`. The caller can invoke `cancel.()` mid-iteration. Simple but pushes lifecycle management onto every caller.
  - *Encapsulated version:* return only `{:ok, stream}` and wire the cancellation through Erlang process messaging. `Stream.transform/3` checks the process mailbox for a `:cancel` message on each iteration; if present, it calls `Req.cancel_async_response/1` and halts. Callers wrap the stream consumer in a `Task.start/1` and `send(pid, :cancel)` when the user wants to stop.

The encapsulated version is idiomatic Elixir — it leans on the language's process model, which is exactly the kind of "use what the platform gives you" payoff that disappears under a portability abstraction. Reinhart concedes the explicit-PID handoff "seems a bit awkward in isolation" but notes that in real Phoenix apps the consumer is already running in its own process, so the integration is natural.

## Where Reinhart admits a library *does* earn its keep

Two carve-outs:

- **Switching providers as a first-class feature.** If your product actually offers users a choice of backends, you do need a shared interface. But Reinhart's suggestion is to *write that thin shared interface yourself*, on top of the per-provider wrappers, keeping "unification logic… in one place, easy to evolve as the providers do." Your shared interface owns its own boundary instead of inheriting someone else's.
- **Agents.** Loops, context management, caching, tool use orchestration. Reinhart concedes this is genuinely more complex but argues it's also (a) not a solved problem with mature generic solutions and (b) too context-dependent for off-the-shelf abstraction to fit. So: "your problem to own for now." This echoes the dominant 2026 view across [[agentic-engineering]] and [[ai-coding-harnesses]] that harness shape is downstream of product shape, not portable.

## Connections and tensions

**The streaming complexity claim.** Reinhart frames SSE parsing as the main reason developers reach for a unified SDK. This is plausibly true in JavaScript (where stream handling is fragmented across `fetch`, `EventSource`, and a half-dozen SSE libraries of varying correctness) but less obviously true in Elixir, where Req + a 100-line parser library covers it. The argument's generalization to other ecosystems would benefit from acknowledging that the "use HTTP + SSE directly" bar is higher in some languages.

**The "axflow author admits SDKs are bad" credential.** Reinhart prominently flags that he previously maintained one of these libraries, which gives the argument insider weight — he's not theorizing about a maintenance burden he hasn't lived. Authorial position is doing real work here.

**The Knightian-uncertainty layer.** The post sidesteps the strategic question of *why* AI provider APIs keep diverging. The strategy literature ([[ai-lab-economics]], [[ai-eats-the-world]]) suggests that until the model layer stabilizes, providers will compete on capability differentiation (extended thinking, prompt caching, computer use, files), which is exactly the surface area that unified SDKs paper over. If the underlying market dynamics push toward divergence, the cost of using a unified SDK is structurally increasing over time.

**Connection to [[choose-boring-technology]].** Req + a tiny SSE parser is the maximally boring choice — battle-tested HTTP client, narrow-scoped parser library, plain functions returning tuples. The "innovation token" goes into the agentic logic you're actually building, not the I/O substrate.

## Sources
- Reinhart, B. (2026-04-27). "Req Is All You Need." <https://benreinhart.com/blog/req-is-all-you-need/> — [[2026-04-27-req-is-all-you-need|local copy]]
