---
source: agent
compiled_from:
  - agent-notes/raw/biology/epigenetics/2020-12-02-osk-reprogramming-vision.md
  - agent-notes/raw/biology/epigenetics/2019-07-31-osk-reprogramming-vision-preprint.md
  - agent-notes/raw/biology/epigenetics/2020-10-22-yamanaka-factors-dentate-gyrus.md
compiled_at: 2026-04-22
model: claude-opus-4-6
confidence: high
---

# In Vivo Epigenetic Reprogramming

In December 2020, Lu, Sinclair, and colleagues published a landmark *Nature* paper demonstrating that ectopic expression of three Yamanaka factors — Oct4, Sox2, and Klf4 (OSK), excluding the oncogene Myc — can safely reverse aging in a complex tissue *in vivo*. Using the mouse eye as a model CNS tissue, they showed that OSK restores youthful DNA methylation patterns, regenerates damaged axons, reverses vision loss from glaucoma, and rejuvenates aged retinal ganglion cells (RGCs) — all without inducing cancer or erasing cell identity.

This paper provides the strongest experimental evidence for the [[information-theory-of-aging]]: mammalian cells retain a retrievable "backup copy" of their youthful epigenetic state.

## The safety problem with full reprogramming

Yamanaka's four factors (OSKM) can reprogram somatic cells all the way to pluripotency — but continuous expression in vivo causes teratomas or death within days. The key insight from Lu et al. was that MYC is an oncogene not required for the initiation of reprogramming. By expressing only OSK, the authors achieved partial reprogramming: cells rejuvenated their epigenome and transcriptome without losing their differentiated identity or becoming tumorigenic. After 15 months of continuous OSK induction in mouse retinas, no tumors or structural changes were observed.

Rodriguez-Matellán et al. (2020) confirmed the lethality problem from a different angle: continuous induction of all four OSKM factors in the mouse brain killed ~50% of mice within 10 days. Their solution was **cyclic dosing** — 3 days of doxycycline-induced expression followed by 4 days of withdrawal, repeated for 15 weeks. This protocol eliminated the mortality observed with continuous expression while still producing measurable rejuvenation effects in the dentate gyrus.

## Axon regeneration in the optic nerve

The CNS loses regenerative capacity within days after birth. RGCs, which project axons forming the optic nerve, are among the first to lose this capacity. Using AAV2-delivered OSK in an optic-nerve crush-injury model:

- All three factors delivered as a **polycistron** (single AAV particle) were required — single factors or separate monocistronic AAVs had no regenerative effect
- Regenerating axon fibers extended over **5 mm** into the optic chiasm after 12–16 weeks of induction
- OSK doubled RGC survival even in 12-month-old mice
- The effect was **cell-autonomous**: OSK in RGCs (not neighboring amacrine cells) drove regeneration
- Suppressing OSK with doxycycline abolished both regeneration and survival benefits

Critically, OSK worked even when induced *after* injury — the first known treatment to induce robust RGC axon regeneration post-crush.

## The TET1/TET2 requirement

The regenerative effects depend on active DNA demethylation by TET1 and TET2 enzymes:

- OSK upregulates TET1 and TET2 (but not TET3)
- Knockdown of either TET1 or TET2 completely blocked axon regeneration, RGC survival, and Stat3 upregulation
- Knockdown of TDG (thymine DNA glycosylase, required for the active demethylation pathway) also abolished all benefits
- However, global DNA demethylation via TET1 catalytic domain overexpression alone had **no** regenerative effect

This establishes that active, targeted DNA demethylation is *necessary but not sufficient* — OSK must be directing the demethylases to specific loci, implying the existence of positional information about which sites to restore. This is arguably the strongest evidence for the "observer" or backup copy hypothesized by the [[information-theory-of-aging]].

## Reversing glaucoma

In a microbead-induced glaucoma model, after significant RGC loss and axon degeneration had already occurred:

- Four weeks of OSK induction restored axon density to non-glaucomatous levels
- Half of the visual acuity lost to elevated intraocular pressure was recovered (optomotor response)
- PERG (pattern electroretinogram) amplitudes similarly improved

This was the **first demonstration of vision-loss reversal** after glaucomatous injury — prior approaches had focused only on neuroprotection to slow further loss.

## Rejuvenating aged vision

In 12-month-old mice (equivalent to middle-aged humans), four weeks of OSK:

- Restored visual acuity and RGC electrical activity to youthful levels
- Reversed ~90% of the 464 age-altered genes to youthful expression levels, including 44 genes linked to sensory perception and axon targeting
- Reversed a machine-learning-derived DNA methylation aging signature (1,226 CpG sites)
- Achieved rejuvenation without increasing RGC number or axon density — the improvements came from **transcriptomic restoration**

The signature CpG sites were enriched for PRC2 (Polycomb repressive complex 2) binding and H3K27me3 marks — the same chromatin machinery involved in maintaining stem cell plasticity and implicated in [[epigenetic-clocks]].

