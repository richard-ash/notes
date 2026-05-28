---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-04-29-quantum-industrial-base.md
compiled_at: 2026-05-27
model: claude-opus-4-7
confidence: medium
---

# Quantum Supply Chains

The industrial base behind quantum computing — the cryogenics, lasers, photonic chips, and specialized materials that go into the machines, and where in the world they're made. In a 2026 ChinaTalk conversation built around her CNAS report *Quantum's Industrial Moment*, **Constanza Vidal Bustamante** argues (with co-authors Chris Miller of *Chip War* fame and Zachary Yerushalmi) that quantum's decisive contest will not be cracking Shor's algorithm first, but locking in the supply chains across multiple hardware modalities — and that the US still can, because the supply chain for *scalable* quantum computers does not yet exist.

This is the quantum analogue of the 2018–2020 semiconductor supply-chain reports that produced the CHIPS Act. The industrial-organization logic — that surplus and leverage accrue to whoever controls the scarce, hard-to-replicate layer of the stack — is the same one that runs through [[ai-value-capture]]. For the strategic primer on quantum computing itself — what it is, the encryption cliff, the talent and cycle-time bottlenecks — see [[quantum-computing]].

## There is no "the" quantum supply chain

There is no single quantum computer. Competing **modalities** — superconducting (IBM, Google), neutral atoms, trapped ions, photonic, and emerging topological qubits — each have a distinct bill of materials. They draw from common *layers* of the quantum stack:

1. **Materials / atomic sources** — specialized wafers, isotopes, substrates.
2. **Environment** — a cryogenic system (millikelvin or single-Kelvin) or an ultra-high vacuum.
3. **Control** — lasers and control electronics to manipulate and read out the quantum state.
4. **Software**, and eventually **networking** as chips are linked.

The mix per layer varies enough that Vidal Bustamante insists these are *multiple* supply chains, heterogeneous both across modalities and over time. The prototype supply chain (globally distributed, with single-source dependencies on China, Europe, Japan) will look nothing like the supply chain for an encryption-breaking machine.

**The strategic thesis:** the US holds an "incredible moat" in semiconductors built over decades, but holds *no* moat in quantum because no one has built a fault-tolerant machine. Yerushalmi frames this as China's opening to leapfrog to near-parity. Vidal Bustamante reframes it as opportunity: **nobody controls a supply chain that doesn't yet exist, so the US can still dominate the next-generation one if it moves fast.** The blocker is a chicken-and-egg capital problem — no one invests in the scaled supply chain without market demand, and demand never matures without the investment.

Both treat the field as **pre-transistor** — even pre-vacuum-tube. The path to scale is roughly known (photonic integration for manufacturability), but the "transistor of quantum" hasn't been invented, and whoever invents and patents the core scaling method gets an unfair manufacturing + IP advantage.

## The cryogenic bottleneck

Superconducting qubits live at the bottom of a "chandelier" **dilution refrigerator**, stepped down in stages from ~4–10 K to millikelvin — colder than deep space — to isolate fragile quantum states from heat, radiation, and cosmic rays.

- **Helium-3** is the irreplaceable coolant (mixed with abundant helium-4). It's a rare, regulated isotope sourced mainly as **tritium decay from the US nuclear weapons stockpile** (Canada also has a stash; the Moon has lots, deposited by cosmic radiation, but lunar mining is widely judged uneconomical). Yerushalmi's near-term read: as long as the US doesn't go nuclear-free, supply is adequate — *for now*.
- **Suppliers are dangerously few.** Three credible Western makers of dilution refrigerators — **Bluefors** (Finland), **Oxford Instruments** (UK, recently acquired), and **Maybell** (US) — and really only ~two at scale.

**The export-control backfire.** US-and-partner controls on dilution refrigerators (2020 → early 2024) appear to have backfired within roughly a year: China went from **zero** cryogenic-refrigerator makers to **more than the rest of the world combined**, and from no publications to **>50%** of new innovation publications in the area. Vidal Bustamante's nuanced read: the controls *accelerated* an indigenization China might otherwise have undertaken more slowly; China can build one or two systems but not yet hundreds, and hasn't matched Bluefors/Maybell quality — but is on that trajectory. Allies like Finland share fridge IP with the US; China will not.

