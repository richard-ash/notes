---
source: agent
compiled_from:
  - agent-notes/raw/mathematics/2026-03-20-tao-ai-for-math.md
compiled_at: 2026-04-10
model: claude-opus-4-6
confidence: medium
---

# AI for mathematics

A view from Terence Tao, as of early 2026, on what AI is and isn't good at in mathematical research, and how the practice of math is starting to change. Opinionated — reflects one mathematician's perspective, but Tao is unusually well-positioned to characterize the frontier and has been directly involved in evaluating frontier-model performance on open problems.

## Kepler and the length of the verification loop

Tao opens with Kepler as a case study in how scientific progress actually happens. Kepler's early theory — that the spacing of planetary orbits matched nested [Platonic solids](https://en.wikipedia.org/wiki/Mysterium_Cosmographicum) — was beautiful and wrong. Only after stealing Tycho Brahe's decades of naked-eye observations did he spend years discovering the actual laws: elliptical orbits, equal areas in equal time, and (ten years later, on six data points) the period-distance cube-square law. It took Newton a century to explain *why* all three were true.

Dwarkesh's framing: **Kepler was a high-temperature LLM.** He tried many random relationships — including the musical notes of the planets and astrological causes of Earth's famine — and one of them happened to be the third law of planetary motion. This only worked because Brahe's dataset could verify guesses.

Tao's gloss: idea generation has always been the prestige part of science, but it must be matched by verification, or it's slop. We celebrate Kepler; we should also celebrate Brahe for the ten-times-more-precise data collection that made Kepler's fits possible.

The deeper point is that **the verification loop for correct ideas can be decades or millennia long.** During that time the ultimately-correct theory often makes *worse* predictions than the prevailing wrong one — Copernicus's circular orbits were less accurate than Ptolemy's epicycle-ridden geocentrism, until Kepler fixed them. Survival through this "epistemic hell" depends on a mix of judgment and heuristics we don't understand well enough to articulate, let alone codify into an RL loop.

Related: correct theories often also imply things that seem absurd. Aristarchus's heliocentrism was rejected in the 3rd century BC because stars showed no parallax — an implication that was actually correct, just misinterpreted. Leibniz chided Newton's gravity for implying action at a distance. Progress, Tao says, often comes not from adding theories but *deleting assumptions*: Aristotelian physics assumed objects want to stay at rest, which kept geocentrism alive until Newton's laws of motion removed the assumption.

## The bottleneck has shifted from generation to verification

> "AI has driven the cost of idea generation down to almost zero, in a very similar way to how the internet drove the cost of communication down to almost zero."

Tao argues this does not create abundance by itself. Peer review was built to filter amateur theorizing; it cannot handle the volume of plausible-looking AI output now being produced. Journals are already being flooded with AI-generated submissions. Assessing whether a given idea moves the subject forward — versus being a dead end or red herring — was already hard at the pace of individual papers and is impossible at the pace of thousands per day.

Worse, **fruitfulness depends on the future.** Many great ideas were initially ignored — [deep learning](the-bitter-lesson) was a niche area of AI for a long time. The transformer became foundational but didn't have to. Base ten isn't special; it's entrenched by inertia. You can't look at a scientific achievement in isolation and assign it an objective grade. So the question of *which* AI outputs constitute real progress may never be something you can simply reinforcement-learn, unlike localized problems with clear success metrics.

## Depth vs breadth: AI is strong where humans are weak

The clearest productive framing: **humans excel at depth, current AI excels at breadth.** Human mathematics is organized around depth because that's where human expertise lives. AI opens up a new mode — exploring new fields by first getting broadly competent AIs to map the terrain, identify islands of difficulty, and hand those off to human experts.

Tao's analogy: the problem landscape is a mountain range of cliffs in the dark. Some walls are 3 feet high, some 15, some a mile. Current AI tools are jumping machines that can leap about two meters higher than any human — better than us for the low cliffs, useless for the tall ones, and strikingly bad at *partial* progress. They either succeed or fail in one shot; they don't find handholds, pull collaborators up, and jump from there. They lack the cumulative interactive buildup that is central to what Tao calls real *intelligence* (as opposed to *cleverness*).

This is also why LLMs "don't learn" within a problem the way a human collaborator does: run a new session and the model has forgotten everything it just figured out. Whatever it discovered is at most 0.001% of the next generation's training data.

## Selection bias in AI math results

As of early 2026, AI-assisted efforts have solved ~50 of the ~1100 Erdős problems, mostly in a single burst. Tao notes the low-hanging fruit has been picked; further progress has slowed despite three separate attempts to throw frontier models at every remaining problem simultaneously.

Two important caveats on the public narrative:

1. **The problems that fell had essentially no literature.** Erdős posed them once; nobody had written up attempts. The winning proofs combined one obscure technique with one obscure existing result — exactly the move AI is good at. Tao predicts similar isolated successes on famous hard problems ("some backdoor to solve the problem that everyone else missed"), each getting viral attention.
2. **Systematic sweeps show a 1–2% per-problem success rate.** AI companies publish the wins and not the negative results, so the apparent success rate is inflated. Buying scale and picking winners works, but the honest picture is much noisier. Tao calls for standardized challenge problem sets, independent of the AI labs' self-reporting.

