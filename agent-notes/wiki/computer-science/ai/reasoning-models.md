---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-09-23-pavlus-ai-reasoning-wrong-reasons.md
compiled_at: 2026-09-23
model: claude-fable-5-1
confidence: medium
---

# Reasoning models

Large reasoning models (LRMs) — o1-style models trained to emit a "chain of thought" before answering — and the unsettled scientific question of what those chains are. Compiled from John Pavlus's July 2026 *Quanta* essay "Is AI Reasoning Right for the Wrong Reasons?", a reported survey of the dispute over whether reasoning traces are (a) faithful records of what the model is doing, (b) causally necessary to its answers, or (c) neither — and whether it matters.

The piece is a journalist's synthesis of interviews (Melanie Mitchell, Subbarao Kambhampati, William Merrill, Pavel Izmailov, Weiyan Shi, Sébastien Bubeck, Tal Linzen, Pradeep Dasigi) rather than a primary result, and it takes a position: Pavlus lands on "wishful mnemonics all the way down." Claims below are attributed accordingly. Several of the events it reports (GPT-5.5, the May 2026 unit-distance disproof, AlphaProof Nexus, ICML 2026) are taken from the article rather than independently checked.

## The whiplash

Pavlus frames the topic as a run of contradictory headlines from 2025 into 2026:

- Apple's "Illusion of Thinking" (2025) found "complete accuracy collapse" on simple puzzle families — then LRMs took gold at the International Mathematical Olympiad.
- Mitchell's Santa Fe Institute group showed LRMs pass carefully designed reasoning benchmarks (ARC-AGI-1) via "surface-level shortcuts" — then DeepMind and Terence Tao used AI to rediscover or improve solutions to 67 problems across analysis, combinatorics, geometry and number theory.
- Linzen's NYU lab showed LRMs fail to apply an algorithm reliably even when they possess it and have the compute budget — then an OpenAI "general-purpose reasoning model" disproved the unit distance conjecture in one shot in May 2026 (see [[ai-for-mathematics]]).

Pavlus's question is not whether the results are real (he thinks they are) but how "BS and not-BS" can both be true at once.

## Mitchell's index card

Mitchell's summary of what is actually known:

1. **It works.** LRMs beat plain LLMs on reasoning tasks.
2. **The trace isn't necessarily faithful** to what is happening inside the model.
3. **Much of the trace isn't even useful.** You can remove it.

Points 2 and 3 are where the paradox lives.

## Faithfulness: the evidence that traces are not what they look like

Chain-of-thought began in 2022 as a prompting hack (Wei et al.; Kojima et al.'s "think step by step"). LRMs, starting with OpenAI's o1 in 2024, are trained — mostly via reinforcement learning — to generate that scaffolding themselves and feed it back into their own context. Because the output is fluent text, it *looks* like a paper trail.

The research Pavlus assembles against the paper-trail reading:

- **Traces can be replaced with garbage.** Kambhampati's ASU lab (NeurIPS 2025) swapped a model's correct traces for incorrect or irrelevant ones on a formal reasoning task; performance did not degrade. Training only on correct traces still produced invalid traces alongside correct answers.
- **Traces can be replaced with dots.** Pfau, Merrill and Bowman (NYU, 2024) showed "meaningless filler tokens" — literal strings of dots — can stand in for a human-readable chain of thought under the right conditions. Merrill: "There's no guarantee the chain of thought has to be meaningful in any sense."
- **RL doesn't ask for faithfulness.** Izmailov (NYU and Anthropic, on Anthropic's original reasoning-model team) doubts RL even incentivizes faithful traces: "maybe it will ... but I would say the chances are not very high."
- **Half the steps don't matter.** Shi and colleagues (Northeastern/Berkeley, 2025) found 30–60% of "thinking steps" in frontier open-source LRMs had "minimal causal impact" on math-benchmark answers; deleting half barely dents performance.

Kambhampati's group's ICML 2026 position paper puts the conclusion in its title: "Stop Anthropomorphizing Intermediate Tokens as Reasoning/Thinking Traces!" His word for the tokens is "mumblings."

The industry counter, from Bubeck (OpenAI): the critical papers deserve "big, big air quotes"; Apple's earlier GSM-Symbolic-era results came from a training quirk in now-obsolete models, and "modern models starting with GPT-5.5 do not suffer from this issue." Every researcher Pavlus spoke to conceded that negative findings on smaller open models may not generalize to frontier products, whose internals are trade secrets. But Pavlus flags the asymmetry: OpenAI's "released chain of thought" for the unit-distance proof is a *rewritten summary* produced by two human experts using Codex, and OpenAI, DeepMind and Anthropic have not published raw traces since 2024. The strongest claims for faithfulness therefore rest on evidence nobody outside the labs can examine.

## Kambhampati's approximate-retrieval hypothesis

Kambhampati's account starts where Bubeck's does — an LRM is just an LLM with more specific training, "there is no extra magic" — and goes the opposite direction:

