---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-09-27-naam-wheres-the-intelligence-explosion.md
compiled_at: 2026-09-29
model: claude-fable-5-1
confidence: medium
---

# Recursive self-improvement

**Recursive self-improvement (RSI)** is the claim that AI systems can do AI research, so each model generation builds a better successor faster than the last, until the loop runs away into a "fast takeoff" (or "FOOM") toward artificial superintelligence (ASI). It is the mechanism behind the intelligence-explosion scenarios debated in [[agi-timelines]] and the "explosive technology growth from automated R&D" assumption in [[ai-explosive-growth]], and the frontier labs treat it as a live goal: in September 2026 Noam Brown said RSI is OpenAI's top priority "by a wide margin," ranked above models that sell.

This article's anchor source is Ramez Naam's September 2026 guest essay on Noah Smith's *Noahpinion*, "Where's the 'intelligence explosion'?", the most data-driven skeptic's case in this wiki. Naam's headline claim: **on the best current data, the self-improvement loop would need to be roughly 5–10× stronger just to sustain itself, let alone run away.** He expects blistering progress by the standard of any other technology, narrow superintelligence in verifiable domains, and eventual autonomous self-improvement, but not a runaway loop without a conceptual breakthrough. Smith's own framing in the introduction is agnostic and worth keeping alongside: the case rests on many assumptions, we will have to wait and see, and in practical terms the debate may matter less than it seems because "the AI of 2040 is going to look godlike, whether or not it explodes into an actual god in 2027."

## Naam's five-type taxonomy

"RSI" gets used for everything from AI boosting human researchers' productivity to AI bootstrapping itself to incomprehensible intelligence. Naam's taxonomy separates productivity gains from autonomy from runaway:

| Type | What it means | Status (Naam, September 2026) |
|---|---|---|
| 1 | AI raises the productivity of human AI researchers and engineers | Clearly happening |
| 2 | A stronger AI trains or improves a weaker one (distillation; teacher/student loops such as Karpathy's autoresearch) | Clearly happening |
| 3 | A further step in autonomy (defined in Naam's figure, not in the text) | No clear evidence; Alibaba has made strong claims |
| 4 | An AI autonomously designs, trains and tests its own successor | Not seen |
| 5 | A runaway loop with *accelerating* returns, ending in superintelligence | Would need a conceptual breakthrough Naam does not see |

The load-bearing distinction is between Types 2–4, which raise autonomy but still face diminishing returns, and Type 5, which requires returns to *accelerate*. Closing the loop (Type 4) says nothing about whether it is strong enough to sustain itself. Naam notes Weco's four levels are close to his and points to Tom Cunningham's definitions guide for the full zoo of meanings. Lilian Weng's harness-layer view of the same question is in [[self-improving-harnesses]].

## Narrow superintelligence is already here

Naam expects, and says we already have, **narrow superintelligence in highly verifiable domains**: chess and Go, the most formal parts of mathematics (proofs and counterexamples to major conjectures, with OpenAI's reported AI-generated resolution of Navier–Stokes existence and smoothness as his example), and the verifiable parts of coding. His criteria for a highly verifiable domain: formal, structured work where machines can generate unlimited training data, verify correct versus incorrect near-perfectly, and do so entirely in software without waiting on the physical world or on humans. That is the same verifiability boundary [[agentic-engineering]] draws for coding agents and [[ai-for-mathematics]] traces inside mathematics. Narrow is not broad: models still need far more training data than humans, learn unreliably from ongoing experience, and fail on tasks people find straightforward. Superhuman math does not imply superhuman judgment elsewhere.

## Real AI research is much harder than benchmarks suggest

The essay's first empirical move compares benchmark horizons against the only public data on AI doing actual AI research.

- **OpenAI's Research Acceleration report** (September 2026) logged how often its models completed internal research tasks with and without human help, bucketed by how long a human would need. Even on sub-15-minute tasks, models succeeded unaided 86% of the time; the 80%-success horizon on research work was roughly **15 minutes**, and July looked like the whole-period average.
- **Anthropic's pace-of-development graph** shows Claude collaborating on or leading more than 90% of internal R&D tasks, and **zero** cases of fully autonomous completion.
- **METR's** evaluation of Mythos Preview put the 80% horizon on its coding tasks at about **3 hours**. Epoch's rule of thumb (five ECI points ≈ one doubling of METR horizon) extrapolates GPT 5.6 Sol to ~4 hours and GPT 6 Astra to ~11 hours; the **AI 2027** scenario forecast ~11 hours by July 2026.

The benchmark-derived horizon is therefore ~16× OpenAI's measured research horizon and the AI 2027 forecast ~44×. Naam concedes the tasks differ, but argues the gap is far too large to be explained by that alone, and reads it as partial vindication of Nathan Witkin's January 2026 critique that the METR graph exaggerates progress. The implication he draws: be wary of declaring AI 2027 "on track" from benchmarks, as the AI 2040 authors do. Fully autonomous RSI needs an AI to chain many research tasks reliably over work humans need weeks or months for; a 15-minute horizon is not close.

## Impressive activity numbers, sharply diminishing results

OpenAI's report also shows 124× more tokens per researcher, ~7× more lines of code per engineer, and **1.6×** more experiments per researcher than the 2025 average. Naam's point is that only the last is close to a research *output*, and an enormous rise in activity has bought a modest rise in experiments. Anthropic's numbers rhyme: engineers write ~8× the code of 2024, and an opt-in survey of 130 staff gave a geometric-mean productivity uplift "on the order of 4×" from Mythos Preview versus no AI. Anthropic's Mythos Preview system card then states that reaching 2× on overall progress through this channel "would require uplift roughly an order of magnitude larger", which Naam translates as roughly 40× productivity to double the pace of progress. He adds a speculative power-law exponent of ~0.2 from experiments to progress, under which 60% more experiments is on the order of a 10% faster improvement rate.

The alternative routes to more capability show the same curve:

- **Test-time compute.** On OpenAI's unsolved-math results, success rises roughly with the log of compute: each doubling buys about the same gain at twice the price.
- **Agent swarms.** Toby Ord's swarm-scaling analysis gives a square-root rule of thumb (100 agents finish in one tenth the time at ten times the cost), and on his three benchmarks a swarm buys less per token than one agent thinking longer. Agents also **think alike**: in a study against 467 people, the first ten LLM responses matched the collective creativity of eight to ten humans, after which two AI responses added about as much as one extra human. Naam grants Lisan al-Gaib's "Accidental Scaling" point that swarms can be a potent cyber-weapon even when inefficient, but rejects giving swarms credit for the math results; Noam Brown would not give multi-agent methods even 10% of the credit for Navier–Stokes, which came from large-scale RL on a pretrained model.
- **Better models.** The strongest version of the RSI argument is that a more capable model can do research no number of copies of the old one can. Naam accepts this, then notes that data, training compute, model size and RL compute all show diminishing returns in Chinchilla, ScaleRL and OpenAI's own scaling plots, so building the better model runs into the same wall.

## No runaway acceleration in the public data

Epoch's ECI frontier has gained about **16 points a year** on a trend fitted from January 2024 to September 2026: fast, but linear. Anthropic's internal AECI series looked like a trend break after Mythos, which Eli Lifland (an AI 2027 and AI 2040 co-author) read as alarm bells for an intelligence explosion; Naam reads the subsequent data as a one-time level jump with no rising rate.

Meanwhile the inputs have grown exponentially: Epoch's estimate of AI chip capacity in H100-equivalents rose ~127× in just over three years, and AI infrastructure now absorbs ~3% of US GDP. Until recently hyperscalers funded this from profits; from here investment increasingly depends on AI revenue, and Naam expects investment growth to slow from exponential to something more modest, which would slow capability progress unless better AI research tools offset it. He then quotes the crux from Anthropic's Claude Fable 5.1 & Claude Mythos 5.1 system card: internal AI use "has been a key factor in *maintaining* the current rate of progress, but we do not yet see clear signs of dramatic acceleration beyond that rate." Better AI may already be needed just to hold the pace. Consistent with that, Opus 5.5 gains substantially on coding and computer-use benchmarks but only 2.6 points (within error bars) over Opus 5 on CoBench, Anthropic's benchmark built from historical AI R&D problems, which in any case tests research debugging rather than the ability to invent a new architecture.

## Why progress gets harder

- **Ideas get harder to find.** Cunningham and Shetty's apple-picking metaphor: AI picks the low-hanging fruit fast, another copy re-picking the same tree adds nothing, a stronger model reaches higher, and (Naam's addition) the apples get sparser as you climb. Bloom et al. document falling research productivity across fields, and Eroom's Law has inflation-adjusted R&D cost per approved drug doubling every nine years.
- **Software R&D shows gentle diminishing returns that do not translate into capability.** Epoch's Stockfish analysis puts returns to research effort at ~0.83, but those are compute-efficiency gains, and capability has steep diminishing returns in compute.
- **Autonomous loops show it too.** In Karpathy's autoresearch (a Type 2 teacher/student loop), one public run did 89 experiments in 7.5 hours with 92% of the gain arriving by run 44; a later run went further, so it was not a hard ceiling, but the shape was front-loaded.
- **Models struggle with big ideas.** The Opus 5.5 system card says the model "mostly tests incremental ideas and prefers less ambitious hypotheses" and "deferred to the published literature" in a biology exercise; METR's assessment in the same card says full automation of AI R&D will need large improvements in foresight, prediction, creating one's own feedback loops, and "judgement or taste." Naam speculates that the training corpus contains far more incremental work than breakthroughs, which may make novelty hard to learn, and that swarms cannot fix this because of the homogeneity problem.

## The quantitative core: threshold versus measured loop strength

Naam's estimate leans on *The Economics of Recursive Self-Improvement* by Tom Cunningham and colleagues at the Elasticity Institute, which parameterizes the loop as **how much more research productivity each additional ECI point buys**. Two numbers matter:

1. **The self-sustaining threshold.** Their model finds roughly **15% more research productivity per ECI point** is where each cycle powers the next; above it the loop accelerates, below it each turn adds less than the last. Naam's re-fit with Stockfish data nudges the threshold to ~19%, a difference he says not to weight. The model isolates the software loop; outside investment can still drive rapid progress below the threshold.
2. **Today's loop strength.** Cunningham et al. estimate ~**9% per point**, derived from Anthropic's 4× survey uplift across ~16 ECI points since early Claude Code (assuming earlier tools added little), and they themselves warn the 4× is probably high. Naam recalibrates with OpenAI's logged data: 1.6× experiments per researcher over the same ~16 points works back to ~**3%**, and because tokens and experiment compute also grew, he adopts **2–3%** as a working assumption.

His reasons for preferring OpenAI's dataset: it is measured directly on infrastructure rather than self-reported, it covers every active experimenter rather than 130 opt-in respondents, and it likely contains tens to hundreds of thousands of experiments across 32 weeks. The result is a **five- to tenfold gap** between measured loop strength and the threshold, with the honest caveats that experiment counts may not capture research quality, the assumed capability change may be wrong, and the datasets are noisy (nobody knows which model researchers used on which day).

## What could change the picture

- **Other loops.** Davidson, Halperin, Houlden and Korinek's "singularities" paper models software, hardware and economic feedback together; several loops can combine to overcome diminishing returns where one cannot, and Naam calls it the most compelling integrated model he has seen. His objection is calibration: their central case puts *fully automated* software research roughly at the explosive threshold on its own, while the measured loop sits far below. Full autonomy removes the human bottleneck without removing diminishing returns in training, test-time compute or algorithm search (the Type 4 versus Type 5 distinction again). He also wants chip-design-to-deployment lag built in, and doubts how much past chip progress came from ideas versus ever-costlier fabs.
- **A transformer-scale breakthrough**, or better memory, training data and research judgment. Naam notes diminishing returns are as old as machine learning (Cortes et al. were fitting power-law scaling curves in 1993), so the default should be that they persist until a new approach demonstrably escapes them.
- **Better data.** Naam admits he may be over-weighting a few observations toward a comforting conclusion. Cheryl Wu welcomed OpenAI's disclosure while listing what is missing, and Wu, Arjun Ramani, Basil Halperin and colleagues at the Elasticity Institute published *How to Measure RSI*, eight things labs could share. The measurement Naam most wants: how much useful research each new model adds at roughly constant resources, and how that turns into capability.

## Synthesis

**Three bear cases, three different targets.** The wiki now holds three skeptical positions on runaway AI, and they attack different links in the chain. Karpathy ([[agi-timelines]]) argues from history that no technology produces a regime change in GDP. Moll and Imas ([[ai-explosive-growth]]) grant a capabilities explosion and argue it will not become an economic one. Naam argues the capabilities explosion itself is not showing up in the data. His is the narrowest and the most falsifiable: he takes the pro-RSI model on its own terms and disputes one coefficient. Naam and Moll–Imas both lean on Bloom et al.'s falling research productivity, so "ideas get harder to find" is the shared spine of the economic skeptics' view.

**A constant rate is an equilibrium, not a reading of loop strength.** The essay's most important inference is easy to miss. A public ECI frontier growing at a steady 16 points a year is compatible with a weak loop, but also with a strong loop being exactly cancelled by rising difficulty and slowing input growth, which is roughly what Anthropic's "maintaining" sentence describes. That is why Naam cannot rest on the trend chart and has to estimate productivity-per-ECI-point directly, and it means the thing to watch is not the frontier slope but that coefficient. The threshold framing has the shape of a reproduction number: 2–3% against 15–19% is an R of roughly 0.1–0.2, and revisions to that estimate matter more than any single model release.

**The macro numbers and the micro bottlenecks agree.** Weng's seven bottlenecks to full RSI in [[self-improving-harnesses]] are the mechanism-level version of Naam's aggregate observations: diversity collapse in evolutionary loops is the agent-swarm homogeneity finding, weak and fuzzy evaluators are why superintelligence stays confined to verifiable domains, and the missing research taste that METR flags is what [[ml-research-craft]] treats as a trainable sub-skill. If taste is trainable, that is the channel through which Naam's coefficient could move.

**Where the argument is weakest.** Experiments per researcher is a poor proxy for research output if better models change experiment quality, which Naam concedes; the 1.6× and the 16 ECI points are stitched together from different populations and periods; and the horizon comparison sets OpenAI's internal research tasks against METR's software tasks, so some of the 16–44× gap is task difficulty rather than benchmark inflation. His critique of Davidson et al. is about calibration rather than structure, so a reader who accepts the multi-loop model but doubts the software calibration lands close to Naam anyway.

**Downstream uses.** [[commodity-trap]] rules out the hard-takeoff-produces-a-monopoly route as something nobody can plan around; Naam supplies the evidence that it is not imminent either. [[labor-share-under-automation]] names RSI and continual learning as the technical questions that decide whether concentration runs away, and [[pacing-the-frontier]] records that Amodei's actual worry is RSI escaping human control. Naam's essay is the current best estimate of how far that worry sits from the data, and the Elasticity Institute's eight disclosures are the list of what would move the estimate. Deutsch's point in [[beginning-of-infinity]] that copying minds is not free is the older, philosophical version of Ord's swarm-cost result.

## Sources

- Naam, Ramez (2026-09-27). "Where's the 'intelligence explosion'?" Guest post on Noah Smith's *Noahpinion*; also published on Naam's own Substack, where the essay's section anchors point. <https://www.noahpinion.blog/p/wheres-the-intelligence-explosion> — [[2026-09-27-naam-wheres-the-intelligence-explosion|local copy]]

Primary sources the essay builds on: Cunningham et al., *The Economics of Recursive Self-Improvement* <https://elasticity.institute/rsi-paper.pdf>; OpenAI, *Research acceleration: a view inside OpenAI* <https://openai.com/index/research-acceleration-view-inside-openai/>; Davidson, Halperin, Houlden & Korinek, *Singularities* <https://basilhalperin.com/papers/singularities.pdf>; Elasticity Institute, *How to Measure RSI* <https://elasticity.institute/how-to-measure-rsi.pdf>; Ord, *Swarm scaling* <https://www.tobyord.com/writing/swarm-scaling>.
