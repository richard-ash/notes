---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-07-08-claire-vo-custom-harness.md
compiled_at: 2026-07-09
model: claude-opus-4-8
confidence: medium
---

# Building Custom Harnesses

A **custom harness** is a bespoke wrapper you build around a general-purpose agent runtime to make it do *one specific workflow* well — with baked-in context, constrained actions, and a fixed set of outcomes. Claire Vo (ChatPRD founder, *How I AI* host) builds one live: a Sentry bug-triage harness on the Claude Agent SDK with a custom Ink terminal UI and opinionated adapters for Sentry, Linear, GitHub, and Vercel. The episode's purpose is to demystify a term that has become jargon — "everybody's saying it's not the model, it's the harness, but nobody's saying *what* a harness is."

This is the practitioner's build-your-own angle on the harness idea, distinct from the three neighboring senses in this wiki:

- [[ai-coding-harnesses]] — the *anatomy* of a general coding harness (the tool-call loop inside Claude Code, Cursor, Codex).
- [[harness-engineering]] — Lopopolo's OpenAI practice of shaping a whole repo/environment so agents can run unsupervised.
- [[agent-harness]] — Taylor's thesis that businesses should expose their *product* to agents (skills/docs/rules) alongside the web app + API.

Vo's contribution is the missing rung: **when and how an individual builder wraps an agent SDK into a vertical tool for a repeated business job.** Her working definition is deliberately deflationary — "a harness is just code around an AI agent that makes it more effective" — and she ends by hypothesizing that *a wrapper is just a harness*, which retroactively reframes everything she's vibe-coded as harness-building.

## The three components

Vo reduces a harness to three parts, mapping onto the classic agent triad:

1. **Specific context** — not "you are Claude Code, make no mistakes," but "you are working inside the ChatPRD engineering harness; here is the plan to attack this specific problem; return X, Y, Z." Encoded as a hard-wired step, not a skill you hope gets invoked.
2. **Specific actions** — an explicit, constrained tool policy: which tools may be called, which may not. Her run has flags gating whether the agent may edit source, modify inputs, or message customers — each off by default and enabled only with approval.
3. **Specific outcomes** — a fixed artifact bundle produced every time (see below), so the workflow's output is standardized for the whole team.

## When to build one (vs. just using Claude Code)

Build a harness, Vo argues, **when the same workflow needs the same setup and the same outcomes** — a mix of deterministic and non-deterministic steps you run repeatedly. Her non-coding examples: production-incident management, release-prep, support escalations, migrations, even "do research in a specific way" or "consolidate docs in a specific way." Coding harnesses are just the most popular instance because coding is a high-frequency job with standard tools.

The payoff over a general-purpose tool is **not raw capability — it's the removal of per-invocation prompting and babysitting:**

- **Intent is pre-loaded.** With Claude Code she'd type "dear agent, please fix this bug, here's the link." With the harness she pastes the Sentry link and the agent already knows the job. (This is the same "the harness carries the intent" logic as [[agent-harness]], turned inward on your own workflow.)
- **Permissions are structural, not prompted.** An "investigate-only" harness *cannot* write code because the tool policy forbids it — no need to plead "only investigate, don't ship a fix" and hope it holds.
- **The process repeats identically every time.** Every closed bug gets a Linear issue, a report, and optional customer follow-up. You *could* encode this in a skill, "but then you have to babysit it" — the harness guarantees it.
- **Multi-model routing** becomes available in ways a single general-purpose tool doesn't expose.

The through-line is Vo's reframe of how work gets done: instead of one open chat field where "if I just type, the agent will do good work," you **constrain a narrow problem tightly and let a general-purpose agent orchestrate the constrained pieces.** This is the constellation/supervisor instinct of [[agent-harness]] and the thin-orchestration layer of Garry Tan's [[agentic-engineering-architecture]], arrived at from a builder's chair.

## The Sentry worked example

**Architecture.** Front end (TUI or CLI) → a **run** → a **task** with a specific input (a Sentry issue) → per-run flags (edit-source / modify-input / message-customer, approval-gated). The core runs on the **Claude Agent SDK** — which supplies Claude Code's primitives (grep files, write files) — and connects to real tools: Sentry, Vercel, Linear, GitHub, running **Sonnet 4.6** as "the right model for the job." An **artifact store** persists all run evidence to the filesystem for future reuse (she notes this echoes other harnesses like OpenCLAW).

