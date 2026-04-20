---
source: agent
compiled_from:
  - agent-notes/raw/health/2016-06-01-cogfx-indoor-air-quality.md
compiled_at: 2026-04-20
model: claude-opus-4-6
confidence: high
---

# Indoor Air Quality and Cognitive Function

Humans spend roughly 90% of their time indoors, yet indoor environmental quality (IEQ) receives remarkably little attention compared to outdoor air pollution. A landmark 2016 controlled-exposure study — the COGfx Study — demonstrated that indoor CO₂ concentrations, ventilation rates, and volatile organic compound (VOC) levels have large, dose-dependent effects on higher-order cognitive function in knowledge workers.

## The COGfx Study

Allen et al. (2016) placed 24 professional-grade knowledge workers (architects, designers, programmers, engineers, managers) in an environmentally controlled office lab (the TIEQ Lab at Syracuse University) for 6 full work days across 2 weeks. Participants were blinded to conditions. Three IEQ regimes were simulated:

| Condition | Outdoor air ventilation | Approximate CO₂ | TVOC level |
|-----------|------------------------|-----------------|------------|
| **Conventional** | 20 cfm/person | ~1,100 ppm | 500–660 µg/m³ |
| **Green** | 20 cfm/person | ~715 ppm | < 50 µg/m³ |
| **Green+** | 40 cfm/person | ~550 ppm | < 50 µg/m³ |

The "Conventional" condition used VOC-emitting materials (including carpet tiles, furniture, cleaning products) at concentrations typical of U.S. office buildings. Green conditions used low-emitting materials. Green+ doubled the outdoor air supply.

Cognitive function was assessed daily using the Strategic Management Simulation (SMS), a validated computer-based test that measures nine domains of management-level decision-making: basic activity, applied activity, focused activity, task orientation, crisis response, information seeking, information usage, breadth of approach, and strategy.

## Key Findings

### Green vs. Conventional buildings

Cognitive scores were **61% higher** on the Green building day and **101% higher** on Green+ days compared to the Conventional day (p < 0.0001 for all nine domains).

The largest effects appeared in the domains most relevant to knowledge work:

| Cognitive domain | Green vs. Conventional | Green+ vs. Conventional |
|-----------------|----------------------|------------------------|
| Crisis Response | +97% | +131% |
| Information Usage | +172% | +299% |
| Strategy | +183% | +288% |

These three domains — crisis response, information usage, and strategy — are indicators of higher-level cognitive function and complex decision-making, precisely the capabilities most valued in knowledge workers.

### CO₂ as an independent factor

When CO₂ was varied while holding other parameters constant, the relationship was approximately linear across the tested range:

- At **~945 ppm** (moderate, typical of many offices meeting code-minimum ventilation): cognitive scores were **15% lower** than at Green+ levels (~550 ppm)
- At **~1,400 ppm** (common in crowded or poorly ventilated rooms): scores were **50% lower**

A **400 ppm increase** in CO₂ was independently associated with a **21% decrease** in cognitive scores across all domains.

### Independent effects of ventilation and VOCs

The study modeled ventilation rate, CO₂, and TVOCs separately to disentangle their contributions:

- **Ventilation**: a 20-cfm/person increase in outdoor air → **18% improvement** in cognitive scores
- **VOCs**: a 500-µg/m³ increase in TVOCs → **13% decrease** in cognitive scores
- **CO₂**: 400 ppm increase → **21% decrease** in cognitive scores

All three effects were statistically significant (p < 0.0001) and independent of one another, meaning each factor contributes its own cognitive penalty.

## Implications

### For office design

The study's conditions were designed to mirror real-world environments. The "Conventional" condition used CO₂ and VOC concentrations commonly found in U.S. offices built to code-minimum standards. The Green+ condition — which produced the highest cognitive scores — required only doubling the outdoor air supply and using low-emitting materials, both achievable with existing HVAC technology.

The authors estimate that the R² of their model was 0.81, meaning indoor environmental conditions explained 81% of the variability in cognitive performance across participants and days. Only 19% was attributable to interpersonal variation or confounds like sleep quality and mood.

### For building codes and standards

ASHRAE 62.1 sets minimum ventilation at 20 cfm/person for offices, a rate driven historically by odor control, not cognitive performance. The COGfx results suggest this baseline is insufficient for optimal cognitive function. The Green+ condition (40 cfm/person) produced substantially better outcomes.

### Historical context: the ventilation-energy tradeoff

The paper traces a direct line from the 1970s energy crisis to modern IEQ problems. As buildings were sealed for energy efficiency, air exchange rates in homes dropped from ~1.0 ACH to ~0.5 ACH, and sick building syndrome emerged in the 1980s. The COGfx study reframes this tradeoff: the productivity cost of low ventilation may far exceed the energy savings.

### Beyond offices

The authors note these findings should be investigated in homes, schools, and airplanes — environments where "small changes in cognitive function and decision-making could have significant impacts on productivity, learning, and safety." This is particularly salient for airplane cabins, where CO₂ concentrations routinely exceed 1,400 ppm, and for classrooms, where studies have linked elevated CO₂ to lower test scores.

## Limitations

- Small sample size (n=24), though the within-subject design (each person serves as their own control) strengthens causal inference
- Single-site study in a controlled lab, not a naturalistic office
- The SMS test measures decision-making simulation performance, not direct workplace productivity
- Environmental conditions were held for single days; chronic exposure effects remain unknown
- Participants were in Syracuse, NY — generalizability to other populations and climates needs verification

## Sources
- Allen JG, MacNaughton P, Satish U, Santanam S, Vallarino J, Spengler JD (2016). "Associations of Cognitive Function Scores with Carbon Dioxide, Ventilation, and Volatile Organic Compound Exposures in Office Workers." <https://doi.org/10.1289/ehp.1510037> — [[2016-06-01-cogfx-indoor-air-quality|local copy]]
