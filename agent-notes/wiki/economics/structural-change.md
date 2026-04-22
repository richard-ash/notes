---
source: agent
compiled_from:
  - agent-notes/raw/economics/2021-01-01-structural-change-income-price-effects.md
compiled_at: 2026-04-22
model: claude-opus-4-6
confidence: high
---

# Structural Change

Structural change (or structural transformation) is the large-scale reallocation of employment and output across economic sectors as economies develop. The stylized facts are remarkably consistent across countries and time periods: agriculture declines, manufacturing follows a hump-shaped trajectory (rising then falling), and services steadily expand. Understanding what drives this process -- whether demand-side forces (income effects through Engel curves) or supply-side forces (differential productivity growth and capital intensity across sectors) -- is one of the central questions in growth economics.

## The empirical puzzle: Engel curves that don't flatten

A key empirical regularity motivates the theoretical framework. When relative sectoral expenditure shares are plotted against income (controlling for relative prices), the relationship is log-linear and *stable* -- it does not level off as income grows. This holds in aggregate OECD data, in U.S. household microdata (CEX), and in Indian household microdata (NSS), despite vast differences in income levels and sectoral composition. The slopes of relative Engel curves remain constant across income groups and over time.

This is a problem for the dominant demand-side model, generalized [[stone-geary-preferences|Stone-Geary preferences]], where nonhomotheticity is driven by subsistence levels. As income rises, the subsistence terms become negligible and preferences converge to homothetic -- Engel curves flatten. The data say otherwise.

## Nonhomothetic CES preferences

Comin, Lashkari, and Mestieri (2021) introduce *nonhomothetic CES preferences*, a class of utility functions that generate non-vanishing income effects at all levels of income while maintaining a constant elasticity of substitution across sectors. Each sector *i* has a nonhomotheticity parameter epsilon_i that controls its relative income elasticity. The preferences are defined implicitly and have two key properties:

1. **Constant relative income elasticities.** The elasticity of relative demand between any two goods with respect to utility is constant: (1 - sigma)(epsilon_i - epsilon_j). This generates Engel curves with constant log-linear slopes that never flatten -- matching the data.

2. **Constant, separable price elasticity.** The elasticity of substitution between any two goods is sigma, independent of income or the nonhomotheticity parameters. This separation means that price and income effects can be independently identified and estimated.

The income (expenditure) elasticity of sector *i* is eta_i = sigma + (1 - sigma)(epsilon_i / epsilon_bar), where epsilon_bar is the expenditure-weighted average nonhomotheticity parameter. Whether a good is a "luxury" or "necessity" is not intrinsic -- it depends on the consumer's current expenditure composition, which itself depends on income.

## Empirical estimates

The preference parameters are estimated at both the household level (U.S. CEX and Indian NSS) and cross-country level (39-country postwar panel):

| Parameter | U.S. Household (CEX) | Cross-Country (39 countries) |
|-----------|---------------------|------------------------------|
| sigma (price elasticity) | 0.26-0.33 | 0.50-0.63 |
| epsilon_a (agriculture) | lower than manufacturing | lower than manufacturing |
| epsilon_s (services) | higher than manufacturing | higher than manufacturing |
| Implied eta: agriculture | 0.37 | 0.56 |
| Implied eta: manufacturing | 0.83 | 1.03 |
| Implied eta: services | 1.20 | 1.14 |

The estimates are remarkably stable: similar across above- and below-median income households, across pre- and post-2005 subsamples, across OECD and non-OECD countries, and between the U.S. and India despite their vastly different income levels. Sectors are estimated as gross complements (sigma < 1) in all specifications.

## Income effects dominate structural change

The central empirical finding: income effects (demand nonhomotheticity) account for the overwhelming majority of within-country structural change, and price effects (supply-side forces) play a secondary role.

For the within-country variance decomposition of sectoral employment shares:

- **Agriculture relative to manufacturing:** income effects account for 98% of variation; price effects account for 2%
- **Services relative to manufacturing:** income effects account for 84%; price effects account for 27% (they sum to more than 100% because the two forces are not independent)

Overall, **nonhomotheticities explain over 73% of within-country structural change** in the 39-country panel.

This contrasts sharply with previous findings using Stone-Geary preferences, where income and price effects appeared roughly equal. The difference arises because Stone-Geary preferences hard-wire income effects to be transitory (flattening Engel curves), which mechanically forces price effects to absorb more of the variation.

## Model fit vs. alternatives

Nonhomothetic CES substantially outperforms both Stone-Geary and PIGL (price-independent generalized linear) preferences in cross-country fit:

| Demand system | Within-R-squared |
|---------------|-----------------|
| Stone-Geary | 0.14 |
| PIGL | 0.13 |
| Nonhomothetic CES | 0.29 |

Stone-Geary underperforms because income effects vanish at high income levels. PIGL tracks services better (it has non-vanishing nonhomotheticity) but assumes a homothetic composite between agriculture and manufacturing. Nonhomothetic CES allows sector-specific nonhomotheticity parameters for an arbitrary number of sectors.

An important out-of-sample prediction: the model generates positive correlations between nominal and real sectoral shares (agriculture/manufacturing: 0.94 model vs. 0.96 data; services/manufacturing: 0.71 vs. 0.87). Standard homothetic CES would predict negative correlations, since with gross complementarity, the price effect implies sectors with faster productivity growth (falling relative prices) should see rising real but falling nominal shares. Nonhomothetic CES resolves this because the income effect pushes both real and nominal shares in the same direction, and at estimated parameter values, it dominates.

## Growth implications

When embedded in a general equilibrium growth model with heterogeneous sectoral productivity growth and capital intensities, nonhomothetic CES preferences affect the macroeconomic dynamics of capital accumulation:

- **Slower convergence to steady state** compared to the Neoclassical Growth Model. The presence of structural change -- whether driven by price or income effects -- implies a slower process of capital accumulation along the transition path.
- **Time-varying elasticity of intertemporal substitution (EIS).** As income rises, the share of high-income-elastic goods in the consumption bundle grows, and the effective EIS rises over time. Early in development, when necessities dominate the budget, households are less intertemporally substitutable; as luxuries (services) grow in share, households become more responsive to interest rate changes.
- **Long-run growth rate** depends on nonhomotheticity parameters, sectoral productivity growth rates, and capital intensities. Generically, only the sectors achieving a specific minimum (involving the ratio of productivity growth to nonhomotheticity) survive in employment terms in the long run.

## Connections

The framework relates to several strands of the growth and development literature:

- [[use-of-knowledge-in-society|Hayek's price system]] acts as the mechanism through which differential productivity growth translates into relative price signals that drive the substitution (price) effects in structural change.
- [[ai-and-relational-scarcity|AI and relational scarcity]]: the prediction that services absorb ever-larger employment shares as economies grow is consistent with the hypothesis that as productivity in goods production rises, spending shifts toward services where human involvement is intrinsically valued.
- [[ai-economics-research|AI and economics research]]: Comin et al.'s framework is an example of the kind of structural estimation work in economics that Syverson (2025) argues AI may complement rather than replace -- it requires deep theoretical modeling, identification arguments, and novel data construction.

## Sources

- Comin, Lashkari, and Mestieri (2021). "Structural Change with Long-Run Income and Price Effects." *Econometrica*, 89(1), 311-374. <https://doi.org/10.3982/ECTA16317> -- [[2021-01-01-structural-change-income-price-effects|local copy]]