**Opinionated adapters, not generic MCP.** The load-bearing design choice: rather than hand the agent a generic Sentry MCP and let it "wander through all these traces," she wrote an adapter that pulls *exactly* what a bug report needs and nothing else. Same for Linear/Vercel/GitHub — "not generally how you can use these tools, but specifically how you'd use them when hunting a bug." This is the opinionated-connector counterpart to [[ai-coding-harnesses]]'s point that the harness shapes behavior more than the model: narrowing the tool surface is itself the engineering. (Contrast the "internalize the dependency" instinct in [[harness-engineering]] — both prefer a tight, purpose-built integration over an opaque general one.)

**The artifact bundle** — the standardized outcome, emitted every run: the full task run (all messages), a brief of what was discovered, relevant logs, what the Claude worker did, an output summary, plus a rendered HTML report and a worker report. In the live run the output was an *investigation brief*: confirmed evidence (real Sentry warning, 150 users, hourly, warning-not-error, Vercel logs unavailable), priority-ranked root-cause hypotheses (invalid / overlapping original range) plus a flagged blind spot, the exact product surface, a verification step (fetch a raw Sentry event), a recommendation to open a Linear issue and assign it, and a judgment that it should *not* auto-fix yet — needs more information. Every one of those fields exists because Vo pre-specified them as the required outcome.

## Building the harness *with* agents — where the models resisted

A sharp meta-observation for anyone replicating this: Vo ran **dueling Claude Code and Codex sessions** (Opus and GPT-5.5) to build the harness, and **both models resisted putting any AI inside the harness** — they kept trying to build something fully deterministic. She had to prompt very specifically to get an AI-in-the-loop design. Practical advice that follows:

- Be very specific about the workflow, the tools, and *where custom prompts belong.*
- Use an agent SDK (Claude's or OpenAI's) to run most of it — without that framing she "did not get what I wanted."
- Amusingly, **Codex did the best job building the agent, but implemented it using the Claude Agent SDK** — spanning models and coding agents.

The finished harness is small — an index into the TUI, ~8 files, the source-adapters, a `bug-hunter` workflow, and TUI/CLI runners. It exposes both a human TUI ("made cute" with Ink) and direct CLI invocation with tool flags, underscoring her point that the interface is a free choice: TUI, CLI, or web app.

## How to build your own — the checklist

Vo's closing recipe:

1. Identify a specific, repeated workflow and **write it down** (paper, HTML, markdown).
2. Determine what a *run against a task* looks like.
3. Make **opinionated adapters** to your tools/data sources — not just "use an MCP."
4. Decide the **structured artifacts** the workflow should emit.
5. Decide the **rules and permissions** — which tools it may and may not use.
6. Pick the runtime — Claude Code, Codex, or a model router.
7. Build a **surface** to interact with it (TUI / CLI / web app).
8. Plug the spec into a coding agent, have it build the harness, and **test against real data.**

## Synthesis

Vo's episode is the most accessible on-ramp to the harness concept, but its real value is the **"a wrapper is just a harness" collapse** — it dissolves the distinction between "build a harness" and "build a normal app around an LLM." Under that lens, Cursor and Claude Code are just *complex, general* harnesses; her bug-triage tool is a *simple, vertical* one; and the design work is identical in kind, differing only in breadth. This is the demand-side, single-builder mirror of the supply-side org accounts ([[harness-engineering]], [[enterprise-agentic-coding-adoption]], [[agentic-pods]]): the same "the leverage is in the scaffolding, not the model" thesis, sized down to a weekend project one person can ship. It also sits underneath [[agent-failure-modes]] — a tightly-scoped vertical harness is precisely the antidote to the overbuilding/tool-space-interference failure mode that afflicts one giant general-purpose agent.

The unstated caveat (compare [[patron-not-wizard]] and [[agi-timelines]]): much of the value here is *constraint* — narrow tools, fixed outcomes, forbidden actions. As base models get more capable and reliable at self-constraining, the marginal payoff of hand-built vertical harnesses may shrink for exactly the workflows where it's largest today. The durable part is likely the opinionated adapters and the standardized artifact bundle, not the surrounding orchestration.

## Sources
- Vo, C. / *How I AI* (2026). "How to build a custom AI harness with Claude SDK." <https://www.youtube.com/watch?v=ofS-4RRw9zw> — [[2026-07-08-claire-vo-custom-harness|local copy]]