## Human neuron validation

OSK expression in differentiated human neurons counteracted vincristine-induced axonal degeneration: neurite area was **15-fold greater** in OSK-treated cells nine days after damage, without cell proliferation or global demethylation. The effect required TET2 but not the mTOR–S6K pathway, suggesting the regeneration mechanism is conserved across species and is independent of the well-studied PTEN–mTOR axis.

## Rejuvenating the dentate gyrus and improving memory

While Lu et al. focused on retinal ganglion cells using three-factor OSK, Rodriguez-Matellán et al. (2020) independently demonstrated in vivo reprogramming in the hippocampal dentate gyrus (DG) using all four OSKM factors with cyclic dosing. The DG is one of the few adult brain regions where neurogenesis persists, but adult hippocampal neurogenesis (AHN) declines sharply with age — the DG of 10-month-old mice shows a ~3-fold reduction in proliferating (P-H3+) and newborn (DCX+) neurons compared to 6-month-old mice.

Using doxycycline-inducible OSKM in i4F transgenic mice (6 months old at start, 10 months at endpoint), the cyclic protocol produced several effects:

- **H3K9me3 restoration**: the age-dependent decline in H3K9me3 (a heterochromatin mark) in DG granule cells was significantly reversed — the first demonstration that in vivo reprogramming can restore this specific histone modification in brain neurons
- **Enhanced newborn neuron migration**: DCX+ cells migrated further, resembling the pattern in younger mice, though total DCX+ and calretinin+ cell numbers were unchanged
- **No effect on neurogenesis itself**: early markers (BLBP+) and progenitor counts were unaffected — the YFs acted on maturation and synaptic properties rather than increasing stem cell proliferation
- **Increased GluN2B NMDA receptor subunit**: suggesting enhanced synaptic plasticity in mature neurons
- **Long-term memory improvement**: at 5 days post-familiarization in an object recognition test, wild-type mice had forgotten previously seen objects while YF-expressing mice retained memory (p < 0.05). YF expression levels correlated with memory index (R² = 0.36)

The finding that reprogramming improved memory *without* increasing neurogenesis is notable — it suggests the primary mechanism acts on existing mature neurons rather than by generating new ones. The H3K9me3 increase in the granular layer (where mature neuron cell bodies reside) supports changes in synaptic plasticity as the functional driver. This contrasts with the Lu et al. results in the eye, where improvements also came from transcriptomic restoration rather than new cell generation, but operated through DNA methylation and PRC2/H3K27me3 rather than H3K9me3. The two studies implicate different but complementary epigenetic pathways in age reversal across different CNS tissues.

## The "observer" question

The most profound implication: if OSK-directed TET1/TET2 can restore ~90% of age-altered genes to their correct youthful expression — hitting the right loci, in the right direction, by the right magnitude — then the youthful pattern must be recorded somewhere accessible. Global demethylation doesn't work; targeted demethylation does. Something is encoding *which specific CpG sites* should be methylated or unmethylated in a young cell of that type. Candidates include covalent DNA modifications, DNA-binding proteins, RNA-guided chromatin modifiers, and RNA–DNA hybrids established during development. Finding this positional memory would be transformative for aging biology.

## Temporal notes

This 2020 paper has been heavily cited and become foundational for the longevity field, but the path to human therapy remains long. Sinclair's later work on whole-organism OSK rejuvenation in mice (extending remaining lifespan by 109% in 2-year-old mice) extended these findings beyond the eye. However, Sinclair's 2023 retraction of a related *Nature* paper on ICE mice raised questions about some experimental specifics — though the retraction concerned a different paper (Yang et al. 2023), not this one. The core findings on OSK-mediated vision restoration in this paper have not been challenged.

## Sources

- Lu, Y., Brommer, B., Tian, X., Krishnan, A., Meer, M. et al. (2020). "Reprogramming to recover youthful epigenetic information and restore vision." *Nature* 588, 124–129. <https://doi.org/10.1038/s41586-020-2975-4> — [[2020-12-02-osk-reprogramming-vision|local copy]]
- Lu, Y., Krishnan, A., Brommer, B., Tian, X., Meer, M. et al. (2019). "Reversal of ageing- and injury-induced vision loss by Tet-dependent epigenetic reprogramming." *bioRxiv* preprint. <https://doi.org/10.1101/710210> — [[2019-07-31-osk-reprogramming-vision-preprint|local copy]]
- Rodriguez-Matellán, A., Alcazar, N., Hernández, F., Serrano, M., and Ávila, J. (2020). "In Vivo Reprogramming Ameliorates Aging Features in Dentate Gyrus Cells and Improves Memory in Mice." *Stem Cell Reports* 15, 1–11. <https://doi.org/10.1016/j.stemcr.2020.09.010> — [[2020-10-22-yamanaka-factors-dentate-gyrus|local copy]]
