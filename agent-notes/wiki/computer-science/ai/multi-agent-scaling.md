---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-10-18-naam-can-a-million-ai-agents-create-superintelligence.md
compiled_at: 2026-10-22
model: claude-fable-5-1
confidence: medium
---

# Multi-agent scaling

**Multi-agent scaling** is the question of what running more copies of a model in parallel actually buys. There are two different answers to keep apart: **speed** (the same result sooner, at some cost in total compute) and **collective intelligence** (a harder problem solved, a benchmark level reached that no smaller team could reach). The distinction matters because the "population" leg of the intelligence-explosion argument rests on the second. Dario Amodei's "country of geniuses in a datacenter," Davidson and Eth's "millions of top-notch human researchers," Benjamin Todd's "millions of competent engineers," and Dwarkesh Patel's "massive population size and perfect knowledge transfer" all assume that a bigger team of AI researchers does research a smaller one cannot, and the software-RSI models in [[recursive-self-improvement]] encode that assumption as a labor exponent.

This article's anchor is Ramez Naam's October 2026 guest post on Noah Smith's *Noahpinion*, "Can a Million AI Agents Create Superintelligence?", the sequel to the essay that anchors [[recursive-self-improvement]]. Naam's headline: **more agents buy speed, at rising cost and with a tapering tradeoff; they buy very little intelligence, with gains that are logarithmic at best and sub-logarithmic or saturating on the hardest tasks; and the hypothetical RSI models assume returns to added researchers that sit orders of magnitude above anything measured.** He is explicit that the data are thin and the curves could change, and he ends with a measurement program and a dated, falsifiable prediction. Smith's framing in the introduction is the same as last time: an intellectually interesting argument whose practical weight is unclear while the underlying models keep improving at a steady rate, swarm or no swarm.

## Three limits on a bigger team

Naam names three reasons a larger team can fail to produce better answers, and notes that they interact:

- **Coordination.** Can the agents divide the problem, manage the work, check each other, and combine results without spending all their time communicating? A team needs project management as well as contributors.
- **Homogeneity of thought.** A hundred copies share the same blind spots. More varied answers help only if some of the variety is right.
- **Structure of the problem.** How much can happen in parallel, and how much has to wait for an earlier result? A million independent searches run at once; a sequential investigation does not. Even finding the right way to divide a conceptual problem may require an insight the team lacks.

A better model can relax all three at once: supply the idea its copies were missing, find a better division of labour, or recognise a solution the team overlooked. That is why Naam insists the *shape* of the scaling curve is the thing to track, per model generation, rather than any single point on it.

## The ladder of diminishing returns

Naam's ladder, from easiest to hardest scaling: **super-linear** (twice the input, more than twice the output), **linear** (independent jobs), **power-law** with exponent below 1 (at 0.5, doubling output takes 4× the input; at 0.2, 32×; at 0.1, 1,024×), **logarithmic** (each multiplication of input buys the same increment), and **sub-logarithmic** (successive tenfold increases buy smaller increments, possibly saturating at a ceiling). Pre-training scaling laws are power laws in loss; most test-time compute curves look roughly logarithmic over the measured range; and the multi-agent intelligence curves below flatten harder than either. His key point about the ladder is that every curve can be made to look the same over its first doubling, so the first expansion tells you nothing about the later ones. For runaway RSI the returns to more researchers have to outrun the rising difficulty of each further improvement, and logarithmic returns cannot do that if every further doubling of software efficiency needs a fixed percentage more research. Sub-logarithmic is weaker still.

## Speed: real, costly, and tapering

Speed is the best case and Naam grants it fully. A million independent jobs, candidates or search locations, each with a reliable success check, can scale almost perfectly, and a huge search can find a rare solution a small one misses entirely. He also grants Lisan al-Gaib's point that this makes swarms a potent offensive-cyber tool even when inefficient, with the caveat that hardened targets (operating systems, browsers) need long attack chains where each step waits on the last, so even speed can saturate there.

The measured numbers come from **Toby Ord's swarm-scaling analysis** of GPT-5.6 Sol, which uses **λ** for how speed scales with agent count: at λ = 0.5 speed and total cost rise by the same factor, and higher λ means speed outruns cost.

