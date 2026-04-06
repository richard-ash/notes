---
source: agent
compiled_from:
  - agent-notes/raw/economics/2023-08-01-location-location-location.md
compiled_at: 2026-04-06
model: claude-opus-4-6
confidence: high
---

# Geographic Wage Premiums

Geographic differences in earnings are large and persistent across U.S. commuting zones (CZs). But how much of this variation reflects the causal effect of *place* on wages, and how much reflects the sorting of higher-skilled workers into higher-paying locations? Card, Rothstein, and Yi (2023) provide the most comprehensive decomposition to date, using establishment-level data from the Census Bureau's LEHD program covering ~110 million U.S. workers.

## The 50/50 split: sorting vs. place

The headline finding is striking in its symmetry: approximately **half** of the variation in mean wages across CZs is attributable to differences in worker quality (measured by person fixed effects in an AKM model), and the other half to genuine locational wage premiums — the causal pay boost a randomly selected worker would receive from moving to a higher-paying CZ.

This result has a sharp implication for cross-sectional studies. Models that control only for *observed* worker characteristics (education, age, gender, race) capture roughly 31% of the CZ wage variation. The remaining 69% gets attributed to "place effects" — but much of it is actually unobserved skill sorting. The AKM approach, by estimating person fixed effects that capture both observed and unobserved skills, reveals sorting to be far more extensive than conventional estimates suggest.

The correlation between mean worker skill and CZ wage premiums is 0.64 — much higher than the 0.18 correlation between person and firm effects at the individual level. This means high-skill workers sort to high-paying *places* more intensely than they sort to high-paying *firms within places*.

## The hierarchy effect: why prior estimates were biased

Card, Rothstein, and Yi identify a systematic pattern they call the "hierarchy effect": workers who move between CZs transit between non-representative firms. Those moving *up* the CZ wage ladder tend to leave above-average firms in their origin city and land at below-average firms in their destination. The reverse holds for downward movers.

This matters because the conventional approach — a two-way fixed effects model with person and *place* effects (rather than person and *establishment* effects) — treats the hierarchy change as part of the error term. Since hierarchy changes are negatively correlated with CZ premium changes, these models systematically attenuate estimates of place effects. Card, Rothstein, and Yi find that person-and-place models understate the gap between high-wage and low-wage CZs by about 20%.

Conversely, cross-sectional models that omit person fixed effects *overstate* place effects by a roughly similar margin, because they attribute unobserved worker skill to place. The two biases approximately cancel: cross-sectional models and person-and-place models bracket the true place effects from opposite directions.

## Industry composition barely matters

A key question in [[urban-economics]] is whether cities like New York pay more because they host high-paying industries (e.g., finance) or because of genuine place-based productivity advantages. Card, Rothstein, and Yi find the answer is overwhelmingly the latter:

- Place and industry effects are approximately **additively separable** — CZ-industry "match" effects account for less than 10% of variation in CZ-by-industry premiums
- Industry **composition** effects (differences in the share of high-wage industries) explain only **2.5%** of cross-CZ variation in average wage premiums
- Local **agglomeration** effects (higher pay in industries with larger local employment shares) are statistically significant but contribute only 2-4% of variance
- These conclusions are robust to using 20 vs. 312 industry categories

In the Oaxaca-style decomposition, over 90% of the variation in CZ average wage premiums is attributable to pure locational wage premia that are common across industries.

## The college wage gap puzzle

The college-high school wage gap is substantially larger in bigger and higher-wage CZs — a fact highlighted by Autor (2019) and Davis and Dingel (2019, 2020). Card, Rothstein, and Yi decompose this pattern into its sources:

- **~63%** is attributable to differences in person effects — college workers in large cities have higher unobserved skills relative to non-college workers than in small cities
- **~25%** reflects enhanced sorting of college-educated workers into high-wage industries in larger CZs (an industry composition effect)
- **Only ~10%** reflects actual differences in local pay premiums between education groups

The sorting of college workers to larger CZs is also more *assortative*: the correlation between worker and firm effects is 0.75 for college workers but only 0.43 for non-college workers. In larger places, high-skill workers are matched more intensively with high-premium firms, consistent with Diamond (2016).

## Housing costs eat the gains

Card, Rothstein, and Yi find that housing costs rise with CZ size with an elasticity of 0.2 or more. Since housing represents at least one-third of household budgets, nominal wages would need a size elasticity of at least 0.07 to keep up with the cost of living. But the size elasticity of causal place effects is only about 0.043 for college workers and 0.02 for non-college workers — well below what's needed.

The implication is stark: **moving to a larger CZ yields approximately zero (or negative) change in real consumption**, net of housing costs. In a Roback (1982) spatial equilibrium framework, this means larger CZs must offer superior consumption amenities — cultural institutions, restaurants, natural beauty, social networks — that offset the real wage penalty. Workers aren't irrational; they're paying for something other than purchasing power.

## Implications

The paper's findings reshape several policy-relevant questions:

1. **Place-based economic development**: Since place effects are real and large (not just sorting artifacts), policies that raise local productivity can genuinely increase workers' nominal earnings. But housing cost offsets mean the welfare gains may flow primarily to landowners unless housing supply is expanded.

2. **Geographic inequality**: The strong sorting of high-skill workers to high-pay places magnifies overall earnings inequality beyond what the place effects alone would produce. This is a feature of locational equilibrium, not a market failure per se.

3. **Returns to education**: The apparent higher return to college in big cities is mostly a composition effect — big cities attract the *best* college graduates, not just more of them. Policy implications differ sharply from a world where big cities genuinely make education more valuable.

4. **Industry policy**: Tax incentives to attract specific industries will have limited effects on local wage premiums, since industry composition explains so little of cross-CZ wage variation. Place-based productivity improvements that operate across industries matter far more.

## Sources

- Card, Rothstein, and Yi (2023). "Location, Location, Location." NBER Working Paper No. 31587. <http://www.nber.org/papers/w31587> — [[2023-08-01-location-location-location|local copy]]
