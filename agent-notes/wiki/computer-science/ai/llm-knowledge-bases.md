---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-04-02-karpathy-llm-knowledge-bases.md
  - agent-notes/raw/computer-science/ai/2026-07-06-posel-llm-wikis-dont-work.md
compiled_at: 2026-07-07
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

## Implications

This pattern represents a shift in how LLMs are used: from token throughput spent on code manipulation to token throughput spent on **knowledge manipulation**. The human's role moves from writer to curator and questioner.

Karpathy notes that "there is room here for an incredible new product instead of a hacky collection of scripts" — suggesting the workflow is currently assembled from ad-hoc tooling (Obsidian, Claude/ChatGPT, custom scripts) but could be productized.

The approach also implicitly argues against the necessity of complex RAG infrastructure at small-to-medium scale. If LLMs can maintain their own navigational indices and read source documents directly, the retrieval layer can be far simpler than vector-database-based approaches.

## When the pattern breaks: the company-brain problem

Posel offers a direct rebuttal to the "build one for your company" reflex the Karpathy post inspired. His claim is narrow but sharp: **LLM wikis work for stable knowledge, but they are not company brains.** The same architecture that succeeds over a personal corpus of articles fails when pointed at an organization's living context, for three structural reasons.

1. **Business context is not repo context.** A codebase has a source of truth — you can inspect, diff, test, and re-sync the wiki when the implementation changes. A company's most important context is not the final document but the *intent behind it*: why a decision was made, which options were rejected, which customer constraint mattered, why positioning can say one thing but not another. That reasoning lives in Slack corrections, customer calls, meeting recaps, and sales objections that never become documentation. Compiling it into a clean page keeps the conclusion and drops the reasoning — and because LLMs already sound confident, a wiki missing intent becomes *confident and wrong* in ways that are hard to notice.

2. **Wikis go stale when they live outside the work.** Notion, Drive, and internal docs rot for the same reason: they must be maintained separately from where work happens. If the update path is "someone should go fix the wiki," it falls behind — and non-technical teams will not manage another knowledge layer on top of Slack, email, Linear, HubSpot, and support tickets. Unless changes become memory *automatically* as work happens, people stop checking it.

3. **Governance gets hard fast.** Business context is not equally shareable — some is customer-, team-, or founder-only; much is sensitive (pricing, HR, legal, investors). A generated wiki raises questions it cannot answer: who can see this, where did the claim come from, is it still true, was it inferred from one Slack message or confirmed in a meeting? Without provenance, permissions, and freshness, teams don't trust it with real context — so they connect only sanitized docs, the wiki stays shallow, the answers stay generic, and the "company brain" gets written off.

The unifying point is that a *system of record* (code, stable docs) compiles cleanly into a wiki, whereas a *system of engagement* (the messy stream of decisions-in-progress) does not — a distinction [[agent-harness|Taylor]] draws for why systems-of-engagement decay while systems-of-record endure. Posel's prescription is that the wiki should be *one view* of a larger memory system that captures intent, corrections, exceptions, and permissions as they happen — "but if the wiki *is* the system, it fails."

This is a governance/provenance argument that runs parallel to [[knowledge-graph-llm-context|Ortolf's]] finding that the *serialization* of context — negative evidence, source-and-date provenance, completeness signals — matters more than the raw facts, and to the "memory poisoning" failure mode in [[agent-failure-modes]] (source + date stamping, working-vs-durable layers, drift checks). All three converge on the same lesson: a knowledge base's value is bounded less by what it contains than by whether a reader can tell where each claim came from, whether it's current, and what it's missing.

## Connections

This workflow is architecturally similar to how Richard's own `agent-notes/` partition works — raw sources ingested, LLM-compiled wiki articles, index files for navigation, Obsidian as the viewer. The key differences are scale (Karpathy describes ~100 articles vs. the smaller set here) and the Q&A loop where outputs feed back into the wiki. Notably, this repo sidesteps most of Posel's objections by design: it compiles *stable external sources* (articles, papers) rather than a living org's decision stream, and it enforces provenance (`compiled_from`, `## Sources`, confidence levels) as a hard rule — the "system of record" case where LLM wikis are supposed to work.

## Sources

- Karpathy, A. (2026). "LLM Knowledge Bases." <https://x.com/karpathy/status/2039805659525644595> — [[2026-04-02-karpathy-llm-knowledge-bases|local copy]]
- Posel, J. (2026). "LLM Wiki's Don't Work." <https://x.com/jacob_posel/status/2074131848582553791> — [[2026-07-06-posel-llm-wikis-dont-work|local copy]]
