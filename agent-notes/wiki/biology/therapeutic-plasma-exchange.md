---
source: agent
compiled_from:
  - agent-notes/raw/biology/2022-08-24-plasma-dilution-biological-age.md
compiled_at: 2026-04-24
model: claude-opus-4-6
confidence: high
---

# Therapeutic Plasma Exchange and Rejuvenation

Therapeutic plasma exchange (TPE), also known as plasmapheresis, replaces a patient's blood plasma with saline and purified albumin. The blood cells are returned, so the cell profile is unchanged — but circulating proteins (cytokines, autoreactive antibodies, pathogenic factors) are diluted. A 2022 clinical study by the Conboy lab at UC Berkeley (Kim, Kiprov, Luellen et al.) demonstrated that repeated rounds of TPE in human subjects produce stable, longitudinal rejuvenation of both the humoral and cellular blood compartments — without any addition of young blood or young factors.

This finding is a direct human translation of the Conboy group's earlier mouse work showing that plasma dilution alone (not young blood transfusion) is sufficient to reset the age-elevated systemic proteome and restore youthful tissue maintenance. It shifts the mechanistic emphasis away from "young factors that rejuvenate" toward "old factors whose accumulation drives aging" — diluting the latter is enough.

## Study design

Eight subjects underwent multiple rounds of TPE over several months (samples at R0 through R5, where R0 is pre-first-TPE baseline). Six subjects were old (ages 60–77), two were middle-aged (46, 52). Each round removed one plasma volume and replaced it with 5% albumin, followed by infusion of 2 g IVIG (Octagam 10%). Blood was collected immediately before and after each procedure, with serum, plasma, and PBMCs isolated for analysis.

The study was longitudinal — tracking the same individuals across rounds — which is a significant methodological advantage over cross-sectional young-vs-old comparisons, allowing detection of within-person trajectories.

## Key findings

### DNA damage and senescence decrease

Oxidative DNA damage (8-OHdG) in PBMCs was high before TPE and decreased significantly with successive rounds. The p16 senescence marker, assayed by qRT-PCR, was similarly elevated before TPE and reduced by subsequent rounds. Tumor suppressor genes p21 and p53 increased expression after TPE, while the oncogene c-Myc showed no significant change — suggesting TPE may shift the balance toward tumor suppression without activating oncogenic pathways.

### Lymphoid/myeloid rebalancing

Aging causes myeloid skewing in hematopoiesis: lymphoid cells (T cells, B cells, NK cells) decline while myeloid cells (especially inflammatory CD68+ macrophages) accumulate. This drives [[rejuvenation-strategies|inflammaging]] and impairs adaptive immunity.

Repeated TPE reversed this skewing:
- **T cell markers** (CD3, CD4, CD8) increased
- **B cell markers** (CD19, B220) generally induced
- **NK cell marker** (CD94) rebounded from low pre-TPE levels
- **Macrophage markers** (CD11b, CD68) decreased

The lymphoid-to-myeloid ratio showed sharp increases across rounds. Critically, these transitions were longitudinal and gradual — becoming more statistically significant with additional rounds and maintained for at least one month between procedures.

### Systemic proteome rejuvenation

Of 507 proteins profiled by antibody array, 72 were significantly different between young (28–32 years) and old (70–79 years) controls. Heat mapping of these 72 proteins across TPE rounds revealed a progressive shift from "old" to "young" proteomic signature. PCA confirmed that each patient's proteome migrated from the old control cluster toward the young cluster with successive TPE rounds.

GO analysis of the 72 differentially expressed proteins identified enrichment in signal transduction, inflammatory response, ERK/ERK2 cascade regulation, cytokine-mediated signaling, and negative regulation of apoptosis. Nineteen pro-inflammatory proteins (including CCL20, CCL25, MIF, TLR3, TLR4, IL-2RA, IL-16) were gradually downregulated by TPE toward young levels.

### TLR4 as the nodal point

KEGG pathway analysis identified 43 enriched pathways spanning the canonical signaling cascades: JAK-STAT, MAPK, TGF-beta, NF-κB, and Toll-like receptor signaling. Protein-protein interaction (PPI) network analysis via String revealed that **TLR4 was the only protein linked to all age-specific TPE-rejuvenated networks** — making it the nodal point of the rejuvenation interactome.

TLR4 levels were significantly reduced by TPE. Independent validation using gene expression data from 349 individuals (GEO datasets) confirmed that TLR4 expression increases significantly with age (young 20–29 years vs. old 65–75 years, p<0.05). TLR4 participates in inflammatory cytokine production via NF-κB signaling, has pleiotropic activities across tissues, and is elevated in the aged brain where it may contribute to neurodegeneration.

Six additional proteins at the intersection of cancer-associated pathways were identified and restored to younger levels by TPE: TGFBR2, TGF-alpha, FGF21, SMAD4, TGFBR1, and FZD3.

### TDP43 reduction and neurological disease implications

UMAP analysis of the blood proteome showed distinct clustering of individuals with Alzheimer's disease and AD-related diseases (ADRDs) vs. healthy age-matched and younger cohorts. TPE moved the old blood proteome cluster toward the younger cohort.

