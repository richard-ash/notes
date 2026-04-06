# agent-notes

The **messy, agent-facing partition** of Richard's notes vault, following the Karpathy/kepano knowledge-base pattern.

## What lives here

- `raw/` — source documents (articles, papers, transcripts, images). One file per source. **Gitignored.**
- `wiki/` — LLM-compiled articles derived from raw sources. **Tracked in git.** Organized by domain, mirroring the personal vault taxonomy (`computer-science/`, `biology/`, `engineering/`, ...).

## What does NOT live here

- Richard's hand-written notes (those live in top-level domain directories: `biology/`, `computer-science/`, etc.).
- Private notes (those live in `private/`, a separate nested repo).

## How to use it

- **Ingest a source:** drop a file in `raw/<domain>/<YYYY-MM-DD>-<slug>.md` (or paste a URL) and run `/ingest <path>`.
- **Query:** ask an agent a question. It routes via `wiki/**/index.md` files and reads specific articles.
- **Cite from a personal note:** write a wikilink like `[[agent-notes/wiki/computer-science/mixture-of-experts|MoE research]]`.

## Contamination mitigations

Single vault + shared graph means search/backlinks/quick-switcher will surface agent content. Mitigated by:

1. **Path prefix** — every agent file lives under `agent-notes/`.
2. **Frontmatter** — every wiki article has `source: agent`.
3. **Obsidian "Excluded files"** — add `agent-notes/` to keep it out of the default graph/search; toggle off when researching.
4. **Directional links** — agent never writes *into* personal notes.

See `CLAUDE.md` in this directory for the full workflow rules.
