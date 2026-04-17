---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2022-12-14-chatgpt-imagenet-moment.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: medium
---

# Generative AI as pattern generation

Benedict Evans frames the generative AI wave as a second "Imagenet moment" — a step change in capability that will generalise far beyond the initial demos, just as ML-based image recognition in the early 2010s generalised far beyond cat pictures.

## The core reframing

Evans argues that classical ML's conceptual shift was turning problems that are "easy for people to do, but hard for people to describe" from logic problems into statistics problems. Generative networks run this in reverse: once you've identified a pattern, you can create something new that fits that pattern. The key insight is that these systems are not working from canonical concepts — they are matching, recreating, or remixing patterns that *look like* those concepts.

This leads to Evans's central strategic question: if the generalisation question for ML was "what can we turn into pattern recognition?", the equivalent for generative AI is **"what can we turn into pattern generation?"** — and crucially, **what error tolerance does each domain have?**

## Error tolerance by domain

Evans introduces a useful taxonomy of output precision requirements:

- **No wrong answers** — creative work (images, style mashups). A 92% accurate "Alien directed by Wes Anderson" is fine; nobody checks Sigourney Weaver's exact hairstyle.
- **Roughly right** — summaries, first drafts, brainstorming. Directional accuracy matters more than precision.
- **Precisely right or wrong** — code, contracts, factual claims. A "98% accurate" JavaScript function where the 2% error breaks execution is effectively 0% useful.

This framework explains why hallucination is devastating in some applications (legal, medical, code) but irrelevant in others (creative ideation, style transfer). Evans illustrates this with ChatGPT's bio of him — it's an *extremely accurate depiction of the kind of thing* bios tend to say, even though the specific facts are wrong. The pattern is right; the instances are fabricated.

## Creation vs. remixing

Evans draws a sharp distinction between recombination within known patterns and genuine novelty. Generative systems can produce "cats in space suits" by combining existing patterns, but the originality lives in the prompt, not the model. He contrasts this with AlphaGo, which could evaluate its own outputs via self-play — it had **automated, scalable feedback**. Generative text and image models lack this: they are Borges's Library, full of masterpieces no one can find because there is no scoring function.

Evans's punk-rock test: a generative system could make more disco, and could make punk if prompted specifically enough, but it would never *know it was time for punk*. The originality that matters is in breaking patterns, not fitting them.

## Humans in the loop

Every billion-scale system requires humans in the loop — the question is where to place them for maximum leverage. Evans traces a progression: Yahoo tried manual cataloguing (unscalable), Google used aggregate human behaviour as signal plus user selection from results (scalable). Generative networks similarly rely on human-created training data on one side and human prompt-crafting and output selection on the other.

Evans's "infinite interns" metaphor for ML extends to generative systems: they're like a ten-year-old who has read every book in the library and can repeat things back to you, but garbled and without understanding that Jonathan Swift wasn't *actually* proposing eating babies.

## Implications for search

Evans poses a question that presaged the generative search debate: how many Google queries are searches for something specific (retrieval) versus requests for an answer that could be generated dynamically (synthesis)? The librarian analogy — do you ask where the atlas is, or ask them to tell you the longest river in South America? Different query types have different tolerance for generated answers.

See also: [[the-bitter-lesson]] for the broader thesis that compute-heavy general methods outperform hand-engineering, and [[ai-judgment-atrophy]] for the downstream risk when humans cede too much of the evaluation loop.

## Temporal notes

This essay was published in December 2022, weeks after ChatGPT's launch. Since then:

- **Error tolerance has shifted.** Chain-of-thought reasoning, tool use, and retrieval-augmented generation have substantially improved factual precision in domains Evans flagged as "precisely right or wrong." Code generation in particular has moved from "98% accurate" novelty to production-grade tooling (see [[ai-coding-harnesses]]).
- **The "scoring function" problem partially solved.** RLHF, constitutional AI, and reward models provide exactly the kind of automated feedback Evans noted was missing — though these still rely on human preference data, vindicating his humans-in-the-loop argument.
- **Generative search shipped.** Google (AI Overviews), Perplexity, and others launched generative search products, answering Evans's question about which queries could be generated. The answer: many, but with persistent hallucination concerns for precise factual queries.
- **The "infinite interns" metaphor evolved.** With agentic systems (see [[agentic-engineering-architecture]]), the metaphor is shifting from "intern who can repeat things back" to "junior engineer who can execute multi-step tasks" — though Evans's core point about lacking structural understanding remains debated.

## Sources

- Evans, B. (2022). "ChatGPT and the Imagenet moment." <https://www.ben-evans.com/benedictevans/2022/12/14/ChatGPT-imagenet> — [[2022-12-14-chatgpt-imagenet-moment|local copy]]
