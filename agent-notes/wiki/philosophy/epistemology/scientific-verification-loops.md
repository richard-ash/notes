---
source: agent
compiled_from:
  - agent-notes/raw/philosophy/2026-04-07-nielsen-alien-tech-stack.md
compiled_at: 2026-04-15
model: claude-opus-4-6
confidence: medium
---

# Scientific verification loops

Scientific progress routinely outpaces experimental verification. The community adopts theories before the decisive experiments exist — and sometimes the verification loop is actively hostile to the correct theory for decades. This has deep implications for whether AI can automate scientific discovery by tightening feedback loops.

## The gap between adoption and verification

Nielsen and Patel trace several cases where the scientific community converged on the correct theory long before experimental confirmation:

- **Special relativity vs. Lorentz ether theory.** Lorentz derived the correct math (Lorentz transformations) but interpreted them as effects of moving through the ether. His theory was experimentally indistinguishable from Einstein's special relativity. The community adopted Einstein's interpretation — that space and time themselves are different — well before the muon decay experiments of 1940 provided strong physical evidence that "local time" was real time.
- **Heliocentrism.** Aristarchus proposed it in the 2nd century BC. The ancient objection was the absence of stellar parallax, which was not measured until 1838. The community did not need to wait for that measurement. Copernicus's model was initially neither simpler (it required *more* epicycles than Ptolemy's) nor more accurate, yet it won out — partially because Newton later showed it unified celestial and terrestrial mechanics under one framework.
- **Prout's hypothesis.** In 1815, Prout proposed all atomic weights are whole-number multiples of hydrogen. Chlorine's measured weight of 35.46 seemed to falsify this. For 85 years, the verification loop was actively hostile — the anomaly was caused by isotopes, which could not be chemically distinguished. The correct theory looked worse under every available measurement.

## Falsification is harder than it looks

Nielsen emphasizes that the naive model of falsification — experiment disproves theory, scientists adopt replacement — misrepresents how science works:

- Experiments don't falsify "the theory." They falsify one version among many. Michelson-Morley didn't disprove "the ether" — it disproved one class of ether theories. Michelson himself believed in the ether until his death (~1929).
- The same anomaly strategy succeeds sometimes and fails other times. Uranus's orbit was wrong → Le Verrier predicted Neptune → found it (1846). Mercury's orbit was wrong → people predicted planet Vulcan → it didn't exist. The actual explanation required general relativity. A priori, you cannot tell which case you're in.
- The Pioneer anomaly (1990s) looked like it might challenge general relativity. It turned out to be asymmetric thermal radiation. Nielsen estimates 99.9% of apparent exceptions have mundane explanations. There is no ex ante heuristic for distinguishing the revolutionary from the prosaic.

## What does distinguish theories, if not experiments?

Nielsen suggests several heuristics the community uses, though he stresses none are reliable processes:

- **Unification across disconnected domains.** Newton's gravitational theory explained planetary orbits, terrestrial parabolas, and tides — three seemingly unrelated phenomena from one set of ideas.
- **Aesthetic parsimony.** Einstein "subtracted" from Poincaré's understanding — dropping the dynamical interpretation of length contraction in favor of the purely kinematic view that space and time are simply different.
- **Resistance to expert lock-in.** Poincaré had almost all the pieces of special relativity but couldn't let go of the dynamical picture. Nielsen speculates he was "a prisoner of his own expertise." Einstein, younger and less invested, could make the leap. This pattern recurs: expertise enables and then constrains.

Nielsen cautions against calling any of these a "process" — the word implies something standardized and repeatable, which scientific theory selection is not.

## Implications for AI and automated science

Patel frames the conversation around closing the RL verification loop for AI-driven scientific discovery. Nielsen is skeptical this addresses the actual bottleneck:

- **AlphaFold is primarily a data-acquisition story.** The Protein Data Bank represents decades and billions of dollars of experimental work. The AI model was a small (impressive) fraction of the total investment. AlphaFold fits models to data — it doesn't generate the kind of explanatory theories that predict surprising new phenomena (the way GR predicted Mercury's perihelion precession).
- **Gradient descent can't easily do paradigm shifts.** Patel argues that training a model on planetary observations in 1500 would produce ever-better Ptolemaic epicycles, not heliocentrism. The shift from Ptolemy to Copernicus requires swapping the reference frame — locally less accurate, globally more progressive. Raw gradient descent optimizes locally.
- **The bottleneck is not verification speed.** An infinite number of theories are compatible with any given experiment. The community's ability to pick the right one relies on heuristics — aesthetic taste, unification, managing competing research programs — that are hard to formalize.
- **Coding bottlenecks are shifting.** Programmers are no longer bottlenecked on producing code; they're bottlenecked on having interesting design ideas. AI can close the code-production loop but there is no verification loop for "is this design idea interesting?"

Nielsen proposes that AI-accelerated science would require maintaining many independent research programs with different initial biases, not one model optimizing a single loss function. The diversity of approaches — some of which will be wrong for decades — is what eventually produces paradigm shifts.

## Three views of AI models as scientific objects

Nielsen offers a taxonomy for how to think about large trained models (like AlphaFold) as explanations:

1. **Conservative:** They're useful predictors but not scientific explanations. They lack the parsimony and few-parameter elegance of classical theories.
2. **Intermediate:** They contain many small explanations that can be extracted via [[surprising-detail|interpretability work]]. AlphaZero's chess strategies, reportedly adopted by Magnus Carlsen, are an example of humans extracting meaning from model internals.
3. **Radical:** They are a genuinely new type of explanatory object. We don't yet have the right "verbs" — the operations — for working with them, just as 100-page equations were useless in 1920 but became workable objects with tools like Mathematica.

## Sources

- Patel, D. & Nielsen, M. (2026). "Michael Nielsen – Why aliens will have a different tech stack than us." <https://www.youtube.com/watch?v=myP8UjAM1pk> — [[2026-04-07-nielsen-alien-tech-stack|local copy]]
