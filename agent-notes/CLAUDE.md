# agent-notes — LLM workflow rules

This partition is agent-owned. Richard does not hand-edit these files (except to fix egregious errors). Everything here is either an ingested raw source or an LLM-compiled wiki article derived from raw sources.

## Structure

```
agent-notes/
├── raw/                        # gitignored, one file per source
│   └── <domain>/<YYYY-MM-DD>-<slug>.md
├── wiki/                       # tracked, compiled articles
│   ├── index.md                # top-level domain directory
│   └── <domain>/
│       ├── index.md            # one-line summaries of this domain's articles
│       └── <slug>.md
└── index.md                    # top-level summary of the whole agent vault
```

Domains mirror the personal vault taxonomy where possible (`computer-science/`, `biology/`, `engineering/civil/`, etc.). Agent-notes may pioneer new sub-domains not yet present in the personal vault — choose paths that would be sensible mirrors if Richard later creates the corresponding personal directory.

## The four disciplines

1. **Path is the boundary.** Write only under `agent-notes/`. Never edit personal notes.
2. **Provenance on every wiki file.** Every `wiki/**/*.md` article has `source: agent` frontmatter and a `compiled_from:` list pointing at the raw file(s) it was derived from.
3. **Links outward only within the partition.** Wiki → Wiki ✅, Wiki → Raw ✅. Wiki → Personal ❌. Raw files are read-only sources; do not rewrite their body text.
4. **URL in Sources section.** Every source listed in `compiled_from` appears in the article's `## Sources` section with its canonical URL inline (so personal-note hover-preview shows the URL), followed by a `[[wikilink]]` to the local raw file.

## Frontmatter templates

### Raw file — `agent-notes/raw/<domain>/<YYYY-MM-DD>-<slug>.md`

Two ingest paths produce raw files with slightly different schemas:

**Obsidian Web Clipper** (user pastes or clips directly) — adopt Web Clipper's schema as-is:

```yaml
---
title: "Article Title"
source: "https://example.com/article"
author:
  - "[[Author Name]]"
published: YYYY-MM-DD
created: YYYY-MM-DD
description: "One-line description"
tags:
  - clippings
type: article       # article | paper | video | transcript | book | other
---
```

**WebFetch** (agent fetches a URL):

```yaml
---
title: "Article Title"
source: "https://example.com/article"
author: Author Name
published: YYYY-MM-DD
created: YYYY-MM-DD
type: article       # article | paper | video | transcript | book | other
---
```

Key fields:
- `source`: canonical URL of the original content
- `published`: when the source was originally published
- `created`: when the raw file was captured (today's date)
- `type`: article | paper | video | transcript | book | other
- `author`: plain string or list of `[[wikilinks]]` (Web Clipper uses the latter)

Body: full raw content of the source. Do not rewrite or editorialize in raw files.

### Wiki article — `agent-notes/wiki/<domain>/<slug>.md`

```yaml
---
source: agent
compiled_from:
  - agent-notes/raw/<domain>/<YYYY-MM-DD>-<slug>.md
compiled_at: YYYY-MM-DD
model: <model-id>
confidence: high    # high | medium | low
---

# <Article Title>

<body with [[wikilinks]] to other wiki articles; no links into personal notes>

## Sources
- Author (YYYY). "Title." <https://example.com/url> — [[YYYY-MM-DD-slug|local copy]]
```

**Confidence semantics:**
- `high` — factual content, well-sourced, multiple inputs or verifiable claims
- `medium` — single opinionated source, or wiki article primarily reflects one perspective
- `low` — speculative, poorly sourced, or derived from a potentially incomplete fetch

## The ingest workflow

Given a path to a raw file, a URL to fetch, or pasted content:

1. **Capture the raw file.**
   - If URL: fetch via WebFetch, clean to markdown, write to `agent-notes/raw/<domain>/<YYYY-MM-DD>-<slug>.md`.
   - If pasted content (from Web Clipper): save directly with the user's frontmatter intact, adding `type:` if missing.
   - If file path: read the existing raw file.
   - **Domain selection:** choose the domain that mirrors the closest personal-vault directory. If the topic clearly fits an existing domain, use it. If unclear, ask. Agent-notes may create sub-domains not yet in the personal vault.
2. **Read the raw file** and determine the primary concept(s).
3. **Check `agent-notes/wiki/<domain>/`** for an existing wiki article on that concept.
   - **If exists:** integrate the new information. Append the raw file to `compiled_from`. Update `compiled_at`. Add a new line to `## Sources` (URL + wikilink).
   - **If not:** create a new wiki article using the template above.
4. **Cross-link.** Add `[[wikilinks]]` in the body to other wiki articles where concepts overlap. Only to other agent wiki articles — never to personal notes.
5. **Update the domain index.** `agent-notes/wiki/<domain>/index.md` must list this article with a one-line summary.
6. **Update top-level index** (`agent-notes/index.md`) if a new domain was added.

## Wiki article naming

Name wiki articles after the **durable concept or primary subject**, not the source. This allows future sources on the same topic to integrate into the same wiki article.

Examples from this repo:
- Source about Israel's water infrastructure → `israel-water-miracle.md` (the country's infrastructure story is the durable subject)
- Source reviewing *Scaling People* → `scaling-people.md` (the book is the anchor; future reviews or reading notes integrate here)
- Source about a specific dev technique → `stacked-pull-requests.md` (the technique is the concept)

## Compilation guidelines

**Add value beyond the raw source.** The wiki article should not just summarize — it should:
- Explain implications the source leaves implicit
- Note what has changed since publication for older articles (add a `## Temporal notes` section only when specific claims, tools, or recommendations are materially outdated)
- Connect ideas to related concepts via `[[wikilinks]]`

**Attribute opinions to their sources.** When the source is opinionated (reviews, essays, arguments), the wiki article should frame claims as "Psmith argues..." or "Zuegel observes..." rather than presenting them as objective fact.

## Index file shapes

### `agent-notes/wiki/<domain>/index.md`

```markdown
# <Domain>
One-sentence scope of this domain within agent-notes.

## Articles
- [[slug-a]] — one-line summary
- [[slug-b]] — one-line summary
```

### `agent-notes/index.md`

Top-level list of all domains with article counts and a one-line scope each. Refreshed whenever a new domain is added or an article count changes.

## Things the agent must NOT do

- Rewrite raw files (body text is read-only after capture).
- Create wiki articles without at least one entry in `compiled_from`.
- Write links from wiki articles into personal-note paths.
- Edit files outside `agent-notes/`.
- Add `Co-Authored-By` trailers to commits (see repo-root `CLAUDE.md`).
