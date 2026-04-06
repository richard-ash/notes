# Repo conventions

This is Richard's personal "second brain" — a hand-curated Markdown knowledge base viewed in Obsidian, versioned in git.

## Two partitions

Every note in this repo belongs to one of two partitions:

- **Personal notes** (everything outside `agent-notes/` and `private/`) — written by Richard. Authoritative. Agents must not modify these files unless explicitly asked.
- **Agent notes** (`agent-notes/`) — written by LLM agents. See `agent-notes/CLAUDE.md` for the compilation workflow and frontmatter rules.

## Boundary rules for agents

1. By default, agents write only inside `agent-notes/`. Writing into any other directory requires an explicit instruction from Richard.
2. Agents never write wikilinks *from* personal notes *to* agent notes. Richard adds those manually when he wants the connection.
3. When working inside `agent-notes/`, follow `agent-notes/CLAUDE.md`.
4. `private/` is a separate nested repo, gitignored. Do not read or write it.

## Personal-note conventions

- Plain Markdown links, not Obsidian `[[wikilinks]]` (only ~2 personal files currently use wikilinks; match the existing convention).
- Commit style: short imperative subject ("Add X", "Update Y"), no body, no `Co-Authored-By` trailer.
- `.obsidian/` is gitignored — vault config is local only.
