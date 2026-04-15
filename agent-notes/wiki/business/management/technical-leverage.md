---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2012-11-04-building-technical-leverage.md
compiled_at: 2026-04-15
model: claude-opus-4-6
confidence: medium
---

# Technical Leverage

Technical leverage is the practice of investing in technology to increase the business value a development group delivers over time. The term, as Will Larson uses it (attributing the framing to Kevin Scott, then SVP of Engineering at LinkedIn), sits alongside two other levers for growing a team's output:

- **Training** — investing in people's skills and knowledge
- **Process** — investing in how people communicate and coordinate
- **Technical leverage** — investing in tools, platforms, and abstractions that multiply what people can accomplish

The key insight is that technical leverage compounds: a well-chosen abstraction doesn't just save time on one project — it raises the baseline for every subsequent project.

## Examples

Larson's examples illustrate the spectrum from external services to internal tooling:

- **Yahoo! BOSS** offered structured search results as a service, letting teams build search pages without first building a search engine.
- **Hive at Digg** replaced hand-written MapReduce jobs with a query language over HDFS, dramatically lowering the cost of data analysis.
- **Language-level arguments** — the case for switching from a lower-level language to a more productive one is fundamentally a technical leverage argument.

## Embedding leverage in product work

Larson describes SocialCode's approach: rather than creating standalone "tech innovation" projects, they ensured each product project had at least one potentially novel or innovative aspect. This created a framework of **low-cost experimentation** where:

- Successful ideas get incorporated into subsequent projects
- Failed experiments don't cause entire projects to be thrown away
- The team accumulates leverage incrementally, as a side effect of shipping

This is a pragmatic alternative to the more common model of a dedicated infrastructure or platform team.

## The dedicated-team trap

Larson is explicitly wary of the seemingly logical next step — pulling out the best engineers into a dedicated tools or infrastructure team. His objections mirror his distrust of the software-engineer-vs-architect divide:

1. **Broken feedback loops** — decision-makers become separated from the consequences of their decisions. The people building abstractions stop feeling the pain of using them.
2. **Class systems** — it creates an implicit hierarchy where infrastructure work is "real engineering" and product teams are second-class, which is both culturally toxic and factually wrong.

This connects to the broader pattern in [[infra-product-management]], where Larson argues that infrastructure teams succeed by adopting product-management practices — discovery, user empathy, validation — rather than by operating as an ivory tower. The leverage argument strengthens this: if leverage comes from embedding innovation in product work, separating the two undermines the mechanism.

## Relationship to technology choice

The concept of technical leverage exists in productive tension with the philosophy of [[choose-boring-technology]]. Boring technology maximizes leverage *from reliability and familiarity* — the team can move fast because they understand the stack deeply. Novel technology gambles on leverage *from capability* — a better tool might multiply output if the adoption cost is manageable. Larson's embedded-experimentation model is one way to resolve this tension: try novel approaches within the safety net of a shipping project, and only adopt what proves its worth.

## Temporal notes

Written in 2012, this is an early-career Larson piece — brief and suggestive rather than prescriptive. His later writing (including the 2018 [[infra-product-management]] piece and the book *An Elegant Puzzle*) develops these themes into more actionable frameworks. The core framing — technical leverage as a named, explicit organizational goal — remains highly relevant. If anything, the rise of AI-assisted development tools has made the concept more urgent: teams choosing the right AI tooling are seeing multiplicative productivity gains, which is technical leverage in its purest form.

## Sources

- Larson, Will (2012). "Building Technical Leverage." <https://lethain.com/building-technical-leverage/> — [[2012-11-04-building-technical-leverage|local copy]]
