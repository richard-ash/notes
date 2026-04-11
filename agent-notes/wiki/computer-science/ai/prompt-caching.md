---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2025-12-16-prompt-caching.md
compiled_at: 2026-04-10
model: claude-opus-4-6
confidence: high
---

# Prompt Caching (KV Caching)

Prompt caching is the reason modern LLM APIs can charge ~10x less for repeated input tokens and serve long-context requests with up to 85% lower latency. The mechanism is specifically **KV caching**: storing the `K` (key) and `V` (value) matrices produced inside the attention layers so that on subsequent requests with the same prefix, the expensive matrix multiplications don't have to be redone.

## The mechanism

Sam Rose (ngrok, 2025) walks through the full transformer stack to explain why caching works where it does:

1. **Tokenization** — text becomes integer tokens (e.g. "Check out ngrok.ai" → `[4383, 842, 1657, 17690, 75584]` under GPT-5's tokenizer).
2. **Embedding** — each token becomes a vector in an n-thousand-dimensional space.
3. **Attention** — the model multiplies embeddings by three learned weight matrices `WQ`, `WK`, `WV` to get per-token query, key, and value vectors, then computes weighted combinations via softmax-normalized attention scores (with future tokens masked so the model can't peek ahead).
4. **Output** — the final layer produces a probability distribution over next tokens.

The crucial insight is that `K = embeddings · WK` and `V = embeddings · WV` depend **only on the input tokens and the fixed model weights** — not on sampling parameters like temperature, top_p, or top_k, and not on anything downstream. That makes them safe to memoize.

> "The data that gets cached is the result of `embeddings * WK` and `embeddings * WV`, so `K` and `V`. As a result, prompt caching tends to be called 'KV caching.'"

## Why it matters for inference

Naïve autoregressive decoding reprocesses the entire prompt on every generated token — O(n²) in the prompt length across a full completion. With a KV cache, the provider processes the full prompt once, stores the K and V matrices, and on each subsequent token only has to run the new token through attention against the cached prefix. The larger the prompt relative to the completion, the bigger the win — which is why cached long-context workloads (agent loops, document Q&A, code review over large repos) are the ones that see the full 10x cost and 85% latency reductions.

Cached requests also produce **consistent outputs** across sampling parameter changes at the cached layer: the K/V matrices are deterministic given the input, so only the post-attention sampling differs.

## Provider implementations differ

The two major providers take opposite design stances:

- **OpenAI** caches automatically. Requests get routed opportunistically to cached entries, landing roughly 50% hit rates in Rose's measurements. No API surface to control it.
- **Anthropic** exposes explicit `cache_control` markers in the API. When you request a cache breakpoint, hit rate is 100% (for the 5-minute window), giving predictable latency for applications that depend on it.

The trade-off is the usual implicit-vs-explicit API question: OpenAI's approach is zero-effort but unpredictable; Anthropic's costs a line of code but lets you reason about your bill and your p99.

Caches typically live for 5–10 minutes, which shapes application design — agent loops and conversational UIs benefit naturally, but batch workloads need to be scheduled to hit the window.

## Implications

- **Prompt architecture matters more than it used to.** Put stable content (system prompts, tool definitions, retrieved context, few-shot examples) at the *front* of the prompt and volatile content (the user's latest message) at the end. Only a common prefix can be cached.
- **Agent frameworks have a hidden cost axis.** Frameworks that reshuffle tool definitions or inject timestamps near the front of the prompt silently break caching and 10x the bill.
- **Determinism is underrated.** Because K/V depends only on the input, two requests with identical prompts but different temperature settings share the same cache entry — useful for A/B testing sampling strategies without paying twice.

## Related concepts

- [[the-bitter-lesson]] — Sutton's argument that compute-leveraging general methods win. KV caching is an engineering optimization on top of the attention mechanism, which itself is the general-method architecture that beat hand-engineered NLP.
- [[llm-knowledge-bases]] — Karpathy's workflow for querying large personal markdown corpora with LLMs depends on cacheable long prefixes to be affordable at all.

## Sources

- Rose, Sam (2025-12-16). "Prompt Caching: 10x Cheaper LLM Tokens, But How?" <https://ngrok.com/blog/prompt-caching> — [[2025-12-16-prompt-caching|local copy]]
