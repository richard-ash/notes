---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-03-11-judgment-creativity-coding-agents.md
compiled_at: 2026-04-22
model: claude-opus-4-6
confidence: medium
---

# Judgment in AI-Assisted Development

As coding agents eliminate implementation time as a bottleneck, software productivity becomes constrained by a hierarchy of increasingly human capabilities: **time → attention → judgment → creativity**. Will Larson argues that judgment — the ability to make decisions that produce maintainable, secure, and reliable software — is the current binding constraint, and that the industry will solve it through ecosystems of packaged expert context ("datapacks" and skill package managers) before creativity becomes the final frontier.

## The constraint hierarchy

Larson identifies four sequential bottlenecks on software productivity, each revealed as the previous one is relaxed:

1. **Time** — already solved. Coding agents provide effectively unlimited implementation capacity at affordable cost. The frenzied sprint of implementation is over.
2. **Attention** — partially solved. Engineers can supervise ~5 concurrent agent workstreams before losing track, but Larson believes this is a tooling and workflow problem ("a skill issue in how I am composing the tools") rather than a hard limit. Coordination across teams will remain a floor.
3. **Judgment** — the current binding constraint. With unlimited time and expanding attention, engineers *can* build anything. The hard question becomes *how* to build it: maintainably, securely, reliably, and in a way that survives staff turnover. This is where most teams are stuck today.
4. **Creativity** — the eventual final constraint, but far enough ahead that Larson considers it a classic entrepreneurship problem amenable to existing approaches.

## Migrations as evidence

Larson grounds the argument in a direct comparison of two large-scale infrastructure migrations he led:

**Uber (2014):** Migrating hundreds of services to a new self-service provisioning platform (a minimal Heroku-like system). A ~3-person team completed it in under six months. The vast majority of engineering time went to *implementing decisions* — writing the scheduler, building the provisioning UX, handling a heterogeneous polyglot environment (Python, Node, Go, and a long tail). Kubernetes effectively didn't exist yet, so the team built infrastructure from scratch.

**Imprint (2025–2026):** Migrating all services and databases to continuous deployment with Kubernetes and ArgoCD. Again ~3 engineers, completed in ~3 months. But the time distribution flipped: nearly all effort went to *designing the approach*, reviewing agent-generated pull requests, and revising designs when reality diverged from plans. Implementation was delegated to coding agents.

The fundamental challenges of [[software-migrations]] — coordination, the last mile, organizational buy-in — remained identical. What changed was that the "essential but mundane minutiae" of implementation no longer consumed engineering hours. The work shifted from *implementing decisions* to *making decisions*.

## Datapacks and skill package managers

Larson proposes **datapacks** (a concept from his earlier writing on competitive advantage for authors in the LLM era) as the mechanism for scaling judgment. A datapack injects expert context for a specific task domain into a coding agent, effectively supplementing the human's judgment with codified expertise.

This is already happening organically:
- Coding agents ship with built-in development skills
- The open-source community develops shared agent skills
- Companies build internal skills encoding their specific practices

Larson predicts the industry will develop a formal ecosystem — skill package managers with curated, maintained skill packages for security engineering, product engineering, and other domains. He draws an analogy to technology publishers (O'Reilly) maintaining "blessed skills," essentially a distribution platform for codified engineering judgment. His own experiment with an [LLM-optimized companion to his book on engineering strategy](https://www.amazon.com/Companion-Crafting-Engineering-Strategy-Thoughtful-ebook/dp/B0FXN2J4PJ) points in this direction, though he notes the distribution platform will be more valuable than any individual datapack.

## Implications

- **The engineer's role shifts from implementation to decision-making.** The comparison between the Uber and Imprint migrations illustrates this concretely: same type of project, same team size, but the human work moved entirely upstream to design and judgment.
- **Financial constraints are not yet binding.** Relative to current software engineering budgets, agent compute costs are affordable. Larson notes this may change as judgment-injection (via datapacks/skills) adds cost, making the net financial picture uncertain.
- **Attention is a workflow problem, not a hard limit.** Unlike judgment, which requires genuine expertise, attention bottlenecks are solvable by better tooling for managing concurrent agent workstreams. This connects to the [[unattended-coding-agents]] pattern, where Stripe engineers routinely manage multiple parallel agent runs.
- **Creativity remains distant but real.** Larson doesn't elaborate on what constraining creativity looks like in practice, framing it as a future entrepreneurship problem rather than an engineering one.

## Cross-connections

- [[software-migrations]] covers the Derisk → Enable → Finish playbook from Larson's 2018 article; this article revisits the same Uber migration as a before/after comparison with agent-assisted development
- [[unattended-coding-agents]] describes the mechanics of autonomous coding agents (Stripe's Minions); Larson's argument explains *why* the human role in that workflow is review and judgment, not implementation
- [[claude-code-skills]] covers the taxonomy and design of agent skills — the very "datapacks" Larson predicts will become an industry ecosystem
- [[claude-code]] documents session management and subagent patterns that address the attention constraint Larson identifies

## Sources

- Larson, Will (2026). "Judgment and creativity are all you need." <https://lethain.com/judgment-is-all-you-need/> — [[2026-03-11-judgment-creativity-coding-agents|local copy]]
