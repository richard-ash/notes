---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2018-08-20-problem-exploration-selection-validation.md
compiled_at: 2026-04-20
model: claude-opus-4-6
confidence: medium
---

# Product Management Framework for Engineering Leaders

Will Larson frames product management as an **iterative elimination tournament** — a repeating cycle of *problem discovery*, *problem selection*, and *solution validation*. Each successful round earns the right to play the next round with greater complexity and scope. Each failure risks forfeiting the game entirely.

This framework is aimed at engineering leaders who find themselves temporarily covering the PM role — a common situation when a PM departs or a new team is forming. It's deliberately simple, trading depth for immediate applicability.

## Problem discovery

Skipping discovery is common and leads to inertia-driven local optimization. Larson considers deliberate problem exploration one of the best predictors of long-term team performance.

Seven lenses for populating the problem space:

1. **Users' pain** — go broad (surveys) and deep (interviews across segments).
2. **Users' purpose** — what motivates engagement? How can you better enable their goals?
3. **Benchmarking** — compare against both similar and dissimilar companies. The most interesting insights come from benchmarking outside your immediate competitive set.
4. **Cohorts** — disaggregate top-level metrics. Hidden user segments often have surprising needs.
5. **Competitive advantages** — where you're exceptionally strong, you're better positioned to pursue opportunities others can't.
6. **Competitive moats** — a stronger variant: what sustaining advantages exist today, what moats could you build, and which moats do competitors enjoy?
7. **Compounding leverage** — composable blocks that pay off more than once. Larson connects this to [[technical-leverage]] — investments whose value compounds over time rather than being consumed in a single use.

This general discovery framework complements the more infrastructure-specific version in [[infra-product-management]], where Larson recommends four discovery channels (users, peers, industry, team brainstorming) tailored to platform and infra teams.

## Problem selection

Selection is where disagreements surface, and Larson argues these are usually rooted in **differing time-horizon assumptions** rather than genuine disagreement about what matters.

Key selection criteria:

- **Surviving this round** — what must happen to avoid cancellation? Revenue targets, adoption thresholds, etc.
- **Surviving the next round** — where do you need to be positioned when the next evaluation cycle starts? Short-term velocity trades may be justified if winning brings significantly more resources.
- **Winning rounds** — survival is necessary but insufficient. What work trends toward actually winning?
- **Time-frame stress testing** — what would you do with 6 months of runway? 2 years? 5 years? Making the assumed time horizon explicit often resolves apparent disagreements.
- **Industry trends** — position for where the industry is heading; avoid work that will need redoing.
- **Return on investment** — Larson believes quick, easy wins are chronically under-prioritized. Compounding wins are especially valuable over the medium and long term.
- **Experiments to learn** — what could you learn now that would make future selection much easier?

The "iterative elimination tournament" metaphor is notable: it encodes the startup reality that product work is not a single optimization problem but a sequence of survival-then-growth gates. This connects to the broader entrepreneurial theme of [[sequencing-startup-ideas]] — choosing what to build is inseparable from choosing when.

## Solution validation

Larson warns against jumping straight to execution after selecting a problem — it's easy to fall in love with a difficult approach. An explicit validation phase de-risks before committing resources.

Validation tactics:

- **Write a customer letter** — draft the launch announcement. If you can't write something exciting, useful, and real, reconsider. Test it with actual users, not your intuition.
- **Identify prior art** — how do peers solve this? Existence proves possibility, though not optimality. Prefer first-hand connections over conference talks (misinformation is rampant).
- **Find reference users** — if nobody will volunteer to be the first user, be skeptical about building it.
- **Prefer experimentation over analysis** — cheap validation beats brilliant prediction. You're almost always missing essential information at the design stage. Experimentation surfaces problems you didn't know to look for.
- **Find the cheapest path** — building the full solution is the most expensive validation. Seek the minimum viable test.
- **Justify switching costs** — even desirable solutions fail adoption if switching costs exceed users' willingness to pay. Test this explicitly.

Larson notes that solution validation skills overlap heavily with [[software-migrations]] — both require cheap validation, user buy-in, and incremental de-risking.

## The framework as a whole

The three phases form a cycle, not a waterfall. Discovery feeds selection; selection constrains validation; validation failures loop back to discovery or re-selection. Larson presents this as a minimum viable PM toolkit — not a substitute for deep product expertise, but a structured starting point for engineers who suddenly find themselves responsible for product direction.

## Sources

- Larson, Will (2018). "Problem exploration, selection and validation." <https://lethain.com/intro-product-management/> — [[2018-08-20-problem-exploration-selection-validation|local copy]]
