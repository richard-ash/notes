---
source: agent
compiled_from:
  - agent-notes/raw/philosophy/2026-04-07-nielsen-alien-tech-stack.md
compiled_at: 2026-04-15
model: claude-opus-4-6
confidence: medium
---

# Tech tree divergence

Michael Nielsen argues that the science and technology tree is vastly larger than commonly assumed, that we are near the bottom of it, and that different civilizations exploring it would end up with radically different technological stacks — not because they are less advanced, but because the branching factor is enormous and exploration is path-dependent.

## The core argument

The default assumption is technological convergence: any sufficiently advanced civilization discovers the same physics, the same math, the same engineering. Nielsen rejects this for everything above the most fundamental layers:

- **A "theory of everything" is the beginning, not the end.** Computer science illustrates this perfectly. Church and Turing laid down the equivalent of a theory of everything for computation in the 1930s. Ninety years later, we're still discovering deep, non-obvious ideas latent within it — public-key cryptography, distributed consensus (cryptocurrency), and much more. The foundational axioms were established early; the consequences are inexhaustible.
- **Phases of matter as a case study.** School teaches three or four phases of matter. Physics has been steadily adding to the list — superconductors, superfluids, Bose-Einstein condensates, quantum Hall systems, fractional quantum Hall systems. Nielsen expects many more remain to be discovered and eventually *designed*. This is "down at the bottom of the tech tree."
- **Programming ideas are not exhausted.** The idea that we've found all the deep ideas in programming is "obviously ludicrous." Knuth's anecdote: a mathematician dismissed computer science in the 1960s, saying "come back when there are a thousand deep theorems." Decades later, Knuth noted there clearly are a thousand deep theorems.

## Why different civilizations diverge

Several factors drive path-dependence in exploration:

- **Sensory biases.** Humans are deeply visual creatures. Other animals are aurally based. These perceptual biases shape which problems feel natural, which representations feel intuitive, and which areas of the tree get explored first. An alien civilization with radically different sensory apparatus would develop different mathematical representations and different engineering priorities.
- **Historical contingency.** Quantum computing could have been invented in the 1950s — von Neumann had the requisite knowledge of both computation and quantum mechanics. It wasn't, because personal computers hadn't yet made computation culturally salient, and the Paul ion trap hadn't yet made single-quantum-state manipulation possible. Feynman got excited about quantum computing partly because he was excited about his new PC in 1981.
- **The "dessert buffet" model of diminishing returns is incomplete.** Nielsen uses an analogy: at a wedding buffet, the best desserts go first, suggesting diminishing returns. But if someone behind the table keeps adding new, better desserts, the low-hanging fruit argument breaks down. Computer science was one such addition — it arose from "abstruse questions in the philosophy of mathematics and logic" and opened an entirely new field where 21-year-olds could make breakthroughs. This keeps happening.

## Gains from trade persist indefinitely

Patel draws out a striking implication: if the tech tree is this large and exploration is this divergent, then **gains from trade between civilizations persist into the far future**. There is no point at which one civilization has "all the science" and nothing to learn from another.

Nielsen agrees but adds important caveats about whether comparative advantage actually leads to trade:

- **Transaction costs matter.** We don't trade with chimpanzees despite their having interesting capabilities, partly because the interface cost is too high. AIs communicating at 1000x human speed by exchanging latent states would face similar transaction costs when incorporating a human into the supply chain.
- **Comparative advantage doesn't guarantee above-subsistence terms.** Horses have a mathematical comparative advantage over cars, but we don't have horses on the roads — the cost of maintaining a horse in San Francisco exceeds the value of its comparative advantage.
- **Power imbalances override trade logic.** When one group has sufficiently more power, they often shift from trade to domination.

## The protein library as alien GitHub

Nielsen's original intuition for this idea came from thinking about biology's protein library. Earth's biology has produced hundreds of millions of proteins — an immense library of molecular machines containing deep ideas about material science, information processing, and engineering. We understand almost none of them in depth (tens of thousands of papers about hemoglobin alone and still not done). 

This is structurally analogous to receiving a GitHub repository from an alien civilization: an enormous body of working solutions encoding principles we haven't independently discovered, which will take centuries to fully mine. The ribosome, kinesin, insulin — each contains engineering ideas that arose from four billion years of exploration down one particular branch of the tree, seeded by one particular chemistry (nucleic acids, carbon-based life).

## Implications for technological determinism

Nielsen explicitly rejects strong technological determinism. Most of the tech tree will never be explored by anyone. Choices about exploration direction — including deliberate bans (DDT, CFCs, nuclear weapons treaties) — are consequential precisely because the tree is so vast. We are already shaping which branches we explore through institutional decisions.

This also bears on the "are ideas getting harder to find?" debate (Bloom et al.). Nielsen notes that the studies measure progress within narrow metrics, missing the creation of entirely new fields. The diminishing-returns finding within semiconductors doesn't account for the emergence of GPUs, which opened a qualitatively different direction. The relevant dynamic is not exhaustion within a field but the periodic opening of new fields — and we have no good theory of why that happens.

## Related

- [[scientific-verification-loops]] — the difficulty of distinguishing which branch of the tree is correct
- [[surprising-detail]] — Salvatier's observation that reality contains far more detail than we expect, a micro-scale version of the tech-tree argument

## Sources

- Patel, D. & Nielsen, M. (2026). "Michael Nielsen – Why aliens will have a different tech stack than us." <https://www.youtube.com/watch?v=myP8UjAM1pk> — [[2026-04-07-nielsen-alien-tech-stack|local copy]]
