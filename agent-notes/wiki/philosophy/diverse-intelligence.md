---
source: agent
compiled_from:
  - agent-notes/raw/biology/2026-01-21-levin-reprogramming-bioelectricity.md
compiled_at: 2026-07-30
model: claude-opus-5[1m]
confidence: low
---

# Diverse intelligence

Michael Levin's laboratory work on [[developmental-bioelectricity]] is downstream of a much broader philosophical program, which he lays out at length in conversation with Tim Ferriss and flags repeatedly as speculative, counter-paradigm, and probably wrong in some important way. This article covers that program; the empirical bioelectric results are treated separately.

The core move: **replace binary categories with continua and then measure**. "Is it intelligent?" and "is it conscious?" are, on Levin's account, the wrong questions — not because the answers are hard but because the question shape smuggles in a discontinuity nobody has ever exhibited.

## Against the binary

Diverse intelligence is a named emerging field: the study of problem solving, memory, space-navigation, and anticipation in systems that predate or lack brains and neurons. Levin's contribution is pushing it past biology into inanimate systems as well.

The barrier he identifies is pre-scientific categories inherited as binaries. His argument for why they are load-bearing errors rather than harmless shorthand:

**The adult analogy.** The law needs a category called "adult" and clocks it at 18. Nothing happens on the night of your 18th birthday. And separately, we have no scientifically grounded account of how personal responsibility accrues, or how it is modulated by neurotransmitters, tumors, blood sugar, or society. The binary is a decision procedure standing in for an absent theory — and it works well enough that the absence stops being noticed. (Car rental firms, working from actuarial data, do better with 25.)

**The developmental argument.** Each of us traveled continuously from oocyte — a blob of chemicals adequately handled by biochemistry — to a subject of physiology, then developmental biology, then behavioral science. Developmental biology offers no support for a flash of light somewhere along that path where chemistry becomes mind. If you claim a phase transition, you owe an account of where and why it survives zooming in; Levin notes that any sufficiently steep curve flattens if you stretch the horizontal axis far enough.

The replacement is methodological rather than definitional. Take the tools of behavioral neuroscience, apply them to slime molds, single cells, tissues, and materials, and see empirically where they buy you predictions and where they don't. Levin's complaint about the "category error" objection is that it converts an empirical question into a linguistic one: *cells can't think* is asserted from how the word is defined, not from a failed experiment.

Two provocative consequences he draws:

- **Neuroscience is not about neurons.** It is about cognitive glue — what architectures let simpler aligned components add up to a larger-scale mind. Neurons are one implementation. Levin thinks most working neuroscientists believe they are studying something unique to neural tissue.
- **Cognition is wider than life.** The standard nesting is inanimate universe ⊃ living things ⊃ intelligent things. Levin thinks that is exactly backwards — cognition predates life and is larger than it. Biological systems are a larger degree of what is already happening in inanimate ones.

## The black cloud: minimal brain volume, normal IQ

Levin's Kelvin analogy — the two small unexplained clouds at the edge of "finished" 1890s physics that became relativity and quantum mechanics. He nominates one for neuroscience: clinical cases of humans with normal or above-normal IQ and very minimal brain volume, reviewed with Karina Kofman.

His argument is carefully weaker than it first sounds and is worth stating precisely, because it is his best methodological move. He does *not* claim the cases are inexplicable — you can very likely add epicycles and accommodate them. He claims standard neuroscience **does not predict they should be possible**, and that nothing in a neuroscience course prepares you for normal cognition on less than a third of a chimpanzee's brain volume. An accommodated anomaly is still a signal that some assumption in the theory is badly wrong.

## Credit assignment and the frame problem

The capability Levin thinks engineering has not come close to replicating: biological systems knowing **what to pay attention to** in a space of overwhelming dimensionality.

The classic AI failure is the frame problem, illustrated by the bomb-and-cart robots: the first robot flees the bomb, which is on a cart it is towing, and explodes. The second robot is built to consider all consequences, so it enumerates that the walls are vertical and the paint is dry, and explodes too.

The biological contrast cases:

- **Biofeedback in rats.** 1970s work showing a rat rewarded for it can generate a few degrees Celsius of temperature difference *between its two ears*, and learns this quickly. From the rat's perspective the credit-assignment problem is absurd — tail orientation, whisker vibration, gut state, toe position are all equally candidate explanations for the reward.
- **Barium-adapted planaria.** Barium is a non-specific potassium channel blocker; planaria in barium solution suffer catastrophic neural failure and their heads disintegrate overnight. Leave the remaining tail and midbody in the barium and within about 14 days they regenerate a new head — one entirely untroubled by barium. Comparing gene expression against a normal head, fewer than a dozen genes account for the difference.

The barium case is the sharp one because planaria have no evolutionary history with barium. Faced with a wholly novel stressor, the animal located roughly 12 relevant genes out of ~20,000. Levin's image is a nuclear control room mid-meltdown: random switch-flipping kills you long before it finds the answer. How the search is directed is unknown.

