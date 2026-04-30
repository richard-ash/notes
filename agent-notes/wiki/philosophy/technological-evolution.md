---
source: agent
compiled_from:
  - agent-notes/raw/philosophy/2026-04-02-information-and-technological-evolution.md
compiled_at: 2026-04-29
model: claude-opus-4-7
confidence: high
---

# Technological evolution as hierarchical search

Brian Potter argues, building on Brian Arthur's work, that creating a new technology is fundamentally a search problem in a combinatorially enormous space — and that the search only becomes tractable when you can decompose the goal into stable, hierarchically composed sub-technologies. Reframed in information-theoretic terms: *finding a new technology is the problem of acquiring information about its design as efficiently as possible per attempt*.

## The Arthur–Polak circuit simulation

In a 2006 paper, Brian Arthur and Wolfgang Polak ran a simulation that randomly evolved boolean logic circuits from three primitive elements: a NAND gate (which is functionally complete — any logic circuit can be built from NAND gates) and two CONST elements outputting 0 and 1.

The mechanic:

- Each iteration, randomly pick 2–12 elements from the current pool and wire them together.
- If the resulting circuit fulfills any goal in a goal list (AND, OR, XOR, 4-bit equal, full adder, 8-bit adder, …), encapsulate that circuit as a new element in the pool.
- Partial fulfillment is also rewarded; cheaper (fewer-component) circuits replace more expensive ones.
- Over hundreds of thousands of iterations, the pool grows from {NAND, 0, 1} to include adders, comparators, and other complex functions.

The headline finding: complex circuits like an 8-bit adder (which requires 68 properly wired NAND gates) only emerge when simpler stepping-stone goals are present in the goal list. Remove the full-adder goal and the 2-bit adder is never found. This mirrors Lenski et al.'s biological-evolution result that complex traits require simpler intermediate functions to be selected for first.

Potter recreated the simulation with AI tools and replicated the core results, but found that Arthur's elaborate "partial fulfillment" mechanic was not load-bearing: turning it off didn't measurably hurt performance. The actual driver of success is the stepping-stone hierarchy of goals, not the partial-credit machinery.

## Why the search is hard: combinatorial explosion

Potter's key sharpening of Arthur's argument is to force a real reckoning with the combinatorics, which Arthur waves at but doesn't dwell on.

For a function with *n* inputs and *m* outputs there are (2^m)^(2^n) distinct truth tables. An 8-bit adder has 16 inputs and 9 outputs, giving on the order of 10^177,554 possible logic functions. For comparison, the universe contains roughly 10^80 atoms and roughly 10^21 milliseconds have elapsed since the Big Bang. Random combination will never find an 8-bit adder; if every atom in the universe were a computer trying a trillion guesses per second, you'd still be guessing for ~10^140 years.

Even restricting attention to wirings of exactly 68 NAND gates yields ~2^852 arrangements — also unreachable by undirected random search.

## Simon's Hora and Tempus

The structural reason hierarchy helps was articulated by Herbert Simon in his 1962 paper "The Architecture of Complexity." Two watchmakers, Hora and Tempus, each assemble 1000-part watches one part at a time. Each has a 1% chance of being interrupted on any step.

- Tempus's watches have no stable subassemblies — interruption shatters everything. Probability of finishing: 0.99^1000 ≈ 0.0043%.
- Hora's watches use ten-part subassemblies that nest ten levels deep. Interruption only sends him back to the last completed subassembly. He finishes ~4,000× faster.

Potter's reframing: invert the model. Instead of a 1% chance of *interruption*, give the assembler a 1% chance of *correctly guessing the next part*. Tempus has probability 0.01^1000 of building a working technology — essentially zero. Hora only has to flip 10 successful coins in a row to lock in a stable subassembly, then move on. The same logic explains why Arthur's stepping-stone hierarchy works: stable partial successes preserve information across failures.

## The information-theoretic reformulation

Potter's deeper synthesis applies Shannon's information theory to technological search. Key facts:

