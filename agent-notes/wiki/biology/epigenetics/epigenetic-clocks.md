---
source: agent
compiled_from:
  - agent-notes/raw/health/2026-04-16-nintil-epigenetic-clocks-review.md
  - agent-notes/raw/biology/epigenetics/2022-06-01-epiage-hallmarks-of-aging.md
  - agent-notes/raw/biology/epigenetics/2026-06-15-horvath-slowing-biological-aging.md
compiled_at: 2026-06-15
model: claude-opus-4-8
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

### Clock selection for in vitro work

Not all clocks perform equally in cultured primary human cells. Kabacik et al. (2022) systematically compared four clocks — Skin&Blood, Horvath, Hannum, and PhenoAge — on keratinocytes and fibroblasts through multiple experimental conditions. The Skin&Blood clock (DNAmAge) produced the most consistent and interpretable results, while the Hannum and PhenoAge clocks exhibited paradoxical or erratic behavior in vitro. This is a critical practical point: studies evaluating anti-aging compounds in cell culture should prefer the Skin&Blood clock over general-purpose alternatives.

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

### Clock initiation at differentiation

Kabacik et al. (2022) provided direct evidence that the epigenetic clock begins ticking when embryonic stem cells lose pluripotency. Human ESCs differentiated into endothelial cells showed no EpiAge increase while pluripotent, but began accumulating epigenetic age upon differentiation. The same pattern held for ESCs differentiated into neural progenitors and for iPSCs differentiated into lung epithelial basal cells (via anterior foregut endoderm and lung progenitor stages) — EpiAge correlated with loss of OCT4 and gain of TP63. This finding strengthens the stem cell differentiation model and is consistent with the [[developmental-theory-of-aging]]'s interpretation of clocks as tracking ontogenetic progression.

## Epigenetic clocks and the hallmarks of aging

Kabacik et al. (2022) systematically tested each classical hallmark of aging against the Skin&Blood epigenetic clock in primary human cells, producing the most comprehensive mapping to date:

| Hallmark | Affects EpiAge? | Key evidence |
|----------|----------------|-------------|
| Cellular senescence | **No** | Replicative, Ras-induced, and X-ray-induced senescent cells showed EpiAge increase, but hTERT cells that bypassed senescence continued accumulating EpiAge at the same rate — senescence itself is not the driver |
| Telomere attrition | **No** | hTERT-expressing fibroblasts maintained telomere length indefinitely yet continued epigenetic aging unabated |
| Genomic instability | **No** | Acute (20 Gy), chronic low-dose (1 mGy/h), and pulsed radiation across HDKs, HDFs, and MEFs produced no significant EpiAge change despite causing DNA damage |
| Deregulated nutrient sensing | **Yes** | Rapamycin (mTOR inhibitor) retarded epigenetic aging in neonatal HDKs and hTERT-immortalized HUVECs |
| Mitochondrial dysfunction | **Yes** | CCCP (mitochondrial uncoupler) highly accelerated EpiAge; bezafibrate (mitochondrial biogenesis enhancer) slowed it |
| Stem cell exhaustion | **Yes** | Stem cell-enriched epidermal fractions (ITGA6+, COL17A1+, p63+) were epigenetically younger than stem cell-depleted fractions; tissue EpiAge is a composite of its constituent cell populations |
| Altered intercellular communication | Not tested in this study (but mouse parabiosis experiments show young plasma rejuvenates EpiAge) |
| Loss of proteostasis | Not tested |

The critical implication: three hallmarks are mechanistically upstream of epigenetic aging (nutrient sensing, mitochondria, stem cell composition), while three others — long considered central to aging — are dissociable from the clocks. This argues against a unified "damage accumulation" model and supports a view where epigenetic aging reflects metabolic and differentiation state rather than genomic integrity.

### Lifespan extension ≠ epigenetic age reduction

A striking finding from Kabacik et al.: several compounds that extend cellular lifespan do not affect epigenetic aging. NAD, nicotinamide riboside (NR), metformin, and Y-27632 all increased proliferative capacity of primary human cells but produced no measurable change in EpiAge. Only rapamycin and bezafibrate both extended lifespan *and* slowed epigenetic aging. This dissociation implies the clocks capture a specific subset of aging biology — not a universal aging readout.