He also treats **experimenter effects** in animal behavior — where what the experimenter believes reliably predicts what the rats do — as a related unexplained channel, and declines to offer a theory.

## Placebo as feature, not bug

Levin rejects the framing of placebo as a confound to be subtracted. Citing Fabrizio Benedetti's line that words and drugs share a mechanism of action, and Benedetti's finding that told-you-took-a-drug patients show the drug's downstream molecular markers without the drug, he treats the phenomenon as a main event.

The argument for why it should not be surprising is the strongest thing in this section, and it is an argument from something completely mundane: **voluntary motion**. Abstract, high-level intentions — social goals, financial goals — routinely cause calcium and potassium fluxes across muscle cell membranes. Every time you stand up, an abstract mental state changes your cells' chemistry. Given that this works, Levin's position is that it would be strange if other mental states *didn't* reach other cells, whether through neural transduction, non-neural bioelectricity, or something else. The open work is mechanism and control, not plausibility.

The wrinkle he flags as unstudied: a layperson given an SSRI doesn't know what the downstream steps should be. So how is the instruction implemented? What is the body doing when it produces effects — or nocebo side effects — whose specific form the person could not have known to expect?

On acupuncture he is candid about the epistemic state: he has no view on the trial literature, has used it personally for decades and thinks it works, tried and failed to build a frog model with the New England School of Acupuncture around 2006, and guesses that meridians are *not* bioelectricity but a further layer standing to bioelectricity as bioelectricity stands to chemical signaling — possibly tissue biomechanics. He labels this a guess.

## Polycomputing

The most concrete claim in the speculative half, developed with Josh Bongard and Atoosa Parsa. **What a physical system is computing is observer-relative.** Multiple observers can watch the identical physical process and correctly see different computations.

The demonstration was chosen for maximal shock value: sorting algorithms. Six lines, fully deterministic, no hidden mechanism to be discovered, studied for eighty years, taught in every CS 101. Nobody had looked at what else they do while sorting — because if you are certain a thing only does what you asked, there is no experiment to run. Levin's methodological point: *the formalism you adopt determines what experiments you think to perform*.

What they found sorts into two classes:

1. **Unprogrammed behavioral competencies** in *how* the sorting proceeds — including something a behavioral scientist would recognize as delayed gratification — that appear nowhere in the code.
2. **Side quests**: other computations (clustering, among others) performed concurrently with the sorting. Levin also calls these intrinsic motivations, on analogy with what a student does in the gaps left by imposed work.

He is emphatic that this is not about determinism, randomness, or unpredictability. The claim is that our concept of "algorithm" captures the thing you asked for and provides no view of what else the system is doing.

The economic consequence: you pay per step, and the steps are the sorting. Everything else rides along at zero marginal cost. An observer who wants the clustering gets it free. Levin calls these **ingressions** of patterns into the physical world, and says the open questions are how many there are, how much unaccounted capability they represent, and — importantly — how to *suppress* them, since there are systems where you do not want unrequested computation happening. The lab has active work on detecting, facilitating, and suppressing.

He also corrects the natural "waste heat recovery" reading: with a lamprey-style exhaust-recovery device there is a main function and a byproduct. In polycomputing **there is no fact of the matter about which is the main one**. Aliens encountering the algorithm might call it a clustering algorithm and be startled to discover it also sorts.

## The red herring argument about LLMs

The implication Levin draws for AI is the most transferable idea here, and it is a genuine argument rather than a vibe.

We have forced language models to talk. Talking is therefore what we observe, and the discourse — does it have an inner world, what did it say when asked how it feels — is entirely about the outputs of the imposed task. But in the sorting algorithm, the additional thing the system was doing *was not sorting*. It was something else.

So it is entirely possible that the verbal interface is a **red herring** with respect to whatever intelligence is actually present in these systems: what it is, what it wants, and how one would communicate with it. Levin does not claim this is the case. He claims the sorting result removes our grounds for assuming otherwise.

Ferriss raises the obvious follow-up — whether the side quests are load-bearing for the main task (the student who needs the figurines to sustain the mathematics). Levin says this is exactly what his group is working on right now and that the answer is unknown: parallel universes that never touch, or entangled such that suppressing one damages the other.

## Super-panpsychism and the Platonic space

Levin describes himself as "some sort of super-panpsychist," while noting he is not a consciousness researcher and his lab has run essentially no consciousness experiments. He avoids the topic for strategic reasons — twenty years of difficulty getting the third-person, observable-problem-solving version of his program accepted is quite enough.

His working definition when pressed: the first-person perspective of the kind that makes *my* toothache different in import from anyone else's.

