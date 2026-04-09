---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-04-02-karpathy-llm-knowledge-bases.md
compiled_at: 2026-04-09
model: claude-opus-4-6
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

## Connections

This workflow is architecturally similar to how Richard's own `agent-notes/` partition works — raw sources ingested, LLM-compiled wiki articles, index files for navigation, Obsidian as the viewer. The key differences are scale (Karpathy describes ~100 articles vs. the smaller set here) and the Q&A loop where outputs feed back into the wiki.

## Sources

- Karpathy, A. (2026). "LLM Knowledge Bases." <https://x.com/karpathy/status/2039805659525644595> — [[2026-04-02-karpathy-llm-knowledge-bases|local copy]]