| Benchmark | 4 agents reach the same result | at a cost of |
|---|---|---|
| Terminal-Bench (command line) | ~1.9× faster | ~2.1× the tokens |
| BrowseComp (web research) | ~2.6× faster | ~1.6× the tokens |

Web research splits into independent searches; a command-line task often has to change a shared environment in sequence. Naam applied the same method to Anthropic's ProgramBench (program reconstruction) results in the Opus 5.5 system card and found the Claude family improving on this tradeoff: with five agents, **Opus 5.5 reaches about 2.7× its solo speed versus 2.2× for Opus 5, at lower added agent-time** (runtime is the cost proxy; tokens and dollars could differ). Fable 5.1 sits between.

But the tradeoff worsens with team size. On the Lean formal-proof task in the same system card, Naam estimated the speed and cost of reaching a score of 0.50 from the published checkpoints: **from 10 to 30 agents λ is about 0.75 (speed outruns cost); from 30 to 100 it falls to about 0.33 (cost outruns speed).** The extra agents still save time, but each expansion buys less for more. His guess is that this is general: problems that split ten ways split a hundred ways less well, more of the work ends up waiting on earlier results, and coordination itself costs work. Better coordination can push the knee outward; the task still imposes it.

## Intelligence: four examples, all sub-logarithmic

**SEC-Bench Pro (OpenAI, GPT-5.6 Sol).** Proof-of-concept generation for software vulnerabilities, with agents coordinating through OpenAI's "ultra" setup, so this is a test of collaboration and not a stack of independent guesses. Peak scores: **71.2 with one agent, 74.3 with four, 76.4 with sixteen.** The first fourfold expansion buys 3.1 points, the next 2.1, with plenty of room below a perfect score. Naam's caveat: these are best-reported results across budgets, not an equal-compute comparison.

**Navier–Stokes (OpenAI).** The 10,000-agent, 88-hour run that solved a Millennium Problem made the swarm idea vivid. Asked by Dwarkesh Patel, who said he was "shocked by the scale of cognitive effort," Noam Brown (o1 co-developer, now on multi-agent systems at OpenAI) said: "I wouldn't even attribute 10% of the credit to multi-agent." He credits the smarter model. OpenAI never ran the single-agent control, so Brown's number is a judgment, but it is the judgment of the person best placed to make it.

**Lean formal proofs, 1 → 10 → 100 Opus 5.5 agents.** The Opus 5.5 system card tests teams on 49 weighted theorem statements checked in Lean, 24 hours per team, agents able to communicate, share a machine and Git repository, and organise themselves (the hundred-agent team spontaneously built a hierarchy with twelve sub-leads). **The first tenfold expansion adds 27 score points; the second adds two,** despite the larger team having roughly ten times the aggregate runtime over the same day. Naam calls this steeply sub-logarithmic and possibly saturation. He offers two candidate causes and does not pick: the remaining work is hard to parallelise because later steps depend on understanding earlier ones, or the remaining problems need insights the model cannot find however many copies run. "A thousand copies don't automatically supply the insight one copy is missing."

**A smarter model beats ten times the agents.** On the same Lean task, **ten Opus 5.5 agents outscore a hundred Opus 5 agents and a hundred Fable 5.1 agents.** The newer model starts higher, gains substantially to ten, then barely moves to a hundred, and its ten-agent score is already above the older models' hundred-agent scores. The analogue on the test-time-compute axis is OpenAI's own unsolved-math chart: the internal model's lowest plotted point beats Astra's highest, and a rough extrapolation of Astra's line says it would need about **300× the compute** to match that lowest point, if it did not plateau first.

## Diversity helps, then flattens

If homogeneity is the limit, different minds should help. A 2026 study of model-and-persona diversity found substantial gains as diverse teams grew to about **eight agents, after which the task average barely moved**. X-MAS and Aitchison and colleagues' forecasting study also find gains from combining different models, but over small ranges; no result shows sustained improvement across many expansions. The underlying problem is that frontier models share overlapping public data, related algorithms, and similar reasoning and coding exercises: the Artificial Hivemind study (NeurIPS 2025) found striking similarity in open-ended responses, and a creativity study against 467 people found that added AI responses eventually contributed less diversity than added human responses. Naam's four proposals for minds that think more differently, all phrased as experiments: vary training data, curricula, RL environments and reward objectives; combine complementary specialists (conjecturer, lemma-finder, counterexample-searcher, proof-checker); have agents propose independently before discussion; and pick teams for complementary error profiles rather than individual rank.

