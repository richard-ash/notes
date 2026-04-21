---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-20-stripe-minions-coding-agents.md
  - agent-notes/raw/engineering/computer/development/2026-04-20-stripe-minions-coding-agents-part-2.md
compiled_at: 2026-04-20
model: claude-opus-4-6
confidence: medium
---

# Unattended Coding Agents

An **unattended coding agent** is a fully autonomous agent that takes a task description as input and produces a ready-to-review pull request as output, with no human interaction during the run. The key distinction from interactive coding assistants (Claude Code in conversational mode, Cursor, Copilot) is the elimination of the human-in-the-loop during execution — the human's role shifts entirely to review.

Stripe's internal system, **Minions**, is the most detailed public account of this pattern deployed at enterprise scale. As of Part 2 of their blog series, Minions produce over 1,300 merged PRs per week at Stripe (up from 1,000 at Part 1's publication), all human-reviewed but containing no human-written code.

## The unattended workflow pattern

The lifecycle of an unattended agent run follows a consistent shape across implementations:

1. **Task intake** — engineer describes the task (Slack message, ticket, CLI). The agent ingests the task description plus any linked context (thread history, documentation URLs, ticket details).
2. **Environment spin-up** — the agent gets an isolated environment with the codebase pre-loaded. Stripe uses pre-warmed "devboxes" that spin up in ~10 seconds, isolated from production and the internet. This isolation enables running agents without human permission checks.
3. **Blueprint execution** — the agent follows a blueprint (see below) that interleaves agentic LLM loops with deterministic code steps.
4. **Feedback iteration** — the agent receives automated feedback and iterates:
   - **Local lints** (< 5 seconds) — run as a deterministic blueprint node before every push
   - **CI** — selective test execution from Stripe's 3M+ test battery, with autofixes applied automatically where available
   - **At most two CI rounds** — diminishing returns make additional rounds not worth the token/compute/time cost
5. **PR creation** — the agent creates a branch, pushes to CI, and prepares a PR following the team's template.
6. **Human review** — engineer reviews, approves, or sends back for another iteration.

The "shift feedback left" principle applies to agents just as it does to humans: every lint that would fail in CI should ideally be enforced locally and caught before the push. Stripe implements this with a background daemon that precomputes lint rule heuristics and caches results, delivering fixes in under a second on push.

## Blueprints: hybrid workflow-agent orchestration

Part 2 of the Stripe series introduces **blueprints** — an orchestration primitive that combines the determinism of fixed workflows with the flexibility of agentic loops. A blueprint is a state machine where each node is either:

- **Deterministic** — runs code with no LLM invocation (e.g., "Run configured linters," "Push changes," git operations)
- **Agentic** — an LLM loop focused on a subtask with wide latitude to make decisions (e.g., "Implement task," "Fix CI failures")

The key insight: writing code to deterministically handle predictable decisions — like "always lint at the end" — saves tokens and CI costs at scale, and reduces the surface area for LLM errors. Stripe describes this as "putting LLMs into contained boxes," which they find compounds into system-wide reliability gains.

Blueprint machinery also simplifies context engineering of subagents: each node can have constrained tools, modified system prompts, or simplified conversation context appropriate to its subtask. Individual teams can build custom blueprints for specialized needs — Stripe cites LLM-assisted migrations that couldn't be accomplished with purely deterministic codemods as an example.

This pattern sits between Anthropic's categorization of pure "workflows" (fixed graph, no agent autonomy) and pure "agents" (loop with tools, full autonomy). It's a pragmatic middle ground for enterprise-scale agent systems.

## Cloud developer environments as agent infrastructure

Stripe's **devboxes** — AWS EC2 instances pre-loaded with source code and services — are the runtime for both human engineers and Minions. Key properties that make them effective for unattended agents:

- **Parallelizable** — each agent gets its own devbox; no interference between concurrent runs. Engineers routinely have half a dozen devboxes active at once.
- **Predictable** — pre-warmed from a pool (git repos cloned, Bazel/type-checking caches warm, code generation services running). Ready in ~10 seconds.
- **Isolated** — run in QA environment with no access to real user data, production services, or arbitrary network egress. This eliminates the need for confirmation prompts — any mistakes are confined to one disposable devbox.
- **"Cattle, not pets"** — standardized and easy to replace, not bespoke.

Stripe built devboxes for humans years before LLM agents existed. The lesson: investment in human developer environments compounds for agents too. Containerization or git worktrees on a developer laptop can approximate these properties but are harder to combine at scale.

## Why build custom vs. use off-the-shelf agents

Stripe's rationale for building in-house highlights constraints that apply broadly to large codebases:

- **Scale and complexity** — hundreds of millions of lines of code across a few large repos. The mental model required to make effective changes is substantial.
- **Uncommon stack** — Ruby (not Rails) with Sorbet typing and vast homegrown libraries that LLMs have little training data for.
- **High stakes** — code that processes $1T+/year in payment volume, with regulatory and compliance obligations.
- **Existing tooling investment** — Stripe's developer productivity infrastructure is deeply custom. The agent harness integrates tightly with existing tooling rather than replacing it.

The agent harness is a fork of Block's [Goose](https://github.com/block/goose), customized specifically for the unattended use case. The key divergence from off-the-shelf agents: Minions can't rely on human-facing features like interruptibility or mid-run commands, since no human is watching.

## Ergonomic integration points

A key design goal is meeting engineers where they already are:

- **Slack** (primary entry point) — tag the Slack app in a thread; the agent ingests the full thread and linked context. Engineers frequently spin up multiple minions in parallel.
- **Internal platforms** — docs platform, feature flag UI, and ticketing system all have "fix with a minion" buttons. Flaky test tickets automatically prompt users to launch a minion.
- **Web UI** — engineers observe the agent's decisions and actions in real time or post-hoc, and can provide further instructions.

## MCP as the universal tool layer

Stripe built a centralized internal MCP server called **Toolshed** hosting nearly 500 tools (up from 400+ at Part 1) spanning internal systems and external SaaS platforms. Toolshed serves as a shared capability layer across Stripe's entire fleet of agents — not just Minions, but also a no-code internal agent builder, custom service agents, third-party off-the-shelf agents, CLI tools, and Slack bots. Adding a tool to Toolshed immediately grants it to hundreds of different agents.

Agents perform best with a curated subset of tools rather than the full catalog, so Minions receive an intentionally small default set. Engineers can configure additional thematically grouped tool sets for their own minions.

A notable optimization: Stripe deterministically runs relevant MCP tools over likely-looking links *before* the agent loop starts, pre-hydrating the context. A security control framework ensures agents can't perform destructive actions through their tools.

## Conditional agent rules at scale

Minions consume the same agent rule files that human-operated tools use. Stripe standardized on Cursor's rule format (which supports subdirectory scoping and file pattern matching) and syncs those rules into a Claude Code-compatible format. This means their three most popular coding agents — Minions, Cursor, and Claude Code — all read the same guidance.

At Stripe's repository scale, unconditional global rules are used sparingly to avoid filling the context window before work begins. Almost all rules are **conditionally applied based on subdirectories or file patterns**.

## Implications

- **Parallelization of developer attention** — the scarce resource is not code production but developer attention. Unattended agents let one engineer spawn multiple parallel workstreams, fundamentally changing the throughput equation.
- **Blueprints as the right abstraction** — neither pure workflows nor pure agent loops fit enterprise-scale coding agents well. The hybrid blueprint pattern — deterministic nodes for predictable work, agentic nodes for creative work — offers a practical middle ground. "Putting LLMs into contained boxes" compounds reliability.
- **Harness architecture matters at enterprise scale** — the [[ai-coding-harnesses|harness]] (tool definitions, context management, feedback loops) determines agent quality as much as the underlying model.
- **Same tools for humans and agents** — the most effective approach is not building agent-specific tooling but making human developer tooling agent-friendly. Investment in developer productivity compounds for both audiences.
- **The two-CI-round limit** — an empirical finding: Stripe caps CI iterations at two, having found diminishing returns beyond that. Agents that can't get code right within ~2 feedback cycles are unlikely to converge with more attempts.
- **Isolation enables autonomy** — the quarantined devbox model (QA environment, no production access, no real data) is what makes fully unattended operation safe. The blast radius of any agent mistake is one disposable environment.

## Cross-connections

- [[ai-coding-harnesses]] covers the technical architecture of the tool-call loop that sits at the core of every agent, including Minions
- [[claude-code]] documents Boris Cherny's design philosophy for Anthropic's coding agent; Cherny's discussion of subagents spawning parallel workstreams mirrors Stripe's pattern of engineers launching multiple Minions concurrently
- The "build for the next model" principle from [[claude-code]] is implicitly present here — Stripe's Minion architecture assumes agent capabilities will improve, investing in the harness and tooling integration rather than compensating for current model limitations
- The blueprints pattern echoes Anthropic's own taxonomy from their ["Building effective agents"](https://www.anthropic.com/engineering/building-effective-agents) post, but sits deliberately in between the workflow and agent patterns they describe

## Sources

- Stripe Engineering (2026). "Minions: Stripe's one-shot, end-to-end coding agents." <https://stripe.dev/blog/minions-stripes-one-shot-end-to-end-coding-agents> — [[2026-04-20-stripe-minions-coding-agents|local copy]]
- Stripe Engineering (2026). "Minions: Stripe's one-shot, end-to-end coding agents—Part 2." <https://stripe.dev/blog/minions-stripes-one-shot-end-to-end-coding-agents-part-2> — [[2026-04-20-stripe-minions-coding-agents-part-2|local copy]]
