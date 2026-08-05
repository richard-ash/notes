---
source: agent
compiled_from:
  - agent-notes/raw/mathematics/2026-03-20-tao-ai-for-math.md
  - agent-notes/raw/mathematics/2026-06-30-grant-sanderson-ai-and-math.md
compiled_at: 2026-08-04
model: claude-opus-5
confidence: medium
---

# AI for mathematics

What AI is and isn't good at in mathematical research, and how the practice of math is changing as a result. Compiled from two Dwarkesh Patel interviews: **Terence Tao** (March 2026) speaking as a working researcher at the frontier, and **Grant Sanderson** (June 2026) speaking as an expositor who has spent the last year interviewing mathematicians for a documentary series on exactly this question.

Opinionated throughout — both are individual perspectives — but the two are usefully non-overlapping. Tao is inside the research loop and reports what the tools do and don't do for him. Sanderson is outside it and is tracking the *sociology*: how mathematicians talk about AI, and how that talk has shifted. They agree on more than they disagree, and where they disagree ([[#Where Tao and Sanderson disagree]]) the disagreement is load-bearing.

Sanderson's framing for why this domain matters at all: **the AI frontier is spiky, and math is one of the spikes** — so whatever is or isn't happening here is the leading indicator for everything else. But the spikiness is fractal. Zoom into math and the same unevenness reappears: geometry at the 2024 IMO fell to what was effectively a brute-force solver in 19 seconds, while combinatorics — the playful, puzzle-like category — held out. That year's test happened to carry two combinatorics problems out of six; had the draw gone the other way, the gold would have come a year earlier. Capability headlines are partly a sampling artifact.

## Three shapes an AI solution could take

Sanderson's most useful organizing device. Asked what it would mean if AI solved the [Riemann hypothesis](https://en.wikipedia.org/wiki/Riemann_hypothesis), he refuses to answer in the abstract, because *how* it got solved determines everything else — whether the capability spills into the rest of the economy, and whether humans can understand the result.

