---
source: agent
compiled_from:
  - agent-notes/raw/economics/2023-11-01-commercial-real-estate-regulations-output.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: high
---

# The Economic Cost of Commercial Zoning

Commercial real estate — roughly $16 trillion and 20% of U.S. fixed assets — is heavily regulated through zoning codes, floor-area ratios, height limits, setback requirements, parking mandates, and discretionary review boards. While the costs of *residential* land use regulation have been studied extensively (see [[geographic-wage-premiums]] for the labor market consequences), the macroeconomic impact of *commercial* zoning has received far less attention.

Babalievsky, Herkenhoff, Ohanian, and Prescott (2023) develop a spatial general equilibrium model to quantify these costs, finding that moderate commercial deregulation could raise U.S. output by 3-6% and welfare by 3-9% of lifetime consumption.

## Measuring regulation from property tax records

The core insight is that property tax assessments — which decompose a parcel's total value into land value and improvement (structure) value — reveal the effective stringency of regulation without needing to parse the actual zoning codes. The intuition: a small building sitting on very expensive land signals that regulations prevented the developer from building more. Formally, the ratio of improvement value to total value identifies a parcel-level "virtual distortion" τ_i, where τ_i = 1 means unregulated and τ_i → 0 means development is effectively forbidden.

This approach sidesteps several measurement challenges:
- Zoning codes are multidimensional (height, FAR, setbacks, parking, use restrictions) and vary across jurisdictions
- Some properties receive variances or exemptions, so the *effective* impact differs from the *statutory* restriction
- Many regulations are informal (community review boards, threatened litigation)

Using CoreLogic's near-universe of commercial parcel records (2009-2018), the authors construct MSA-level indexes for both the average level of regulation (T_j) and within-city dispersion of regulations (D_j).

## The deregulated benchmark: Midland, Texas

The least-regulated metro is Midland, Texas (pop. ~130,000), known as "the Tall City" for its disproportionately tall commercial buildings. The authors calibrate their model by treating Midland as the benchmark where T_j = 1, which yields an implied improvement share (γ) of 0.92 — meaning the building production function is nearly linear in improvements, and doubling a building's height only slightly more than doubles its cost.

The most regulated cities include beach towns (Ocean City NJ, Naples FL, Myrtle Beach SC) and some smaller metros. The authors speculate that cities with desirable natural amenities may use commercial restrictions to avoid over-development. California metros (LA, SF) are consistently more regulated than Texas metros (Dallas, Houston), confirming the conventional wisdom.

## Counterfactual findings

The paper runs five national experiments and one local (NYC) experiment:

| Counterfactual | Output | Building stock | Welfare (cons. equiv.) |
|---|---|---|---|
| Baseline (all cities → Midland level) | +3.0% | +17.6% | +2.9% |
| Reduce within-MSA dispersion | +6.1% | +59.9% | +9.2% |
| Baseline + 40% remote work | +1.5% | +19.4% | +1.3% |
| Local reform (worst parcels → MSA median) | +3.1% | +26.0% | +6.4% |
| Baseline + doubled congestion externality | +3.0% | +17.8% | +3.0% |

Several results stand out:

**Dispersion matters more than levels.** Making regulations *uniform* within each MSA (without changing the average stringency) produces larger gains than reducing the average level nationwide. This parallels the Hsieh-Klenow (2009) finding that misallocation across firms — not the average level of distortion — is the primary source of efficiency losses.

**Remote work attenuates but doesn't eliminate gains.** Even with 40% of jobs remote (an upper bound from Dingel and Neiman 2020), deregulation still yields +1.5% output. Office buildings are only ~20% of commercial building stock; the rest (retail, industrial, warehouses) is unaffected by remote work.

**Congestion externalities don't justify current regulation levels.** Doubling the congestion externality barely changes the aggregate results, because there is little correlation between MSA productivity and amenities — deregulation doesn't simply push workers into already-congested high-productivity cities.

**Developer profits fall.** More building supply lowers rents, reducing developer profits by ~3%. This suggests commercial regulations partly reflect rent-seeking by incumbents who benefit from supply constraints, not just congestion management.

## NYC floor-area ratio reform

As a local case study, the authors simulate raising all floor-area ratios in NYC to the maximum observed level. Results: NYC MSA output rises 1.8%, building stock increases 6%, and commercial real estate prices fall 4%. Business activity shifts from Midtown Manhattan (which already has high FARs) to the Upper East and West Sides (which have much lower FARs and are known for opposing development). Notably, the least-regulated buildings *shrink* as the equilibrium price per square foot falls.

## Implications

The welfare gains from commercial deregulation (1.3-2.8% of lifetime consumption in the baseline) are comparable to those found in the residential land use literature. Combined, the total drag from land use regulation on the U.S. economy is substantial — potentially the single largest class of distortions outside the tax code.

The framework enables granular, address-level counterfactuals that can inform specific local reforms. Future work could extend it to residential regulations, heterogeneous workers, and transition dynamics — including the interaction between regulation, inequality, and homelessness.

## Sources

- Babalievsky, Herkenhoff, Ohanian, and Prescott (2023). "The Impact of Commercial Real Estate Regulations on U.S. Output." NBER Working Paper No. 31895. <https://www.nber.org/papers/w31895> — [[2023-11-01-commercial-real-estate-regulations-output|local copy]]
