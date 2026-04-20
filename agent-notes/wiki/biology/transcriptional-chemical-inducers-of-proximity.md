---
source: agent
compiled_from:
  - agent-notes/raw/biology/2023-07-26-rewiring-cancer-drivers-tcips.md
compiled_at: 2026-04-20
model: claude-opus-4-6
confidence: high
---

# Transcriptional Chemical Inducers of Proximity (TCIPs)

Chemical inducers of proximity (CIPs) are bivalent small molecules that force two proteins into close contact, exploiting the physical principle that effective collisions between molecules scale inversely with the cube of distance. CIPs have been used to recapitulate steps in signal transduction, protein localization, and transcription. The most commercially successful CIP derivatives are **PROTACs** (proteolysis-targeting chimeras), which recruit target proteins to the proteasome for degradation.

Gourisankar, Crabtree, Gray et al. (2023) introduced a new subclass — **transcriptional/epigenetic CIPs (TCIPs)** — that instead of degrading a protein, **rewire an endogenous cancer driver to activate cell death genes**. The approach is conceptually analogous to rewiring a circuit board: rather than removing a component, you reroute its output.

## The TCIP concept

A TCIP is a bivalent molecule with two binding moieties joined by a chemical linker:

1. **One side** binds a transcriptional or epigenetic regulator (e.g., a cancer-driving transcription factor or a bromodomain protein like BRD4).
2. **The other side** binds to a transcription factor that sits on the promoters of therapeutic target genes (e.g., pro-apoptotic genes).

By bringing a transcriptional activator into proximity with silenced therapeutic gene promoters, the TCIP converts epigenetic repression into transcriptional activation — a **gain-of-function** mechanism. This is fundamentally different from conventional approaches (inhibition, degradation, RNAi, CRISPR), all of which require near-complete removal of the target protein and often produce mechanism-based toxicity because the cancer driver is also essential in normal cells.

## TCIP1: proof of concept in DLBCL

The first TCIP, **TCIP1**, targets diffuse large B-cell lymphoma (DLBCL), where the transcription factor **BCL6** is constitutively deregulated. BCL6 binds to the promoters of pro-apoptotic genes (including *TP53*, *BIM/BCL2L11*, *PMAIP1*, *FOXO3*) and epigenetically silences them by recruiting corepressors NCOR, BCOR, and SMRT. This silencing is a key survival mechanism for DLBCL cells.

TCIP1 covalently links:
- **BI3812** — a small molecule that binds the BCL6 BTB domain, displacing corepressors
- **JQ1** — a BET bromodomain inhibitor that binds BRD4 (a transcriptional activator involved in MYC-driven oncogenic programs)

The result: BRD4 is recruited to BCL6-occupied promoters, converting repressed pro-apoptotic genes into actively transcribed ones.

### Key results

| Metric | Result |
|--------|--------|
| EC50 in KARPAS422 (chemo-resistant, TP53-mutant DLBCL) | **1.3 nM** |
| EC50 across 4 high-BCL6 DLBCL lines | **1–10 nM** |
| Time to apoptosis onset | **4–8 hours** |
| BRD4 redistribution at BCL6 sites | **Within 15 minutes** |
| BRD4 increase at BCL6 binding sites | ~1.5-fold |
| BRD4 decrease at enhancers | ~10% |
| Potency vs. JQ1 + BI3812 combined | **100–1,000x more potent** |
| Cell-cycle dependence | **None** (kills throughout cycle) |

### Mechanism of action

1. **Ternary complex formation**: TCIP1 induces a cooperative BRD4–TCIP1–BCL6 ternary complex (Kd ~340 nM by isothermal calorimetry). The cooperativity is critical — negative controls that bind only one side are 100-fold less effective even in combination.

2. **Transcriptional activation of pro-apoptotic genes**: Within 1–2 hours, ~140 genes are upregulated, including classical BCL6-repressed apoptotic regulators (*BCL2L11/BIM*, *PMAIP1*, *FOXO3*, *BCL6* itself). BRD4 density at BCL6 summit sites increases within 15 minutes, with Pol II Ser2 phosphorylation (productive elongation marker) following shortly after.

