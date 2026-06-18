---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-06-18-how-to-be-good-at-research.md
compiled_at: 2026-06-18
model: claude-opus-4-8[1m]
confidence: medium
---

# ML Research Craft

Vivek (@itsreallyvivek) argues that ML research competence is not a gift but a **stack of trainable sub-skills**, and that most newcomers optimize the wrong target: they reverse-engineer the job from its visible outputs (papers, threads, announcements) and learn to *look* like a researcher instead of *being* one. The essay's organizing claim is that each underlying skill — problem selection, input curation, writing, loop speed, output analysis, breadth, collaboration — can be deliberately practiced.

## Pick your own problems

The central distinction: an **absorbed** problem (from an advisor, a big-lab announcement, this week's quote-tweets) gives you the conclusion without the reasoning. You know a lab cares about a direction but not *why*, not what would make them abandon it — so when they pivot you find out a year late, and meanwhile you're racing thousands of better-resourced people on something already fashionable.

The fix is what Vivek attributes to **John Schulman's ML-research guide**: two modes of work — (1) read the literature and hunt for improvements, vs. (2) pick an outcome you genuinely want to exist and reason backwards to the experiments. The second mode *manufactures originality*, because a goal you actually care about pulls you into territory no survey paper covers.

**Taste is a muscle, not a gift.** The training protocol: predict every experiment's result before running it; cover a paper's results section and guess the numbers from the method alone; record which current releases will matter in two years and check your hit rate. Forecast + correction, repeated hundreds of times, is how any predictor gets trained — including the one in your head. This is the same predict-then-verify discipline that [[agentic-engineering]] frames as the human's irreducible contribution (taste as the bottleneck).

## Upgrade your inputs

Shared reading lists produce shared (hence worthless) ideas. Two correctives:

- **Old material is underpriced.** The field reruns its own past on a delay — MoE (1991), LSTMs (1997), backprop going mainstream (1986). [[the-bitter-lesson]] (Sutton, 2019, ~1000 words) predicts the field's shape better than surveys ten times longer. Shannon's 1952 creative-thinking talk offers the load-bearing move: shrink a problem until it's nearly trivial, solve the small version, then reintroduce difficulty one piece at a time.
- **Range beats depth-only.** Interpretability borrows from neuroscience; eval design is mechanism design in a lab coat; knowing how GPUs actually move memory tells you which architecture papers are doomed before the benchmarks do. Honest statistics is "the rarest skill in ML, where a lot of published rigor is vibes with error bars."

Operational rule: read the paper, not the thread. The appendix is where the bodies are buried; the limitations section is the most honest paragraph.

## Write everything down

The argument chains three sources:
- **Paul Graham** — an idea feels fully formed until you try to write it; the page exposes the untested assumption, the step that doesn't follow, the two claims that contradict.
- **Feynman** — the first person you must not fool is yourself, because you're the easiest mark; writing is the cheapest defense.
- **Darwin** — made it procedural: any fact cutting against his theory got written down *on the spot*, because memory deletes inconvenient evidence faster than convenient evidence. Your memory does the same to failed runs.

The recommended artifact is a **research log**: hypothesis, setup, expectation, result, updated belief. Rereading last month's entries is more humbling than any reviewer. Then publish some of it — Vivek cites Olah & Carter's *research debt* essay: clear explanation is a genuine contribution, not a service job, and public writing is an unfakeable credential. (This is the same "compile raw sources into a queryable written corpus" instinct behind [[llm-knowledge-bases]], applied to one's own experiments rather than reading.)

## Tighten the loop

"Research speed is mostly the speed at which you discover you're wrong." The Alec Radford stories are about *volume* — more runs/day, more wrong ideas discarded/week — not single strokes of genius. Consequences:

- **Tooling is a first-class research activity.** Launch a run in one command, plot in one more, reproduce any experiment from its config, compare two runs in seconds.
- **Karpathy's recipe**: overfit a single batch before scaling — 30 seconds, half your bugs gone. Shrink until cheap, get it right, then spend the compute (the Shannon move again, applied to engineering).
- **Engineering is no longer the junior partner.** At the frontier the two jobs have fused; the researcher who can build the harness, eval, and data pipeline is the one whose hypotheses actually get tested. This is the research-side mirror of [[ai-coding-harnesses]] / [[agent-harness]]: the harness is what converts a hypothesis into a tested result.

## Stare at the outputs

A descending loss curve is reassurance, not analysis. Experiments emit far more signal than people consume — transcripts, failure cases, the distribution's strange tail — most of which dies unread in a logs folder.

- **Karpathy**: spend hours on raw data by hand *before* writing training code; most ML bugs live in the data and fail silently (no crash, just a mediocre model and a wrong theory of why).
- **Andrew Ng's** decade-old move: pull 100 failures, read all of them, sort into piles, attack the biggest pile. Works for models and for evals — a benchmark whose transcripts you've never read is one you don't understand. One transcript of genuinely strange behavior teaches more than the next decimal of accuracy.

## Wander on purpose, then concentrate

Your first subfield is an accident of timing; treat it like one. Pay "tuition" across interpretability, evals, RL, systems to locate the corner where your specific weirdness is an unfair advantage. Tactical discipline within work: run the disposable version of every idea first and let most die young; **tune baselines until it hurts** (the ML graveyard is full of gains that evaporate against a properly tuned baseline, and a reviewer is the worst person to learn that from); **ablate** until you know which single component carries the result — "usually one, and usually not the one in the title." Breadth is also insurance: subfields saturate right after they peak on Twitter, and the people who keep producing across transitions already know the neighboring territory.

## Find your people / the long game

Hamming's observation: closed-door colleagues got more done in a given year; open-door colleagues did the work that *mattered*, because interruptions carried information about what the world needed. "Your open door is probably an inbox — keep it that way." Generosity compounds: replicate and publish, release your tools, explain hard things plainly, float half-formed ideas publicly (being wrong on the timeline is cheaper than being wrong in print). The collaborator who kills your bad idea before you sink three months into it is "worth more than compute."

The closing frame is Pasteur ("luck favors the prepared mind") via Hamming: knowledge and productivity **compound like interest**. The daily edges — what you read, what you record, how fast your loop runs, who you argue with — look trivial in isolation and, given years, produce careers that look like luck from outside. Start compounding earlier than feels necessary.

## Sources
- @itsreallyvivek (2026-06-10). "how to be good at research." <https://x.com/itsreallyvivek/status/2064686372737454155> — [[2026-06-18-how-to-be-good-at-research|local copy]]