- One bit of information halves the space of possibilities. Specifying a unique design from 2^852 possibilities requires only 852 bits — comparable to the bits needed to specify one short sentence of English.
- The information yielded by an outcome of probability *p* is −log₂(*p*). The entropy (expected information per attempt) is maximized when outcomes are equally likely. A coin with a 99% chance of heads carries only 0.08 bits of entropy per flip — most of the time you learn nothing you didn't already know.
- For a sequential gate-by-gate 68-NAND search, each attempt has a ~1/(few thousand) chance of success, yielding ~0.003 bits per attempt. ~453,000 attempts accumulate the needed bits.
- Trying to guess two gates at once collapses success probability to ~1/(several million) and entropy to <0.000001 bits per attempt — the search becomes intractable. Three gates at once: ~9.3 trillion expected iterations.

The unifying claim: **building technology hierarchically works because each verifiable subassembly massively raises the information yield per attempt**. Knowing "the whole 8-bit adder doesn't work" eliminates one leaf from a tree of 2^852 leaves. Knowing "this particular sub-gate is wired correctly" eliminates an entire branch — and 99.9% of downstream possibilities along with it.

## Implications and corollaries

Several otherwise-puzzling results in Arthur's paper drop out of the information-theoretic framing:

- **Why the maximum-components-per-iteration parameter doesn't matter much.** Combining 12 random components yields so much higher cardinality (and thus so much lower probability of any given combination being useful) that those attempts contribute almost nothing. Capping at 4 works just as well as capping at 12.
- **Why narrow goal lists help find complex goals faster.** A smaller goal list keeps the component pool smaller, which keeps the per-attempt branching factor lower, which raises information yield per attempt.
- **Why "stepping stones" work.** Hierarchical decomposition is hill-climbing: each verified subassembly is a new, higher base camp from which the next short search can begin, rather than a return to sea level.
- **Why real-world invention proceeds combinatorially from existing technology.** Arthur's example: the 1912 amplifier was built from the existing triode tube; the amplifier enabled the oscillator; oscillator + amplifier + heterodyne mixer enabled continuous-wave radio; that enabled broadcast radio. Each layer is a "subassembly" in Hora's sense and a "stable verified component" in the information-theoretic sense.

## The general principle

Potter's strongest takeaway, more general than Arthur's "use simpler technologies as stepping stones" framing: **successful technological search is the problem of acquiring information as quickly as possible per attempt**. Modular, hierarchical design helps not because hierarchy is intrinsically virtuous but because it lets you verify subparts independently, and verifying small subparts is enormously more informative per attempt than verifying complete designs.

This has direct corollaries for engineering practice and R&D strategy: short feedback loops, decomposable architectures, fast-failing components, and well-defined sub-goals are not just good hygiene — they are how you make the search problem tractable. The same logic underwrites why test-driven development, integration testing pyramids, modular software design, and the unbundling of monolithic engineering problems all work.

It also bears on questions about tech-tree exploration ([[tech-tree-divergence]]): whether a civilization or research community will reach a particular technology depends not just on the size of its search space but on whether it has discovered or specified the right sub-goals to provide a hill-climbing path. Civilizations or fields with poorly factored goal structures can be permanently stuck below a frontier that is, in raw combinatorial terms, only modestly distant.

## Related

- [[tech-tree-divergence]] — Nielsen's argument that the technology tree is vast and path-dependent; this article supplies a mechanism for *why* path-dependence is so strong (the search is intractable without the right intermediate goals)
- [[creative-thinking-claude-shannon]] — Shannon's six tactical heuristics for creative problem-solving, by the same Shannon who founded the information theory invoked here
- [[surprising-detail]] — Salvatier's argument that reality contains far more detail than we expect, related to why search spaces are larger than they appear
- [[superlinear-returns]] — Graham's analysis of why thresholds and exponentials drive outsized returns; hierarchical technology search is itself a threshold/exponential dynamic at the level of subassembly completion

## Sources

- Potter, B. (2026). "Information and Technological Evolution." Construction Physics. <https://www.construction-physics.com/p/information-and-technological-evolution> — [[2026-04-02-information-and-technological-evolution|local copy]]
