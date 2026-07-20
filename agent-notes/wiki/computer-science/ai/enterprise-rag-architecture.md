---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-07-20-cerebras-knowledge-base.md
compiled_at: 2026-07-20
model: claude-opus-4-8
confidence: medium
---

# Enterprise RAG Architecture

A production account, from Cerebras engineers Isaac Tai, Daniel Kim, and Mike Gao, of building an internal knowledge base that fields ~15,000 questions/day across humans, automations, and agents three months after launch. Where [[llm-knowledge-bases]] debates *whether* an LLM-queryable company brain can work, this is a worked description of one that does — and its central lesson is that at company scale, naive vector RAG is not enough. You need **hybrid retrieval**: several independent scorers, each covering the others' blind spots, fused and reranked.

## The founding constraint: meet data where it lives

The authors open by rejecting the recurring "single source of truth" fantasy — the quarterly proposal to record everything in one platform. Information is generated wherever it's ergonomic: suggested edits in docs, threads in Slack, code in GitHub, status in Jira. Each platform is tailor-made for its domain ("discussing a pull request in Google Docs would be a terrible experience"). So the design goal is *minimal change to existing behavior*: extract data from each platform directly rather than forcing people to relocate it.

This is the same premise Posel argues from in [[llm-knowledge-bases]] — that a company's real context lives in the messy stream of work (Slack, calls, corrections), not in clean documentation — but turned from an objection into an architecture. Cerebras Knowledge is essentially **Posel's prescription built**: not a compiled static wiki but "one view of a larger memory system that captures intent... as it happens."

## Anatomy: one embeddings table, one connector per source

The knowledge base provides three things: (1) a store for internal data, (2) a query surface, (3) an auth/authz layer with auditing and analytics. At the core is a **single Postgres table** holding embeddings, raw summaries, and metadata from every source.

The interface is deliberately simple so other teams can build connectors: every source — Slack threads, wiki pages, code, netlists, custom databases — lands in the *same* embeddings table (document, embedding, metadata, source + timestamps), and anything in that table is immediately queryable through the same interface (MCP, web UI, agents). Each data source declares what the data is, how to connect, and how often to fetch. This is a "fat code, thin schema" bet in the spirit of [[agentic-engineering-architecture]]: a narrow, stable row shape absorbs arbitrary source heterogeneity, so the rest of the stack needs no special-casing.

Custom sources exploit this directly: a team opens a PR with a small Python module that reads its system and emits rows shaped like the shared table. No other part of the stack changes.

## Slack ingestion: the hard case

Slack was the most important source — "where the most up-to-date engineering discussions happen." It's also the hardest, and the authors are candid that **vector search alone failed** here:

- Information density varies wildly ("hey yeah sure mike" vs. a detailed kernel explanation are both messages).
- Short messages frequently beat longer, more informative ones in cosine similarity.
- A message's meaning often depends on surrounding conversation.

### Real-time capture via Socket Mode

A Slack bot runs in **Socket Mode** — Slack pushes every message event over a persistent WebSocket, avoiding Web API polling and rate limits. On each event: acknowledge immediately, deduplicate by stable event ID, mark for the ingest consumer. Critically, the consumer never saves a message in isolation — it **re-fetches the whole thread** (parent + every reply) and writes it back as one row, so stored content, participant list, and last-activity timestamp always reflect the complete conversation. Every channel is its own data source, so freshness is tunable per-channel (a busy incident channel can be ingested more often).

### Distillation, not raw embedding

Raw Slack text is keyword-searchable immediately via a Postgres full-text (GIN) index. But the *embedded* content is not the transcript — during **distillation**, an LLM extracts structured fields from the thread: a one-line question an engineer would actually search for, a short summary, the resolution, and the code/system references. Only these are embedded. Accuracy "increased significantly when the thread was normalized into a consistent format" — an instance of the general finding (also in [[knowledge-graph-llm-context]]) that *how* context is serialized for the model matters as much as what it contains.

### Bursting: rescuing the buried answer

Thread-level summaries lose important individual messages. A **burst** is a run of consecutive messages from one author, embedded with the thread topic prepended as context — a direct application of Anthropic's [contextual retrieval](https://www.anthropic.com/news/contextual-retrieval). Bursts are gated to keep noise out: they must contain a rare token (corpus IDF ≥ 4.0), be ≥ 200 characters, and ideally carry a reaction (a social-signal boost). Qualifying bursts are embedded alongside the thread record.

## The core idea: hybrid retrieval, no scorer trusted alone

The load-bearing insight is that **every thread is retrievable through several techniques at once, each covering the others' weaknesses**:

- **Full-text search** catches exact tokens embeddings blur together — error strings, flag names, hostnames. When someone pastes a literal error, a lexical match is the best evidence and no semantic similarity should outrank it.
- **Embedding search** catches paraphrase — "restore hangs after manifest load" ↔ "checkpoint stalls on the NFS mount" may share no vocabulary.
- **Inverse document frequency (IDF)** separates signal from filler — a short message built on a rare config flag deserves to rank; "sounds good, thanks!" sits near many queries in embedding space but scores ~0 once term rarity counts.
- **Age decay** encodes that Slack answers expire — an eight-month-old thread may describe infrastructure that no longer exists, so when relevance is otherwise equal, the newer thread wins.

This directly answers the "confident and wrong" failure Posel warns about in [[llm-knowledge-bases]]: age decay is freshness-as-a-ranking-signal, and IDF is a filler filter. No single scorer is trusted; each produces its own ranked view, fused at query time.

## Reranking: RRF then a reranker model