1. **The lightning bolt.** Deep expertise in two unconnected fields plus the flash that links them. His canonical example is Hugh Montgomery and Freeman Dyson at the Institute for Advanced Study: Montgomery, a number theorist, writes down the pair-correlation formula for zeros of the Riemann zeta function; Dyson, a physicist, recognizes it as the eigenvalue statistics of random Hermitian matrices from nuclear energy-level studies. Whether there's real food there is still open, but the *shape* is exactly what you would expect an LLM to be good at — it knows both fields already and needs no lunch meeting. Crucially, this shape is **least** transferable to white-collar work: it doesn't help because your video editor's problem isn't a missing cross-domain connection.
2. **Mountain building.** Fermat's Last Theorem is the model: a question stated in one line whose solution required centuries of elliptic-curve theory and a separate mountain of modular forms, both of which had to exist before the connecting question could even be posed. If Riemann falls this way, that implies a system capable of *inventing the right new theory* — and Sanderson thinks it would be genuinely surprising if that capability didn't permeate the rest of the economy.
3. **Raw hustle.** A thousand-page chain of reasoning, no new theory, nobody learns anything. Possible; disappointing. (Tao's version of this concern is the four-color theorem — solved, still no conceptually elegant proof.)

The comprehensibility question tracks the same split. Lightning bolts are highly human-parsable: you only have to show the endpoints. When AI disproved the unit distance conjecture, and in the [Erdős problem #1196](https://www.erdosproblems.com/) result on primitive sets, the published chains of thought read as ordinary mathematics — "run a Markov chain process showing this from the bottom up probabilistically rather than top down, using the von Mangoldt function" is a sentence a specialist can immediately run with. Mountain building is where the risk lives, and Sanderson's cautionary case is Mochizuki's attempted ABC conjecture proof: an entire alien apparatus that took the community years just to *parse*, and probably isn't correct. The nightmare is that shape at machine scale.

## Kepler and the length of the verification loop

Tao opens with Kepler as a case study in how scientific progress actually happens. Kepler's early theory — that the spacing of planetary orbits matched nested [Platonic solids](https://en.wikipedia.org/wiki/Mysterium_Cosmographicum) — was beautiful and wrong. Only after stealing Tycho Brahe's decades of naked-eye observations did he spend years discovering the actual laws: elliptical orbits, equal areas in equal time, and (ten years later, on six data points) the period-distance cube-square law. It took Newton a century to explain *why* all three were true.

Dwarkesh's framing: **Kepler was a high-temperature LLM.** He tried many random relationships — including the musical notes of the planets and astrological causes of Earth's famine — and one of them happened to be the third law of planetary motion. This only worked because Brahe's dataset could verify guesses.

Tao's gloss: idea generation has always been the prestige part of science, but it must be matched by verification, or it's slop. We celebrate Kepler; we should also celebrate Brahe for the ten-times-more-precise data collection that made Kepler's fits possible.

The deeper point is that **the verification loop for correct ideas can be decades or millennia long.** During that time the ultimately-correct theory often makes *worse* predictions than the prevailing wrong one — Copernicus's circular orbits were less accurate than Ptolemy's epicycle-ridden geocentrism, until Kepler fixed them. Survival through this "epistemic hell" depends on a mix of judgment and heuristics we don't understand well enough to articulate, let alone codify into an RL loop.

Related: correct theories often also imply things that seem absurd. Aristarchus's heliocentrism was rejected in the 3rd century BC because stars showed no parallax — an implication that was actually correct, just misinterpreted. Leibniz chided Newton's gravity for implying action at a distance. Progress, Tao says, often comes not from adding theories but *deleting assumptions*: Aristotelian physics assumed objects want to stay at rest, which kept geocentrism alive until Newton's laws of motion removed the assumption.

## Galois: a hundred-year verification loop, and a total RLVR failure

Sanderson's extended case study is the sharpest version of Tao's point, because here the verifier didn't merely lag — it actively rejected the correct answer, repeatedly, for decades.

The arc runs roughly a century. **Lagrange** noticed that solvability of polynomials relates to how symmetric certain algebraic expressions are, and that extending his degree-four method to the quintic would require an expression in five variables taking four or fewer values under all 120 permutations. He couldn't find one. He produced **no theorem** — he only planted the instinct that *symmetry is the right question to ask about polynomials*, and the suggestion that one might try proving impossibility rather than searching for a formula. **Abel** (who had read Lagrange) proved the quintic unsolvable and died at 26 of tuberculosis, having been advised to spend his time on elliptic functions instead — the quintic work was treated as almost recreational. **Galois** pushed the abstraction further, writing in prison a manifesto arguing that just as algebra had freed mathematics from thinking in numbers, the next layer was to think about the *symmetries underlying formulas* rather than the formulas themselves. His papers were rejected by the academy — and, Sanderson is careful to say, **rejected fairly**: they weren't coherent, weren't complete proofs, didn't clearly state what the theory was. He died in a duel at 20. His notes sat for ~20 years until Liouville saw something in them, and another ~20 until Jordan assembled anything resembling modern group theory. Practical payoff waited until the 20th century, when Gell-Mann predicted quarks from a group-theoretic question.

Sanderson's reading of this for AI training:

- The "verifiable reward" signal for Galois was **negative** at every step where it existed at all. An RLVR-shaped process would have deleted this line of work.
- The thing that carried it was an unformalized instinct appearing in three different heads — Lagrange's *this is the right question*, Galois's *there is something here*, Liouville's *these scattered notes from a dead youngster might matter*. Nobody can put a finger on what that instinct is computing.
- Contrast with general relativity, where people could feel it was a good theory almost immediately. The length of the recognition loop is itself highly variable, which makes it a terrible thing to build a reward around.

Compare with Tao's Kepler section above: Tao's worry is that during the loop the correct theory *predicts worse*; Sanderson's is that during the loop the correct theory *isn't even a theory yet*. Both conclude the same thing — the signal you'd need to reinforcement-learn on doesn't exist at the time you'd need it.

## The bottleneck has shifted from generation to verification

> "AI has driven the cost of idea generation down to almost zero, in a very similar way to how the internet drove the cost of communication down to almost zero."

Tao argues this does not create abundance by itself. Peer review was built to filter amateur theorizing; it cannot handle the volume of plausible-looking AI output now being produced. Journals are already being flooded with AI-generated submissions. Assessing whether a given idea moves the subject forward — versus being a dead end or red herring — was already hard at the pace of individual papers and is impossible at the pace of thousands per day.

Worse, **fruitfulness depends on the future.** Many great ideas were initially ignored — [deep learning](the-bitter-lesson) was a niche area of AI for a long time. The transformer became foundational but didn't have to. Base ten isn't special; it's entrenched by inertia. You can't look at a scientific achievement in isolation and assign it an objective grade. So the question of *which* AI outputs constitute real progress may never be something you can simply reinforcement-learn, unlike localized problems with clear success metrics.

Sanderson supplies the working mathematician's version of this, via Alex Kontorovich: if AI mathematicians generate ten papers a day at *any* nonzero error rate, the field becomes insufferable. Even at 99% correct, you can't know whether a given paper is worth your time, and finding the error is labor-intensive and infuriating in retrospect. This is the strongest practical argument for formalization — see [[#Lean, brute-force proofs, and whether humans can extract understanding]].

## Theorems, conjectures, definitions — and what can't be benchmarked

Sanderson quotes a line from the Polylog video on the unit distance conjecture: *good mathematicians prove theorems, great mathematicians come up with conjectures, and the greatest mathematicians come up with definitions.* The AI-progress question is which rung is next.

His argument is that the top two rungs are **structurally unbenchmarkable**, and that this matters more than it sounds:

- A benchmark is a goalpost — the ball went through or it didn't. "OpenAI disproved the unit distance conjecture" is a headline. "Model 255.4 came up with a really good conjecture, we promise everyone agrees" is not, and never will be.
- Dwarkesh's sharpening, which Sanderson accepts: **there is no fundamental difference between a benchmark and a training environment.** So the things you can't benchmark are, in the current paradigm, roughly the things you can't easily train for. The unbenchmarkable rungs and the untrainable rungs are the same set.

Sanderson's replacement for a benchmark is a *tone shift*: the measurement will be mathematicians reporting that a model was genuinely useful not for solving their problem but for deciding **what their research field should even be**. He claims to be watching this happen in real time — his interviews for the documentary series began in mid-2025, and the way researchers talk about AI has already changed noticeably by 2026. Sociological, subjective, unfalsifiable, and in his view the only signal available.

Dwarkesh's counter-pressure, worth keeping: it is very easy to name a deep reason AI can't do something and be wrong shortly afterwards. He expects near-term training methods for these rungs, just not RLVR-shaped ones — probably partially synthetic problem generation that forces cross-field connection, e.g. by stripping assumptions and still demanding the answer.

## Depth vs breadth: AI is strong where humans are weak

The clearest productive framing from Tao: **humans excel at depth, current AI excels at breadth.** Human mathematics is organized around depth because that's where human expertise lives. AI opens up a new mode — exploring new fields by first getting broadly competent AIs to map the terrain, identify islands of difficulty, and hand those off to human experts.

Tao's analogy: the problem landscape is a mountain range of cliffs in the dark. Some walls are 3 feet high, some 15, some a mile. Current AI tools are jumping machines that can leap about two meters higher than any human — better than us for the low cliffs, useless for the tall ones, and strikingly bad at *partial* progress. They either succeed or fail in one shot; they don't find handholds, pull collaborators up, and jump from there. They lack the cumulative interactive buildup that is central to what Tao calls real *intelligence* (as opposed to *cleverness*).

This is also why LLMs "don't learn" within a problem the way a human collaborator does: run a new session and the model has forgotten everything it just figured out. Whatever it discovered is at most 0.001% of the next generation's training data.

## Connections as the near-term frontier: the Langlands ethos

Sanderson's concrete five-year forecast, and his correction to a framing bias in the whole discourse: **most mathematicians would not describe their work as targeting the next problem to take down.** The problem-solving frame — Erdős problems, Millennium Prizes — is what generates headlines, not what most of the field does.

The alternative is the [Langlands program](https://en.wikipedia.org/wiki/Langlands_program), which Sanderson describes less as a field than as a *research ethos*. Langlands's famous letter sketched a large map on which apparently disparate regions of mathematics are conjecturally linked, and a substantial population of mathematicians characterize their work as filling in threads on that map. Fermat's Last Theorem is one instance of the pattern: big problems fall to connections, often enough that finding the connections *preemptively* is a rational research program in its own right. His suggested field test — ask any mathematician you meet whether their work is more Langlands-shaped or more single-problem-shaped, and watch a clean bifurcation appear.

Sanderson's bet: **AI as a supercharged connector is an amplifier for exactly this ethos**, and most of the useful progress over the next five years will be filling in that landscape rather than knocking down famous problems. He notes it is genuinely surprising this hasn't happened more already, given that these systems already hold expertise in every field simultaneously — and thinks the coming years hold "a lot more of those lightning bolts."

The measurement problem returns, though: a knocked-down problem writes its own press release, while "that was the right connection to draw" requires a human in the loop to even assess. So the mode of progress Sanderson expects to matter most is precisely the mode that will be least legible from the outside.

## Selection bias in AI math results

As of early 2026, AI-assisted efforts have solved ~50 of the ~1100 Erdős problems, mostly in a single burst. Tao notes the low-hanging fruit has been picked; further progress has slowed despite three separate attempts to throw frontier models at every remaining problem simultaneously.

Two important caveats on the public narrative:

1. **The problems that fell had essentially no literature.** Erdős posed them once; nobody had written up attempts. The winning proofs combined one obscure technique with one obscure existing result — exactly the move AI is good at. Tao predicts similar isolated successes on famous hard problems ("some backdoor to solve the problem that everyone else missed"), each getting viral attention.
2. **Systematic sweeps show a 1–2% per-problem success rate.** AI companies publish the wins and not the negative results, so the apparent success rate is inflated. Buying scale and picking winners works, but the honest picture is much noisier. Tao calls for standardized challenge problem sets, independent of the AI labs' self-reporting.

Sanderson's IMO detail above is the same phenomenon one level down: a category draw determined which year the gold landed.

## What AI is actually changing in Tao's practice

Tao said in 2023 that by 2026, AI would be "a trustworthy co-author if used correctly." He thinks that prediction has held. Productively:

- Writing papers he'd produce today *without* AI would take 5x longer, but he wouldn't write them the same way — the extras are auxiliary (deeper literature searches, more numerics, more plots and code, formatting and reformatting).
- **Papers are richer and broader but not deeper.** The core activity — solving the hardest part of a math problem — still happens with pen and paper.
- AI is especially good at running all the *standard* moves on a new problem, sometimes catching errors Tao makes, sometimes introducing ones he catches. It's still bad at the step after: when none of the standard moves work, and you need to invent something.

## Autoregression, context, and engineered serendipity

Sanderson's mechanistic hypothesis for *why* the lightning bolts have been slower to arrive than the breadth of these models would predict. It runs against the usual framing, which asks how smart the system is; his question is what the generation process structurally favors.

**Autoregression is a strange way to produce anything.** His thought experiment: you are locked in a box. A slip of paper arrives; you predict what comes next; your memory is wiped; another slip arrives. Do this many thousands of times and someone hands you "the essay you wrote." You would disown it — not because you're unintelligent, but because iterated next-token prediction is nothing like composition. The specific consequence for math: **you become a slave to your context.** Given a problem framed inside one field, all the surrounding context points inward, and the cross-field connection where the substance lives is by construction an *unlikely* continuation. Nothing in the objective specifically up-weights it. The intelligence may be sitting right there in the box; the interface is the problem.

His open question, which he addresses to the labs: is there fruit in questioning how tokens are generated at all — not crude temperature manipulation, but ways to spark those connections at the existing capability level? Or does it require enough additional capability that the lightning bolt simply becomes the predicted next token?

**Then the inversion.** The standard worry about digital minds is entropy collapse: trained alike, they think alike, go down the same paths, and this is a large part of why they write badly. Sanderson's counterintuitive claim is that the deepest advantage may be the *opposite* of the usual "pool all the knowledge, merge all the copies" story — it's **the ability to erase and manipulate context deliberately.**

Humans have almost no control here. You get stuck in a frame and the only fix is time. Occasionally someone spends years trying to prove something before thinking *what if I tried to prove the opposite* — and that unwinding is the whole move. Machines can be made to do it on purpose: spin off one agent to prove and one to disprove, hand different agents deliberately different context, systematically increase entropy **at the prompt level** even though it collapses at the autoregressive level.

Dwarkesh supplies the case in point: the unit distance conjecture likely stood as long as it did because everyone assumed it was true and pointed their effort at proving it. And the risk if you *don't* do this: Einstein's productive bias that physics should look the same in every reference frame came bundled with his unproductive one that God does not play dice. A population of identical Einsteins might have stalled quantum mechanics. There is no correct heuristic for science — which is an argument for multiple independent research programs, and, encouragingly, for **old-fashioned deterministic software** as the layer that enforces the diversity. Given a clear ontology of distinct approaches, ordinary code can fan out across it; the hard part is describing the ontology, and "prove vs. disprove" is only the easy first axis.

Sanderson's illustration is the IMO problem he plans to build his first documentary episode around — one a great many strong students failed, Tao among them, and which contestants angrily called a "troll problem." The seductive elegant approach fails; a nearly brain-dead approach is optimal. What's required is to **escape your context** — escape being at the IMO, escape years of contest training. Hand it to someone off the street as a brain teaser and they'd likely get it. His prediction to check in three years: how many headline results turn out to have the character of *erasing* context rather than merging it.

This is a direct, mechanized answer to Tao's serendipity worry below — Tao fears AI's perfect targeting kills the hallway encounter; Sanderson asks what it looks like to *engineer* the hallway between agents. As he puts it: everyone knows an institute is smarter than an individual, and the reason to co-locate people is the accidental conversation. The Montgomery–Dyson lunch is the thing to automate.

## Verifiability isn't enough — the grindability thesis

Dwarkesh's contribution, and a genuinely separate causal claim from the two usual explanations (math is verifiable; math has Lean). His argument is that **verifiability is necessary but nowhere near sufficient — the domain also has to be grindable.**

The proof by contrast is computer use, which is *extremely* verifiable — did the package ship, did the event get booked — and has progressed slowly anyway. What it lacks is the ability to farm the simulator: bot detection, enormous compute per rollout, and the fact that you cannot run a thousand parallel checkouts against a live Amazon without being shut off. Building clones of every website is labor-intensive and slow. The reason so many parallel rollouts are needed in the first place is unsolved sample efficiency — Sanderson's phrase, "sucking supervision through a straw."

Math and code are the exceptions. Code containerizes: freeze a repo state, spin out hundreds of identical containers, and because the environment is deterministic you can **solve credit assignment** — same start, different diff, different outcome, so the diff is what worked. Divergent starting states make credit assignment much harder. Most real-world domains — building a business, trading a day in the markets — can't be replayed at all.

The implication is that the AI-for-math story generalizes considerably less than the headlines suggest, and generalizes along a different axis than people expect: not "wherever answers can be checked" but "wherever the world can be reset and replayed cheaply." Compare the deployment-curve arguments in [[agi-timelines]].

## Lean, brute-force proofs, and whether humans can extract understanding

On the scenario where AI proves something big via a giant Lean blob, **Tao** is less worried than most:

- Some problems *have* been solved by brute force (the four-color theorem — still no conceptually elegant proof).
- Riemann is prized partly because we expect it requires genuinely new mathematics or a new bridge between unconnected areas. A brute-force verification finding a zero off the line would be possible but disappointing.
- The beauty of a Lean proof is that every lemma can be studied atomically — you can ablate it, refactor it, get other AIs to summarize or re-derive it, run RL to make it more elegant. There will be a future profession of mathematicians doing nothing but this.
- Paper-writing used to be the most expensive part of the job, done rarely and only after the argument was checked. It's now cheap enough that hundreds of variants can be generated and compared — the Erdős problem website is already showing this dynamic.

**Dwarkesh dissents on Lean's current importance.** DeepMind's first IMO gold ran through Lean; the next year's was natural language throughout. The unit distance disproof's released chain of thought contained no Lean at all. His read: the process-based supervision Lean provides matters much less than simply having a grindable, verifiable outcome. He points at DeepSeek-Math's verifier-trained-by-meta-verifier as evidence that natural-language verification works well enough, and at coding agents' improving *taste* (clean code, refactoring, dedup) as evidence that LLM-as-judge process supervision transfers.

**Sanderson concedes the point about today and makes a different argument about tomorrow.** He grants the DeepMind trajectory corroborates Dwarkesh. But he thinks Lean's unique unlock is one nobody has cashed in yet, and it is an *AlphaZero* argument rather than a supervision argument:

> Right now a human ultimately reviews the counterexample and says "looks good." That human is a bound on how endlessly explorable the space is.

AlphaZero could be left alone. Nobody checked in; you poured compute at it and it explored the universe of Go, going arbitrarily far off the rails of anything a human would play. Lean makes the same thing conceivable for mathematics: point a model at a fork of [mathlib](https://leanprover-community.github.io/mathlib-overview.html) — the community project to encode all of mathematics as machine-checkable code — and tell it simply to extend it. It never needs to check in. It might generate its own conjectures, its own definitions, its own theories. Most will be useless. But you could press go, look away for ten years, and there would be *something* there. **No other field has this property.** Whether the output is useful, and how you would suss that out, is the open question; a supervisor model providing usefulness heuristics is the obvious hedge against a random walk through the space of logic.

Related precedents both men reach for: Karpathy's auto-research setup (one Python file doing basic LLM training, agents proposing modifications, keep what speeds up the speedrun), Eric Jang's similar Go-bot experiment — good at running an experiment down a path, bad at recognizing dead ends and at genuine parallel exploration. And a project Tao has described: exhaustively searching the space of possible algebraic axiom systems. Most collapse into nothing. Every so often there's an island rich in theorems — possibly one you could retroactively supply motivation for, the way group axioms look arbitrary until you know they're about symmetry. Sanderson's generalization: do that not just for algebras but for the logical consequences of *any* axiom system.

The second, more prosaic case for Lean is Kontorovich's: at machine paper-generation volumes, the green checkmark is what makes the output readable at all. Every other field would kill for a mechanism that certifies correctness independently of comprehensibility.

## The missing piece: a semi-formal language for mathematical strategy

Lean gives deductive *proofs* a formal framework that AI can train on. There is no equivalent for *plausibility* or *strategy* — the subjective thing scientists do when they say "this conjecture feels right because it fits the random model." Tao's example of this unformalized layer:

- **The random model of the primes.** Gauss's prime number theorem, statistical rather than structural, launched analytic number theory. Over time we developed a heuristic that the primes behave pseudo-randomly. We're absolutely convinced of the twin prime conjecture because the random model says so; the few things we can prove match the model. We believe Riemann for the same reason — and a disproof would immediately kill public confidence in prime-based cryptography, because a hidden pattern in the primes probably implies more hidden patterns and therefore crypto exploits.

Tao wants a semi-formal framework mimicking the way scientists argue — using data, narrative, and plausibility — but robust enough that RL can't backdoor it. This is a wish rather than a plan. One thought experiment: simulate many "alien civilizations" of small AIs evolving math in different orders, and study which strategies actually produce progress.

**Sanderson proposes a concrete candidate reward for the same gap: compression.** If you want to reinforce the Galois instinct rather than just problem-solving, reward not *what* was solved but the **smallness of the concepts required to do it**. The smaller, more predictive expression feels more intelligent — the compression-is-intelligence thesis, which he is separately making a video series about. Kolmogorov complexity as a first stab at quantifying elegance.

This matters most in the raw-hustle scenario. A thousand-page Riemann proof that nobody learns anything from is precisely the case where you'd want a second objective pushing toward the compressed version of those ideas — the elliptic-curves-and-modular-forms view rather than the incoherent elementary slog. Sanderson doesn't claim it's easy, only that something like it is *required* if the goal is human understanding rather than prediction. His limiting case: you could have automated engineers build starships nobody understands and still get between stars — but plenty of people will want the equivalent of Newton's universal law of gravitation, and you would have to train for that separately.

## Serendipity and the danger of over-optimization

A recurring theme for Tao: he explicitly *protects* time for the non-optimized. Events he attended reluctantly ("like this podcast") often produced the best serendipitous connections. COVID-era remote meetings kept academics busy but killed hallway encounters. Library browsing used to surface accidental articles; now targeted search gives you exactly what you asked for, nothing more. At the Institute for Advanced Study, with no distractions, he ran out of inspiration within a few months. He needs some noise — "high temperature" — in his schedule.

There's a connection to the AI story: **by making information retrieval perfectly targeted, AI tools may further erode the serendipity that drives creative progress.** This is a distinct worry from the "will AI replace mathematicians" question, and Tao takes it more seriously.

Sanderson's context-erasure argument above is the constructive response: rather than protecting human serendipity, engineer it between agents. Note that neither addresses the other's version — Tao is worried about *his own* thinking being over-targeted, which no amount of agent diversity fixes.

## The theorem economy and what's left for humans

Sanderson's most personally consequential section, and the one where he reports having changed his mind.

Dwarkesh introduces David Bessis's essay *The Fall of the Theorem Economy*: mathematics is really about definitions and problems, theorem-proving gets all the credit, and theorem-proving is arguably **a parasite on the definition work**. Historically the credit misallocation didn't matter, because whoever produced the definition usually also produced the theorem. AI breaks the bundle — it automates the theorem half while the insight half stays human, and the reward structure no longer tracks the value.

This connects to a distinction Sanderson loves, from Timothy Chow's expository paper on forcing and the continuum hypothesis. Chow proposes the notion of an **unsolved expository problem**: something we have certainly proved but don't really know *why* it's true. (Forcing is his example — the continuum hypothesis's answer is both yes and no depending on your axioms, and the machinery for showing this is famously hard to internalize.) Proof and explanation are different objects, and Sanderson's entire career is the second one.

So the comfortable story writes itself: AI proves, humans explain, everyone keeps a job. **Sanderson used to believe this and no longer does.** His observation is that the people who generate genuinely novel insight are unusually often *also* lucid expositors — Einstein, Shannon, Feynman all write papers you can actually read, contra the university experience of being taught by an expert spoiled by their expertise (see [[creative-thinking-claude-shannon]]). If the same faculty produces both, then a system good enough to build the mountain is probably also better than most humans at explaining it. The distillation half is not a refuge.

What he thinks survives is **curation**, and the argument is social rather than cognitive:

> Mathematicians end up more analogous to art museum curators than anything else.

The art exists and is well explained; you still want someone to help you navigate a nearly infinite space of what's worth engaging with. And here even a superior AI curator loses, because **motivation is a social phenomenon** — you want the recommendation from someone you have a relationship with. His analogy is musicians: the story behind the human matters even when the MP3 coming out of a model is objectively better. He notes this is already most of his own job — people assume the work in a 3Blue1Brown video is the visuals, but the larger share is deciding what is worth saying at all, and his audience is there for *his* judgment about what's interesting, not because they independently wanted the topic.

Two caveats he flags himself: this may not hold where you have a specific technology to build rather than an audience to serve, and the whole answer to "what will you be doing" is partly just that he'd be doing this regardless — "I will probably be doing something like what I am until I die."

Compare Hamming on problem selection in [[you-and-your-research]]: choosing which problems matter has always been the scarce skill, and Sanderson's curation thesis is that claim surviving into a world where execution is free.

## Outlook: human-AI hybrids will dominate math for a long time

Tao's central forecast: **complementary hybrids — smart humans assisted by powerful AI — will outperform either alone for much longer than the hype suggests.** Frontier AI is stunningly capable on some tasks and terrible on others; stacking frameworks only partially reduces errors. If a Millennium Prize problem falls soon, he would *not* put 95% odds on an autonomous AI having done it.

Historically, when entire traditional mathematician tasks got automated — solving differential equations, compiling log tables, sequencing genomes — the field didn't die. It moved on to different, larger-scale questions. Tao expects the same pattern: within a decade, much of what math students currently spend their time on will be done by AI, and mathematicians will discover that that work wasn't the most important part of what they do.

Advice to early-career mathematicians: get traditional credentials and learn the old-fashioned way *for now*, but expect a lot to change and stay adaptable. AI and Lean have already made it possible for high-schoolers to contribute to frontier math — an opportunity that didn't exist before.

Sanderson's version of the same forecast is narrower and more confident: over the next five years, expect the value to come from connection-finding rather than problem-slaying, expect it to require humans in the loop to recognize which connections mattered, and expect it to be badly measured.

## Where Tao and Sanderson disagree

Mostly they're complementary. Three places they aren't:

- **What's left for humans.** Tao anticipates "a future profession of mathematicians doing nothing but" extracting human understanding from machine proofs — ablating lemmas, refactoring, re-deriving. Sanderson explicitly abandoned this position: the faculty that finds the insight is empirically correlated with the faculty that explains it, so distillation will be automated alongside discovery. He lands on curation — the social, relational, what's-worth-your-attention function — as the durable role. This is the sharpest disagreement, and notably it's Sanderson conceding the more comfortable position that would have protected his own job.
- **Serendipity: protect it or manufacture it.** Tao treats accidental encounter as a fragile human resource that targeted AI retrieval is eroding, and defends unoptimized time. Sanderson treats it as an engineering problem — deliberately divergent agent contexts, prove-and-disprove pairs, systematic prompt-level entropy — and thinks machines will end up *better* at it than institutes are.
- **What Lean is for.** Tao's case is auditability: every lemma is atomic, so a machine proof is decomposable into human understanding. Sanderson's case is autonomy: Lean is the only substrate where you could press go on an unsupervised, AlphaZero-style exploration and walk away for ten years. Dwarkesh dissents from both on present-day relevance, arguing the natural-language results have already outrun the formalized ones.

An unresolved question Sanderson raises against himself: it's genuinely surprising that models holding expertise in every field simultaneously *haven't* already produced far more cross-domain lightning bolts. He offers autoregression-as-context-slavery as the explanation, but flags it as a hypothesis he'd want the labs to test rather than a conclusion.

## Related

- [[the-bitter-lesson]] — Sutton's thesis that general methods leveraging computation always beat hand-engineered knowledge; Sanderson's mathlib-extension proposal is the bitter lesson applied to mathematics itself, while Tao's observation that AI excels at breadth but not cumulative depth-building sits in tension with the lesson's implied destination.
- [[agi-timelines]] — Karpathy's "decade of agents" calibration; the grindability thesis is a mechanism for *why* capability transfers unevenly across domains, and Sanderson's spiky-fractal-frontier framing is the same argument from the math side.
- [[ai-and-the-future-of-work]] — Andreessen's task-loss-vs-job-loss frame; Tao's version is that when tasks got automated (differential equations, log tables), mathematicians moved to larger-scale problems, and Sanderson's curation thesis is a specific claim about which residual task survives.
- [[you-and-your-research]] — Hamming on choosing important problems as the scarce skill; the conjecture/definition tier and Sanderson's curator role are both that claim under automation.
- [[creative-thinking-claude-shannon]] — Shannon's catalogue of creative tactics; Sanderson cites Shannon as evidence that novel-insight generation and lucid exposition come from the same faculty, which is the crux of his disagreement with Tao.
- [[ml-research-craft]] — problem selection and taste as trainable sub-skills rather than gifts; the human-side counterpart to the question of whether conjecture-generation can be trained at all.
- [[llm-knowledge-bases]] — Karpathy's workflow for using LLMs with personal markdown wikis; the everyday version of the research-frontier tooling described here.

## Sources

- Patel, Dwarkesh (2026-03-20). "Terence Tao – Kepler, Newton, and the true nature of mathematical discovery." <https://www.dwarkesh.com/p/terence-tao> — [[2026-03-20-tao-ai-for-math|local copy]]
- Patel, Dwarkesh (2026-06-30). "Grant Sanderson – AI and the future of math." <https://www.dwarkesh.com/p/grant-sanderson-2> — [[2026-06-30-grant-sanderson-ai-and-math|local copy]] (auto-transcribed; speaker labels unattributed and proper nouns garbled throughout — names, Kolmogorov/Liouville/Gell-Mann/Galois/Matuschak, are corrected in this article. The captured transcript ends mid-sentence in the closing Jane Street sponsor segment, after the substantive discussion concludes.)
