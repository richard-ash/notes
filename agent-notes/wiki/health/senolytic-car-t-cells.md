---
source: agent
compiled_from:
  - agent-notes/raw/health/2024-01-24-senolytic-car-t-cells-aging.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: high
---

# Senolytic CAR T Cells

Senolytic CAR T cells are a cell therapy approach that uses chimeric antigen receptor (CAR) T cells to selectively eliminate senescent cells — the damaged, non-dividing cells that accumulate with age and secrete pro-inflammatory factors (the senescence-associated secretory phenotype, or SASP). The leading program targets **uPAR** (urokinase plasminogen activator receptor), a surface protein upregulated on senescent cells across multiple tissues. Developed primarily at Cold Spring Harbor Laboratory and Memorial Sloan Kettering by Corina Amor, Scott W. Lowe, Michel Sadelain, and colleagues.

## Why target senescent cells?

Cellular senescence is one of the [[information-theory-of-aging|hallmarks of aging]]. Senescent cells accumulate in tissues over time and, through the SASP, create a chronic pro-inflammatory environment that drives age-related pathologies: metabolic dysfunction, tissue fibrosis, decreased physical fitness, and impaired immune function. Genetic experiments ablating senescent cells (using the p16-INK-ATTAC and similar models) demonstrated that removing these cells extends healthspan in mice — establishing senolysis as a viable therapeutic strategy.

## The small-molecule problem

Existing senolytic drugs (dasatinib + quercetin, navitoclax, fisetin) target poorly defined molecular dependencies in senescent cells and must be administered repeatedly. Their mechanisms are often incompletely understood, and they show variable efficacy across tissues and senescence triggers. A "living drug" approach — one that persists, self-renews, and scales its response to the burden of target cells — addresses these limitations.

## uPAR as a senolytic antigen

uPAR (encoded by *PLAUR* in humans, *Plaur* in mice) is a cell-surface protein involved in extracellular matrix remodeling during fibrinolysis, wound healing, and tumorigenesis. Amor et al. demonstrated that:

- **uPAR is broadly upregulated on senescent cells** across multiple tissues (liver, adipose, skeletal muscle, pancreas) and across multiple cell types (endothelial, myeloid, fibroblasts, preadipocytes).
- **uPAR levels increase with age** in both mice (immunohistochemistry, scRNA-seq from the Tabula Muris Senis atlas) and humans (scRNA-seq of human pancreas datasets).
- **uPAR-positive cells account for 63–92% of the senescent cell burden** in aged tissues, making it a high-coverage senolytic target.
- Soluble uPAR plasma levels correlate with the pace of aging in humans and are a component of the SenMayo senescence gene signature.

## Therapeutic results in aged mice

In a 2024 *Nature Aging* study, Amor et al. infused 18–20-month-old C57BL/6 mice with a single dose of anti-uPAR CAR T cells (m.uPAR-m.28z, a fully syngeneic second-generation construct). Key findings:

1. **Senescent cell clearance.** Reduced SA-β-gal-positive and uPAR-positive cells in pancreas, liver, and adipose tissue. Decreased plasma SASP cytokines (IL-6, TNFα, IL-1β, and others).
2. **Metabolic improvement.** Significantly lower fasting glucose, improved glucose tolerance, lower basal insulin with improved insulin response (better pancreatic beta cell function), and improved peripheral insulin sensitivity.
3. **Physical fitness.** Improved exercise capacity (treadmill endurance and maximum speed) at 2.5 months post-treatment.
4. **Safety.** No morbidity, weight loss, organ damage, or hematological abnormalities. Serum chemistry and complete blood counts remained normal.
5. **Persistence.** CAR T cells expanded and trafficked to liver and spleen, predominantly as cytotoxic CD8+ T cells with effector phenotype.

## Prophylactic potential — the striking result

Perhaps the most remarkable finding: a single dose of anti-uPAR CAR T cells given to **young mice (3 months old)** prevented age-related metabolic decline when assessed months later:

- CAR T cells were still detectable in spleens and livers **12 months after infusion**, at levels substantially above controls.
- Persisting cells were mostly CD8+ memory/effector T cells — the CAR T cells adapted to an ongoing, slowly increasing target population.
- Prophylactically treated mice showed lower fasting glucose, better glucose tolerance, enhanced beta cell function, and higher exercise capacity at 9 months of age.
- Senescent cell burden was reduced in pancreas, liver, and adipose tissue compared to controls.

This "vaccinate once against aging" profile distinguishes CAR T senolytics from every small-molecule approach, which requires lifelong dosing.

## Metabolic syndrome model

The therapy also worked in a high-fat diet (HFD) model of metabolic syndrome:

- **Therapeutic:** Mice on HFD for 2 months, then given CAR T cells → lower body weight, better fasting glucose, improved glucose/insulin tolerance persisting for 2.5+ months.
- **Prophylactic:** CAR T cells given 1.5 months *before* HFD → blunted weight gain, improved glucose levels sustained for 5.5+ months despite continuous HFD exposure.

## Open questions

- **Which cell populations matter most?** uPAR is expressed on senescent endothelial cells, macrophages, fibroblasts, and preadipocytes. It is unclear which populations' elimination drives the metabolic benefits. Senescent pancreatic beta cells, adipose cells, and macrophages are all candidates.
- **Longevity.** The study was not powered to assess lifespan extension. Genetic and pharmacological senolysis studies have been equivocal on longevity, even when healthspan improves.
- **Safety at scale / in humans.** uPAR is expressed at low levels on some normal tissues (bronchial epithelium, certain myeloid subsets). Clinical translation will likely require safety switches (e.g., AND-gate CARs requiring two antigens) or other controls.
- **Clinical timeline.** No human trials of senolytic CAR T cells have been reported as of the paper's publication (January 2024). The authors note that a separate group has shown mice and primates tolerate CAR T cells targeting a natural killer cell ligand upregulated on senescent cells, suggesting the field is moving toward clinical feasibility.

## Relationship to other senolytic approaches

| Approach | Mechanism | Persistence | Key limitation |
|---|---|---|---|
| Dasatinib + quercetin | Tyrosine kinase / BCL-2 family inhibition | None (requires repeated dosing) | Variable efficacy, poorly defined targets |
| Navitoclax (ABT-263) | BCL-2/BCL-xL inhibition | None | Thrombocytopenia (on-target toxicity) |
| [[glp1-drugs\|GLP-1 receptor agonists]] | Indirect — reduce metabolic stress that triggers senescence | Requires continuous dosing | Not directly senolytic |
| GPNMB vaccination | Immune response against GPNMB+ senescent cells | Moderate (immune memory) | Early-stage; single antigen |
| **uPAR CAR T cells** | Direct cytotoxicity against uPAR+ cells | **High** (living drug, persists 12+ months) | Requires lymphodepletion; manufacturing complexity |

## Sources

- Amor, C. et al. (2024). "Prophylactic and long-lasting efficacy of senolytic CAR T cells against age-related metabolic dysfunction." *Nature Aging* 4, 336–349. <https://doi.org/10.1038/s43587-023-00560-5> — [[2024-01-24-senolytic-car-t-cells-aging|local copy]]