TDP43 — a protein elevated in ALS, Parkinson's, frontotemporal dementia, and AD — was significantly higher in old vs. young individuals (12,024 vs. 7,732 pg/mL). TPE produced rapid and sustained reduction of circulating TDP43, with levels remaining low for at least one month between rounds. This suggests a potential preventive capacity against age-associated neurological diseases, not just treatment.

### Biological noise as a direct measure of biological age

The study's most novel contribution is defining biological age as the standard deviation (noise) of protein levels, not their mean values. Using Levene's test with Benjamini-Hochberg correction, the authors identified 10 proteins whose biological noise (SD) increases with age and decreases with TPE:

1. TRAIL R1
2. IL-16
3. TIMP-1
4. IL-15R alpha
5. CD27
6. APJ
7. TNFRSF27
8. uPAR
9. CCL25
10. TGFBR2

The mean SD of these 10 proteins plotted against chronological age yielded a **natural linear relationship** (Pearson's R = 0.7269, p < 0.0001). This is a direct measurement of biological age — not a machine learning prediction trained on chronological age, but an experimentally observed linear relationship between proteomic noise and aging.

Striking applications of this biomarker:
- **Mild cognitive impairment (MCI)** increased biological age by ~50 years (average biological age = 130.9 years for MCI patients)
- **Three rounds of TPE** reduced biological age by decades in individuals aged 60–70+, with sharper reductions in older subjects
- The effect was more moderate in middle-aged subjects (46–52 years)

## Implications

### The dilution hypothesis confirmed in humans

The earlier Conboy mouse work established that diluting old plasma factors — without adding anything young — is sufficient for rejuvenation. This clinical study confirms the same principle in humans. The key insight is that aging may be driven more by the *accumulation* of pro-aging circulatory factors than by the *depletion* of pro-youth factors. This reframes the therapeutic target: rather than searching for specific rejuvenating molecules to administer, simply diluting the age-elevated molecular excess may be sufficient.

### Mechanistic clarity via TLR4

The identification of TLR4 as the single nodal point linking all rejuvenated pathways provides mechanistic focus. TLR4 sits at the intersection of innate immunity, inflammation, and multiple tissue-maintenance signaling cascades. Its age-associated elevation may be a key driver of the transition from productive inflammation to chronic [[rejuvenation-strategies|inflammaging]]. This suggests TLR4-targeted therapies (antagonists, modulators) could potentially achieve some of TPE's benefits without the full plasmapheresis procedure.

### Biological noise as an aging biomarker

The 10-protein noise panel offers a potentially transformative measurement tool. Unlike [[epigenetic-clocks|epigenetic clocks]], which are trained on chronological age and predict mortality risk, this approach directly measures a physical quantity (protein level variance) that has a natural linear relationship with age. It requires no machine learning model and is not confounded by the circularity of training on chronological age. However, the sample size is small (N=8 for TPE, N=5 each for young/old controls), and independent validation is needed.

### Connection to cancer

The downregulation of cancer-pathway proteins and upregulation of tumor suppressors p21/p53 without c-Myc activation suggests TPE may reduce cancer propensity — consistent with the known relationship between [[rejuvenation-strategies|inflammaging]], myeloid skewing, and age-associated malignancies.

## Limitations

- **Small sample size:** 8 TPE subjects (6 old, 2 middle-aged), 5 young controls, 5 old controls
- **No placebo control:** all subjects received TPE; no sham procedure comparison
- **IVIG co-administration:** each TPE round included 2 g IVIG infusion, making it impossible to fully separate TPE effects from IVIG immunomodulatory effects
- **Short follow-up:** effects tracked over months (up to R5), not years; long-term durability and safety unknown
- **Biological noise panel:** the 10-protein biomarker was discovered and validated in the same dataset; independent replication in a larger cohort is essential
- **Levene's test limitations:** the test has possible shortcomings with small sample sizes and asymmetric distributions; the authors added Benjamini-Hochberg correction and required significance in multiple comparisons to address this

## Connections

- [[rejuvenation-strategies]] reviews the four major rejuvenation strategy classes; TPE is the clinical translation of the "blood factors" approach, specifically validating the *dilution* hypothesis over the *young factor supplementation* hypothesis
- [[neural-stem-cell-aging]] covers intrinsic and extrinsic drivers of neural stem cell decline; TPE's reduction of circulating TDP43 and neuroinflammatory markers connects to the extrinsic (blood-borne) drivers of neurogenic niche deterioration
- [[epigenetic-clocks]] provide alternative measures of biological age; the 10-protein noise panel described here takes a fundamentally different approach — measuring protein variance rather than DNA methylation — and claims to avoid the circularity of ML-trained clocks
- [[information-theory-of-aging]] posits aging as epigenetic information loss; TPE's ability to reverse biological age by diluting systemic factors suggests that at least some aging "information loss" may be driven by circulatory signals rather than cell-autonomous epigenetic drift

## Sources

- Kim, D., Kiprov, D.D., Luellen, C. et al. (2022). "Old plasma dilution reduces human biological age: a clinical study." *GeroScience*. <https://doi.org/10.1007/s11357-022-00645-w> — [[2022-08-24-plasma-dilution-biological-age|local copy]]