**Scaling doesn't multiply.** Today's best fridges host ~1,000 qubits. A million-qubit machine cannot be reached by ganging dozens of fridges together: more qubits need more cabling, cabling adds heat load, heat load degrades cooling efficiency. The cooling system itself must be reinvented for efficiency at scale — the "transistor of the scaled cryo system." (Maybell's *ColdCloud*, shown at APS, is cited as the kind of next-gen work needed.)

## Lasers, photonics, and specialized materials

Lasers are central to the **photonic and atomic** modalities — a *chain* of lasers cools atoms to ultracold, drives energy transitions, and reads out results, each tuned to a precise, ultra-stable wavelength, plus the optics to route/focus/frequency-double the light.

- High-priority lasers come from **Japan, Europe, and China**. A Chinese maker produced lasers near-identical to a **Danish** firm's at a fraction of the price (suspected reverse-engineering, documented CCP subsidies) and is now a major US-ecosystem supplier — still bought under R&D tariff exemptions.
- Only **two** credible US laser providers for quantum systems: **Vector Atomic** and **Vescent**, both mid-sized.
- **Specialized materials** (photonic wafers/substrates) are upstream of everything and partly **single-sourced from China**.

**The price gap is the weapon.** A Chinese **wiring tree** (needed per experimental setup) costs ~**one-tenth** of the US equivalent even after tariffs. Cheaper components → more experimental runs → faster iteration.

**Iteration speed is the real lever.** A 40-hour cooldown caps you at one test/week; halving it to 12 hours yields one test/day. A new photonic integrated circuit (PIC) takes **12–18 months** to obtain in the US versus **~2 weeks** in China, which has deep photonics fabs serving many industries. Yerushalmi calls a supply-chain lock a "**supply chain OODA loop**" — it lets you be 10× more reactive than your adversary, which matters more than fundamental-physics breakthroughs at this stage.

**Quantum sensors** share the laser/optics supply chain and are a *nearer-term* market than computing (e.g., GPS-denied navigation — salient after the Iran conflict), which makes these components a real bottleneck sooner than quantum computing alone implies.

## "Being first isn't winning"

Vidal Bustamante's most distinctive claim: even if a US superconducting machine cracks Shor's algorithm first, she "wouldn't call victory." The finish line moves — a cheaper, more manufacturable Chinese *photonic* machine could clear the same bar with a nimbler supply chain and win the war. So the goal is **all hands on deck across every modality**, treating quantum as an innovation/industrial-policy *portfolio* rather than a single race.

The cautionary tale is **quantum key distribution (QKD)**: cryptographically weak and economically marginal ("just look up 'NSA QKD'"), yet Pan Jianwei, head of China's quantum program, has poured resources into it. The lesson cuts both ways — intense competition demands industrial policy, but policy is easy to get badly wrong; you mostly hope your rival errs more than you do.

## Policy levers

Vidal Bustamante and Yerushalmi converge on a menu, not a single fix (the supply chain is too heterogeneous):

- **Targeted multi-year *advanced* R&D** on cryogenics, lasers, and optics — not just fundamental research, given the race clock.
- **Co-design** between enabling-tech makers (fridge/laser companies) and end users (computing integrators) so components are built to real requirements.
- Yerushalmi's **three levers**: (1) *supply* — is the widget on the shelf? (2) *innovation* — skating to where the puck is going; (3) *market-failure capacity* — funding **high-mix, low-volume fabs** that are structurally unprofitable (his Elevate fab: ~$40M capex hoping for ~$1M/yr revenue — "no investor gives you that"). Government must underwrite this to preserve industrial capacity.
- **Helium-3**: a cleanly bounded, high-intervention case — have **DOE's isotope program** audit inventories, reserve some for quantum, and recompute repurposing of helium-3 already in use.
- On **banning Chinese components**: Vidal Bustamante would block the strategic, high-sophistication inputs (the lasers, where the US has talent and a path) while using strategic financing/tax breaks for domestic suppliers — but not the "screws and light bulbs." Yerushalmi's end-state triad: **access** (widget availability), **security** (no hidden chips / Stuxnet-style implants in end-stage products), and **out-innovation** (iteration speed). Drawing the line precisely is unsolved.

## US vs. China: structure of the contest

The "China has a Manhattan Project, the West has chaos" analogy *used to* hold but is breaking down: China is now diversifying into neutral-atom, photonic, superconducting, and topological **private startups**, often spun out of Pan Jianwei's circle — not merely state labs, so "state-driven therefore ineffective" is a dangerous assumption.

- **China's edge:** thoughtful end-to-end supply-chain investment (react fast to whichever modality wins) and frequent provincial **moonshot programs** that act as a forcing function of demand — fire off a thousand crazy-deadline solicitations, 999 fail, one succeeds. Plus a reactive academic sector willing to fuse two material systems where US grant bureaucracy forbids it.
- **US's edge:** deep technical talent inside government (DARPA, DOE, NIST) crafting a *few very thoughtful* programs rather than a million scattershot ones — an asset even over Europe. Vidal Bustamante worries this capacity is eroding; Yerushalmi credits DOE leadership (Dabbar, Gil) with pushing a faster, more creative paradigm.

## Why quantum isn't (yet) semiconductors

Jordan Schneider's takeaway: semiconductors are **consolidated** — two EDA players, a few photomask makers, one EUV maker (ASML) — with the whole industry pulling one direction. Quantum has **~90 companies** building hardware across modalities, "90 little empires," with the very shape of the eventual machine still up for grabs. Yerushalmi's preferred analogy is **biotech**, where many approaches (small molecules, CAR-T, antibodies, immunotherapies) all mature against a unified target — and where decades of cross-disciplinary public-policy/finance/scientific fluency exist that quantum still lacks. His closing plea: build that interdisciplinary rigor *now*, while the field is pre-transistor.

The existing US scaffolding is the **National Quantum Initiative** (first Trump administration) and the **National Quantum Initiative Act**, which provide funding mechanisms across agencies.

## Sources
- ChinaTalk / Jordan Schneider, with Constanza Vidal Bustamante (CNAS), Chris Miller, and Zachary Yerushalmi (2026-04-29). "Quantum 201: The Supply Chain." <https://www.chinatalk.media/p/the-quantum-industrial-base> — [[2026-04-29-quantum-industrial-base|local copy]]
- Underlying report: Vidal Bustamante & John Burke (CNAS, 2026). "Quantum's Industrial Moment: Strengthening US Quantum Supply Chains for Scalable Advantage." <https://www.cnas.org/publications/reports/quantums-industrial-moment>
