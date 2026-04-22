---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-22-claude-code-skills.md
compiled_at: 2026-04-22
model: claude-opus-4-6
confidence: medium
---

# Claude Code Skills

Skills are Claude Code's primary extension mechanism — reusable, shareable packages that teach the agent new capabilities. Shihipar reports that skills have become "one of the most used extension points" in Claude Code, with hundreds in active use at Anthropic. This article synthesizes the taxonomy, design patterns, and distribution strategies that emerged from that internal usage.

A common misconception is that skills are "just markdown files." The more important insight is that a skill is a **folder** — it can include scripts, assets, data files, reference docs, and configuration alongside the prompt text. The file system itself becomes a form of context engineering.

## Taxonomy of skill types

Shihipar observes that Anthropic's skills cluster into nine recurring categories. The best skills fit cleanly into one; skills that straddle several tend to confuse the model.

1. **Library & API Reference** — explain how to correctly use a library, CLI, or SDK. Include reference code snippets and gotchas. The `frontend-design` skill at Anthropic was built by iterating with customers to push Claude past its default design taste (avoiding Inter font and purple gradients).

2. **Product Verification** — describe how to test or verify that code works. Paired with external tools (Playwright, tmux). Shihipar argues it can be worth having an engineer spend a full week making verification skills excellent. Techniques include recording video of Claude's output and enforcing programmatic assertions at each step.

3. **Data Fetching & Analysis** — connect to data and monitoring stacks. Include credential helpers, dashboard IDs, and instructions on common query workflows.

4. **Business Process & Team Automation** — automate repetitive workflows into one command. Saving previous results in log files helps the model stay consistent across executions.

5. **Code Scaffolding & Templates** — generate framework boilerplate. Especially useful when scaffolding has natural-language requirements that can't be purely covered by code generators.

6. **Code Quality & Review** — enforce org code quality standards. Can include deterministic scripts for robustness and run automatically via hooks or GitHub Actions. The `adversarial-review` pattern spawns a fresh-eyes subagent to critique, iterating until findings degrade to nitpicks.

7. **CI/CD & Deployment** — help fetch, push, and deploy code. The `babysit-pr` pattern monitors a PR, retries flaky CI, resolves merge conflicts, and enables auto-merge.

8. **Runbooks** — take a symptom (Slack thread, alert, error signature) and walk through a multi-tool investigation to produce a structured report.

9. **Infrastructure Operations** — routine maintenance with guardrails for destructive actions. The `<resource>-orphans` pattern includes a soak period and explicit user confirmation before cascading cleanup.

## Design principles for effective skills

### Focus on non-obvious knowledge

Claude already knows a lot about coding. Shihipar advises focusing skill content on information that **pushes Claude out of its normal way of thinking** — org-specific conventions, internal API quirks, failure modes the model wouldn't predict from general training.

### Build a gotchas section

Shihipar calls the gotchas section "the highest-signal content in any skill." These should be built up from actual failure points encountered during use and updated over time. This is the section that prevents Claude from repeating the same mistakes.

### Use progressive disclosure via the file system

Rather than packing everything into one markdown file, distribute content across the skill folder: `references/api.md` for detailed function signatures, `assets/template.md` for output templates, folders of examples and scripts. Tell Claude what files exist in the skill, and it reads them at appropriate times. This is [[claude-code|context engineering]] in practice — controlling what the model attends to and when.

### Avoid railroading

Because skills are reusable across many situations, overly specific instructions break in edge cases. Provide the information Claude needs but leave flexibility for it to adapt.

### Design the description field for model routing

Claude Code builds a listing of all available skills at session start. The `description` field is what the model scans to decide whether a skill matches a request. This means the description should specify **when to trigger** the skill, not summarize what it does.

### Think through first-run setup

Skills that need user context (e.g., which Slack channel to post to) should store setup information in a `config.json` within the skill directory. If the config doesn't exist, the skill prompts the user. This is a clean separation between skill logic and user-specific state.

## Persistence and memory within skills

Skills can maintain state across invocations. Options range from simple append-only log files to JSON files to SQLite databases. A `standup-post` skill might keep `standups.log` so Claude reads its own history and reports only what changed since yesterday.

Important caveat: data stored in the skill directory may be deleted on upgrade. For durable state, Anthropic provides `${CLAUDE_PLUGIN_DATA}` as a stable per-plugin folder.

## Scripts as composable building blocks

Shihipar argues that giving Claude pre-built scripts and library functions is one of the most powerful skill design patterns. Instead of reconstructing boilerplate each turn, Claude composes existing helper functions into one-off analysis scripts. This shifts the model's effort from code generation to composition and decision-making.

## On-demand hooks

Skills can register hooks that activate only when the skill is invoked and last for the session duration. This enables opinionated guardrails that would be annoying if always-on:

- `/careful` — blocks `rm -rf`, `DROP TABLE`, `force-push`, `kubectl delete` via a `PreToolUse` matcher on Bash
- `/freeze` — blocks any `Edit`/`Write` outside a specified directory, preventing accidental edits during debugging

## Distribution

Two distribution mechanisms:

1. **Check into the repo** (`.claude/skills/`) — works well for smaller teams and few repos, but each checked-in skill adds to the model's context budget.
2. **Plugin marketplace** — scales better; lets individual engineers choose which skills to install. Anthropic's internal marketplace uses an organic curation process: new skills go to a sandbox folder on GitHub, get traction via Slack, then a PR promotes them to the marketplace.

Shihipar warns that it's easy to create bad or redundant skills, so some curation method before marketplace release is important.

### Composition and measurement

Skills can reference other skills by name without formal dependency management — the model invokes them if installed. To measure skill health, Anthropic uses a `PreToolUse` hook that logs every skill invocation, letting them find popular skills and ones that undertrigger relative to expectations.

## Connections

- The progressive-disclosure and folder-structure patterns connect to [[claude-code|Cherny's "build for the model's desires" principle]] — skills are the mechanism for giving the model the tools and context it wants to reach for.
- The adversarial-review and subagent patterns in quality/review skills echo [[unattended-coding-agents|the trend toward agent swarms]] that pick up work items independently.
- On-demand hooks like `/careful` and `/freeze` are a practical implementation of the guardrail philosophy — destructive power gated by explicit user intent rather than always-on restriction.

## Sources

- Shihipar, T. (2026). "Lessons from Building Claude Code: How We Use Skills." <https://x.com/trq212/status/2033949937936085378> — [[2026-04-22-claude-code-skills|local copy]]
