---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-02-10-harness-engineering.md
compiled_at: 2026-06-25
model: claude-opus-4-8
confidence: medium
---

# Harness Engineering

**Harness engineering** is the discipline of designing the *environment* an autonomous coding agent operates in — tools, scaffolding, documentation, feedback loops, and mechanical constraints — rather than writing the application code itself. The term comes from a February 2026 OpenAI post by Ryan Lopopolo describing an internal experiment: building and shipping a real software product (internal beta, hundreds of users) with **0 lines of manually-written code**. Over five months, a team that grew from three to seven engineers drove Codex to produce ~1M lines of code across ~1,500 merged PRs (≈3.5 PRs/engineer/day), estimated at ~1/10th the hand-coding time.

The slogan is **"humans steer, agents execute."** The central reframe: when a team's job is no longer to write code, the scarce resource becomes *human time and attention*, and the engineer's work shifts to building the harness that lets agents do reliable work unsupervised. This is the OpenAI-internal companion to the externally-observed [[agentic-engineering]] discipline (Willison/Karpathy) and the [[enterprise-agentic-coding-adoption|Airbnb adoption account]] — same era, same direction, but reported from inside a fully agent-generated codebase.

> **Terminology note.** "Harness" here is broader than in [[ai-coding-harnesses]], where it means the *program* wrapping the LLM (Claude Code, Codex CLI). Harness *engineering* is the practice of shaping the whole repo-and-tooling environment around that program. The two senses are compatible: harness engineering is what you do to the codebase; the coding harness is one tool inside it.

## The core constraint shapes everything

OpenAI deliberately chose "no manually-written code" as a forcing function. The point wasn't purity — it was that the *only* way to make progress is to make the agent capable, so every failure becomes a systems question instead of a "write it yourself" escape hatch. When something broke, the fix was never "try harder." Engineers asked: **"what capability is missing, and how do we make it both legible and enforceable for the agent?"**

Work proceeds **depth-first**: decompose a goal into building blocks (design, code, review, test), have the agent construct each block, then use those blocks to unlock harder tasks. The early bottleneck wasn't model capability — it was an *underspecified environment*. The slow start was the agent lacking tools, abstractions, and structure, not lacking intelligence.

## Agent legibility is the goal

The governing principle: **from the agent's point of view, anything it can't access in-context while running effectively doesn't exist.** Knowledge in Google Docs, Slack threads, or people's heads is invisible to the system — illegible in the same way it would be to a new hire who joined three months after a decision was made. So the repository is optimized first for *Codex's legibility*, the way a human-first codebase is optimized for new-hire navigability.

The operational consequence is that you must continuously **push context into the repo** as versioned, repo-local artifacts (code, markdown, schemas, executable plans). This drives concrete tradeoffs:

- **Favor "boring" technologies** — composable, API-stable, well-represented in the training set, so the agent can fully model them in-repo.
- **Sometimes reimplement rather than depend.** Rather than pull in a generic `p-limit`-style library, they wrote their own map-with-concurrency helper: tightly integrated with their OpenTelemetry instrumentation, 100% test coverage, behaving exactly as the runtime expects. Opaque upstream behavior costs more than reimplementing a subset. (Compare [[agent-harness]]'s "internalize the system" instinct and the general agent-native-infrastructure thread in [[agentic-engineering]].)

## Repository knowledge as the system of record

The earliest hard-won lesson: **"give Codex a map, not a 1,000-page instruction manual."** The "one big `AGENTS.md`" approach failed predictably — context is scarce (a giant file crowds out the actual task), too much guidance becomes non-guidance (when everything is important, nothing is), it rots into a graveyard of stale rules, and a single blob resists mechanical verification.

The fix is **progressive disclosure**: a short `AGENTS.md` (~100 lines) acts as a *table of contents*, pointing into a structured `docs/` directory that is the real system of record:

- **Design docs** — catalogued and indexed with verification status, plus a `core-beliefs.md` of agent-first operating principles.
- **`ARCHITECTURE.md`** — top-level map of domains and package layering (the matklad convention).
- **A quality document** — grades each product domain and architectural layer, tracking gaps over time.
- **Execution plans** as first-class artifacts — lightweight ephemeral plans for small changes; checked-in [exec plans](https://cookbook.openai.com/articles/codex_exec_plans) with progress and decision logs for complex work. Active, completed, and tech-debt plans are versioned and co-located so agents need no external context.
- **`references/*-llms.txt`** — vendored LLM-friendly docs for dependencies (design system, nixpacks, uv).

This is the same instinct as the [[llm-knowledge-bases|markdown-knowledge-base]] pattern — a structured, navigable wiki the model reads — applied to an entire engineering org. Crucially, **it's enforced mechanically**: linters and CI jobs validate the knowledge base is current, cross-linked, and well-structured, and a recurring **"doc-gardening" agent** scans for docs that no longer reflect real code behavior and opens fix-up PRs.

## Application legibility: making the running system observable to the agent

As throughput rose, the bottleneck moved to human QA. The response was to make the *running application* — UI, logs, metrics, traces — directly legible to Codex, so the agent can validate its own work instead of waiting on a human:

- **Per-worktree bootable app.** Each change gets its own running instance, so the agent can launch and drive it in isolation.
- **Chrome DevTools Protocol wired into the runtime**, with skills for DOM snapshots, screenshots, and navigation — so the agent reproduces bugs, validates fixes, and reasons about UI behavior directly (snapshot-before / trigger / snapshot-after / fix / restart / re-validate loop).
- **Ephemeral per-worktree observability stack.** Logs/metrics/traces flow through Vector into Victoria Logs/Metrics/Traces, queryable by the agent via LogQL/PromQL/TraceQL and torn down when the task completes. This makes performance prompts tractable: *"ensure service startup completes in under 800ms"* or *"no span in these four critical journeys exceeds two seconds."*

With these loops closed, single Codex runs routinely work a task for **upwards of six hours**, often overnight.

## Enforcing architecture and taste mechanically

Documentation alone won't keep a fully agent-generated codebase coherent — because Codex faithfully **replicates existing patterns, including the bad ones**. The principle: **enforce invariants, not implementations.** Care deeply about boundaries, correctness, and reproducibility; allow agents freedom in how solutions are expressed within them. (E.g., require [parse-don't-validate](https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/) at boundaries, but don't mandate Zod — the model picked it on its own.)

The codebase uses a **rigid layered domain architecture**: within each business domain, code may only depend "forward" through fixed layers (Types → Config → Repo → Service → Runtime → UI). Cross-cutting concerns (auth, connectors, telemetry, feature flags) enter only through a single **Providers** interface. Everything else is disallowed and enforced via custom (Codex-generated) linters and structural tests. Additional "taste invariants" are statically enforced: structured logging, schema/type naming, file-size limits, reliability requirements. Because the lints are custom, **error messages inject remediation instructions into the agent's context** — the failure teaches the agent how to fix it.

The mindset is **platform-org leadership**: enforce boundaries centrally, allow autonomy locally. This is architecture you'd usually postpone until hundreds of engineers; with agents it's an *early prerequisite*, because the constraints are precisely what allows speed without architectural drift. Human taste is fed back continuously — review comments, refactor PRs, and user-facing bugs become doc updates or encoded tooling. **"When documentation falls short, we promote the rule into code."**

## Throughput changes the merge philosophy

High agent throughput inverts conventional norms. The repo runs with **minimal blocking merge gates**, short-lived PRs, and treats test flakes with follow-up runs rather than indefinite blocking. The logic: when agent throughput far exceeds human attention, **corrections are cheap and waiting is expensive.** Lopopolo is explicit that this would be irresponsible in a low-throughput environment — it's a tradeoff that only pencils out at high agent velocity. (Contrast [[ai-code-review]]'s slower, quality-reinvestment stance — both reinvest agent velocity, but harness engineering spends it on throughput-plus-GC where Lawson spends it on depth.)

Review itself is pushed **agent-to-agent**: humans may review PRs but aren't required to. To drive a PR home, Codex reviews its own changes locally, requests specific agent reviews (local and cloud), responds to feedback, and loops until all agent reviewers are satisfied — a **[Ralph Wiggum loop](https://ghuntley.com/loop/)**.

## Entropy and garbage collection

Full autonomy creates a novel failure mode: **drift**, as the agent compounds uneven patterns. OpenAI's first attempt was manual — every Friday (20% of the week) spent cleaning "AI slop" — which didn't scale. The replacement is automated **garbage collection**:

- Encode **"golden principles"** — opinionated, mechanical rules — directly in the repo (e.g. *prefer shared utility packages over hand-rolled helpers*; *don't probe data "YOLO-style" — validate boundaries or use typed SDKs so the agent never builds on guessed shapes*).
- Run **background Codex tasks on a cadence** that scan for deviations, update quality grades, and open targeted refactor PRs — most reviewable in under a minute and automerged.

The framing: **technical debt is a high-interest loan**, cheaper to pay down continuously in small increments than to let compound. Human taste is captured once, then enforced on every line forever.

## The autonomy threshold

By the time of writing, the repo had crossed a threshold where a single prompt can drive an end-to-end feature: validate codebase state → reproduce a reported bug → **record a video of the failure** → implement a fix → validate by driving the app → **record a second video of the resolution** → open a PR → respond to agent and human feedback → remediate build failures → escalate to a human only when judgment is required → merge.

Lopopolo is careful: this **depends heavily on the specific structure and tooling** of this repo and **should not be assumed to generalize** without comparable investment. That caveat is the load-bearing claim of the whole post — the result is a property of the *harness*, not the model. It echoes [[ai-coding-harnesses]]'s benchmark point (same model, different harness, large accuracy swing) at the scale of an entire engineering org.

## Open questions

OpenAI flags what they don't yet know: how architectural coherence evolves over *years* in a fully agent-generated system; where human judgment adds the most leverage and how to encode it so it compounds; and how the whole apparatus shifts as models get more capable (much of today's scaffolding may be a temporary crutch — cf. [[patron-not-wizard]] and [[agi-timelines]] on how fast the capability floor is rising). The closing thesis: building software still demands discipline, but **the discipline now lives in the scaffolding, not the code** — and "our most difficult challenges now center on designing environments, feedback loops, and control systems."

## Sources
- Lopopolo, R. (2026). "Harness engineering: leveraging Codex in an agent-first world." OpenAI. <https://openai.com/index/harness-engineering/> — [[2026-02-10-harness-engineering|local copy]]