## Validation: do known longevity interventions show up?

This is the key practical question. If the clocks are real biomarkers of aging, interventions known to extend lifespan should register.

**Caloric restriction (CR):** consistently shows effects across multiple studies — 5 months younger (Thompson et al., 2018), 9.4 months younger (Wang et al., 2017), 20% reduction (Petkovich et al., 2017). The most reliable signal.

**Rapamycin:** initially appeared negative (Thompson et al., 2018 — only 4 mice per group), but later studies found 6-month epigenetic age reductions (Wang et al., 2017). Rapamycin also reduces epigenetic age in human cells in vitro. The effect appears smaller than CR, which Ricon notes may suggest CR mimetics are not as potent as CR itself. Kabacik et al. (2022) confirmed rapamycin's effect in primary human keratinocytes and hTERT-immortalized endothelial cells, and showed the effect persists even when applied at late cellular ages — connecting it specifically to the deregulated nutrient sensing hallmark via mTOR inhibition.

**Dwarf mice (Ames/Snell):** Ames dwarfs, which achieve 65% maximum lifespan extension, show up as epigenetically younger in most studies. Petkovich et al. found 50% younger epigenetic ages. Results vary by tissue and sequencing method, partly because Ames dwarf data was often obtained via WGBS rather than the RRBS used to train the clocks.

The verdict: yes, the clocks track known interventions, though with meaningful variance depending on clock type, tissue, and sequencing method. Second-generation clocks trained on mortality endpoints are the right tool for evaluating lifespan interventions; first-generation age-predicting clocks are less informative.

## The intervention landscape (Horvath, 2026)

In a 2026 FoundMyFitness interview, Horvath gave a practitioner's-eye update on what the clocks now show across human interventions. Two framing claims anchor everything below:

1. **Prevention, not reversal.** Interventions reliably move the clocks in people whose epigenetic age is already *accelerated* (obese, inflamed, deficient) and barely move them in already-healthy people. The lever is removing accelerants, not magical rejuvenation. Horvath is openly skeptical of "reversed my age 5 years in 7 months" biohacker claims unless the person started with a high BMI and a GrimAge ~8 years above expected. This is the human-population counterpart to the in-vitro dissociation already documented above (lifespan extension ≠ epigenetic age reduction).
2. **Different clocks have different sensitivities, by training.** Which clock detects an intervention is largely a function of what it was trained on — so the field now reports ~5 clocks per intervention paper and lets the reader judge. DunedinPACE was trained on BMI change and so reliably catches weight loss; GrimAge was trained on mortality and so catches inflammation/smoking-like exposures. Clocks correlate only ~0.5 after regressing out age and sex.

### Clock-by-intervention sensitivity

The recurring methodological lesson is that a "negative" result usually means *wrong clock for that biology* or *underpowered*, not "no effect":

| Intervention | Which clock caught it | Notes |
|---|---|---|
| GLP-1 (semaglutide), obese, 33 wk | **All** clocks | Strong weight loss → reduced lipolysis/inflammation; bioRxiv preprint (Kley/Conley, San Diego) |
| Caloric restriction (CALERIE, 2 yr, 25%) | **DunedinPACE only** (~2–3% slowing) | GrimAge/PhenoAge missed it — poor adherence + DunedinPACE trained on BMI |
| Multivitamin (COSMOS substudy, ~2 yr) | **GrimAge, PhenoAge** (~2.7–5 mo) | DunedinPACE right direction, not significant; brain aging slowed 2.1 yr, episodic memory ~5 yr; hard endpoints (mortality/CVD) null |
| Omega-3 (DO-HEALTH, ≥71 yr) | **GrimAge2, PhenoAge, DunedinPACE** | Most credible supplement result; combined D+omega-3+exercise best by PhenoAge (3.8 mo / 3 yr), dose-dependent |
| Intense cycling (4.5 h/wk, 6 mo, VO2max +20%) | **PC-GrimAge** (7-mo reduction) | Dwarfs other interventions; no control arm; "Vanam" first author |
| Step-count exercise | weak (r ≈ −0.1) | Needs ~3,000 people to detect; muscle methylation clocks unconvincing |

