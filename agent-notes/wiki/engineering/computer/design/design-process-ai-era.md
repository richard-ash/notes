---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/design/2026-03-01-design-process-ai-era.md
compiled_at: 2026-04-20
model: claude-opus-4-6
confidence: medium
---

# Design Process in the AI Era

The traditional design process — discover, diverge, converge, iterate, hand off — is being dismantled not by a deliberate redesign of the discipline, but as a second-order effect of engineering velocity. Jenny Wen (head of design for Claude Co-work at Anthropic, previously director of design at Figma) argues that when engineers can spin up seven coding agents simultaneously and ship features faster than designers can mock them, the old "trust the process" gospel becomes a bottleneck rather than a safeguard.

## The forcing function

Wen's core claim: design isn't changing because designers decided it should. It's changing because engineering changed first. When any engineer can talk through an idea, have an agent produce a working version, and ship it in hours, the designer's traditional gatekeeping role — producing beautiful mocks, leading with pixel-perfect specs — becomes untenable. The timeline for one mock-to-handoff cycle now exceeds the time for multiple build-test-learn cycles.

This echoes [[linear-design-process|Linear's approach]] of treating the live product as source of truth rather than the design file, but at a more radical scale. Linear's insight was that design files are disposable references; Wen's observation is that the entire upstream process (discovery → mocks → specs) is collapsing into two stratified modes.

## The two types of design work

Wen identifies two distinct modes that are replacing the old unified process:

**1. Execution support (consulting mode).** The designer works alongside engineers as features ship, providing feedback, polish, and coherence rather than upfront specifications. This includes:
- Jamming and whiteboarding with engineers on in-progress work
- Giving design feedback on working prototypes (not static mocks)
- Doing "last mile" implementation — actually writing code to polish UI, fix spacing, swap components
- Pointing engineers toward design systems and shared patterns

**2. Short-horizon vision setting.** Rather than 2-5 year design visions in polished decks, this mode produces 3-6 month directional prototypes that point the team toward coherence. The purpose is alignment: when anyone can build anything, someone needs to ensure the collective output makes sense together.

## The time allocation shift

Wen quantifies the change in her own work:

| Activity | Before AI agents | Now |
|---|---|---|
| Mocking & prototyping | 60-70% | 30-40% |
| Engineer pairing & consulting | ~20% | 30-40% |
| Implementation (writing code) | 0% | ~10-20% |
| Coordination | ~10% | remainder |

The traditional elements (user research, prototyping, mocking) haven't disappeared — they've shrunk proportionally. The new slice is the designer as implementer, directly polishing code and shipping.

## Why Figma still matters

Despite the shift toward code, Wen argues design tools like Figma retain a critical advantage: **parallel exploration**. Coding with AI agents is inherently linear — you invest deeply in one direction and iterate. Figma's canvas lets you explore 8-10 different directions simultaneously, which Wen considers essential for the best design work. Fine visual and interaction details (typography, micro-interactions) also benefit from the canvas model.

This suggests a future where design tools serve exploration and code tools serve execution, rather than design tools being replaced entirely.

## Building trust through speed

Wen introduces a philosophy for maintaining craft and quality when shipping velocity exceeds design capacity: **build trust through speed**. The approach:

1. Ship early with clear caveats ("research preview")
2. Commit publicly to iteration
3. Respond visibly to user feedback
4. Ship improvements fast enough that users see continuous progress

The key risk: shipping early and then going silent. That degrades brand trust. But shipping early with visible, responsive iteration actually builds trust — users feel heard and see the product improving in response to their input.

## AI and taste

Wen takes a less defensive position on AI's design capabilities than many in the field. She believes AI will get meaningfully better at taste and judgment, and that designers may be "holding on too much" to the idea that aesthetic and product taste will remain exclusively human domains.

However, she identifies the durable human role as **decision accountability** — someone still has to decide what gets built, resolve disputes between people with competing visions, and be accountable for whether the product actually works. The hardest parts of building software, she argues, are interpersonal and political, not technical.

Her assessment of Claude as a designer (as of early 2026): good at first passes and generating multiple options, but not yet at the level of a "hireable" designer — lacking the strong generalist depth, deep specialist skill, or the eager adaptability of the best new grads.

## Three archetypes for hiring designers

Wen identifies three designer profiles that are especially valuable in the AI era:

1. **The strong generalist ("block-shaped")**: Not just mediocre at many things, but 80th-percentile good across multiple skills — design, PM, engineering. Rare, but critical when the design role is expanding into adjacent disciplines.

2. **The deep specialist ("deep T")**: Top 10% in a specific area — could be a designer who's essentially half software engineer, or someone with extraordinary visual design or icon work. In a world where anyone can produce adequate work, deep specialization is what differentiates.

3. **The craft new grad**: Early-career, humble, wise beyond their years, eager to learn. Wen argues these are systematically overlooked because companies default to hiring senior talent. But new grads benefit from having no entrenched processes to unlearn — they adapt to the new workflow natively.

## Management in the AI era

Wen moved from Director of Design at Figma (managing 12-15 designers) to IC at Anthropic, partly to stay close to how the work is actually changing. Her observations on management:

- **Pure people management is declining.** The future manager combines direction-setting with people management, not just career coaching and 1:1s.
- **IC rotations build empathy.** Design managers should periodically return to IC work to understand how the process has changed, similar to engineering managers who take coding rotations.
- **"Low leverage" tasks are high leverage when leaders do them.** Senior leaders who dogfood the product, repro bugs, and make anniversary cards create outsized cultural and operational impact precisely because the work is "beneath" their level.
- **Psychological safety enables high standards.** Teams where members feel comfortable enough to roast each other (and their manager) are teams where critical feedback flows freely. The key balance: combine deep caring with high standards — radical candor by another name.

## The legibility framework applied to design

Wen adapts Evan Tana's (SPC partner) legibility framework — a 2x2 of legible/illegible founders crossed with legible/illegible ideas — to the designer's role at a frontier AI lab. If both the founder and idea are legible, the opportunity isn't novel. The interesting space is where the idea is illegible: on the frontier, not yet articulable, but generating energy among the people close to it.

Wen sees part of the designer's role as **spotting illegible ideas and making them legible** — through UX, form factor, and storytelling. She cites Claude Studio, an internal Anthropic prototype with a dense, powerful interface that she initially couldn't make sense of, but which had strong energy from research teams. From that illegible prototype, the team extracted the skills framework (markdown instruction files) and the information patterns (Claude's plan, to-dos, context) that eventually shaped Claude Co-work's interface.

The implication: designers at the frontier should operate like internal VCs — scanning for illegible prototypes with disproportionate energy, then translating them into legible products.

## Sources

- Wen, J. (2026). "The design process is dead. Here's what's replacing it." Lenny's Podcast. <https://www.youtube.com/watch?v=eh8bcBIAAFo> — [[2026-03-01-design-process-ai-era|local copy]]
