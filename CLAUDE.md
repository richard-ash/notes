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

- Use Obsidian `[[wikilinks]]` for links between personal notes. Use plain Markdown links only for external URLs.
- Commit style: short imperative subject ("Add X", "Update Y"), no body, no `Co-Authored-By` trailer.
- `.obsidian/` is gitignored — vault config is local only.

## gstack

Use the `/browse` skill from gstack for all web browsing. Never use `mcp__claude-in-chrome__*` tools.

Available skills: `/office-hours`, `/plan-ceo-review`, `/plan-eng-review`, `/plan-design-review`, `/design-consultation`, `/design-shotgun`, `/design-html`, `/review`, `/ship`, `/land-and-deploy`, `/canary`, `/benchmark`, `/browse`, `/connect-chrome`, `/qa`, `/qa-only`, `/design-review`, `/setup-browser-cookies`, `/setup-deploy`, `/retro`, `/investigate`, `/document-release`, `/codex`, `/cso`, `/autoplan`, `/plan-devex-review`, `/devex-review`, `/careful`, `/freeze`, `/guard`, `/unfreeze`, `/gstack-upgrade`, `/learn`.

## Skill routing

When the user's request matches an available skill, ALWAYS invoke it using the Skill
tool as your FIRST action. Do NOT answer directly, do NOT use other tools first.
The skill has specialized workflows that produce better results than ad-hoc answers.

Key routing rules:
- Product ideas, "is this worth building", brainstorming → invoke office-hours
- Bugs, errors, "why is this broken", 500 errors → invoke investigate
- Ship, deploy, push, create PR → invoke ship
- QA, test the site, find bugs → invoke qa
- Code review, check my diff → invoke review
- Update docs after shipping → invoke document-release
- Weekly retro → invoke retro
- Design system, brand → invoke design-consultation
- Visual audit, design polish → invoke design-review
- Architecture review → invoke plan-eng-review
- Save progress, checkpoint, resume → invoke checkpoint
- Code quality, health check → invoke health