The cycling-vs-step-count contrast points to a **threshold/intensity effect**: ordinary activity (10,000 steps) barely registers, but pushing VO2max produces the single largest clock movement in the supplement/lifestyle category.

### Effect sizes are tiny but compound

Supplement/lifestyle effects are months, not years (a multivitamin ~3 months per 2 years). Horvath's argument for taking them anyway is compounding: 3 months/2 yr sustained from 50 to 80 could accumulate to ~2.5 years, for the effort of swallowing a pill. Medical interventions are stronger than supplements — HIV anti-retroviral therapy reverses the ~5–7 yr HIV-induced acceleration by ~4–5 yr within weeks; anti-TNF-α therapy in autoimmune disease is strong; metformin is real but weak (consistent with the Kabacik in-vitro finding above that metformin extends cellular lifespan *without* moving EpiAge).

### The surprising winners and losers

- **Vegetables dwarf exercise.** Blood carotenoid level (an objective fruit/veg proxy, unlike unreliable food questionnaires) correlates with GrimAge at ~ **−0.3** in the Women's Health Initiative — comparable in magnitude to smoking (+0.4) and roughly 3× the exercise correlation (−0.1). Mechanism unknown (carotenoids? fiber? lutein/zeaxanthin?). Red meat shows only a negligible acceleration; no evidence meat-eaters age faster than vegans (vegan trials confounded by weight loss).
- **Social connection** was Horvath's biggest recent surprise: in Kubzansky's (Harvard) "social cumulative advantage" study the GrimAge readout *dwarfed* the cortisol and inflammatory readouts, which didn't work at all — despite social connection being mechanistically "far removed" from DNA in blood. Loneliness is a mortality risk at the level of smoking.
- **Short-term psychological stress** does *not* register on the clocks; only severe chronic stress (childhood abuse, PTSD) does — a hopeful asymmetry.
- **Vitamin D** moves the clock only in deficient people (BASE-II Berlin, 7 yr): the lesson is "correct deficiency," not "supplement = anti-aging." Trials that fail to measure baseline status are uninterpretable.
- **Lower core body temperature**: pre-optic-neuron stimulation lowered mouse body temp ~3°C and slowed methylation-clock aging across organs (Veratin, Harvard); hibernating marmots' clocks don't advance — connecting to the "slow metabolism, slow damage" intuition.

### GrimAge is a hazard ratio, not a death date

A persistent consumer misconception Horvath flags: GrimAge cannot predict *when* you die (±~6 yr error) and a younger GrimAge does **not** translate into that many extra years of life. Mathematically GrimAge is an instantaneous hazard ratio — your annual mortality risk vs a same-age, same-sex peer. A GrimAge 8 years above chronological means >2× the annual death risk. Reporting a literal death age would be both unethical and unsound.

### Consumer testing

The honest case for paying several hundred dollars: not new knowledge ("you already know to stop smoking, exercise, eat vegetables") but **adherence** — longevity doctors report measurement is the #1 driver of patients sticking to regimens. Practical guidance: use a lab experienced with the Illumina array (standardized; the five standard clocks + DunedinPACE all run on it, enabling comparison to ~10 years of legacy data), expect ~100 readouts including protein surrogates and now organ-specific ages (kidney/lung/heart), run multiple clocks (GrimAge + DunedinPACE, like ordering multiple labs), and note PC-GrimAge test-retest noise is ~2–5 months. A $50 test is technologically possible but would use a less-characterized clock without legacy data.

### What the clocks still miss

Reinforcing the hallmarks dissociation above, Horvath stresses the clocks are *integrators* of many stressors but blind to several: senescent cells / senolytics, telomere biology, and double-strand-break / radiation damage are all poorly captured. He frames partial reprogramming (Yamanaka factors, [[in-vivo-epigenetic-reprogramming]]) as resetting many hallmarks but *not* somatic mutations or telomere length — and argues that even perfectly stopping somatic mutation would not stop aging, because damage accrues at every level (epigenome, transcriptome, proteome). On genetics: SNP/polygenic associations (even APOE4) are minute and "dwarfed by walking your 10,000 steps"; methylation is an order of magnitude more informative than SNPs.

