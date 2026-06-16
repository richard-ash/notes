---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-06-16-airbnb-agentic-coding.md
compiled_at: 2026-06-16
model: claude-opus-4-8[1m]
confidence: medium
---

# Enterprise Agentic Coding Adoption

How a large engineering org rolls out [[agentic-engineering|agentic coding]] internally — the platform, the adoption curve, the culture, and the lessons. The canonical field report is Szczepan Faber and Mike Nakhimovich's DPE Summit 2025 talk on Airbnb's Developer Platform group, which is unusually concrete about numbers and missteps. This article treats their experience as a case study, not as settled fact; the productivity claims are self-reported and the tooling specifics are Airbnb-internal.

## The vision-and-work-backwards framing

Faber's pitch to leadership at the start of 2025 used a deliberately **bold vision** rather than incremental targets, on the theory that step-function change is hard to reach by planning increments. The frame: the historical arc runs from typing code by hand → copy-pasting from ChatGPT/Copilot → a human engineer steering *multiple* agentic sessions that materialize code changes. The third stage is the paradigm shift; the first two are "good tools" but "not where the magic happens."

Their own predictions undershot. They forecast 20–40% of engineers materializing code via agents daily by end of 2025; by the talk they were at ~64% (and elsewhere cite 60% of PR authors). The lesson they draw is not "we were wrong" but "predictions are for explaining direction to leadership, not for measuring success."

## The pair-programming analogy

Faber frames agentic coding through classic pair programming's **driver/navigator** split: the driver holds the keyboard and is tactical; the navigator is strategic, seeing "the forest, not just the one tree." Agentic coding makes the developer the *permanent navigator* while the agent drives. He concedes the analogy breaks once you parallelize — a single navigator can't pair with five drivers at once — and predicts the future engineer's core skill shifts **from flow to context-switching**.

## Measuring success: a holistic, three-lens method

Adoption predictions are not KRs. Airbnb measures impact across three lenses, echoing the DX/SPACE school of developer-productivity measurement:

1. **Developer sentiment** — surveys; agentic coding was the top-voted productivity tool for four consecutive surveys.
2. **Tool usage / adoption** — the adoption *curve* is the headline finding (below).
3. **Objective engineering-system metrics** — chiefly PR velocity, viewed **in aggregate, never as personal productivity**. They claim correlation between agentic-tool adoption and PR-velocity metrics, with the usual caveats about confounds.

The adoption curve is the most striking data point: earlier non-agentic IDE plugins climbed gradually, but once true agentic tools landed (~6–7 months before the talk, gated on model quality and tool maturity), adoption went "almost vertical." Crucially, **usage is not mandated** — it's a supplemental, opt-in tool; the org invests in encouragement, teaching, and one-click integration instead of forcing it.

## Defining the loop

Airbnb's working definition: from the **inner developer loop**, an engineer specs or prompts to kick off an **agentic loop**. It's a *loop* because the agent may call LLMs many times, call MCP tools many times, load config ([[agentic-engineering|AGENTS.md / CLAUDE.md / cursor rules]] are all "configuration"), and apply guardrails. The defining property is **autonomy under uncertainty**: you don't know in advance how many LLM calls, which tools, or which prompts the session will use. The loop's output is code changes that **a human must review before the PR is submitted** — a hard rule, on top of the second human review the PR itself gets. (See [[ai-coding-harnesses]] for the mechanics of this loop.)

## The skill-ladder model of adoption

Airbnb models individual proficiency as a ladder, used to spot engineers moving too fast or too slow:

1. First steps.
2. Using the tool, **approving every operation** — the normal beginner state.
3. **Auto-approve** ("keep going, show me the diff") — earned not by *trusting the AI* but by trusting one's own skill at prompting and contextualizing.
4. **Building the platform** — writing MCP servers, integrating tools, contributing to open source.

The explicit warning: reaching auto-approve **too fast** produces large PRs the author hasn't fully read, with test code reviewed less rigorously than production code. Faber's repeated conference refrain — **hold test code to production-code quality**; refactor and maintain it. A second discipline is **pushing back on the agent**: when something looks wrong, interrogate it ("why line 120?"); the agent answers confidently, but after a few rounds you reach "the satisfying moment" where it concedes it was wrong. Don't take the first confident answer. This is the operational counterpart to [[ai-judgment-atrophy|judgment atrophy]] — the human muscle that auto-approve threatens to let waste.

## Parallelism needs infrastructure, not just a tool

The productivity multiplier comes from running **multiple agentic sessions in parallel** — power users run up to five workspaces at once, each on a different prototype. Faber's load-bearing claim: **the agentic tool is not enough**; you need a stack around it — remote IDEs, sandbox environments, and strong code-review tooling and culture. He explicitly **recommends cloud sandboxed environments over local git worktrees** for parallel sessions (more consistent, more reliable); Airbnb uses internal "AirDev workspace" tech for this. The provocative endpoint: software engineering's future may be "all code review."

## The platform story: Airchat, MCP, and "bring Airbnb to the agents"

Mike Nakhimovich's half is the platform-engineering case study. Airbnb has **no typical engineer** (17-year-old company, full stack, 60% remote workspaces / 40% local, IDE *and* CLI loyalists, six-plus languages), so the guiding principle is **meet developers where they are** — never force a tool or editor switch.

