---
source: agent
compiled_from:
  - agent-notes/raw/systems-thinking/2026-10-20-how-complex-systems-fail.md
compiled_at: 2026-10-20
model: claude-fable-5-1
confidence: high
---

# How Complex Systems Fail

Richard I. Cook's *How Complex Systems Fail* (1998, revised through 2000) is a four-page treatise of eighteen numbered theses on why catastrophes happen in systems like healthcare, transportation, and power generation, and why the way we investigate them afterward is usually wrong. Cook was an anaesthesiologist at the University of Chicago's Cognitive Technologies Laboratory, and the subtitle frames it as a contribution to patient safety. It outgrew that: the paper became the founding text for the "New Look" at human error that Cook and David Woods had been developing since the early 1990s, and later the most-cited single document in the software reliability community's thinking about incidents. The site at how.complexsystems.fail is a re-hosting of the original, with the supporting Cook and Woods papers attached.

The structure of the argument is a reversal. Common sense says a system is safe until something breaks it, and the job of an investigation is to find what broke it. Cook argues the opposite: the system is always already broken, it is continuously *held* safe by the people operating it, and accident investigations that look for a broken part are describing a social need rather than a technical reality.

## The eighteen theses

Cook numbers them without grouping, and people cite them by number. They cluster into four themes.

### How failure is structured (1 to 6)

1. **Complex systems are intrinsically hazardous.** The hazard is in the process itself, not a defect to be removed. The presence of hazard is what drives the construction of defenses.
2. **They are heavily and successfully defended.** Technical defenses (backups, interlocks), human ones (training), and organizational ones (procedures, certification, work rules) form layered shields that normally divert operations away from accidents.
3. **Catastrophe requires multiple failures; single-point failures are not enough.** Each small failure is necessary but only the combination is sufficient. Most failure trajectories are blocked by design; those that reach the operational level are mostly blocked by practitioners.
4. **Systems contain changing mixtures of latent failures.** It is impossible to run a complex system without multiple flaws present. They are tolerated because each is individually insufficient, and the mix changes constantly with technology, work organization, and the fixes applied to earlier failures.
5. **Complex systems run in degraded mode.** The system works because of redundancy and because people make it work despite the flaws. Post-accident reviews nearly always find prior "proto-accidents," and the claim that these should have been recognized rests on a naive picture of what normal operation looks like.
6. **Catastrophe is always just around the corner.** Practitioners are always in close physical and temporal proximity to potential disaster. This potential cannot be eliminated.

### How failure is evaluated after the fact (7, 8, 15)

7. **Post-accident attribution to a root cause is fundamentally wrong.** Since failure needs multiple contributors and only their linkage is sufficient, no isolated cause exists. Root-cause reasoning reflects "the social, cultural need to blame specific, localized forces or events for outcomes," not a technical understanding. Cook's footnote points to anthropological work (Goldman on the Huli, Tasca) showing that cause is socially constructed.
8. **Hindsight biases post-accident assessments of human performance.** Knowing the outcome makes the warning signs look salient in a way they never were at the time. Cook calls hindsight bias "the primary obstacle to accident investigation, especially when expert human performance is involved," and notes this is a feature of all human cognition about the past, not of medicine.
15. **Views of cause limit the effectiveness of defenses.** Remedies aimed at obstructing the "cause" of the last accident do little, because the pattern of latent failures has already shifted and an identical accident was vanishingly unlikely anyway. What the remedies reliably do is add coupling and complexity, which increases the number of latent failures and makes future trajectories harder to see and block.

### Practitioners at the sharp end (9 to 14)

9. **Operators have dual roles, as producers and as defenders against failure.** They balance production against incipient failure continuously. Outsiders see only one role at a time: production in calm periods, defense after accidents.
10. **All practitioner actions are gambles.** Every action is taken under uncertainty. After an accident the losing gambles look like blunders; the fact that successful outcomes are also the result of gambles goes unappreciated.
11. **Actions at the sharp end resolve all ambiguity.** Organizations are ambiguous, often deliberately, about how production targets, cost, and acceptable risk trade off. The practitioner's action is what makes the tradeoff concrete, and the practitioner is then judged on it with hindsight and without regard to production pressure.
12. **Practitioners are the adaptable element.** They restructure the system to reduce exposure, concentrate scarce resources where demand is expected, build pathways for retreat and recovery, and set up early detection so production can be cut back gracefully.
13. **Expertise is constantly changing.** Experts leave and must be replaced, and the technology they are expert in changes. Training is part of the system's function, and at any moment the system holds a mix of expertise levels, with the dilemma of spending scarce expertise on the hardest work versus developing it for the future.
14. **Change introduces new forms of failure.** A low accident rate invites changes, especially new technology, aimed at frequent low-consequence failures. These often open new pathways to rare, high-consequence ones. Because such accidents are rare, many changes accumulate before one occurs, hiding the contribution of any single change.

### What safety is (16 to 18)

