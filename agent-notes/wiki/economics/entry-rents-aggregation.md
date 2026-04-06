---
source: agent
compiled_from:
  - agent-notes/raw/economics/2020-05-01-entry-vs-rents-aggregation-economies-of-scale.md
compiled_at: 2026-04-06
model: claude-opus-4-6
confidence: high
---

# Entry vs. Rents: Aggregation with Economies of Scale

How do microeconomic disturbances — firm-level productivity shocks, markup changes, entry and exit — translate into macroeconomic outcomes? Baqaee and Farhi tackle this "aggregation problem" by generalizing Hulten's (1978) classical result to economies with non-constant returns to scale, product entry and exit, input-output linkages, and distortions. Their central finding: **accounting for the entry margin roughly doubles the estimated efficiency losses from markups in the U.S.**, from ~20% to ~40% of GDP.

## The Core Decomposition

The paper decomposes changes in aggregate output into two components:

1. **Technical efficiency** — the direct, mechanical effect of productivity shocks, holding the allocation of resources fixed. Captured by forward Domar weights (a cost-based analogue to sales shares that accounts for cumulated distortions downstream).

2. **Allocative efficiency** — the indirect effect from reallocation of resources across producers and into/out of entry. This is where the action is in distorted economies.

The key insight is that allocative efficiency changes can be summarized by two sufficient statistics: **rents** (variable profits from markups or decreasing returns) and **quasi-rents** (the portion of rents dissipated by entry costs). Which statistic matters depends on the source of scale economies:

- For goods with **decreasing returns to scale** (DRS): the gap between rents and quasi-rents matters. If rents grow faster than quasi-rents, entry isn't keeping up with sales growth, firms are scaling up into diminishing returns, and allocative efficiency falls.
- For goods with **increasing returns to scale** (IRS): the level of quasi-rents matters. Rising quasi-rents mean more entry, which generates consumer surplus through love-of-variety effects.

## Efficient Benchmark

Under efficiency (Theorem 1), firms must be allowed to charge markups equal to gamma_i — the ratio of the area under the residual demand curve to sales — to properly incentivize entry. This markup compensates entrants for both the producer surplus and consumer surplus their entry creates. An offsetting output subsidy restores marginal-cost pricing conditional on entry.

When the economy is efficient, Hulten's theorem holds: the response of output to a productivity shock is simply the producer's sales share of GDP, and the details of production structure don't matter (Theorem 2).

## Entry Matters More Than You Think

A seemingly innocuous claim — that entry costs are small as a share of GDP, so entry can be ignored — is wrong. Even when variable profits and entry costs are tiny fractions of GDP, free entry can **qualitatively** alter the economy's response to shocks. Under constant returns to scale with free entry, only the direct technology effect matters and reallocations are irrelevant — even if the equilibrium is inefficient. This is because entry absorbs or exudes resources in precisely the right way to neutralize reallocation effects.

The paper also shows that folk wisdom equating entry via diminishing returns (Lucas, 1978) with entry via love-of-variety (Dixit-Stiglitz, 1977) is "highly fragile and fails outside of very simple single-sector models." Whether entry is directed (entrants choose their market) or undirected (random assignment post-entry) fundamentally changes the aggregation formula.

## Harberger Triangles for Entry

Baqaee and Farhi generalize Harberger's (1954) welfare triangles to economies with entry. The social cost of distortions is approximately a Domar-weighted sum of Harberger triangles, some from variable production and some from entry. This yields several surprising results:

- **Non-monotonicity in elasticity of substitution**: In models without entry, higher elasticity of substitution means larger welfare losses from [[misallocation-markups|markup dispersion]]. With entry and IRS, the relationship becomes U-shaped — lower elasticities reduce intensive-margin misallocation but magnify extensive-margin (entry) misallocation.

- **Irrelevance of cross-sector elasticities for DRS**: In sectoral DRS models, the elasticity of substitution across sectors is irrelevant to a second-order approximation. Only within-sector returns to scale and markup dispersion matter.

## Policy Implications

The paper derives "bang-for-buck" formulas for two types of interventions, formalizing and revising Hirschman's (1958) argument about targeting sectors with strong linkages:

- **Markup regulation** (competition policy): most effective when targeted at industries that are **downstream** of sectors with strong scale economies. The formula captures how reducing markups in i benefits sectors upstream via backward linkages.

- **Entry subsidies** (industrial policy): most effective when targeted at industries that are **upstream** in supply chains with strong returns to scale. Subsidizing entry upstream propagates benefits forward through the production network.

In both cases, the goal is to boost the sales of sectors that are upstream and have strong scale economies downstream from themselves.

## Quantitative Results

Using U.S. data (66 BEA industries, Compustat firm-level markups estimated via De Loecker et al., 2019):

| Scenario | No Entry | Entry (Factors) | Entry (Goods+Factors) |
|---|---|---|---|
| IRS, high elasticity | 36% | 50% | 41% |
| IRS, low elasticity | 19% | 32% | 37% |
| DRS, high elasticity | 26% | 35% | 32% |
| DRS, low elasticity | 10% | 19% | 20% |

Key findings:
- Entry roughly doubles the estimated welfare losses
- Without entry, almost all losses come from within-sector markup dispersion
- With entry, the level effect (too much/too little total entry) becomes equally important
- With high estimated markups and free entry, there is **excessive entry** in equilibrium — surprisingly, some barriers to entry would actually improve efficiency
- Losses are non-monotonic in entry barriers: the distance to the frontier first decreases then increases as barriers grow

## Temporal Notes

The paper was first circulated in May 2020. Emmanuel Farhi passed away in July 2020; the paper was revised posthumously in December 2021. The rising-markups literature it builds on (De Loecker et al., 2019) remains actively debated, and the specific quantitative magnitudes depend on markup estimation methodology. However, the qualitative message — that entry matters for aggregation and can roughly double estimated losses — is robust across specifications.

## Sources

- Baqaee, D. and E. Farhi (2020, rev. 2021). "Entry vs. Rents: Aggregation with Economies of Scale." NBER Working Paper No. 27140. <https://www.nber.org/papers/w27140> — [[2020-05-01-entry-vs-rents-aggregation-economies-of-scale|local copy]]