## The best cases are logarithmic

The strongest multi-agent intelligence results Naam can find are **logarithmic**: the same increment per multiplication. Ryan Greenblatt's ARC-AGI experiment, which sampled and checked many candidate programs, kept gaining roughly the same amount per doubling of samples (parallel search, not a communicating team). A molecular-exploration study scaling from one to 128 agents found the same shape, with multiple learning agents beating one agent given the same evaluation budget. Communicating teams have encouraging early results too, notably Argus on web research and the Microsoft–Berkeley ARC-AGI-3 work, which finds unusually strong gains from one to five agents; Naam flags both as worth attention and untested at larger sizes. His verdict: logarithmic beats sub-logarithmic, but if research output grows logarithmically in agents while each improvement gets harder to find, even billions of agents do not make a self-sustaining loop plausible.

## Against the RSI models' labor assumptions

The three software-RSI models Naam checks the data against:

| Model | Assumed return to added research labor |
|---|---|
| Chan et al. (2026; co-authors include Hinton and Bengio) | doubling effective labor → ~**2.6×** the rate of software improvement, software level held fixed |
| Eth & Davidson (2025, Forethought) | **linear**: twice the researchers, twice the papers; acceleration comes from researcher count growing faster than per-improvement difficulty |
| Davidson & Houlden (2025, Forethought) | power law with central exponent **0.6** (10× labor → ~4× research pace); **0.3** when experimental compute is fixed and binding |

Naam normalises every curve to the same gain from one to ten agents and then extends them. At a hundred agents the measured benchmark shapes already sit in a different zone from the model assumptions; at a billion, the hypothetical power-law and super-linear curves are orders of magnitude above the logarithmic and sub-logarithmic benchmark curves even when the math-proof curve is allowed to keep rising slowly. His conclusion is that removing humans from the loop removes the human bottleneck without removing shared blind spots or sequential dependencies, and that adding copies of today's models has not shown the sustained intelligence gains repeated conceptual breakthroughs would need. He finds the Chan et al. figure "implausible as a general assumption about adding copies of today's AI models."

## Will agents get better at scaling?

Naam expects the labs to work hard on coordination and expects speed scaling to keep improving, as ProgramBench already shows across Claude generations. On intelligence he sees **no clear direction**: the Lean score gains across Opus 5, Fable 5.1 and Opus 5.5 are noisy, and newer models do not consistently get a larger boost from larger teams. His encouraging analogy is single-agent thinking-time scaling. Ord's comparison of AI and human scaling found that humans get more relative benefit from additional time than models get from additional reasoning tokens, but newer models are closing on the human reference on cyber tasks, so a scaling parameter that was poor has improved; it could happen for team size too. The Fork-and-Flush study (periodically branch with fresh context, keep the accumulated work, continue from the best branch; better results on thirteen research and engineering tasks at equal compute) is the kind of mechanism that helps agents out of cognitive ruts. Diversity he regards as tractable with effort; problem structure as the hardest limit, since some discoveries must happen before the next useful step exists.

## How to measure it

Naam proposes three parameters, tracked per task type and per model generation, and especially for internal AI research:

- **G, intelligence scaling:** verified task performance added per multiplication of agents (local gains, slopes or exponents; a task-specific proxy, not an intelligence unit).
- **λ, speed-cost scaling:** how much faster the team reaches the same result and at what extra compute or agent-time, over successive team-size ranges.
- **N, where gains weaken or saturate:** the team size at which score or speed curves bend, and whether the bend moves outward with newer models.

The operational rule is to measure **1→10, 10→100 and 100→1,000 separately**, because a newer model can scale better over the first interval and worse over the next, and G and N answer different questions (how much a defined expansion buys; how many agents you can add before it stops buying anything).

## The Anthropic natural experiment