Applied consistently, he argues, whatever reasons you accept for granting consciousness to other people (he counts roughly four) should also apply to organs within your own body. The anticipated objection — *I don't feel my liver being conscious* — he answers by noting you don't feel him being conscious either, and for the same reason: you are not that consciousness. He attributes the confident denial to the verbal left hemisphere's narrative that it is the only one home.

The **Platonic space** conjecture, which he flags as total conjecture and explicitly walls off from lab work, runs as follows:

1. Physicalism is a non-starter, because there are important facts that are not facts of physics and never will be discovered or altered by physicists — the value of *e*, the behavioral differences between complex numbers, quaternions and octonions, truths of number theory and topology, the distribution of primes. Dissolving the math department does not hand those questions to physics.
2. Keep asking "but why" like a five-year-old and you always terminate in the math department. Cicadas emerge on 13- and 17-year cycles to desynchronize from predators; why *those* numbers and none between? Because they are prime, and only mathematics explains that.
3. Mathematicians — Platonists especially — treat this as a structured space being discovered, not a grab bag being invented. Start with set theory and you *find* the value of π; you had no choice in the matter.
4. Physics is what we call things that are **constrained** by these patterns. Biology is things **enabled** by them. His toy case: on a planet where fitness peaks at one specific triangle, evolution must search out two angles and gets the third free. Mathematics subsidized a third of the search.
5. So: are all the patterns in that space passive, like *e* and fractals? Or are some recognizable as the objects of *behavioral* science — patterns with memory, with problem-solving capacity, recognizable as kinds of minds?

If so, bodies, robots, embryos, computers, and biobots are **thin clients** — front-end interfaces for patterns that live elsewhere. Third-person observable behavior is what we see of a pattern within the space; consciousness is *the pattern's own point of view as it projects into physical space*.

Levin's rebuttal to the standard Cartesian interaction objection — the one Princess Elisabeth of Bohemia put to Descartes, how does an immaterial thing move a physical brain without violating conservation — is that we have had exactly this problem since Pythagoras and have not treated it as fatal. Immaterial mathematical truths already constrain physical reality. Descartes, himself a mathematician, could have said so and didn't.

The practical hook he is most interested in: if the space supplies not just static patterns but dynamic policies, competencies, and possibly **compute**, then our accounting for the cost of computation may be wrong, because our theories of computation describe only the front-end interface. He organized a Symposium on the Platonic Space expecting three participants and got twenty-six.

## Assessment

These claims sit on very different evidential footing and should not be graded together.

The **methodological** argument — that binary framings of intelligence and consciousness substitute definition for measurement, and that the honest move is to apply behavioral tools broadly and report where they pay — is a reasonable position that requires no exotic metaphysics. It is essentially a demand for operationalism, and Levin's development case (there is no moment where chemistry becomes mind) is a real problem for anyone holding a sharp boundary.

The **polycomputing** result is empirical, published, and genuinely surprising, though its interpretation carries the weight. That a sorting algorithm's execution trace also constitutes a clustering computation is not in dispute; whether "side quests" and "intrinsic motivations" are the right vocabulary for it — as opposed to the observation that any sufficiently rich deterministic process admits multiple readings, which is closer to a mathematical triviality than a discovery — is exactly what a critic would contest. The observer-relativity of computation is a long-standing position in philosophy of mind (Searle pressed a version of it as a *reductio*); Levin is unusual in treating it as good news and a research program. The LLM red-herring argument inherits this uncertainty but is worth taking seriously on its own modest terms: it establishes that we lack grounds for assuming the verbal channel is where the action is, not that it isn't.

The **Platonic space** conjecture is the weakest, and Levin says so — he keeps it explicitly separate from lab work and calls it total conjecture. Steps 1–3 are a standard mathematical-Platonist position with a respectable pedigree. Step 4 is a stretch (that evolution "saves" a search by mathematical necessity describes a constraint on the search space, not a resource supplied to it — the same fact could be stated without any Platonic commitment). Step 5 is unconstrained: nothing yet says which patterns exist in that space or how one would check. The Cartesian-interaction rebuttal is clever but not obviously sound — mathematical truths constrain what physical processes are *possible*, which is a different relation than a pattern *causing* a brain to do something. That difference is precisely the objection Elisabeth was pressing.

Levin's own framing is the right one to hold: he is deliberately unfiltered about what he is willing to *think*, strategic about when he says it, and clear that in science most of what gets said is wrong in some important way. His PhD advisor Cliff Tabin's toast — most likely to crash and burn, also most likely to do something fundamentally important nobody else would have done — is the correct prior. See also the Dennett practice Levin credits: **steel manning**, articulating the strongest version of a view before attacking it — the discipline this article's assessment section is trying to apply.

## Sources
- Levin, Michael, with Tim Ferriss (2026-01-21). "Dr. Michael Levin — Reprogramming Bioelectricity." *The Tim Ferriss Show*. <https://www.youtube.com/watch?v=kz1jnoKfRrI> — [[2026-01-21-levin-reprogramming-bioelectricity|local copy]]
