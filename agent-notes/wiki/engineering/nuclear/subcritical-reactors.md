---
source: agent
compiled_from:
  - agent-notes/raw/engineering/nuclear/2026-05-13-sabine-subcritical-reactors.md
compiled_at: 2026-05-15
model: claude-opus-4-7
confidence: medium
---

# Subcritical Reactors

A **subcritical reactor** is a nuclear fission reactor whose fuel assembly is *deliberately* below the critical mass threshold, so the chain reaction cannot sustain itself. The reactor only produces power while an *external* neutron source (a proton accelerator firing at a spallation target, or a compact deuterium-tritium fusion source) is feeding it neutrons. Turn the beam off and the fission tapers out within milliseconds. There is no runaway reaction available as a failure mode, because criticality was never on the table — the system is held in fission only by an active, externally-powered input that any sane operator can simply switch off.

This is structurally different from the standard reactor-safety story. In a conventional critical reactor, you assemble fuel that *is* above critical mass and then engineer a way to *slow* it (moderators, control rods, coolant) so that the chain reaction proceeds steadily rather than explosively. Safety is the *absence* of the catastrophic mode — every failure has to be actively prevented. In a subcritical reactor, the catastrophic mode is structurally unavailable. Safety is *the presence* of the harmless mode — the worst case is "the lights go out."

## The fission chain reaction and what subcritical defeats

Fission begins when a neutron — uncharged and so not repelled by the positively charged nucleus — enters a heavy nucleus (uranium, plutonium, thorium-bred uranium-233), destabilizes it, and causes it to decay into two smaller daughter nuclei *plus*, crucially, two or more additional free neutrons. Those free neutrons split further nuclei, releasing more neutrons, and so on — the classic 1 → 2 → 4 → 8 chain. The chain is only self-sustaining if there are enough target nuclei densely enough packed that newly-emitted neutrons hit fissile material before escaping; that threshold is the **critical mass**.

Critical reactors sit above this threshold and engineer the timing down with moderators (water, graphite) that slow neutrons into the cross-section range where they're more likely to be captured. Subcritical reactors sit below the threshold by design. Neutron multiplication still happens — each external neutron can trigger fissions that produce a few more neutrons that trigger a few more, etc. — but the multiplication factor *k* is less than 1, so each "generation" of neutrons is smaller than the last and the cascade dies out without continuous external feeding. Power output is roughly proportional to the external neutron source strength multiplied by 1/(1−k); turning the source off collapses output to background.

## Neutron-source architectures

The whole engineering question of subcritical reactors collapses into the neutron source. Two main approaches:

**Accelerator-driven systems (ADS).** Accelerate protons (typically to ~1 GeV) and slam them into a heavy-metal target (lead, tungsten, mercury); each proton kicks out ~20-30 neutrons via *spallation*. This is the most studied approach. The catch is scale: GeV-class proton accelerators are typically several hundred metres long, which is why ADS reactors have historically been infrastructure-scale, not transportable. **SubCritical Systems** (Austin) and **Muon Inc** are pursuing this path, targeting 50-100 MW for data-centre or factory-complex applications and aiming for first power in the 2028 window. Hossenfelder reads 2028 as ambitious but achievable, since the underlying physics is known and the engineering challenge is integration rather than discovery.

**Fusion-driven neutron sources.** Compact deuterium-tritium (D-T) fusion devices produce ~14 MeV neutrons. A single fusion event yields one neutron, vastly less than spallation, so the device has to run a high D-T fusion rate to drive a useful subcritical fission output — but it can be benchtop-scale rather than building-scale. **Ampera**, the US startup, describes its design as a "hybrid fission-fusion machine" with a sealed 3D-printed thorium-fuelled subcritical core that "operates for decades and is never refueled," small enough to fit on a truck (~10 m × 2-3 m × 2-3 m), at 15-30 MW output. The thorium breeds U-233, which is then fissioned. Hossenfelder is skeptical: the company materials don't explain the fusion side, and a D-T fusion source compact enough to be truck-scale has yields she suspects are far too low to drive useful fission — and if they *had* solved D-T fusion at usable scale, the fission half would be superfluous. Her summary: "personally I would not invest into this company." This is one source's read; treat it as a flagged-skeptic prior, not a verdict.

## Waste burning as a secondary capability

A second, less marketed virtue of subcritical reactors is **transmutation**: their externally-driven neutron flux can be tuned to fission long-lived actinides (the most awkward fraction of spent fuel from conventional reactors), converting hundred-thousand-year-half-life waste into fission products with much shorter (centuries-scale) half-lives, while extracting energy from the process. **Transmutex** (Switzerland) specialises in this application; the broader European interest in ADS has long been tied to the waste-disposal use case rather than primary power generation. This converts a current liability — spent-fuel inventories sitting in cooling ponds and dry casks — into a fuel stream, which is the part of the subcritical thesis with the clearest existing-infrastructure overlap.

## Government programmes

Belgium, China, and Japan are running governmental subcritical/ADS projects. Belgium's MYRRHA programme (at SCK CEN, Mol) is the longest-running and best-known of these, originally targeted at minor-actinide transmutation. Hossenfelder mentions these only in passing; the durable observation is that subcritical reactors are not a purely-startup phenomenon — state-funded programmes have been advancing the same architecture at scale for decades, which is part of why the underlying physics is well-understood.

## What this is and isn't

The structural claim — *runaway reactions are impossible because the assembly is subcritical* — is straightforward and correct. The marketing claim that subcritical reactors will be **cheap or small** is much weaker. Hossenfelder's net read is that subcritical reactors "could indeed make nuclear fission power much safer" but that she is "skeptical they will be either cheap or small." The reason is the same one that has held back ADS for decades: high-current GeV proton accelerators are expensive and large, and the compact-fusion-source workaround requires solving a problem (high D-T fusion yield in a small package) that, if solved, would obviate the fission half of the machine.

The deeper point sits in [[induced-demand|systems-thinking]] territory: subcritical reactor designs are answering a *political* failure mode of conventional fission (public fear of runaway reactions, regulatory burden derived from that fear), not its *engineering* failure modes (cost, construction time, waste, fuel cycle). They may succeed at the political problem while failing at the cost problem. Whether the political win is worth the cost depends on whether public acceptance is the actual binding constraint on nuclear deployment — which in most jurisdictions today it appears to be.

The transmutation use case is more compelling on its own terms, because it solves a current waste-disposal liability rather than re-litigating the safety case for new build.

## Sources

- Sabine Hossenfelder (2026-05-13). "These Reactors Solve The Nuclear Safety Problem." YouTube. <https://www.youtube.com/watch?v=d96WHYOHoU8> — [[2026-05-13-sabine-subcritical-reactors|local copy]]
