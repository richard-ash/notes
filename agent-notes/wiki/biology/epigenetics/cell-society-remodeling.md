---
source: agent
compiled_from:
  - agent-notes/raw/biology/epigenetics/2026-08-14-aging-as-a-program-cao.md
compiled_at: 2026-08-18
model: claude-opus-5
confidence: medium
---

# Cell Society Remodeling

Junyue Cao (Rockefeller, Laboratory of Single-Cell Genomics and Population Dynamics) argues that mammalian aging is not the linear accumulation of molecular damage but a **staged redistribution of the body's cell populations** — "a remodeling of the cell society." His lab built a whole-organism single-cell atlas across the mouse lifespan and found that aging proceeds in discrete time windows, each defined by the coordinated collapse or expansion of *specific* cell types, with the rest of the body's cell inventory left largely untouched.

The framing is a direct challenge to the damage paradigm. Cao's claim: "The destruction of the system is programmed at a very early stage." In humans, the program likely begins before age 30.

## The atlas

Two *Science* papers (2025, 2026) underlie the argument. The experimental design:

| | |
|---|---|
| Cells profiled | ~21 million (a single study within the series: >20 million) |
| Tissues/organs | 14 |
| Animals | ~50 mice, male and female |
| Timepoints | 3, 6, 12, 16, 23 months (≈ human 20, 30, 50, 60, 75) |
| Genes per cell | ~20,000 |
| Cell types resolved | 536 main types, 1,828 subtypes |

The headline statistic is the one Cao found most surprising: **only about a quarter of the 1,828 subtypes shift strongly with age.** The remaining three-quarters are stable across the lifespan. Aging is selective, not universal — which is hard to square with entropy acting on everything at once.

## The four windows

| Mouse age | Human equivalent | What happens |
|---|---|---|
| 3–6 mo | ~20–30 yr | Depletion: certain fat and muscle cells; two immature brain cell types with the capacity to regenerate brain tissue |
| 6–12 mo | 30s–40s | Deep depletion of tissue-maintenance cells — tenocytes (tendon), vascular mural cells, colonic smooth muscle, kidney epithelium; tissue-resident immune cells (e.g. intestinal) also decline |
| ~12 mo | 40s–50s | **Inflection**: depletion gives way to expansion. First expansion wave is immune-dominated, plus stress/inflammation-altered cells in lung, kidney, and elsewhere |
| ~16 mo+ | late 50s+ | Aging-associated immune cell types expand — Cao calls them "selfish, uncontrolled"; plausibly upstream of the age-linked rise in heart disease, arthritis, cancer, and chronic respiratory illness |

The shape matters more than the cell-type list: **the regenerative and maintenance compartments are gutted first, and the inflammatory compartment expands only afterward.** Loss of capacity precedes visible decline by decades. That ordering is what motivates Cao's intervention conclusion (below), and it is what a pure damage model does not naturally predict.

## The evidence for "program" rather than "damage"

Cao offers two arguments:

**1. Chromatin reproducibility.** Using accessibility profiling alongside expression, the lab asked which genomic regions are open (active) and which are closed (silent) in each cell type at each stage. Random molecular damage should produce random changes. Instead they see **~280,000 genomic regions that are reproducibly open or closed at specific stages in specific cell types** — the same regions, animal to animal. This is the strongest empirical claim in the work: determinism at the level of chromatin state.

**2. Abruptness.** The transitions are step changes, not slopes. Cao's analogy is a tree in autumn: leaves fall over roughly two weeks, not gradually across the season, because a daylight cue triggers a signal that reconfigures the system. Abrupt, synchronized change across many organs implies an upstream signal. The lab reports both internal drivers (transcription factors) and external ones (secreted cytokines).

## Human correspondence

Cao points to "abrupt aging" in humans as convergent evidence: blood proteomic signatures shift sharply between the mid-40s and late 50s, people self-report a discontinuous functional decline in middle age, and susceptibility to cancer and neurodegeneration rises in the same window. The mouse inflection at ~12 months maps onto exactly this period. This is correlational alignment between two independent measurement modalities (mouse single-cell transcriptomics, human plasma proteomics), not a demonstration that the same program runs in humans.

## Where this sits among theories of aging

Cao's data are an empirical result; "programmed aging" is the interpretation laid on top. The distinction matters, because the data are compatible with several existing frameworks:

- [[developmental-theory-of-aging]] — de Magalhães argues aging is the developmental software running on past its useful term. Cao's staged windows, each with its own coordinated cell dynamics "akin to those of embryonic development," are close to a direct empirical instantiation of that claim. Cao himself says aging "is more like a developmental process."
- [[somatic-restriction-theory]] — West et al. propose aging as staged developmental repression of regenerative potential. Cao's first two windows — depletion of regenerative brain progenitors, then of tissue-maintenance cells — are precisely the loss of regenerative capacity that theory predicts, now measured cell type by cell type.
- [[information-theory-of-aging]] — Sinclair's ITOA runs the causality the other way: DNA damage relocalizes chromatin modifiers, producing epigenetic noise. Cao's finding of *reproducible* rather than *stochastic* chromatin changes is the sharpest available evidence against noise-first models, though the ICE mouse remains a strong counterweight since induced non-mutagenic breaks alone drive aging phenotypes.
- [[developmental-bioelectricity]] — Levin's account of aging as the blurring of a stored target pattern, with a cybernetic ultimate cause (goal-directed controllers degrade once their goals are met), is a different level of description of a similar intuition: aging as a control system doing what it was built to do, not a machine wearing out.
- [[epigenetic-clocks]] — clock CpGs are enriched at developmental (PRC2) targets, consistent with clocks tracking program progression. Cao's 280,000 stage-specific regions are, in effect, a cell-type-resolved version of the same signal.
- [[neural-stem-cell-aging]] — the stage-1 loss of immature, regeneration-competent brain cell types is the whole-organism-atlas view of a decline that literature has characterized in detail mechanistically.
- [[body-brain-inflammatory-circuit]] — Cao's late-stage inflammatory expansion is the cell-population substrate of inflammaging; the Zuker circuit is the neural controller that reads and rheostats those cytokines. Together they suggest the late phase may be a control loop losing authority, not merely cells misbehaving.
- [[rejuvenation-strategies]] and [[therapeutic-plasma-exchange]] — systemic-factor interventions act on exactly the secreted-cytokine layer Cao identifies as a driver.

## Critical assessment

**What is solid.** The atlas is a large, well-powered descriptive result, and two claims from it are hard to argue with: aging is selective (three-quarters of cell subtypes are stable), and chromatin changes are reproducible across animals rather than random. Both are genuine constraints on any theory of aging.

**Where "program" overreaches.** *Programmed* carries an evolutionary connotation — that aging was selected for — which the data do not establish and which faces the standard group-selection objection: an allele causing an organism's own death is not favored unless kin-selection or lifespan-truncation conditions hold. The observations Cao reports (coordination, abruptness, reproducibility) are equally well explained by a *shared upstream driver* under antagonistic pleiotropy: a developmental program that was selected for its early-life effects and runs on past reproduction. That yields determinism without aging being adaptive. Cao mostly uses "program" in this weaker, mechanistic sense — but the framing invites the stronger reading.

**Reproducible ≠ non-damage.** Genetically near-identical mice on identical diets in identical cages should produce reproducible damage patterns too; the same cell types are load-bearing in every animal. Reproducibility across a highly controlled cohort constrains stochastic-damage models less than it appears to at first. The stronger version of the argument rests on abruptness and on the discovery of actual upstream signals — the cytokines and transcription factors — rather than on reproducibility alone.

**Descriptive, not causal.** The atlas shows *what* changes and *when*, not *why*. Naming the upstream signals and demonstrating that manipulating them moves the stage boundaries is the experiment that would convert this from a strong description into a mechanism. Cao's tree analogy is honest about this: he has observed the leaves falling in two weeks, and inferred a daylight cue.

**Mouse-to-human timelines are interpolated.** The month-to-year mappings (3 mo ≈ 20 yr, and so on) are conventional approximations, and the human claims rest on separate proteomic studies rather than on the same measurement.

## Implications

The most actionable consequence is a timing claim, and it cuts against how longevity intervention is usually staged. If regenerative and maintenance capacity is being depleted from a mouse's third month — a human's twenties — then interventions aimed at the visible symptoms of old age are operating decades downstream of the causal window. Cao: "the regenerative capacity and robustness of the system decrease before middle age. So if we want to rescue aging, we should start early."

Two therapeutic openings follow from the atlas:

1. **Rare vulnerable cell types as targets.** If only ~25% of subtypes shift and specific populations collapse in a known order, interventions can be aimed at preserving or restoring named populations rather than at global damage reduction. This is a fundamentally different target class from senolytics or antioxidants.
2. **Reprogramming the chromatin code.** The 280,000 stage-specific accessible regions are, in principle, an addressable instruction set — a more surgical target than whole-cell [[in-vivo-epigenetic-reprogramming|OSK reprogramming]], and one that could sidestep the identity-erasure and cancer risks of full dedifferentiation.

Both remain proposals. Neither has been demonstrated to extend lifespan.

## Sources

- Wickelgren, I. (2026). "Why Aging May Be a Program, Not a Breakdown." *Quanta Magazine.* <https://www.quantamagazine.org/why-aging-may-be-a-program-not-a-breakdown-20260814/> — [[2026-08-14-aging-as-a-program-cao|local copy]]
- Underlying primary papers (not read for this article): Cao lab, *Science* (2025), <https://www.science.org/doi/10.1126/science.adn3949>; Cao lab, *Science* (2026), <https://www.science.org/doi/10.1126/science.adw6273>