## Open problems

The field faces significant unresolved challenges. Single-cell epigenetic sequencing is needed to determine whether age-related methylation drift occurs uniformly or in a subset of cells. Current microarrays (Illumina MethylationEPIC) assess only ~850k sites — 3% of total CpGs. Clock reproducibility in model organisms is limited by reliance on low-depth sequencing. And the fundamental question of whether the aged epigenome is a therapeutic target — not just a biomarker — awaits direct experimental manipulation. Publication bias has been documented for first-generation clock mortality predictions, reinforcing the preference for GrimAge and PhenoAge in outcome studies.

## Temporal notes

This review was written in 2020 (last updated 2022). Since then, GrimAge version 2 and third-generation clocks (e.g., DunedinPACE, which measures rate of aging rather than biological age) have been published — and by Horvath's 2026 account these are now the standard repertoire: papers routinely report ~5 clocks (PhenoAge, GrimAge/GrimAge2, DunedinPACE, plus others), and principal-component versions (PC-GrimAge) are preferred for their test-retest reproducibility. Horvath's pan-mammalian clock was released in 2022 across ~60 species. The field has also moved toward causal inference methods (Mendelian randomization studies on epigenetic age acceleration), commercial direct-to-consumer epigenetic age testing (now including organ-specific methylation ages), and LLM-built clocks (e.g., "GrimAge v3," "systems age," "OmicM/H") that as of 2026 await community validation — though GrimAge (2019) remains the best mortality predictor. Surrogate-endpoint validation is now funded through the Biomarker of Aging Consortium and ARPA-H.

## Connections

- The [[information-theory-of-aging]] provides the theoretical framework for the "epigenetic noise" interpretation of what the clocks measure — Sinclair's ICE mice and OSK reprogramming experiments are key evidence discussed in both contexts.
- [[senolytic-car-t-cells]] target a downstream consequence of aging (senescent cell accumulation) that epigenetic clocks can quantify — the two approaches are complementary as measurement and intervention.
- [[cellular-memory]] explores how cells encode and retrieve information at scales beyond the epigenome; the "observer problem" in the ITOA — where is the youthful backup copy stored? — connects the biology of aging clocks to broader questions about cellular information storage.
- The [[developmental-theory-of-aging]] interprets epigenetic clocks as reflecting the running of the developmental software program — the clocks tick because they track ontogenetic progression, not damage accumulation. The enrichment of developmental genes (PRC2 targets) at clock CpG sites supports this reading.
- [[in-vivo-epigenetic-reprogramming]] demonstrated that OSK factors reverse a machine-learning-derived DNA methylation aging signature (1,226 CpGs) in retinal ganglion cells, and that the signature sites are enriched for PRC2 binding and H3K27me3 — connecting clock biology to the functional reversal of age-related decline.
- [[rejuvenation-strategies]] surveys the broader landscape of lifespan-extending interventions (parabiosis, senolytics, rapamycin, reprogramming); the Kabacik hallmarks mapping clarifies which of these act through epigenetic aging pathways and which extend lifespan through independent mechanisms.
- [[neural-stem-cell-aging]] explores stem cell decline in the brain; the finding that stem cell-enriched fractions are epigenetically younger connects to the broader principle that tissue EpiAge reflects stem cell composition.

## Sources

- Ricon, J. L. (2020). "Epigenetic clocks: A review." *Nintil*. <https://nintil.com/epigenetic-clocks/> — [[2026-04-16-nintil-epigenetic-clocks-review|local copy]]
- Kabacik, S. et al. (2022). "The relationship between epigenetic age and the hallmarks of aging in human cells." *Nature Aging*, 2, 484–493. <https://doi.org/10.1038/s43587-022-00220-0> — [[2022-06-01-epiage-hallmarks-of-aging|local copy]]
- Patrick, R. & Horvath, S. (2026). "The 7 Habits of People Who Age Slower." *FoundMyFitness* (YouTube). <https://www.youtube.com/watch?v=3pRiY2zHt8c> — [[2026-06-15-horvath-slowing-biological-aging|local copy]]
