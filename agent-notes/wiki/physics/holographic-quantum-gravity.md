---
source: agent
compiled_from:
  - agent-notes/raw/physics/2026-06-03-entanglement-builds-space-time-magic-gives-gravity.md
compiled_at: 2026-07-31
model: claude-opus-5[1m]
confidence: high
---

# Holographic Quantum Gravity: Entanglement, Magic, and Space-Time as a Code

The holographic research program tries to derive space-time — and eventually gravity — from nothing but quantum information. Its organizing target is John Archibald Wheeler's 1973 two-sentence summary of general relativity: "Space acts on matter, telling it how to move. In turn, matter reacts back on space, telling it how to curve." The program has had the first sentence for about a decade; a cluster of recent results claims to have found the ingredient responsible for the second. That ingredient is a quantum-information quantity called **magic** (non-stabilizerness), which Charles Cao (Virginia Tech) calls "the fabric softener of space."

## The holographic setup

Two historical steps set up the frame:

1. **Early 1970s — Bekenstein and Hawking.** A black hole and everything that fell into it can be reinterpreted as a spherical collection of particles on its surface. Information about a 3D interior is carried by a 2D boundary.
2. **Late 1990s — Maldacena, Witten and others.** The same move extends to a whole (exotic, static) universe: an anti-de Sitter space described as a throng of interacting particles arranged on its boundary sphere.

The general statement is the **holographic principle**: a 3D region of space-time is equivalent to a 2D surface's worth of quantum particles, the way a holographic sticker encodes a 3D scene on a flat surface without loss. The practical payoff is that black holes — where general relativity's geometric description tears — become describable in a formalism that never breaks down.

**Entanglement is the connective tissue.** The now-standard picture is that entanglement between boundary particles is what gives the bulk its geometry. The canonical illustration is a wormhole: holographically, a 3D wormhole is two entangled sets of particles, and snipping the entanglement "threads" one at a time thins the tunnel until, with the last thread cut, the two regions disconnect entirely. This delivers Wheeler's first sentence — a geometric arena in which matter can move.

## Space-time as a quantum error-correcting code

Daniel Harlow (MIT), building on work by John Preskill and others, identified the mathematics for the 2D→3D perspective shift: encode a region of space *and its matter contents* into boundary particles using a **quantum error-correcting code**.

The analogy is not decorative. Quantum computers need error correction because qubits lose superposition easily, so one qubit's information is spread redundantly across many physical qubits and survives the loss of some of them. Holography has the same redundancy structure: a single bulk location is not stored in one set of boundary particles but smeared across many, precisely because they are entangled. Bartek Czech (Tsinghua) puts it as "when you design codes for quantum computing, you're doing the same kind of thing that holography already did for you." Almheiri, Dong and Harlow made this concrete with an explicit code in 2014, and Harlow fleshed out the correspondence in a 2016 paper.

**The dead end.** The codes used were **stabilizer codes**, and they cleanly partition the boundary entanglement into two non-interacting kinds: entanglement responsible for the geometry, and entanglement responsible for the matter in it. That perfect isolation is a *feature* in quantum computing — you want encoded data insulated from its environment — but it is fatal in holography, because it forbids exactly the matter→geometry back-reaction Wheeler's second sentence demands. In Czech's phrasing: "We knew how to build a space-time, but this space-time was inert. It didn't do anything." The bowling ball sat on the mattress without making a dent.

## Magic

Magic is a measure of how far a quantum state sits from the states a classical computer can efficiently simulate. Background: researchers once assumed entanglement was the source of quantum computational advantage, but classical algorithms were found that mimic broad classes of entangling operations on a laptop. In 2004 Sergey Bravyi and Alexei Kitaev drew attention to **non-Clifford gates** — the T gate is the simplest example, the Toffoli gate another — whose presence makes the equivalent classical simulation blow up. They named the resulting complexity "magic." The more non-Clifford gates a state requires to prepare, the more magical it is.

The bridge to gravity came in stages:

- **2020 — Cao & Lackey** tweaked an existing holographic code and found it allowed the encoded space to change, though not in response to matter. Progress, but they did not understand *why* the tweak worked.
- **2021 — Pollack and collaborators** showed that actually running the tweaked code on a quantum computer would require a T gate. That was the missing explanation: the tweak had smuggled in magic.
- **2020 — Cao, Swingle & White** found that the boundary states dual to anti-de Sitter space are themselves highly magical, raising the question of what that magic *does* to the bulk.
- **2024 — Cao, Hamma and collaborators**, building on work by Xi Dong (UCSB), answered it: magic is what gives space its springiness — its capacity to bend, and therefore its gravity. Ning Bao (Northeastern) summarizes: "If you have one, you always have the other."
- **Early 2026 — Cao, Preskill and collaborators** assembled the pieces into a next-generation code, successor to the stabilizer codes of a decade earlier, built with many non-Clifford gates. The magic makes the two kinds of entanglement — geometric and material — able to affect one another. Cynthia Keeler (ASU), not involved in the work, notes the significance: "In quantum gravity, we don't expect the background is fixed. It should fluctuate."