- Given how LLMs are trained, narrating a genuine step-by-step derivation before answering is a *harder* task than guessing the answer directly. So it's implausible that this is what the model does.
- Working hypothesis: LRMs perform **approximate retrieval** over their training corpus — "somewhere in the middle" between pattern matching and reasoning, closer to the former.
- The job of thinking tokens is not to narrate a chain of thought (there isn't one) but to **load the context window** so that reasoning-shaped continuations become more likely to be retrieved. Analogy: mumbling words to yourself to jog memory. The words barely matter as long as they knock something loose.
- Because the operative objects are embeddings rather than words, tokens need not be coherent English. They can be fragments of other languages, fake "aha" exclamations, or dots. "Whether the embedding corresponds to a single word or not is beside the point."

This dissolves the paradox directly: traces can be semantically junk and still elicit correct answers, because their function is contextual priming rather than reporting.

It also explains the shape of progress. LRMs improve fastest in **verifiable domains** — code runs or doesn't, proofs check or don't — because binary outcomes plus written steps make cheap training signals. The model doesn't have to learn a general reasoning procedure; it has to absorb enough examples of what steps *look like* to mimic them while "stitching together" a plausible result that something else then verifies. The limit of that step-following capability is what Kambhampati calls the **inference horizon**, and he reads Apple's accuracy-collapse results as a measurement of it. Newer models push the horizon out, jaggedly, most likely by "leveraging an ever-enlarging set of examples and clever reward signals" rather than by learning the algorithm.

A further reason state-of-the-art systems work, per both Kambhampati and Mitchell: they are usually wrapped in ordinary software that guides and verifies — agentic coding systems, or DeepMind's AlphaProof Nexus with Lean. Kambhampati wants to explain the stand-alone "think" part, which OpenAI is doubling down on. Bubeck found the Lean question almost nonsensical: "the model is reasoning like a human would. And when humans reason, we don't use Lean."

## Does it matter?

Mitchell: it depends. AlphaFold is a black box doing "incredibly complex statistical associations" nobody understands, and biology embraced it anyway; if LRMs do the same for mathematics, verify the outputs and move on. Bubeck's line is the same: more productive to talk about what the models can do than why.

The counterarguments Pavlus collects:

- **Trust outside verifiable domains.** Mitchell: "You want the right answer for the right reason, so you can trust these things" — precisely where no verifier exists.
- **Reliability regardless of label.** Linzen: whatever you call it, you want a system that can apply an algorithm reliably.
- **Foregone improvements.** Dasigi (AI2): treating chains of thought reverently may leave better ways of biasing LRMs toward correct outputs unexplored.
- **A fake theory is worse than none.** Kambhampati calls taking traces seriously a scientific rabbit hole on the order of geocentrism or the ether — intuitive models that fit the visible evidence and were wrong. "A fake theory is worse than admitting that we don't have a theory."

## Wishful mnemonics

Pavlus's own resolution reaches (via Mitchell) for Drew McDermott's 1976 paper "Artificial Intelligence Meets Natural Stupidity": naming your program's main loop UNDERSTAND begs the question and misleads the researcher most of all; call it G0034 and then try to *convince* anyone it implements understanding. "Reasoning model," "chain of thought," and "thinking tokens" are, in Pavlus's reading, wishful mnemonics all the way down — not fraud, and not evidence the systems don't work, but shorthand plus suspended disbelief that the field has not yet earned. Mitchell's gloss: "We react to language in a way that is very anthropomorphizing." His closing analogy is horsepower — the word is fine as long as nobody thinks there are hooves under the hood.

## Connections and implications

**The direct tension with [[latent-space]].** Kelly's "the words are the thinking" — the scratchpad *is* the reasoning, not a report of reasoning that happened elsewhere — is presented there as the standard interpretability-informed view. Pavlus's sources split that claim in two. The *computational* half survives and is arguably strengthened: filler tokens helping at all means extra tokens buy extra compute regardless of content, which is Kelly's "more tokens makes it smarter." The *semantic* half — that reading the words tells you what the computation did — is what Kambhampati, Merrill and Shi deny. And the 30–60% causally inert steps cut against even the computational reading for a large fraction of any given trace. The reconciled position is roughly: the tokens are part of the mechanism; the meaning of the tokens mostly isn't.

**Karpathy's RL critique supplies the mechanism.** In [[agi-timelines]] Karpathy describes outcome-based RL as "sucking supervision through a straw": every token in a correct rollout is upweighted, wrong alleys included. That is a direct account of why traces accumulate non-load-bearing text, why Izmailov doubts RL selects for faithfulness, and why Kambhampati's mumblings look the way they do. Karpathy's "dhdhdhdh" reward-hacked completion is the degenerate limit of the same phenomenon.

**Verifiability explains the jaggedness on both accounts.** Karpathy's verifiability framework in [[agentic-engineering]] says capability peaks where RL has a checker. Kambhampati's hypothesis says *why* that would hold even without genuine reasoning: mimic-then-verify only needs the verifier. Mitchell's corollary is the uncomfortable one — the right-for-the-wrong-reasons risk is largest exactly where capability is weakest and no checker exists.

**Consistent with the deflationary readings elsewhere in this wiki.** Evans's pattern-generation framing ([[generative-ai-as-pattern-generation]]), Chiang's coding-is-pattern-matching argument against the 1979 Hofstadter intuition ([[ai-consciousness-and-moral-status]]), and Sutton's Deep Blue example ([[the-bitter-lesson]]) all point the same way: a system can beat humans at a task without doing what humans do to accomplish it. Mitchell and Izmailov both invoked Deep Blue as the previous unthinkable thought that became obvious. Kambhampati's "it's the training" is also a strong-form bitter lesson — general method, more examples, more compute, no reasoning module.

**Evans's caveat made concrete.** [[token-pricing]] flags that, unlike prior infrastructure cycles, there is no theory of *why* these models work, so the ceiling is unknown. Pavlus's essay is that caveat at the level of mechanism: the models' own creators disagree about what the most visible feature of the product is.

**Tao's jumping machines.** [[ai-for-mathematics]] records Tao's description of current tools as one-shot jumpers that either clear the cliff or don't, with little capacity for partial progress. That behaviour is what an inference horizon over approximately-retrieved step patterns would predict. The same article notes the published chains of thought for the unit-distance disproof "read as ordinary mathematics" — worth reading alongside Pavlus's point that what was published is a human-rewritten summary, not the raw trace. Goedecke's observation in [[expertise-as-llm-leverage]] that OpenAI's expert mathematicians "check and filter" the model's suggestions is the human-verifier version of the wrapper Kambhampati and Mitchell describe.

**Practical upshot for anyone building on these models.** Jozefiak's rule in [[agent-failure-modes]] — check the outcome, not the log line — is the engineering translation of this whole debate. A reasoning trace is not an audit log; treat it as a diagnostic at best. Put the verifier in the harness (per [[harness-engineering]] and [[self-improving-harnesses]], where evaluators stay outside the optimized loop for the same reason), and be most suspicious of confident traces in domains where nothing can check the answer.

**The epistemology.** Kambhampati's geocentrism analogy and McDermott's G0034 belong with Nielsen's argument in [[scientific-verification-loops]]: intuitive theories that fit the visible evidence can persist for decades, and a field's verification loop is not guaranteed to correct them on any schedule. Pavlus's honest bottom line is that this loop hasn't closed.

## Cited research (not ingested)

- Wei et al. (2022). "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models." <https://arxiv.org/abs/2201.11903>
- Kojima et al. (2022). "Large Language Models are Zero-Shot Reasoners." <https://arxiv.org/abs/2205.11916>
- McCoy et al. (2023). "Embers of Autoregression" — the "it's the training" approach Pavlus cites as kin to Kambhampati's. <https://arxiv.org/abs/2309.13638>
- Pfau, Merrill, Bowman (2024). "Let's Think Dot by Dot." <https://arxiv.org/abs/2404.15758>
- Mirzadeh et al. (2024). "GSM-Symbolic" — the Apple result Bubeck calls "wrong." <https://arxiv.org/abs/2410.05229>
- Apple (2025). "The Illusion of Thinking." <https://machinelearning.apple.com/research/illusion-of-thinking>
- Kambhampati group (2025, ICML 2026). "Stop Anthropomorphizing Intermediate Tokens as Reasoning/Thinking Traces!" <https://arxiv.org/abs/2504.09762>
- Linzen lab (2025). Algorithm-application failures. <https://arxiv.org/abs/2506.05205>
- Mitchell group (2025). Surface-level shortcuts on ARC-AGI-1. <https://arxiv.org/abs/2510.02125>
- Northeastern/Berkeley, incl. Shi (2025). Causal impact of thinking steps. <https://arxiv.org/abs/2510.24941>
- DeepMind & Tao (2025). 67 problems. <https://arxiv.org/abs/2511.02864>
- DeepMind (2026). AlphaProof Nexus. <https://arxiv.org/abs/2605.22763>
- OpenAI (2026). Unit-distance disproof announcement and rewritten chain-of-thought summary. <https://openai.com/index/model-disproves-discrete-geometry-conjecture/>
- McDermott (1976). "Artificial Intelligence Meets Natural Stupidity." <https://dl.acm.org/doi/10.1145/1045339.1045340>

## Sources

- Pavlus, John (2026). "Is AI Reasoning Right for the Wrong Reasons?" *Quanta Magazine*, 31 July 2026. <https://www.quantamagazine.org/is-ai-reasoning-right-for-the-wrong-reasons-20260731/> — [[2026-09-23-pavlus-ai-reasoning-wrong-reasons|local copy]]
