---
name: ingest
description: Ingest a URL, file path, or pasted article into agent-notes. Saves raw source, compiles wiki article, updates indexes.
allowed-tools: Read Write Edit Glob Grep WebFetch Bash
argument-hint: "[url or file path]"
---

Ingest a source into the agent-notes knowledge base.

**Input:** $ARGUMENTS

Read `agent-notes/CLAUDE.md` first — it defines frontmatter templates, naming conventions, the four disciplines, and compilation guidelines. Follow it exactly.

## Determine input type

- **URL** (starts with http/https): Fetch the article via WebFetch. Determine the appropriate domain. Save as a raw file at `agent-notes/raw/<domain>/<YYYY-MM-DD>-<slug>.md`. Then compile.
- **File path** (points to an existing file): Read the raw file at that path and compile a wiki article from it.
- **Pasted content** (content follows this prompt in the user's message): Save as a raw file preserving any existing frontmatter (e.g. from Obsidian Web Clipper), adding `type:` if missing. Then compile.
- **Empty or unclear**: Ask what to ingest.

## Workflow

1. Save or read the raw file per the templates in `agent-notes/CLAUDE.md`.
2. Determine primary concept(s) and select the wiki slug — name after the **durable concept**, not the source article.
3. Read `agent-notes/index.md` to see existing domains. Check `agent-notes/wiki/<domain>/` for existing articles on the same concept.
   - If an existing article covers this concept: **integrate** (append to `compiled_from`, update `compiled_at`, add to `## Sources`, weave new info into the body).
   - If no match: **create** a new wiki article.
4. Cross-link to other wiki articles via `[[wikilinks]]` where concepts overlap.
5. Update `agent-notes/wiki/<domain>/index.md` — create if this is a new domain.
6. Update `agent-notes/index.md` if a new domain was added or article count changed.

## Key rules

- Every wiki `## Sources` entry: canonical URL inline first, then `[[wikilink]]` to local raw copy.
- Add synthesis value beyond the raw source: implications, temporal notes for old articles, connections between concepts. But attribute opinions to their sources ("Psmith argues...", not stated as fact).
- Confidence: `high` (factual, well-sourced), `medium` (opinionated or single-source), `low` (speculative or incomplete).
- Never write links from wiki articles into personal-note paths.
- Never edit files outside `agent-notes/`.
- Domain selection: mirror the personal vault's directory structure where possible. If no personal-vault domain fits, create a new sub-domain that would be a sensible mirror.