The clean statement of the emerging picture: **entanglement gives space its shape; magic gives it its flexibility.** The two defining features of quantum mechanics map onto the two defining features of space.

## Gravity as imperfect encoding

The most conceptually striking consequence is inverted from the engineering intuition. Non-magical (stabilizer) codes protect their encoded information *perfectly*, and they produce inert, gravity-free space. Gravity arises from the **mixing** of encoded information — so the encoding must be only approximate, and some facts about the bulk cannot be perfectly recovered by measuring a subset of boundary particles in the usual way. What a quantum engineer would classify as a badly written code is, in Czech's line, "the reason Newton's apple fell on him." Cao's own reading is that quantum error correction and quantum computing are human pursuits, and there is no reason gravity should honor our preference for perfection.

This has a methodological corollary Swingle emphasizes: if quantum gravity intrinsically requires high magic, then classical simulation of it is off the table by construction, and simulating gravity in regimes where general relativity fails genuinely requires a quantum computer. Magic is the same resource that separates quantum from classical computing, so a "gravity needs magic" result is simultaneously a "gravity needs quantum hardware" result.

## How much has actually been shown

Cao is explicit that this is early: "This gets you a precursor of gravity. You satisfy one of the necessary conditions. Right now, we are at step 0.5 of 5." Concretely, the 2026 code:

- does not describe the kind of space we actually live in (the holographic setting is anti-de Sitter space, which has negative curvature; our universe does not),
- does not reproduce the specific dynamics of Einstein's field equations,
- **contains no time** — the ticking of time is absent from the construction.

Speaking at the American Physical Society's annual summit in Denver, Cao joked that he was the only speaker not actually studying quantum gravity. The result is best read as a **structural constraint on what a theory of quantum gravity must look like** — if you want your encoded space to bend, your code must be magical — rather than as a candidate theory. The claim is one of necessity, not of sufficiency, and the entanglement→geometry half of the correspondence remains far better established than the magic→curvature half.

Two further caveats worth holding. First, the whole program lives inside AdS/CFT, a duality for a universe with the wrong sign of cosmological constant; the extent to which any of it survives translation to de Sitter or flat space is a long-standing open problem the source does not address. Second, "magic" here is doing double duty as a rigorously defined resource-theoretic quantity *and* as a heuristic gloss ("fabric softener"), and the popular framing compresses a decade of technical results — the AdS/CFT correspondence itself is still a conjecture, not a theorem.

## Connections

- The distinctive epistemic posture — deriving a physical phenomenon from an information-theoretic resource rather than positing new fields or particles — parallels other "reformulate rather than add" moves in physics, such as [[modified-newtonian-dynamics|MOND's]] attempt to explain galactic dynamics by changing the force law instead of adding dark matter. Both are bets that the anomaly lies in the framework, not in a missing ingredient.
- The finding that the vacuum's quantum structure has direct physical consequences echoes the experimental result on [[virtual-particles-qcd-vacuum|virtual quark–antiquark pairs in the QCD vacuum]] — in both cases a "merely bookkeeping" quantum property turns out to be doing real work.
- Cao's "step 0.5 of 5" is an unusually honest calibration statement, of the kind that is usually missing from popular coverage and that a reader should look for by default. Compare the framing discipline in [[jwst-early-universe-puzzles|JWST's early-universe puzzles]], where the constraint is an *oversupply* of viable theories rather than an undersupply.

## Sources
- Wood, Charlie (2026). "Entanglement Builds Space-Time. Now 'Magic' Gives It Gravity." *Quanta Magazine*. <https://www.quantamagazine.org/entanglement-builds-space-time-now-magic-gives-it-gravity-20260603/> — [[2026-06-03-entanglement-builds-space-time-magic-gives-gravity|local copy]]

Primary literature referenced by the source:
- Almheiri, Dong & Harlow (2014). "Bulk Locality and Quantum Error Correction in AdS/CFT." <https://arxiv.org/abs/1411.7041>
- Dong (2016). "The Gravity Dual of Rényi Entropy." <https://arxiv.org/abs/1601.06788>
- Harlow (2016). "The Ryu-Takayanagi Formula from Quantum Error Correction." <https://arxiv.org/abs/1607.03901>
- White, Cao & Swingle (2020). "Conformal field theories are magical." <https://arxiv.org/abs/2007.01303>
- Cao & Lackey (2020). "Approximate Bacon-Shor Code and Holography." <https://arxiv.org/abs/2010.05960>
- Cao, Hamma et al. (2024). "Gravitational back-reaction is magical." <https://arxiv.org/abs/2403.07056>
- Cao, Preskill et al. (2026). <https://arxiv.org/abs/2603.13475>