Anthropic's October 2026 employment report gives Naam a test with a date on it. Research agents logged about **one agent-hour per human work-hour in April, three by late May, nine by mid-July and nineteen by late August** (company-wide, about six), ratios that already count round-the-clock agent operation against a forty-hour human week. Under the generous assumptions that an agent-hour is worth a human research-hour, headcount is unchanged, and added runtime is parallel labor, total research labor grew about **5× by July and 10× by August** against the April baseline.

What each scaling rule then predicts for research pace by August, relative to April:

| Rule | Software research pace |
|---|---|
| Chan et al. labor exponent | ~25× |
| Davidson & Houlden (0.6 / 0.3) | ~4× / ~2× |
| Logarithmic | ~2× |
| Naam's sub-log benchmark shapes | ~1.1–1.8× |

Translating to the Epoch Capabilities Index: if software research supplies half of baseline capability improvement and the compute contribution is unchanged, 4× the software pace is about **2.5× the ECI slope**. With a six-month research-to-release lag, the August labor increase should show in releases around **January–February 2027**, and the late-May doubling around **November 2026**. Log scaling and the 0.3 power law nearly tie at this scale because a tenfold labor increase is small; they diverge by a hundred agents and massively by a billion.

**Naam's prediction:** no sustained acceleration in Anthropic's ECI slope through the first half of 2027, and if any, at the low end of the sub-log bar. He lists what would make him wrong (parallel search over training parameters, AI-coded RL environments, recombination of existing ideas, or a next-increment model that bends the scaling laws or adds a new scaling axis as reasoning models did) and commits to updating in proportion to the data.

## Synthesis

**The structure limit is Amdahl's law in agent counts.** Naam does not name it, but his third limit is the serial fraction: the speedup from N workers is bounded by the share of the task that must run in sequence, and the Lean λ collapse from 0.75 to 0.33 is what that bound looks like as a team grows. The intelligence question is the harder cousin: not how long the serial part takes, but whether the serial part contains a step no copy of the current model can take at all. His two candidate causes for the 10→100 plateau map onto exactly those two readings, and distinguishing them is the single most informative experiment nobody has run.

**The variable that moves capability is model generation, not population.** Ten Opus 5.5 agents beating a hundred of either predecessor, and Astra needing 300× compute to touch the internal model's floor, are the same fact seen twice. Read against [[scaling-hypothesis]], this is a refinement rather than a rebuttal: scale does buy capability, but the scale that buys it is training scale, and inference-time population is a weak substitute. Brown's refusal to credit the swarm for Navier–Stokes is the lab-insider version of the same point. The practical rule that follows is to spend on a better model or more thinking time before spending on more copies, unless the task decomposes cleanly and has a verifier.

**This essay disputes the second coefficient of the same loop.** The September essay in [[recursive-self-improvement]] took the pro-RSI models on their own terms and measured research productivity per capability point at 5–10× below the self-sustaining threshold. This one measures the other input, returns to added researchers, and finds the labor exponent similarly over-assumed. The two together cover both multiplicands in the software loop. The remaining escape routes are the ones Naam himself lists: a better model that changes the curve's shape, or other loops (hardware, economic) compounding where the software loop alone cannot, which is the Davidson–Halperin–Houlden–Korinek argument he found most compelling last time.

**Homogeneity is the diversity-collapse bottleneck, and ensembles already show the knee.** The eight-agent diversity plateau is the same finding as Weng's diversity collapse in [[self-improving-harnesses]] and as the think-alike result already in [[recursive-self-improvement]]. The practitioner-scale version is the cross-model ensemble in [[ai-code-review]]: the gains there come from *different* models, and the research says they plateau after a handful. That argues for a few heterogeneous reviewers or proposers over many copies of one, and for independent proposals before discussion, which is Naam's third diversity fix and already how ensemble review works.

