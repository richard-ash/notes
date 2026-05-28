---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-04-21-quantum-101.md
compiled_at: 2026-05-27
model: claude-opus-4-7
confidence: medium
---

# Quantum Computing

What quantum computing is, why it suddenly matters, and what it would mean for the US to "win" the race against China. This is the strategic-primer entry; the supply-chain mechanics (cryogenics, helium-3, lasers, PICs, export controls) live in [[quantum-supply-chains]]. Both come from ChinaTalk's 2026 quantum series with **Zach Yerushalmi** (CEO of Elevate Quantum, the US government's only place-based quantum investment) and **Chris Miller** (*Chip War*).

Yerushalmi's framing claim: with AI "on the doorstep," quantum is the single biggest lever left for the next couple of decades — and the stakes are higher than any US industrial program since the atomic bomb. The contrast with semiconductors recurs throughout: the US has *decades* of moat in chips and can afford mistakes; in quantum the moat is small and **the margin of error is freakishly thin**.

## Why classical computers can't do it

The idea dates to **Richard Feynman (1981)** — "nature is quantum mechanical, dammit." The physics that governs the atomic realm (drug discovery, catalysts, materials) is intractable classically because quantum systems scale as **2ⁿ**: a 20-atom system has ~a million states. **Penicillin (42 atoms)** would need ~**10⁸⁶ transistors** to model from first principles — more than there are atoms in the observable universe — yet only ~**186 qubits**. Because the scaling is exponential, going from 186 → 187 qubits isn't a marginally better machine; it adds an entire interacting neighbor.

