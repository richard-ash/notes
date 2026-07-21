---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-04-02-karpathy-llm-knowledge-bases.md
  - agent-notes/raw/computer-science/ai/2026-07-06-posel-llm-wikis-dont-work.md
  - agent-notes/raw/computer-science/ai/2026-07-21-state-of-agent-wikis.md
compiled_at: 2026-07-21
model: claude-opus-4-8
confidence: medium
---

# LLM Knowledge Bases

A workflow pattern where LLMs serve not as code-writing assistants but as **knowledge compilers** — ingesting raw sources (articles, papers, repos, datasets, images) and incrementally building a structured markdown wiki that grows richer with each query.

## The architecture

Karpathy describes a pipeline with distinct stages:

1. **Ingest.** Raw sources are collected into a `raw/` directory. The Obsidian Web Clipper extension converts web articles to markdown; images are downloaded locally so the LLM can reference them.
2. **Compile.** An LLM reads the raw sources and produces a wiki — a directory of `.md` files organized by concept, with summaries, backlinks, and cross-references. The wiki is maintained entirely by the LLM; the human rarely edits it directly.
3. **Query.** Once the wiki reaches meaningful scale (~100 articles, ~400K words in Karpathy's case), an LLM agent can answer complex research questions by navigating the wiki's index files and summaries — without requiring a traditional [[retrieval-augmented-generation|RAG]] pipeline.
4. **Output.** Answers are rendered as markdown files, Marp slide decks, or matplotlib visualizations, all viewable in Obsidian. Outputs are often filed back into the wiki, so queries compound the knowledge base over time.
5. **Lint.** LLM "health checks" find inconsistent data, impute missing information via web search, and surface connections that suggest new articles. This maintains data integrity as the wiki grows.

## Key design choices

- **Obsidian as the IDE.** The human views and navigates the wiki in Obsidian but does not write it. The LLM is the author; the human is the reader and questioner.
- **Index files over RAG.** At the scale Karpathy describes, LLM-maintained index files and document summaries are sufficient for navigation. The model reads relevant documents directly rather than relying on embedding-based retrieval. This works because context windows have grown large enough to hold the summaries and several full articles simultaneously.
- **Compounding returns.** Each query that produces output can be filed back into the wiki. The knowledge base grows not just from new source ingestion but from the user's own explorations — a flywheel effect.
- **Auxiliary tooling.** Karpathy describes vibe-coding a small search engine over the wiki, usable both via web UI and as an LLM CLI tool for larger queries.

## The pattern becomes a category: four independent implementations

By mid-2026 the workflow had a name — the **LLM Wiki**, or, once agents rather than humans became the primary reader, the **agent wiki** — and Mem0's survey *The State of Agent Wikis* documents four teams shipping the same architecture within months of Karpathy's gist, without coordinating. (The naming is loose: Karpathy's original post is titled "LLM Knowledge Bases" and the gist "LLM Wiki"; they describe the same thing.) Mem0 factors the shared shape into **three layers** — immutable **raw sources** the model reads but never edits; the **wiki** of LLM-owned markdown (summaries, entity pages, cross-references); and a **schema** file (CLAUDE.md, AGENTS.md, or similar) that tells the model how the wiki is organized and which workflows to run, "what makes it a disciplined maintainer rather than a chatbot with file access" — with the same three operations Karpathy describes running on top (ingest, query, lint).

The four implementations differ mostly in corpus and in how they handle *currency*:

- **Cognition — DeepWiki** points the pattern at every public GitHub repo (swap `github.com` → `deepwiki.com`), generating architecture overview, file index, dependency graph, and search with links back to source. Over 50,000 top repos are indexed, and — the load-bearing detail — the wiki is not the product's endpoint but **retrieval infrastructure for the agent**: Devin uses it to locate context, so DeepWiki is the compiled layer that grounds Devin's code search. This is the same "wiki as the agent's retrieval substrate" move [[enterprise-rag-architecture|Cerebras]] makes internally.
- **Factory — AutoWiki** frames the pattern in CI terms — *"documentation should be a build artifact, not a side project."* It is the most explicitly engineered: a two-pass generation (structural scan of README/manifests/CI/entry-points, then a semantic scan of routes/endpoints/service classes/schemas/feature flags), split across **specialized agents each scoped to one facet** — a direct answer to the context problem that makes single-agent doc generation mediocre at scale (the multi-agent decomposition [[agent-failure-modes|argued about]] elsewhere). Currency is infrastructure, not discipline: `/install-wiki` writes a CI workflow refreshing the wiki on every push to the default branch, syncing into the repo's own wiki tab.
- **LangChain — OpenWiki** started as a repo-doc CLI, then split into **Code Brain** (the original repo case) and **Personal Brain**, which ingests Gmail, Notion, git, X, Hacker News, and web search into a local markdown wiki. That second mode is the significant move: from "document my repo" to "compile my working life" — the same expansion Posel warns against below.
- **Garry Tan — GBrain** is the personal-scale open-source version: markdown in git, a schema file, an auto-maintained entity-cross-link graph. No vector database, no service — the clearest demonstration the pattern is substrate-simple, and the closest analogue to this `agent-notes/` partition.

Mem0's argument from the convergence: *when independent teams solving different problems land on the same shape — markdown in git, a schema file the model obeys, synthesis at ingest, refresh on change, pages written for an agent to read — the shape is usually right.* The one axis of real divergence is currency, and it is the tell for maturity: Factory solves staleness in CI, while everyone else refreshes on demand and is therefore only as current as the last time someone ran the command. Mem0 also traces the lineage back to Vannevar Bush's 1945 **Memex** — a curated store of documents with associative trails — whose unsolved problem was *who maintains the trails*; the answer, eighty years later, is the model. That reframes *why* the pattern works: the bottleneck was never reading the sources or having the insight, it was the unbounded bookkeeping (updating cross-references, reconciling each new document against forty existing pages) that every human wiki eventually drops — and that is exactly the labor a model performs for free.

## Implications

This pattern represents a shift in how LLMs are used: from token throughput spent on code manipulation to token throughput spent on **knowledge manipulation**. The human's role moves from writer to curator and questioner.

Karpathy notes that "there is room here for an incredible new product instead of a hacky collection of scripts" — suggesting the workflow is currently assembled from ad-hoc tooling (Obsidian, Claude/ChatGPT, custom scripts) but could be productized.

The approach also implicitly argues against the necessity of complex RAG infrastructure at small-to-medium scale. If LLMs can maintain their own navigational indices and read source documents directly, the retrieval layer can be far simpler than vector-database-based approaches.

## Where it stops: the general limits

Beyond Posel's company-specific rebuttal below, Mem0 names four limits that apply to the pattern even in its home territory of stable external corpora:

- **Scale.** Index-first with no embeddings is a moderate-scale technique — Karpathy's own ~100 sources / few-hundred pages. Past that you are back to a search engine, which is why the gist itself recommends adding hybrid BM25 + vector search ([qmd](https://github.com/tobi/qmd)). This is the boundary [[enterprise-rag-architecture|Cerebras crosses]] at ~15k questions/day, where naive index-reading fails and hybrid retrieval becomes mandatory — the same spectrum, just further along it.
- **Fidelity.** Compiling at ingest means an early summary can quietly drop a detail from the source, and every later answer inherits the loss. RAG against raw chunks has no equivalent failure mode. You are trading re-derivation cost for **compression risk** — the same lossy-summary hazard [[knowledge-graph-llm-context|Ortolf]] guards against with negative-evidence and completeness signals.
- **Staleness.** A compiled page is only as true as its last refresh, and a stale wiki is *worse* than none — it is confidently wrong in a format that looks authoritative. This is why Factory's CI framing matters more than it first appears, and it is the general form of Posel's "wikis go stale outside the work."
- **Compile cost.** You pay real tokens up front to build pages you may never query, and to re-lint pages nothing changed about — the mirror image of RAG's "pay at query time."

## When the pattern breaks: the company-brain problem

Posel offers a direct rebuttal to the "build one for your company" reflex the Karpathy post inspired. His claim is narrow but sharp: **LLM wikis work for stable knowledge, but they are not company brains.** The same architecture that succeeds over a personal corpus of articles fails when pointed at an organization's living context, for three structural reasons.

1. **Business context is not repo context.** A codebase has a source of truth — you can inspect, diff, test, and re-sync the wiki when the implementation changes. A company's most important context is not the final document but the *intent behind it*: why a decision was made, which options were rejected, which customer constraint mattered, why positioning can say one thing but not another. That reasoning lives in Slack corrections, customer calls, meeting recaps, and sales objections that never become documentation. Compiling it into a clean page keeps the conclusion and drops the reasoning — and because LLMs already sound confident, a wiki missing intent becomes *confident and wrong* in ways that are hard to notice.

2. **Wikis go stale when they live outside the work.** Notion, Drive, and internal docs rot for the same reason: they must be maintained separately from where work happens. If the update path is "someone should go fix the wiki," it falls behind — and non-technical teams will not manage another knowledge layer on top of Slack, email, Linear, HubSpot, and support tickets. Unless changes become memory *automatically* as work happens, people stop checking it.

3. **Governance gets hard fast.** Business context is not equally shareable — some is customer-, team-, or founder-only; much is sensitive (pricing, HR, legal, investors). A generated wiki raises questions it cannot answer: who can see this, where did the claim come from, is it still true, was it inferred from one Slack message or confirmed in a meeting? Without provenance, permissions, and freshness, teams don't trust it with real context — so they connect only sanitized docs, the wiki stays shallow, the answers stay generic, and the "company brain" gets written off.

The unifying point is that a *system of record* (code, stable docs) compiles cleanly into a wiki, whereas a *system of engagement* (the messy stream of decisions-in-progress) does not — a distinction [[agent-harness|Taylor]] draws for why systems-of-engagement decay while systems-of-record endure. Posel's prescription is that the wiki should be *one view* of a larger memory system that captures intent, corrections, exceptions, and permissions as they happen — "but if the wiki *is* the system, it fails."

This is a governance/provenance argument that runs parallel to [[knowledge-graph-llm-context|Ortolf's]] finding that the *serialization* of context — negative evidence, source-and-date provenance, completeness signals — matters more than the raw facts, and to the "memory poisoning" failure mode in [[agent-failure-modes]] (source + date stamping, working-vs-durable layers, drift checks). All three converge on the same lesson: a knowledge base's value is bounded less by what it contains than by whether a reader can tell where each claim came from, whether it's current, and what it's missing.

## A wiki is not memory

Mem0's sharpest contribution — and the point where its status as a memory-layer vendor's blog is worth keeping in view — is a vocabulary distinction. As these systems get marketed as "memory" (LangChain literally calls OpenWiki a "wiki memory layer"), Mem0 argues the word is doing double duty across two different axes:

- **Corpus knowledge** — what a wiki does. Compile what a set of documents, a repository, or your Gmail archive *says*. It answers "what does this body of material contain."
- **User and experience memory** — what a specific *person* prefers, decided last week, or already rejected; what an agent tried in another app yesterday and how it turned out. It is scoped to an identity rather than a corpus, accumulates from interaction rather than ingestion, and must handle contradiction, staleness, provenance, and deletion *per user*.

A wiki does the first and does not attempt the second: compiling your Gmail tells an agent what is *in* your Gmail, not that you changed your mind about a vendor in a conversation last Tuesday, or that a suggested approach already failed for you once. Mem0's pitch — unsurprisingly, since they sell it — is a dedicated layer keyed to a `user_id` that follows a person across sessions and apps and is *updated in place* when facts change rather than appended forever. Discount the product placement and the distinction still holds, and it sharpens Posel's company-brain critique: what he calls "intent" (why a decision was made, which option was rejected) is largely the user/experience axis, which is why compiling the org's *documents* into a wiki structurally cannot recover it. It is also the axis this repo's own memory files target — updated-in-place user/feedback/project facts — as a complement to, not a substitute for, the compiled wiki. The failure mode to avoid: believing you have "solved memory" because you compiled a corpus. This is the same identity-scoped, contradiction-handling memory layer whose absence drives the "memory poisoning" and proactive-recall failures in [[agent-failure-modes]] and the "business context is the bottleneck, not intelligence" lesson in [[company-wide-agent]].

## Connections

This workflow is architecturally similar to how Richard's own `agent-notes/` partition works — raw sources ingested, LLM-compiled wiki articles, index files for navigation, Obsidian as the viewer. The key differences are scale (Karpathy describes ~100 articles vs. the smaller set here) and the Q&A loop where outputs feed back into the wiki. Notably, this repo sidesteps most of Posel's objections by design: it compiles *stable external sources* (articles, papers) rather than a living org's decision stream, and it enforces provenance (`compiled_from`, `## Sources`, confidence levels) as a hard rule — the "system of record" case where LLM wikis are supposed to work.

## Sources

- Karpathy, A. (2026). "LLM Knowledge Bases." <https://x.com/karpathy/status/2039805659525644595> — [[2026-04-02-karpathy-llm-knowledge-bases|local copy]]
- Posel, J. (2026). "LLM Wiki's Don't Work." <https://x.com/jacob_posel/status/2074131848582553791> — [[2026-07-06-posel-llm-wikis-dont-work|local copy]]
- Mem0 (2026). "The State of Agent Wikis" (In Context #17). <https://x.com/mem0ai/status/2079585032587694582> — [[2026-07-21-state-of-agent-wikis|local copy]]