**Strategy evolution:**
- **IDE-first** (their starting point): beautiful UX, tight context (open tabs, local edits), and a unique edge — a **RAG pipeline over Airbnb-internal knowledge**. But IDE plugins were pre-agentic: one-shot chat, not multi-step tool-calling.
- **CLI-first** (the tempting pivot): open-source CLI agents (Aider, OpenHands, Claude Code, Codex, Gemini) gave **top-of-market answer quality**, ran anywhere including headless workspaces, and were faster to a solution — but had **zero Airbnb awareness** (didn't know the repos, design patterns, or mono-repo). Great for side projects, weak on the giant internal codebase.
- **Resolution:** invest in the system. Spin up a small **DevAI core team** (~4–7 engineers + product) plus a ~30-person cross-functional working group / champion program.

**Three bets:** (1) bring external agents *to* Airbnb, (2) bring Airbnb knowledge *to* the agents, (3) go early on **MCP**.

**Airchat** — the keystone abstraction. A thin CLI wrapper with **swappable engines**, single-command install, and auto-update. It decouples the org from any one vendor: when Codex or Gemini or a new model becomes best-in-class, Airchat swaps it in without re-training users. This is the practical answer to "the market moves too fast to standardize" — standardize the *wrapper*, not the engine. (Compare the vendor-agnostic [[agent-harness|agent-harness]] thesis: expose capability through a stable interface, not a specific model.)

**MCP as the integration substrate** — "REST for LLMs." Nakhimovich bet on it in week three, "the standard that came out yesterday," because it matched what they already did (tool-calling via provider SDKs) but was *publishable* across non-internal clients. The ecosystem snowballed: IDE tools exposed as MCP servers (usable from the CLI), MCP clients inside IDE plugins, config-sync through Airchat, and 12+ internal MCP servers (analytics, CI, internal tools you can't find publicly). The core team's leverage moves: a **paved path** for auth (auto-injected user auth + pre-cleared security review, skipping the two-week review), project templates for cheap hackathon experimentation, homebrew-style one-command install, and now **client-building SDKs** as people want agentic apps everywhere (web, desktop), not just CLI/IDE.

**The orchestrator-of-agents detour.** Following Anthropic's *Building Effective Agents*, they tried to build their own orchestrator registering planning/coding/validation agents that delegate to each other (an agent = a prompt + a tool list + a way to call an LLM). It **failed** — too small a team, market five steps ahead before they finished. "Can't beat them, join them": they pivoted to **delegate to the Airchat CLI** as the engine, with a thin shim above it for other apps to interface — a unidirectional data flow with single responsibility. This is a concrete instance of the [[the-bitter-lesson|don't-out-engineer-the-frontier]] pattern and the [[ai-eats-the-world|value-moves-up-the-stack]] thesis: own the integration layer, rent the engine.

**Tool-calling is all you need (for internal knowledge).** Rather than fine-tune or train a model on Airbnb knowledge — "expensive, doesn't quite work out," as peer companies found — they **re-wrapped the old one-shot RAG REST endpoint as an MCP tool** with good descriptions. The LLM then *navigates* the knowledge base: query, dislike the answer, re-query with new terms. They "got agentic search and deep research for free" — and answers became Airbnb-specific ("how do I set up an S3 resource *here*" vs. a generic answer). The general claim — **the world moved from training-in knowledge to tool-calling-in knowledge** — is the [[knowledge-graph-llm-context|structure-beats-retrieval]] and [[the-bitter-lesson|bitter-lesson]] story applied to enterprise knowledge.

## Six lessons (the war stories)

1. **It takes a village.** Too big and fast for a few experts in a dark room. Empower local experts/champions; the talks, hackathons, docs, and slash commands from *outside* the core team turn it into an ecosystem, not a fiefdom.
2. **Don't call CLI an underdog.** CLI-agent adoption went hockey-stick; ~80% of engineers shifted to preferring CLI + multiple tabs. IDE usage didn't *tank* — CLI usage *skyrocketed* on top of it. (Nakhimovich, a self-described "can't-do-git-from-the-command-line" IDE loyalist, hasn't used an IDE in months — debugging and exploring entirely through agents.)
3. **Remove barriers.** One-click, pre-installed, where developers already are.
4. **Don't do too much at once.** They briefly considered force-migrating all IntelliJ users to VS Code "for the agentic tools" and abandoned it within days — people love their editors; meet them there.
5. **Standardize, but not prematurely.** Don't chase every trend; wait for the industry to stabilize, then pick. Most of their decisions "would have been much easier six months later" — so weigh the cost of being an early adopter. Measure impact (quant + qual; vendors like DX now instrument agentic tools), acknowledging productivity measurement for agents is unfinished work.
6. **Don't drop your standards for AI.** Nakhimovich, a former "this is all slop / vibe coding" skeptic (true under GPT-3.5), reports getting "lapped" by agentic coding — it brought him to parity with stronger engineers on tasks he couldn't have attempted. The standards point cuts both ways: AI raises the floor, but only if you keep reviewing to the old bar. (The skeptic-to-convert arc mirrors the practitioners in [[agentic-engineering]] and the velocity-into-quality reinvestment in [[ai-code-review]].)

## Why this matters

The talk is one of the clearer enterprise counterweights to the "AI replaces engineers" narrative: humans stay in the loop as navigators and mandatory reviewers, and the *bottleneck shifts to review and context-switching*, not disappears. It also validates a specific platform shape now recurring across orgs — **a thin vendor-agnostic wrapper + MCP as the internal-knowledge bus + paved-path security/auth + champion-driven culture** — which is the org-level complement to the individual-level discipline in [[agentic-engineering]] and the harness mechanics in [[ai-coding-harnesses]]. Read it alongside [[decide-execute-deliver-sandwich]] (why this compresses the *execute* layer, not the job) and [[ai-lab-economics]] / [[ai-eats-the-world]] (why owning the integration layer and renting commodity engines is the rational bet).

## Sources
- Faber, S. & Nakhimovich, M. (2025-10-15). "Agentic coding at Airbnb." DPE Summit 2025 (Gradle). <https://www.youtube.com/watch?v=o6oYc9-X9Iw> — [[2026-06-16-airbnb-agentic-coding|local copy]]
