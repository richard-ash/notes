---
source: agent
compiled_from:
  - agent-notes/raw/health/2026-04-16-nintil-epigenetic-clocks-review.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: high
---

# Epigenetic Clocks

Epigenetic clocks are statistical models — typically elastic net regressions — that predict age, mortality risk, or general health from CpG methylation data. A small set of CpG sites (88 to ~1000, depending on the clock) is sufficient to estimate chronological age within ~3.6 years or to stratify mortality risk with a hazard ratio of 4 between the most and least aged quintiles. They have become a central tool in aging research for evaluating anti-aging interventions without waiting for full survival curves.

## How they work

The underlying method is straightforward: fit an elastic net (mixed L1/L2 penalized linear regression) on CpG methylation values to predict an endpoint of interest. The resulting model is $DNAmAge = a + b_1 \cdot CpG_1 + b_2 \cdot CpG_2 + \ldots$ Ricon notes that the simplicity of elastic nets is a feature — fewer hyperparameters mean it is hard to fudge results and hard to overfit. Even deep neural networks applied to the same data (Levy et al., 2020) improve only marginally over the linear models, suggesting CpG–CpG interactions are limited.

Only CpG methylation is used in practice because it is the most accessible epigenetic mark. Non-CpG methylation is rare (initially thought not to exist), though it may be relevant in tissues like the brain.

## The epigenome and aging

70–80% of CpGs are methylated in mammalian tissue, but at the level of CpG islands (clusters), only 6–8% are methylated in any given tissue. Once a cell is fully differentiated, CpG methylation patterns are largely fixed — the cell loses the capacity for de novo methylation and its maintenance methylation degrades over time.

With age, a characteristic bidirectional drift emerges: methylated islands lose their marks, while extraneous methylation appears at sites that should be unmethylated. This pattern persists even when young cells are transplanted into old bodies (and vice versa), suggesting it is an intrinsic cellular property rather than a response to the tissue environment.

## Generations of clocks

### First generation — predicting chronological age

| Clock | Year | CpGs | Key features |
|-------|------|------|-------------|
| Bocklandt et al. | 2011 | 88 | First epigenetic clock; r = 0.85 with chronological age |
| Hannum | 2013 | 71 | Blood-based; included BMI, gender, diabetes as covariates |
| Horvath (pan-tissue) | 2013 | 353 | Multi-tissue; methylation-only with logarithmic age transform; ~3.6 year average error |

### Second generation — predicting morbidity and mortality

| Clock | Year | CpGs | Key features |
|-------|------|------|-------------|
| PhenoAge (Levine et al.) | 2018 | 513 | Trained on 10-year mortality risk via phenotypic covariates (albumin, creatinine, CRP, etc.) |
| GrimAge (Lu et al.) | 2019 | 1030 | Trained on time-to-death via intermediate surrogates (smoking pack-years, plasma protein levels); best mortality predictor |

The critical methodological difference: first-generation clocks were trained on **cross-sectional** data (people of different ages sampled once), while second-generation clocks incorporate **longitudinal** data (same individuals tracked over time). This matters because a CpG strongly correlated with early death would be underrepresented in old-age cross-sections — the people carrying that mark are already dead.

Both generations derive "age acceleration" metrics (e.g., AgeAccelGrim) by regressing epigenetic age on chronological age and taking residuals. These acceleration scores are what predict health outcomes. GrimAge's AgeAccelGrim achieves a hazard ratio of ~4 between the top 95th and bottom 5th percentile — by comparison, smoking 10 cigarettes/day has an HR of only 1.9 relative to nonsmokers.

## The causality question

Do aged epigenomes *cause* aging, or merely reflect it? Ricon identifies three competing views:

