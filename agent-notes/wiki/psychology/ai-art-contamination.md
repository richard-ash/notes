---
source: agent
compiled_from:
  - agent-notes/raw/psychology/2026-04-22-ai-art-contamination.md
compiled_at: 2026-04-22
model: claude-opus-4-6
confidence: high
---

# AI art and psychological contamination

When people learn that AI was involved in creating a work of art, they devalue it — and the pattern of that devaluation follows the logic of *contamination*, not proportional discounting. Mandel and Imas (2026) demonstrate this through incentive-compatible auctions where participants bid real money (via a BDM mechanism) for physical art prints, avoiding the hypothetical-valuation inflation that plagues most survey-based studies of AI aversion.

## The exclusivity mechanism

Experiment 1 (N=150) varied two dimensions: who made the art (human / AI / partially AI) and how many copies existed (one / thousands). The core finding is an interaction effect:

- **Human-made art** commanded a 44% exclusivity premium when described as a single copy vs. mass-produced.
- **AI-made art** gained only a 21% premium from the same exclusivity manipulation.

This asymmetry suggests that AI art is *already perceived as non-exclusive* — people intuit that an AI can reproduce the work trivially, so limiting copies doesn't carry the same signal of uniqueness. The exclusivity premium that drives much of art's value partly relies on the perception that a human being's creative output is inherently one-of-a-kind; AI disrupts that perception at the source. Mandel and Imas note that participants' response to AI-generated art more closely resembled prior research on duplicate *artifacts* (furniture, cars) than on duplicate *artworks* — suggesting AI involvement categorically shifts how people classify the object.

## The contamination pattern

Experiment 2 (N=201) varied AI involvement on a continuous scale from 0% to 100%, using two framing conditions:

1. **Simple percentage** — "This art piece was X% the effort of AI and Y% the effort of a human artist."
2. **Artistic process** — detailed descriptions of which creative tasks (aesthetic decisions, brushstrokes, ideation) were performed by whom.

In the *artistic process* condition, devaluation was sharply **nonlinear**. Going from 0% to just 1% AI involvement — described as AI "[filling] in a very small section of the piece" — caused a 16.12% drop in willingness-to-pay. By contrast, going from 25% to 50% AI involvement caused only a ~3% additional drop. The best-fitting statistical model was a **double-kinked** function with breakpoints at 1% and 99%, not a linear slope.

The reverse asymmetry also held: a piece described as 99% AI-generated gained 27.92% in value when a human artist was described as having "filled in a very small section of the piece by hand," compared to the fully AI condition.

This is the signature of **psychological contamination** as theorized by Rozin and colleagues: a trace amount of a contaminant is sufficient to spoil the whole, while a trace amount of the "pure" substance can partially redeem a contaminated object. The pattern mirrors how people respond to physical contaminants (a cockroach briefly touching food renders it inedible, regardless of quantity) and maps onto what Rozin calls the "laws of sympathetic magic" — the principle that contact with an essence transfers its properties to the whole.

In the *simple percentage* condition, where participants saw only a number rather than a narrative about the creative process, devaluation was better fit by a simple linear model. This suggests the contamination response is activated more strongly when people think concretely about *what* the AI did, not just how much.

## Ideative vs. mechanical involvement

An important null result: there was no significant difference in devaluation between AI used for *mechanical* tasks ("filling in a section") versus *ideative* tasks ("helping refine an idea"). Both types of trace involvement produced comparable drops in valuation relative to fully human-made work. This undermines the intuition that using AI "just as a tool" for execution is acceptable while using it for creative conception is not — in practice, any AI touch contaminated the work roughly equally.

## Theoretical connections

The contamination account places AI aversion in an unexpected psychological category. Rozin's contamination framework was developed for **disgust** — an emotion evolved to protect against pathogens, poisons, and boundary violations. That AI triggers a structurally similar response suggests it may be activating deep intuitions about the boundary between human and non-human agency, not merely a preference for effort or skill.

This connects to several related lines of work:

- **The handmade effect** (Fuchs et al. 2015): consumers pay more for hand-made goods, partly because they infer the maker "put love into it." AI removes this inference entirely.
- **The effort heuristic** (Kruger et al. 2004): people use perceived effort as a proxy for quality. AI's effortless production undercuts this signal.
- **Essentialism** (Newman & Bloom 2012): people value originals over duplicates because they believe the original contains the artist's "essence." AI has no essence to transfer.

Mandel and Imas's contribution is showing that these effects are not just about the *absence* of positive signals (effort, love, essence) but about the *presence* of a negative one: AI involvement actively contaminates in a way that trace exposure matters disproportionately.

## Implications for the AI economy

This paper is the empirical complement to Imas's theoretical argument in [[ai-and-relational-scarcity]]: if AI commodifies production, what remains scarce is human involvement itself. The contamination findings sharpen this: it's not that human involvement adds value linearly — it's that *pure* human involvement commands a discontinuous premium. For artists and creators, this creates a stark binary: a work is either fully human or it isn't, and the market penalty for "isn't" kicks in immediately.

For platforms and marketplaces, the exclusivity interaction matters: restricting copies of AI art recovers less value than restricting copies of human art. Artificial scarcity is less effective when the audience already perceives the production process as inherently non-scarce.

The finding also offers a counterpoint to catastrophist narratives about AI replacing creative workers. If [[ai-judgment-atrophy|human judgment is the scarce resource]], and if the market structurally rewards its uncontaminated exercise, then human artists retain pricing power precisely because their work *cannot be replicated by AI without losing the premium*. The question is whether this premium will endure as AI-generated art becomes more prevalent, or whether it reflects a transient novelty aversion that will decay as exposure normalizes.

## Sources

- Mandel, G. & Imas, A. (2026). "Art and the Machine: Why People Devalue AI-Generated Creative Work." <https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6302659> — [[2026-04-22-ai-art-contamination|local copy]]