Retrievers produce incompatible score scales, so they're first combined with **reciprocal rank fusion (RRF)** ([Cormack et al., SIGIR 2009](https://dl.acm.org/doi/10.1145/1571941.1572114)): each document scores `Σ weight / (60 + rank_L)` across every list `L` it appears in (default weight 1.0, smoothing constant K=60). The smoothing constant makes **consensus beat a single strong vote** — a document ranking near the top across several retrievers outscores one that ranks first in only one. Duplicate chunks are merged to their source and per-file contribution is capped, yielding a diverse top ~20.

Those candidates plus the original query go to a small **reranker model** scoring each 0–10; the top 10 survive. Finally, context is added back to the winners — e.g., a matched wiki section pulls in its two neighboring sections so headings, preconditions, and caveats that chunking split apart aren't lost. This last step is a deliberate guard against the "lost in the middle" / lonely-paragraph problem ([Liu et al.](https://arxiv.org/abs/2307.03172)). The output of `search` is thus fused → deduplicated → reranked → context-expanded evidence.

## Code embeddings: "grep is all you need" wasn't

The team initially doubted code embeddings were worth it given Claude Code and ripgrep ("grep is all you need"), but Cursor's semantic-search findings changed their minds. They use **CocoIndex** (open-source), splitting each repo with language-aware regex boundaries ordered coarse-to-fine: try class-level first, fall back to methods, then smaller blocks — so one file yields multiple embeddings at different specificity (file-level and function-level). CocoIndex tracks sync metadata *in the same Postgres*, so each commit re-embeds only changed chunks. Repos onboard via team-submitted config files with path-level allow/deny lists. Some internal repos exceed 40 GB, so incremental re-embedding is the whole game.

## Serving: retrieval primitives + agent-as-orchestrator

The serving design mirrors the "fat code, thin harness" split of [[agentic-engineering-architecture]] and the retrieval-as-tools posture of [[agent-harness]] / [[company-wide-agent]]:

- **MCP exposes retrieval primitives directly** — `search`, `search_slack`, `search_code`, `who_knows`, etc. — each a narrow, stable, "as LLM-free as possible" tool that runs one pipeline (vector / lexical / ripgrep), applies light heuristics, and returns raw evidence rows. The retrieval layer does not depend on LLM decisions to serve. **Claude Code (or any MCP agent) becomes the orchestration engine**, deciding which tools to call and how to assemble the answer.
- **The web UI runs the full pipeline itself** via a fixed **planner → executor → synthesizer** loop: a lightweight LLM planner picks tools given the query + active project; the executor fans them out in parallel and normalizes results into a shared evidence schema (scores, recency, source hints); a final synthesis LLM produces the answer with citations and caveats. From the user's side it's "ask a question, get an answer"; under the hood it's the same pattern an MCP client can reconstruct explicitly.

Keeping the primitives LLM-free and pushing orchestration to the client is the same discipline as [[harness-engineering]]: the deterministic substrate stays cheap and legible, and intelligence lives in the harness layer, not baked into every tool.

## Projects: relevance by default

"Search everything everywhere" stopped scaling — compiler engineers don't want infra runbooks in their results. A **project** is a lightweight named bundle of data sources (specific channels, repos, DBs, doc spaces); the same source (e.g., a shared incidents channel) can be referenced by many projects without duplication. During onboarding a user picks a default project, stored on their profile, which scopes queries automatically — a new engineer gets high-signal answers without first learning which channels and repos matter.

## Why this matters: the empirical answer to the company-brain objections

Read against [[llm-knowledge-bases]], Cerebras Knowledge is a point-by-point response to Posel's three reasons LLM wikis fail as company brains:

| Posel's objection | Cerebras' design answer |
| --- | --- |
| **Intent lives in Slack, not docs** — compiling to a clean page drops the reasoning | Ingest Slack directly via Socket Mode; distill the *question + resolution + refs* from live threads, not just final docs |
| **Wikis go stale outside the work** | Nothing is a static wiki — continuous real-time ingestion, per-channel freshness tuning, per-commit code re-embedding, and **age decay** as a ranking signal |
| **Governance/provenance breaks trust** | Auth/authz + auditing as one of three core pillars; every row carries source + timestamps (provenance built into the schema) |

It equally **contradicts Karpathy's "index files over RAG" claim** in the same article: Karpathy argued that at ~100 documents an LLM navigating index files needs no RAG pipeline. Cerebras is the large-scale counterexample — at company scale with a living Slack corpus, they found "vector search alone was insufficient" and built exactly the heavy hybrid-retrieval + fusion + reranking infrastructure Karpathy said you could skip. The two aren't in conflict so much as scale-dependent: index-files-over-RAG holds for a stable personal corpus; production hybrid RAG is what a messy, high-volume, staleness-prone org stream demands.

The durable takeaways, independent of Cerebras: (1) **no single retrieval scorer is trustworthy** — lexical, semantic, rarity, and recency each fail differently, so fuse them; (2) **normalize before embedding** — distilling messy content into a consistent structured shape beats embedding raw text; (3) **keep retrieval primitives deterministic and LLM-free**, and let the agent orchestrate; (4) **freshness and provenance are ranking features, not afterthoughts**.

## Caveats

This is a single, self-reported source — a company engineering blog describing its own product, with self-reported adoption numbers (15,000 questions/day) and no external benchmark. The retrieval techniques themselves (RRF, IDF, reranking, contextual retrieval) are well-established and verifiable; the *specific* claims about this system's effectiveness are not independently confirmed. The post is also light on how authorization is actually enforced at query time — arguably the hardest of Posel's three objections — describing it as a "layer" without detail.

## Sources
- Tai, I., Kim, D., & Gao, M. (2026). "How Cerebras Built Its Enterprise Knowledge Base." <https://www.cerebras.ai/blog/how-we-built-our-knowledge-base> — [[2026-07-20-cerebras-knowledge-base|local copy]]