**The encouraging axis is depth, not breadth.** The one scaling parameter Naam shows improving across generations on the hard tasks is single-agent thinking-time (Ord's human-versus-AI comparison), and Fork-and-Flush improves it further at fixed compute. [[reasoning-models]] are the depth axis made explicit. If the breadth axis saturates at ten to a hundred agents while the depth axis keeps improving, the labs' own harness work will drift toward longer, better-managed single runs with periodic forking, which is roughly what the Lean team's self-organised hierarchy and Fork-and-Flush both are.

**A falsifiable bear case, with a date.** Of the skeptical positions in this wiki, this is the only one with a public prediction tied to a published dataset and a calendar: Anthropic's own agent-runtime ratios, the ECI, and January–February 2027. Karpathy's [[agi-timelines]] argument is historical, Moll and Imas's [[ai-explosive-growth]] is economic, and deBoer's [[ai-skepticism]] is epistemic; Naam's can simply be checked. The report card is also the right one for the worry [[pacing-the-frontier]] records as Amodei's real concern, RSI escaping control: if the slope does not move by mid-2027, the population route to that outcome is slower than the models assume, whatever the better-model route does.

**Where the argument is weakest.** Each intelligence curve rests on two or three points reconstructed from system-card charts, and Naam says so. SEC-Bench's points are peak-over-budget rather than equal-compute. The Lean teams ran under a fixed 24-hour wall clock, so the hundred-agent team may have been coordination-bound rather than insight-bound, which is the cause Naam could not isolate. Benchmark scores are ceiling-bounded, so a curve can look sub-logarithmic near the top of a benchmark even when the underlying capability is still rising; SEC-Bench at 76 of 100 has room, but the Lean task's headroom is unstated. Brown's 10% is a judgment without a control. And the Anthropic test assumes equal value per agent-hour, parallel rather than sequential use of the added runtime, and a six-month lag; a null result in February 2027 could reflect a longer lag or sequential use rather than weak scaling. None of these reverses the direction of the finding, but together they mean the right confidence is "the measured curves are far below the models' assumptions," not "the curves are known."

## Sources

- Naam, Ramez (2026-10-18). "Can a Million AI Agents Create Superintelligence?" Guest post on Noah Smith's *Noahpinion*; also published on Naam's own Substack, where the essay's section anchors point. <https://www.noahpinion.blog/p/can-a-million-ai-agents-create-superintelligence> — [[2026-10-18-naam-can-a-million-ai-agents-create-superintelligence|local copy]]

Primary sources the essay builds on: Ord, *Swarm scaling* <https://www.tobyord.com/writing/swarm-scaling> and *AI scaling vs human scaling* <https://www.tobyord.com/writing/ai-scaling-vs-human-scaling>; Anthropic, *Claude Opus 5.5 System Card* (ProgramBench and Lean team results) <https://www.anthropic.com/claude-opus-5-5-system-card>; Anthropic, *Employment at Anthropic* (October 2026) <https://www.anthropic.com/research/employment-at-anthropic>; OpenAI, *GPT-5.6* (SEC-Bench Pro) <https://openai.com/index/gpt-5-6/> and *Navier–Stokes solution* <https://openai.com/index/navier-stokes-solution/>; Patel, interview with Noam Brown <https://www.dwarkesh.com/p/noam-brown>; Chan et al. (2026) <https://arxiv.org/abs/2609.36054>; Eth & Davidson, *Will AI R&D automation cause a software intelligence explosion?* <https://www.forethought.org/research/will-ai-r-and-d-automation-cause-a-software-intelligence-explosion>; Davidson & Houlden, *How quick and big would a software intelligence explosion be?* <https://www.forethought.org/research/how-quick-and-big-would-a-software-intelligence-explosion-be>; model-and-persona diversity study <https://arxiv.org/abs/2602.03794>; Greenblatt, *Getting 50% SOTA on ARC-AGI with GPT-4o* <https://www.redwoodresearch.org/blog/getting-50-sota-on-arc-agi-with-gpt>; molecular exploration with multiple agents <https://arxiv.org/abs/2501.19153>; *Fork-and-Flush* <https://arxiv.org/abs/2610.07447>; *Artificial Hivemind* (NeurIPS 2025) <https://papers.neurips.cc/paper_files/paper/2025/hash/754d5a526a5ee5a47220664a0eb92751-Abstract-Datasets_and_Benchmarks_Track.html>; creativity study with 467 participants <https://arxiv.org/abs/2412.03151>; Epoch AI, *Epoch Capabilities Index* <https://epoch.ai/eci>.
