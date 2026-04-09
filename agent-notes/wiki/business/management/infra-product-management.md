---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2018-02-06-product-management-infra-engineering.md
compiled_at: 2026-04-09
model: claude-opus-4-6
confidence: medium
---

# Product Management in Infrastructure Engineering

Infrastructure engineering teams operate in two distinct modes, and the transition between them is one of the hardest shifts a team can make. Will Larson describes these as **foundation mode** and **innovation mode**, and argues that most infra teams are well-practiced at the former but struggle with the latter.

## Two modes of operation

**Foundation mode** is maintenance-driven: compliance, security, reliability, scaling. Work is mostly mandatory, and the game is execution, focus, and limiting WIP. Kanban fits naturally here.

**Innovation mode** appears when a team has paid down enough technical debt to have surplus capacity. Now the question shifts from "what must we do?" to "what should we do?" — and that flexibility is disorienting. The game becomes listening to users, exploring solution spaces, and validating solutions as cheaply as possible.

Most teams cycle between the two over time. The dangerous moment is when foundation work recedes but the team hasn't built the muscles for innovation — they default to clearing the backlog rather than doing deliberate discovery.

## Problem discovery

Larson's core advice: when surplus capacity appears, resist the backlog. Instead, cast a broad net and deliberately separate idea generation from evaluation. He recommends a four-prong approach:

1. **Learn from users** — SLA discussions, surveys, coffee chats, discussion groups, and customer advisory boards. The most valuable conversations focus on understanding what users *do*, not just what they want improved.
2. **Learn from peers** — conversations with engineers at other companies solving similar problems. Larson acknowledges the cargo-culting risk, which is precisely why discovery must be decoupled from prioritization.
3. **Learn from the industry** — academic papers, big-tech research publications, open-source project landscapes, and cloud vendor offerings.
4. **Brainstorm with the team** — leverage the collective experience already on the team.

The goal is to load as much context as possible before making any prioritization decisions.

## Prioritization framework

From the discovery phase, Larson produces three artifacts:

- A **charter**: the team's unique value proposition, competitive advantages, and strategy.
- An **optimistic three-year vision**: what could be achieved if everything went perfectly. Constrained by possibility, not reasonableness.
- A **prioritized list of user pain**: active needs bucketed into addressable clusters — problems that a single solution might address, eliminate, or empower.

The aim is to relieve user pain *and* make progress toward the vision simultaneously. Larson's default allocation is **70% immediate user needs, 30% future-facing work** — deliberately skewed toward the present because teams tend to over-index on the future. In areas where cloud vendors are rapidly expanding, he suggests it may even be reasonable to devote 100% to immediate pain, strategically underinvesting in custom solutions that cloud offerings will absorb within 2-3 years.

Early priority alignment is critical: involve users early so they can weigh in on what's independently useful, enabling incremental value delivery rather than a big-bang release.

## Solution validation

Larson warns against the "full waterfall" instinct — immediately designing a 12-month roadmap once priorities are set. The problem isn't estimation difficulty but the assumption that proposed solutions are good. Most solutions, he argues, are pretty bad. The secret is skepticism, not brilliance.

Key validation tactics:
- **Evangelize existing capabilities** before building new ones — sometimes the solution already exists but is poorly documented or requires architectural familiarity to recognize.
- **Do the hardest migration first** to validate feasibility early, then follow with a burst of easier integrations to test broad applicability.
- **Embed with users** — place the solution-building team inside the team they're building for, to iterate quickly and avoid falling in love with elegant but useless solutions.
- **Try to prove the solution cannot work** — gather disconfirming data, run experiments, check whether the approach has worked for others.

This connects to the broader theme in [[software-migrations]]: the hardest part of cross-cutting work is coordination and validation, not the technical implementation itself.

## The transition as identity shift

Larson frames the foundation-to-innovation transition as more than operational — it's an identity shift. Infra teams that successfully make the transition move from being perceived as cost centers to becoming acknowledged sources of innovation, with more direct contribution to colleagues' success. But many teams never make this transition, and some intentionally choose not to.

## Temporal notes

Written in 2018, this reflects Larson's experience at Stripe-era scale. The cloud vendor strategy ("underinvest because AWS/GCP will absorb it") has partially played out — managed databases, Kubernetes, observability platforms have indeed reduced the need for custom infra in many areas. But the core discovery-prioritization-validation cycle remains highly relevant regardless of build-vs-buy decisions. The advice to [[choose-boring-technology]] in foundation mode complements this framework: boring tech reduces maintenance burden, freeing capacity for the innovation mode Larson describes.

## Sources

- Larson, Will (2018). "Product management in infrastructure eng." <https://lethain.com/product-management-infra-engineering/> — [[2018-02-06-product-management-infra-engineering|local copy]]