16. **Safety is a characteristic of systems, not components.** It is emergent, resides in no person or department, and cannot be purchased or stockpiled like a raw material. The state of safety is always dynamic.
17. **People continuously create safety.** Failure-free operation is the product of ongoing human adaptation, mostly by selecting a well-rehearsed routine from a store of responses, sometimes by novel combination or outright invention.
18. **Failure-free operations require experience with failure.** Operators need intimate contact with failure to recognize the "edge of the envelope," the region where performance degrades, becomes unpredictable, or cannot be recovered. Safety improves by giving operators calibrated views of hazard and of how their actions move the system toward or away from the edge.

## The argument underneath

Three ideas carry the whole paper.

**Causation is a story, not a finding.** Theses 3, 4, and 7 together deny that an accident has a cause in the sense an investigation wants. The accident is the conjunction of latent conditions that were each individually tolerable; pulling any one out and calling it "the" cause is a choice made after the fact. Cook's companion paper with Woods and Miller, *A Tale of Two Stories*, makes this the "first story" (human error as cause) versus "second story" (how the system normally produces success) distinction that later became standard vocabulary.

**The sharp end absorbs the organization's ambiguity.** Thesis 11 is the one with the most political bite. Organizations decline to specify how much risk is acceptable for how much throughput, so the operator's moment-to-moment choices are where that policy actually gets set. When a gamble fails, the organization gets to discover retroactively that it had always wanted the safer choice.

**Safety is produced, not possessed.** Theses 16 to 18 relocate safety from a property of the artifact to an activity of the people. This is why Cook's prescription is not more barriers but better calibration: operators who know where the edge is.

## Implications

These are the author's synthesis, not Cook's text.

- **Incident review.** The paper is the intellectual basis for blameless postmortems and for replacing "root cause" with "contributing factors." Its sharper claim, thesis 15, is less widely absorbed: every post-incident action item that adds a check, a gate, or a procedure is itself a change under thesis 14, and tends to add the coupling that makes the next accident harder to see. A postmortem that produces ten new safeguards may have made the system less safe.
- **Degraded mode as the design baseline.** Keathley's [[resilient-application-boot|stacked boot sequence]] takes thesis 5 as its premise: something is always broken at scale, so the engineering problem is preventing two simultaneous faults from combining. The same reasoning underlies the multiplicative "step math" in [[agent-failure-modes]]: every added surface is a new latent failure, and risk compounds rather than adds.
- **Automation and thesis 14.** Retries, autoscaling, orchestration, and failover each remove a class of frequent small failures and introduce rarer, larger ones (retry storms, thrashing, split-brain). Cook's point is not that these are bad but that their new failure modes are invisible before the fact because attention goes to the benefit.
- **Chaos engineering and game days** are thesis 18 operationalized. A system kept far from its edge produces operators who cannot recognize the edge. Deliberately injected failure keeps calibration current.
- **Hindsight bias** belongs in the cognitive-bias catalogue in [[mental-models]], but Cook's framing is the more useful one for engineers: it is not a quirk to correct for but the default state of any observer who knows the outcome. The practical response is to reconstruct what the operator could see at the time, before reading the outcome.
- **Leverage.** In Meadows's terms ([[leverage-points]]), post-accident rules and checks are low-rung interventions on parameters and buffers. Thesis 16's claim that safety is emergent says the leverage is higher up, in information flows (what operators can see) and goals (what the organization will admit it is trading off).

## Lineage and reception

The paper distills a research program: Cook and Woods's *Operating at the Sharp End* (1994), *Behind Human Error* (Woods, Johannesen, Cook, and Sarter, 1994), and *Perspectives on Human Error* (1999), all linked from the site. It sits alongside James Reason's latent-failure and "Swiss cheese" model (1990) and Charles Perrow's *Normal Accidents* (1984), whose "tight coupling" is what thesis 15 warns remedies will add. Sidney Dekker's *Field Guide to Understanding Human Error* and Erik Hollnagel's Safety-II (the study of why things go right, which is thesis 17 as a discipline) are the main later developments.

Software operations adopted the paper around 2012, when John Allspaw's blameless-postmortem writing at Etsy and Cook's own Velocity talk brought it to web engineers. Cook, Allspaw, and Woods went on to found Adaptive Capacity Labs to bring these methods to software incident analysis. Cook died in 2022.

## Sources

- Cook, R. I. (1998, rev. 2000). "How Complex Systems Fail." Cognitive Technologies Laboratory, University of Chicago. <https://how.complexsystems.fail/> — [[2026-10-20-how-complex-systems-fail|local copy]]

Companion papers hosted on the same site: [A Tale of Two Stories](https://how.complexsystems.fail/citations/TaleOfTwoStories.pdf) (Cook, Woods, Miller, 1998), [Operating at the Sharp End](https://how.complexsystems.fail/citations/operatingatthesharp.pdf) (Cook and Woods, 1994), [Perspectives on Human Error](https://how.complexsystems.fail/citations/Perspectives_on_Human_Error.pdf) (Woods and Cook, 1999), [Behind Human Error](https://how.complexsystems.fail/citations/SOAR-BHE-original.pdf) (Woods, Johannesen, Cook, Sarter, 1994).