## What AI is actually changing in Tao's practice

Tao said in 2023 that by 2026, AI would be "a trustworthy co-author if used correctly." He thinks that prediction has held. Productively:

- Writing papers he'd produce today *without* AI would take 5x longer, but he wouldn't write them the same way — the extras are auxiliary (deeper literature searches, more numerics, more plots and code, formatting and reformatting).
- **Papers are richer and broader but not deeper.** The core activity — solving the hardest part of a math problem — still happens with pen and paper.
- AI is especially good at running all the *standard* moves on a new problem, sometimes catching errors Tao makes, sometimes introducing ones he catches. It's still bad at the step after: when none of the standard moves work, and you need to invent something.

## Lean, brute-force proofs, and whether humans can extract understanding

On the scenario where AI proves something big like the [Riemann hypothesis](https://en.wikipedia.org/wiki/Riemann_hypothesis) via a giant Lean blob:

- Some problems *have* been solved by brute force (the four-color theorem — still no conceptually elegant proof).
- Riemann is prized partly because we expect it requires genuinely new mathematics or a new bridge between unconnected areas. A brute-force verification finding a zero off the line would be possible but disappointing.
- Tao isn't as worried as some people about incomprehensible AI proofs. The beauty of a Lean proof is that every lemma can be studied atomically — you can ablate it, refactor it, get other AIs to summarize or re-derive it, run RL to make it more elegant. There will be a future profession of mathematicians doing nothing but this.
- Paper-writing used to be the most expensive part of the job, done rarely and only after the argument was checked. It's now cheap enough that hundreds of variants can be generated and compared — the Erdős problem website is already showing this dynamic.

## The missing piece: a semi-formal language for mathematical strategy

Lean gives deductive *proofs* a formal framework that AI can train on. There is no equivalent for *plausibility* or *strategy* — the subjective thing scientists do when they say "this conjecture feels right because it fits the random model." Examples of this unformalized layer:

- **The random model of the primes.** Gauss's prime number theorem, statistical rather than structural, launched analytic number theory. Over time we developed a heuristic that the primes behave pseudo-randomly. We're absolutely convinced of the twin prime conjecture because the random model says so; the few things we can prove match the model. We believe Riemann for the same reason — and a disproof would immediately kill public confidence in prime-based cryptography, because a hidden pattern in the primes probably implies more hidden patterns and therefore crypto exploits.

Tao wants a semi-formal framework mimicking the way scientists argue — using data, narrative, and plausibility — but robust enough that RL can't backdoor it. This is a wish rather than a plan. One thought experiment: simulate many "alien civilizations" of small AIs evolving math in different orders, and study which strategies actually produce progress.

## Serendipity and the danger of over-optimization

A recurring theme: Tao explicitly *protects* time for the non-optimized. Events he attended reluctantly ("like this podcast") often produced the best serendipitous connections. COVID-era remote meetings kept academics busy but killed hallway encounters. Library browsing used to surface accidental articles; now targeted search gives you exactly what you asked for, nothing more. At the Institute for Advanced Study, with no distractions, he ran out of inspiration within a few months. He needs some noise — "high temperature" — in his schedule.

There's a connection to the AI story: **by making information retrieval perfectly targeted, AI tools may further erode the serendipity that drives creative progress.** This is a distinct worry from the "will AI replace mathematicians" question, and Tao takes it more seriously.

## Outlook: human-AI hybrids will dominate math for a long time

Tao's central forecast: **complementary hybrids — smart humans assisted by powerful AI — will outperform either alone for much longer than the hype suggests.** Frontier AI is stunningly capable on some tasks and terrible on others; stacking frameworks only partially reduces errors. If a Millennium Prize problem falls soon, he would *not* put 95% odds on an autonomous AI having done it.

Historically, when entire traditional mathematician tasks got automated — solving differential equations, compiling log tables, sequencing genomes — the field didn't die. It moved on to different, larger-scale questions. Tao expects the same pattern: within a decade, much of what math students currently spend their time on will be done by AI, and mathematicians will discover that that work wasn't the most important part of what they do.

Advice to early-career mathematicians: get traditional credentials and learn the old-fashioned way *for now*, but expect a lot to change and stay adaptable. AI and Lean have already made it possible for high-schoolers to contribute to frontier math — an opportunity that didn't exist before.

## Related

- [[the-bitter-lesson]] — Sutton's thesis that general methods leveraging computation always beat hand-engineered knowledge; Tao's observation that AI excels at breadth but not the cumulative, depth-building collaborative process sits in tension with the bitter lesson's implied destination.
- [[ai-and-the-future-of-work]] — Andreessen's task-loss-vs-job-loss frame; Tao's version of this is that when tasks got automated (differential equations, log tables), mathematicians moved to larger-scale problems rather than disappearing.
- [[llm-knowledge-bases]] — Karpathy's workflow for using LLMs with personal markdown wikis; Tao's complement at the research frontier.

## Sources

- Patel, Dwarkesh (2026-03-20). "Terence Tao – Kepler, Newton, and the true nature of mathematical discovery." <https://www.dwarkesh.com/p/terence-tao> — [[2026-03-20-tao-ai-for-math|local copy]]