So a quantum computer is **not a faster classical computer** — it's a different machine for *simulating nature*. Yerushalmi's analogies: classical is a car, quantum a rocket ship (a faster car won't reach space); and Matt Langione's (BCG) **maze** — a classical computer walks the maze sequentially and backtracks, while a quantum computer uses superposition, entanglement, and interference to evaluate every junction in parallel.

## Two application classes

1. **Simulation / molecular design** — the near-term tractable killer app may be **corrosion modeling** (tens of billions to shipping and defense), then nuclear chemistry, drug discovery, materials, and room-temperature superconductors. The "Jetsons age" of rational design at the atomic level.
2. **The hidden subgroup problem → breaking encryption.** Quantum computers are exceptionally good at **factoring large primes** and **elliptic-curve** problems — the math underpinning essentially all current cryptography (and Bitcoin signatures). This is the near-term, scary class (see *The encryption cliff* below).

Yerushalmi's deeper worry is **recursive material-science design**: a machine that rationally designs superconductors or nuclear chemistry lets you "lock down IP space and know-how" against rivals. His framing — AI is "sophisticated curve-fitting, stabbing in the dark," whereas quantum "solves from first principles and locks in the correct solution" — so the moat is not just building the system but **securing the inventions the system creates**.

## The 2025 inflection: error correction

The turning point both guests identify is **error correction** (Google's *Willow* and related work, 2025). Until then, *adding* a qubit made the whole system *less* stable — bad news for usefulness. The sea change: a scheme where adding a qubit makes the system *more* stable. That flips the question from **"if"** these capabilities arrive to **"when."** Industry timelines compressed from "~10 years out" to "**3–5 years**."

Miller's analogy: quantum today is "like 2015 in AI" — insiders see rapid progress, outsiders dismiss it. Yerushalmi sharpens it: the ChatGPT moment hasn't happened, but 2025 was quantum's **"Attention Is All You Need" (2017)** moment — the time to get attuned is *before* the public shock, not after.

## From science to engineering — and the biotech model

Both frame the field as having crossed from a *science* phase into an *engineering/scaling* phase (without abandoning fundamental R&D — the vacuum-tube-to-transistor lesson). Yerushalmi's governing mental model is **biotech**, not semiconductors: many competing **modalities** (like small molecules vs. CAR-T), and the field has just "entered phase 1 clinical trials," so the right policy toolset resembles how the US fosters biotech. The catch: in biotech the US has a huge moat (the Boston cluster), so mistakes are survivable; quantum is far earlier-stage with a thin moat. (Yerushalmi uses the same biotech analogy in [[quantum-supply-chains]].)

**Industry structure:**
- **Big tech** (Google, Microsoft, IBM) spend billions/year to avoid a "strategic surprise" / Sputnik moment — rounding errors on their balance sheets. IBM runs the flagship program.
- **Startups** play the disruptive-academia role (as in biotech). **Neutral atoms** went from "science fiction / a joke" ~5 years ago to a leading approach; Google, a **superconducting** pioneer, nonetheless put **$250M into QuEra** (neutral atoms). Superconducting qubits (John Martinis, 2025 Nobel) have drawn 60–80% of investment to date.
- **DARPA's Quantum Benchmarking Initiative (QBI)** — the largest public program in DARPA history (~$600M this year) — exists so the US "can't be surprised that China can break its codes." Its design reconstructs an **advanced market commitment** / grand-challenge prize ladder mapped onto biotech staging: ~$1M (table stakes) → $15–20M → up to **$300M** for a credible demonstration-scale system → an implied government purchase (the "FDA approval") → ~$1B beyond. The payouts are deliberately large enough to pull venture capital into the flywheel.

## What "winning" means

Yerushalmi: **get there first** (the first *commercially useful* — people say "fault-tolerant" — machine, like the first useful vacuum-tube computer) **and sustain** the best capability/access long-term. The hard part is that with no price signal, there's no obvious **lead indicator** of who's winning (his candidate: cycle time — below).

A recurring correction to lay intuition: **quantum will not replace classical.** Miller's three-paradigm model — **CPU + GPU + QPU** working in tandem, each for the problems it suits. QPUs are Turing-complete (they *can* compute anything) but only *efficient* on specific problem classes, just as GPUs never displaced CPUs. Expect **purpose-built machines** for the foreseeable future, possibly converging later on a transistor-like common architecture.

## Diffusion: a "hardware sport"

In AI, frontier techniques diffuse fast (arXiv, SF parties, even rival labs scraping each other's models). Quantum is different because it's **"very much a hardware sport"** with long iteration times and heavy *tacit* knowledge (how to fix optics to a breadboard). The research/algorithm layer diffuses via publication, but **manufacturing know-how doesn't** — Miller's parallel to AI, where algorithms diffuse but chip-fab know-how stays put. Received wisdom: China keeps publications on lockdown until a Western breakthrough appears. The double edge: **a genuine Chinese breakthrough would be correspondingly hard to transmit back to the US** — a stickier moat in both directions.

## The encryption cliff

The most concrete near-term threat. **NIST** post-quantum standards (2024) recommend upgrading government systems by 2028–29 and consumer systems by 2035 — but crypto-breaking machines may be online by **~2030**, a **3–5 year window** against the usual 10–15 year security-upgrade cycle. The mechanism is **Shor's algorithm** against factoring and elliptic-curve cryptography. The migration target, **lattice-based cryptography**, is theoretically sound but **immature in implementation** — so the US must move faster than ever to something not yet deployed at scale.

Miller draws the key game-theoretic distinction: AI's payoff is a *gradient* (always more productivity to come), whereas **decryption is a threshold** with immediate fruits. That makes "Defense-Production-Act-style" full mobilization of quantum resources plausible if a power is months from breaking encryption — and you "can't bomb a quantum computer" (one room, anywhere, and the know-how persists). Yerushalmi tempers this: the *first* machine is slow — a single code might take months — so you "choose your bullets assiduously" (the practical shape of *harvest-now-decrypt-later*). Western governments have committed ~**$23B** to quantum over three years, motivated, he suspects, mostly by encryption fear.

## Bottlenecks: talent and cycle time

You *can* brute-force an inefficient RSA-breaker with money now that more qubits help rather than hurt — but **how** you spend dominates:

- **Talent** is the first constraint — ~**3 quantum job postings per 1 qualified candidate**, and a PhD takes 5–7 years that money can't compress. The highest-leverage trainees: **quantum systems engineers** and **technicians**. A fixable absurdity: technician/undergrad training is all-theory because the hardware is too expensive to let students touch, so new hires must be retrained from scratch — solvable by funding *physical access* to systems.
- **Cycle time / access to capital-intensive services** is, Yerushalmi argues, the bigger lever and the best **North Star metric** — access to superconducting fabs, **III-V semiconductor fabs**, and scaled cryogenics. A **photonic integrated circuit (PIC)** takes 12–18 months to obtain for big US players vs. *weeks* next to a fab; China's 5G/photonics edge was building and testing ~10× faster. Americans excel at *learning*; they lag badly on cycle time. (Miller's caveat: optimize **cycle time × per-cycle improvement**, not cycle time alone — a slow TSMC node is fine if each node leaps.)

The institutional fix Yerushalmi most wants is an **IMEC** (Belgium) — the canonical semiconductor public-private nonprofit that masters the **"middle TRL"** valley between fundamental R&D and market competitiveness. Korea (KAIST), Taiwan, and China all have such institutions; the US largely doesn't for quantum. **Elevate Quantum** is the partial answer: the Mountain West cluster holds ~half of US quantum jobs and capital; Elevate's federally funded fab costs **$40–50M to stand up to earn ~$1M/year** — a clear VC no-go that only makes sense as a nonprofit national-competitiveness play. This same market-failure-fab argument anchors the policy section of [[quantum-supply-chains]]. Cost context: ~$5–50B for the first RSA-breaking machine, with **cost-per-calculation** (what QBI assesses) the metric that decides whether any given problem is worth running.

The industrial-organization throughline — surplus and leverage accrue to whoever controls the scarce, hard-to-replicate layer, and "intelligence/capability" is rarely the binding constraint — is the same logic [[ai-value-capture]] applies to AI.

## Sources
- ChinaTalk / Jordan Schneider, with Zach Yerushalmi (Elevate Quantum) and Chris Miller (2026-04-21). "Quantum 101: What exactly is quantum computing?" <https://www.chinatalk.media/p/quantum-101> — [[2026-04-21-quantum-101|local copy]]