1. **Epigenetic noise** (Sinclair's camp, via the [[information-theory-of-aging]]): aging is progressive degradation of epigenetic information. Damage triggers sirtuin relocalization, introducing noise. The fact that aged CpG patterns converge across individuals — methylated sites lose marks, unmethylated sites gain them, trending toward a "mushy dysregulated homogeneity" — is consistent with directional noise rather than random gaussian noise.

2. **Programmed aging**: the clock patterns begin ticking from the embryonic stem cell stage, well before significant damage accumulates, which some argue implies a developmental program rather than a damage response. Ricon notes this explanation is hard to justify on evolutionary grounds (group selection required).

3. **Stem cell differentiation** (Raj and Horvath, 2020): each asymmetric stem cell division — where one daughter differentiates into a transit-amplifying cell — changes the tissue's methylation profile slightly. This is consistent with the observation that isolated stem cells are epigenetically younger than their surrounding tissue, and that the clock ticks very slowly (~3.2% of cells per interval). However, this model doesn't explain why damage to non-stem cells also advances the clocks.

Ricon argues these are likely not mutually exclusive — multiple mechanisms contribute, with stem cell differentiation as a baseline and damage/noise as an accelerator.

### Experimental evidence for causality

- **ICE mice** (Sinclair lab): engineered mice expressing inducible DNA double-strand breaks showed 50% epigenetic age acceleration plus phenotypic aging (fur loss, muscle weakness, arthritis, vision loss) — without direct epigenetic manipulation, but consistent with the RCM → epigenetic noise pathway described in the [[information-theory-of-aging]].
- **Epigenetic reprogramming**: transient OSK factor expression in progeroid mice increased maximum and median lifespan by 20% and 33% respectively, and this showed up as rejuvenation in the clocks. Crucially, knocking out TET1/TET2 (demethylation enzymes) greatly reduced the effect, suggesting the rejuvenation is mediated through epigenetic changes specifically.
- **Embryonic stem cells** do not epigenetically age even after hundreds of passages — consistent with the clocks measuring differentiation-related changes rather than replication count.
- **Telomerase immortalization** does not prevent epigenetic aging, and **faster replication** does not accelerate it.

## Validation: do known longevity interventions show up?

This is the key practical question. If the clocks are real biomarkers of aging, interventions known to extend lifespan should register.

**Caloric restriction (CR):** consistently shows effects across multiple studies — 5 months younger (Thompson et al., 2018), 9.4 months younger (Wang et al., 2017), 20% reduction (Petkovich et al., 2017). The most reliable signal.

**Rapamycin:** initially appeared negative (Thompson et al., 2018 — only 4 mice per group), but later studies found 6-month epigenetic age reductions (Wang et al., 2017). Rapamycin also reduces epigenetic age in human cells in vitro. The effect appears smaller than CR, which Ricon notes may suggest CR mimetics are not as potent as CR itself.

**Dwarf mice (Ames/Snell):** Ames dwarfs, which achieve 65% maximum lifespan extension, show up as epigenetically younger in most studies. Petkovich et al. found 50% younger epigenetic ages. Results vary by tissue and sequencing method, partly because Ames dwarf data was often obtained via WGBS rather than the RRBS used to train the clocks.

The verdict: yes, the clocks track known interventions, though with meaningful variance depending on clock type, tissue, and sequencing method. Second-generation clocks trained on mortality endpoints are the right tool for evaluating lifespan interventions; first-generation age-predicting clocks are less informative.

## Open problems

The field faces significant unresolved challenges. Single-cell epigenetic sequencing is needed to determine whether age-related methylation drift occurs uniformly or in a subset of cells. Current microarrays (Illumina MethylationEPIC) assess only ~850k sites — 3% of total CpGs. Clock reproducibility in model organisms is limited by reliance on low-depth sequencing. And the fundamental question of whether the aged epigenome is a therapeutic target — not just a biomarker — awaits direct experimental manipulation. Publication bias has been documented for first-generation clock mortality predictions, reinforcing the preference for GrimAge and PhenoAge in outcome studies.

## Temporal notes

This review was written in 2020 (last updated 2022). Since then, GrimAge version 2 and third-generation clocks (e.g., DunedinPACE, which measures rate of aging rather than biological age) have been published. Horvath's pan-mammalian clock was released in 2022 across ~60 species. The field has also moved toward causal inference methods (Mendelian randomization studies on epigenetic age acceleration) and commercial direct-to-consumer epigenetic age testing.

## Connections

- The [[information-theory-of-aging]] provides the theoretical framework for the "epigenetic noise" interpretation of what the clocks measure — Sinclair's ICE mice and OSK reprogramming experiments are key evidence discussed in both contexts.
- [[senolytic-car-t-cells]] target a downstream consequence of aging (senescent cell accumulation) that epigenetic clocks can quantify — the two approaches are complementary as measurement and intervention.
- [[cellular-memory]] explores how cells encode and retrieve information at scales beyond the epigenome; the "observer problem" in the ITOA — where is the youthful backup copy stored? — connects the biology of aging clocks to broader questions about cellular information storage.
- The [[developmental-theory-of-aging]] interprets epigenetic clocks as reflecting the running of the developmental software program — the clocks tick because they track ontogenetic progression, not damage accumulation. The enrichment of developmental genes (PRC2 targets) at clock CpG sites supports this reading.
- [[in-vivo-epigenetic-reprogramming]] demonstrated that OSK factors reverse a machine-learning-derived DNA methylation aging signature (1,226 CpGs) in retinal ganglion cells, and that the signature sites are enriched for PRC2 binding and H3K27me3 — connecting clock biology to the functional reversal of age-related decline.

## Sources

- Ricon, J. L. (2020). "Epigenetic clocks: A review." *Nintil*. <https://nintil.com/epigenetic-clocks/> — [[2026-04-16-nintil-epigenetic-clocks-review|local copy]]