3. **MYC repression**: MYC and its target genes are downregulated starting at sub-nanomolar TCIP1 concentrations within 2 hours — earlier and at lower doses than JQ1 alone (which requires ~500 nM). The authors hypothesize this is a gain-of-function consequence: by relocating BRD4 from MYC-driving enhancers/super-enhancers to BCL6 sites, TCIP1 simultaneously deprives MYC of its transcriptional fuel.

4. **BCL6 autoregulatory circuit rewiring**: BCL6 normally autorepresses its own expression via binding sites in its first intron. TCIP1 converts this negative feedback loop into a positive one — BCL6 protein levels increase dose-dependently, amplifying the pro-apoptotic signal.

### Selectivity and safety

- **BCL6-dependent**: EC50 anti-correlates with BCL6 expression across 14 cell lines. Cells with no detectable BCL6 (e.g., OCILY19) show no response.
- **TP53-independent**: Killing does not require functional p53, making TCIPs effective against chemo-resistant lines.
- **No toxicity in mice**: 10 mg/kg IP daily for 5 days produced no adverse effects, no behavioral abnormalities, and no significant gene expression changes in liver, lung, or spleen.
- **No effect on primary human cells**: Normal tonsillar lymphocytes and fibroblasts were unaffected at therapeutic concentrations.
- **~250-fold tissue specificity advantage** over conventional BCL6 inhibitors or degraders.

## Generalization: TCIP2 and beyond

To test whether the TCIP concept generalizes beyond BRD4, the authors designed **TCIP2**, which borrows the transcriptional activity of the estrogen receptor (ER) rather than BRD4 to activate BCL6 target genes. TCIP2 showed antineoplastic activity (EC50 ~355 nM) and was non-toxic in cells lacking BCL6, demonstrating that diverse transcriptional activators can be "hijacked" to drive pro-apoptotic transcription.

This modularity suggests a broad design space: any combination of (cancer driver binding site) + (linker) + (therapeutic gene promoter binder) could yield a TCIP tailored to a specific cancer genotype.

## Why this matters beyond cancer

The TCIP paradigm has implications beyond oncology:

- **Regenerative medicine**: TCIPs could activate expression of genes needed for tissue repair or regeneration by rewiring available transcription factors to silent developmental gene promoters.
- **Developmental disorders**: Diseases caused by insufficient expression of specific genes could potentially be treated by recruiting endogenous transcriptional machinery to the affected loci.
- **Combinatorial specificity**: Because TCIPs depend on the co-presence of two specific proteins at the same genomic loci, they inherit the combinatorial specificity of transcription itself — a selectivity advantage that single-target drugs cannot achieve.

## Relationship to other approaches

| Approach | Mechanism | Limitation TCIPs address |
|----------|-----------|--------------------------|
| Small-molecule inhibitors | Block protein function | Require near-complete target occupancy; mechanism-based toxicity |
| PROTACs | Degrade target protein | Remove essential proteins entirely; off-tissue effects |
| RNAi / CRISPR | Eliminate target mRNA/gene | Permanent or semi-permanent; delivery challenges |
| **TCIPs** | **Rewire target to activate therapeutic genes** | **Gain-of-function; substoichiometric; reversible; tissue-selective** |

The key conceptual shift: conventional approaches treat the cancer driver as something to remove. TCIPs treat it as an asset to redirect — the cancer cell's own oncogenic machinery becomes the engine of its destruction.

## Connection to the [[warburg-effect|Warburg Effect]]

The Warburg Effect article documents how cancer cells co-opt normal metabolic machinery (lactate production/shuttling) for pathological purposes. TCIPs exploit a parallel insight at the transcriptional level: cancer cells co-opt transcriptional regulators like BRD4 and BCL6 for survival, and that same co-option creates a vulnerability that can be turned against the cell. Both observations reflect the broader principle that cancer's dependencies are also its attack surfaces.

## Sources

- Gourisankar, S. et al. (2023). "Rewiring cancer drivers to activate apoptosis." *Nature* 620, 417–425. <https://doi.org/10.1038/s41586-023-06348-2> — [[2023-07-26-rewiring-cancer-drivers-tcips|local copy]]
