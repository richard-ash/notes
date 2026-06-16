---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2026-06-15-revised-rules-engineering-leadership.md
compiled_at: 2026-06-15
model: claude-opus-4-8[1m]
confidence: medium
---

# AI-Era Engineering Leadership

Will Larson's (CTO of Imprint, author of *An Elegant Puzzle* and lethain.com) revision of his engineering-leadership rules after a year of AI-tooling-driven change. The framing comes from hypergrowth: its educational value is that "your mistakes reveal themselves next month rather than next year," and Larson argues the AI shift has restored that hypergrowth pace — so the same feedback loop now applies to AI-tooling decisions. Each rule is paired with concrete projects from Imprint's past year, which is what distinguishes this from speculative AI-org commentary like [[ai-and-org-design]].

## The five revised rules

**1. Migrations can be done by an individual, not a team.** Even complex, large changes can be 95% owned by one driving individual and completed in ~10% of the prior time. Larson's counterintuitive corollary: as the *cost* of migrations drops, the *reward/penalty* of each migration's quality rises — small sharp edges break colleagues' mental models of co-maintained software. So "the impact of individual judgment on your company has never been higher." Cheap execution raises, not lowers, the premium on taste.

**2. First-pass code is nearly free; *working* code is not — its cost depends on your development harness.** Writing code that works well and avoids messy edge cases remains hard, and how hard is a function of your harness: tests, CI/CD, validation environments, change preview-ability. The optimistic implication: the investments that most sped up engineering two years ago (good tests, good CI) are still the highest-leverage investments today — the AI shift didn't obsolete them, it made them load-bearing. On "everyone codes," Larson reframes the debate as a miscommunication: even where everyone codes, marketing isn't tuning server allocations; the real question is whether there's a *safe boundary* where non-engineers can participate (analogous to a SaaS product that allows customer scripting).

**3. Optimize the base case of process for agents.** Most steps of most processes can be fully automated *in the base case* with the right harness, controls, domain context, and designer judgment. His example: a good harness' first-pass code review is faster and more effective than a human's — it misses things, but so do human reviewers, and most areas are safe to change. The value is in *capturing the distinction* between safe base cases and higher-risk areas; doing so lets you go faster without adding risk, while failing to do so creates innumerable problems. Corollary: weekly/bi-weekly sprint planning now operates "at too low an altitude" — human planning still matters but should move up a level.

**4. Durable, high-ownership teams with domain context matter *more*, not less.** Echoing his Uber lesson that [persistent teams work magic](https://lethain.com/durably-excellent-teams/) by accumulating context, camaraderie, and ownership. Even when *doing* a thing is cheap, you still have to do *the right thing*, which has gotten only slightly easier. His sharp example: a production issue where the data needed to optimize simply wasn't being captured, so the harness' proposals were reasonable but wrong — the only path was instrumenting the missing information, which requires someone who holds the domain context. This is his explicit rebuttal to the "AI-first companies run by a few genius engineers building perfect, maintenance-free things" vision: high-judgment generalists *can* roam and do remarkable work, but they get hemmed in by lack of domain context, so durable teams remain the fundamental building block.

**5. Quick, good, durable decision-making is a prerequisite to benefiting from AI.** Replacing a legal review with automation only pays off if Legal can *commit* to the change; shipping a feature only matters if you can *decide* to launch it. Faster execution is worthless without faster durable decisions. Larson argues this is why the average CTO role has become more technical and less bureaucratic over the past year: he is often the only person who can make a binding call when teams disagree, so he's "making decisions constantly" to maintain pace. The caveat — executives aren't better decision-makers; binding executive decisions are simply uniquely powerful, conditional on the executives being aligned enough to honor them.

## Concrete evidence from Imprint

The rules are grounded in named projects, which is the article's distinguishing feature:

- **Deploy frequency went from ~6/week to 200–400/week** over a year (20–30× even after normalizing for doubled headcount) — a two-month deploy/migration overhaul done 90% by two infrastructure engineers.
- **AI-tool adoption went from ~25% daily users (early January) to 100% (end of February)** with *no top-down mandate* — just good tooling plus talking to non-adopters to remove friction. Nearly every PR is now harness-written in the first pass.
- **Configuration consolidation** from many mechanisms to two (rarely-changing constants vs. frequently-changing product values), done as a relay of isolated single-engineer projects: one cleaned up the architecture, one built a reference implementation, others followed it across the codebase — a former multi-year project compressed to under a quarter.
- **Multi-repo → mono-repo frontend** in ~a month, 95% by one engineer; **full static typing** of a largely-untyped frontend by one engineer "and a lot of tokens" in a few weeks; **npm → pnpm** in a few hours/day over a few days.
- **Agent-first process automation**: customer-ops issue triage via a harness with team context and scoped data-warehouse access (humans still triage edge cases, workflow unchanged); first-pass code review by the same harness that wrote the change, *cleared of the authoring context*; fraud-team automation doing first-pass attack investigation; migration to Linear (off Jira) for better MCP/Slack integration, with an internal harness that pulls and auto-resolves Linear issues in alpha.
- **Failure mode named**: throwing AI-generated design docs and PRs "over the wall" to other teams never works. "Slop" artifacts are cheap but *actively harmful* — they must be cleaned up, and their context *poisons the LLM*, producing worse outcomes than starting over. Conversely, managers contributing code works **only** when they validate directly, watch dashboards post-deploy, and fix what they break; no positive impact otherwise.

## Synthesis and connections

The through-line is a barbell: AI collapses the cost of the *first draft* of almost anything (code, migration, review, triage), which shifts all the remaining value to the things AI doesn't cheapen — judgment, domain context held by durable teams, harness quality, and the organizational ability to make binding decisions fast. Larson's closing observation reinforces it: the aperture of the possible keeps widening, but the constraints haven't changed — "organizational misalignment, lack of clarity, and poor technical architecture."

- [[ai-and-org-design]] — Bret Taylor's "atomic unit of productivity is a process, not a person" is the complementary half of Larson's rule 3 (optimize the *process* base case) and rule 4. Where Taylor diagnoses the cross-departmental seams that no one owns, Larson supplies the org-design answer: durable teams that own an area end-to-end, plus an executive who can make the binding cross-team decision (his rule 5) — exactly the "no one owns supplier-onboarding cycle time" gap Taylor names. Larson is the practitioner counterweight to Taylor's flatter-org / hyper-generalist thesis: he explicitly *disagrees* that a few roaming geniuses replace durable teams.
- [[elon-operating-philosophy]] — Larson's "decide fast and bindingly" maps onto Musk's single-metric, vector-sum teams; both treat decisiveness as the scarce input once execution is cheap.
- [[manager-anti-patterns]] / [[ic-anti-patterns]] — the "manager who codes but doesn't validate dashboards" and the "slop PR thrown over the wall" are new AI-era entries in Larson's own taxonomy of how managers and ICs get stuck.
- [[how-to-operate]] — Rabois's "barrels vs. ammunition" prefigures the durable-team-with-ownership claim: the constraint is people who own outcomes end-to-end, not raw execution capacity.

## Sources
- Will Larson (2026-06-15). "Revised rules of engineering leadership." <https://lethain.com/revised-rules-of-engineering-leadership/> — [[2026-06-15-revised-rules-engineering-leadership|local copy]]
