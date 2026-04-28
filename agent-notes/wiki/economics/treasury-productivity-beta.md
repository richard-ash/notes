---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-04-23-treasury-investors-ai-bet.md
  - agent-notes/raw/economics/2026-04-23-bonds-long-ai-paper.md
compiled_at: 2026-04-27
model: claude-opus-4-7
confidence: high
---

# Treasury bonds as a productivity claim

Howard Kung, Hanno Lustig, and James Paron argue that U.S. Treasury bonds are implicitly long productivity growth — and therefore long AI. The mechanism is fiscal: government debt is backed by future primary surpluses, and surpluses respond very asymmetrically to GDP growth. Tax revenue scales slightly more than one-for-one with GDP (because progressive brackets generate "real bracket creep"), while most spending is essentially inelastic to growth. The result is that bondholders hold something close to a *levered* claim on GDP. This reframes a puzzle in the recent empirical literature: nominal Treasury yields *fall* on frontier AI model release days, which Lustig et al. argue is exactly what one would expect if investors are revising productivity expectations modestly upward. Their paper concludes that bondholders are betting on one of three outcomes: a large fiscal correction, high unanticipated inflation, or higher economic growth — and that the long-AI position is implicit in the third.

## The puzzle the framework explains

Two recent papers argue current Treasury prices are inconsistent with AI optimism. [Andrews and Farboodi (2025)](https://www.nber.org/papers/w34243) document that across 17 frontier-model release events, 10-year nominal Treasury yields *fell* — by 6.6bp in a 3-day window and 9.0bp over 15 days. [Chow, Halperin, and Mazlish (2025)](https://basilhalperin.com/papers/) note that long-term real rates remain low, suggesting markets are not pricing in near-term transformative AI. Standard consumption-smoothing intuition predicts the opposite: better expected growth should push real rates *up* as households try to borrow against future income. Both readings implicitly assume Treasuries have *zero* productivity beta.

Kung, Lustig, and Paron flip this. If Treasuries are a productivity-linked claim, falling yields on positive AI news are price-consistent: better growth raises the present value of future surpluses, which makes the same coupon stream more valuable, which compresses yields. The event-window decomposition makes the channels concrete:

| Component | ±3 days (bp) | ±15 days (bp) |
| --- | --- | --- |
| Nominal yield (10yr) | −6.6 | −9.0 |
| Breakeven inflation | −1.5 | −2.4 |
| ACM term premium | −3.0 | −3.1 |
| AAA credit spread | +0.8 | +0.2 |

All three fiscal channels move in the predicted direction:

- **Breakeven inflation falls.** Productivity growth is disinflationary, and in a fiscal-theory reading, a better-collateralized debt stock pulls inflation expectations down.
- **The term premium compresses.** Less uncertainty about debt service capacity reduces the risk premium on long-duration Treasuries.
- **Convenience yields rise** (AAA credit spread widens). A lower projected debt-to-GDP ratio means a smaller supply of safe assets, raising the convenience premium on the remaining stock.

The yield path drifts down for ~20 trading days *before* the release (consistent with pre-announcement leakage) and remains depressed for roughly two weeks after.

## Why bondholders are long growth: the fiscal mechanism

Government bonds are backed by future primary surpluses (taxes minus non-interest spending), much as a mortgage-backed security is backed by future mortgage payments. The valuation framework, due to [Jiang, Lustig, Van Nieuwerburgh, and Xiaolan (2022)](https://www.brookings.edu/wp-content/uploads/2022/09/BPEA-FA22_WEB_Jiang-et-al.pdf), is:

`D₀ = Σ S_t / (1+r_t)^t + TV`

where TV is the post-horizon terminal value. Surpluses are discounted at the Treasury yield curve plus a 2.6pp GDP risk premium that compensates investors for the positive covariance of surpluses with GDP — surpluses are low precisely when the economy is weak.

The CBO's published "rules of thumb" pin down the asymmetry between revenue and spending response. A 0.1pp productivity *slowdown* over the next decade reduces revenue by **$572B**, reduces mandatory spending by only **$43B**, and widens the cumulative deficit by **$388B**. Spending falls about $0.08 for every $1 of revenue lost.

Translated into elasticities of cumulative nominal flows to cumulative nominal GDP:

| Component | Elasticity | Mechanism |
| --- | --- | --- |
| Revenue | 1.07 | Progressive income tax (real bracket creep) |
| Social Security | 0.25 (10y) → 0.81 (30y) | Wage-indexed at claim, CPI-indexed thereafter |
| Medicare / Medicaid | ~0 | Demographic, not growth-driven |
| Discretionary | ~0 (revealed-preference: negative) | Set by appropriations |

The revenue elasticity exceeds one because progressive brackets push households into higher rates as real incomes rise ("real bracket creep"). Discretionary spending's *revealed-preference* elasticity is arguably negative: discretionary spending as a share of GDP has fallen from ~10% in the 1960s to ~5% today.

Social Security is the subtle case. Initial benefits are wage-indexed (via the AIME formula), but once a beneficiary starts collecting, payments are inflation-indexed. Existing beneficiaries are therefore locked in at pre-shock wage levels. Lustig et al. model the turnover as exponential, ε_SS(t) = 1 − e^(−t/D), with D = 18.3 years calibrated to reproduce the CBO's 10-year SS elasticity of 0.25. By year 20, the elasticity reaches 0.66; by year 30, 0.81. The calibrated D is consistent with SSA data on average claiming age (~64) and life expectancy for beneficiaries (~84).

Net: when GDP grows faster, the government collects a lot more and spends only a little more. Bondholders are implicitly holding a levered claim on GDP, financed by an effective short position in an inflation-indexed bond. Under the +0.5pp scenario, revenue overtakes spending around 2035 — the government moves from persistent primary deficits to persistent surpluses.

## The valuation: how big is the bet?

Lustig et al. take the CBO's 30-year baseline (real GDP growth of 1.8%/yr), apply CBO-implied elasticities, and roll the debt forward under alternative growth scenarios. Real interest rates rise with productivity using the CBO's own pass-through (the rules-of-thumb workbook implies that a permanent −0.1pp productivity shock reduces the 10-year Treasury rate by 1.2bp in year 1, ramping to 10.9bp by year 10 — close to full pass-through Δr ≈ Δg in the long run). The terminal value is calibrated so that the baseline reproduces the actual $32.1T market value of debt.

| Scenario | PDV(S) | TV* | Fundamental Value | ΔVal | Implied Δy | Debt/GDP 2055 |
| --- | --- | --- | --- | --- | --- | --- |
| CBO Baseline | −$12.5T | $44.6T | $32.1T | — | — | 172% |
| AI +0.1pp | −$11.2T | $44.6T | $33.4T | +$1.3T (+4.2%) | −71bp | 162% |
| AI +0.5pp | −$5.9T | $44.5T | $38.6T | +$6.5T (+20.2%) | −344bp | 124% |

The +0.5pp scenario — a growth rate only modestly above the post-2000 average — completely changes the fiscal trajectory: debt-to-GDP stops exploding and stabilizes. The CBO's own May 2025 alternative-scenarios analysis is consistent: it projects that 0.5pp of higher productivity growth would reduce the 2055 debt-to-GDP ratio by 43 percentage points (156% → 113%). This is one of the largest "knobs" in the long-run U.S. fiscal outlook, and it sits in productivity, not in tax or spending policy.

Implied yield changes use the weighted-average duration of the Treasury portfolio (70.4 months / 5.87 years, from the December 2025 TBAC presentation): Δy = −(ΔVal/D₀)/Duration.

### Where the gain comes from

The structural decomposition is the surprising part. In the +0.1pp case, the entire $1.3T gain comes from within-horizon surpluses (improving from −$12.5T to −$11.2T). The terminal value is essentially flat — higher GDP raises the nominal terminal surplus, but higher discount rates almost exactly offset the gain (with Δr = Δg, the Gordon denominator r − g is unchanged, so TV* scales with GDP level only).

The effective duration of the cash-flow stream is **36.8 years**, well past the 30-year projection horizon. Under the baseline, *all* of the $32.1T market value of debt is collateralized by the terminal value; the within-horizon PDV is *negative* $12.5T. Productivity shocks therefore work primarily by reducing the bondholder's reliance on the post-2055 terminal claim, not by inflating its size.

### Without the rate pass-through

Holding discount rates fixed at the baseline (no CBO pass-through) inflates the gains substantially: the +0.1pp scenario delivers $2.5T instead of $1.3T, and the +0.5pp scenario delivers $13.3T instead of $6.5T. The difference is concentrated in TV*: when rates stay low, GDP-scaled post-horizon surpluses are capitalized at unchanged rates and TV* rises with the GDP level. The CBO pass-through is the conservative assumption.

### Yield-decline feedback loop

If the market actually prices in the fiscal windfall, falling yields reduce the government's interest expense, which feeds back into the surplus path. Phasing the yield decline in linearly over 10 years brings the +0.5pp 2055 debt-to-GDP ratio down to **91%** — far below the 124% path that holds yields at baseline.

### Channel decomposition of the implied yield move

[Gómez-Cram, Kung, and Lustig (2025)](https://www.nber.org/papers/w33604) study high-frequency Treasury reactions to CBO cost estimates and find that 39% of the yield response runs through expected inflation, 44% through nominal term premia, and 17% through convenience yields. Applying these shares to the +0.1pp scenario's 71bp implied move gives ~28bp from lower inflation expectations, ~31bp from compressed term premia, and ~12bp from higher convenience yields — all three channels move the right direction in the observed event-study data.

## The Jones-Tonetti scenario: timing matters

The baseline assumes AI raises the growth rate *permanently*. [Jones and Tonetti (2026)](https://web.stanford.edu/~chadj/) argue that complementarities among production tasks ("weak links") prevent AI-driven automation from permanently raising growth, even as it generates large level effects. In their calibration, output is only 4% above baseline by 2040 and 19% by 2060 — back-loaded.

Lustig et al. approximate this with a smooth GDP path (+0.5% by 2030, +4% by 2040, +15% by 2055):

| Scenario | ΔVal | Implied Δy |
| --- | --- | --- |
| Permanent +0.5pp (15% GDP gain by 2055) | +$6.5T | −344bp |
| Jones-Tonetti (15% GDP gain by 2055, back-loaded) | +$1.5T | −81bp |

Same terminal GDP level. Vastly different fiscal value. The JT terminal value falls from $44.6T to $41.7T because elevated within-horizon discount rates (reflecting contemporaneous growth) reduce the 30-year discount factor by 19% — more than offsetting the 15% terminal-GDP gain. Early surpluses barely improve under back-loading because the growth boost arrives after 2040.

The implication: **the fiscal bet is not just on whether AI will raise productivity, but on how soon**. Investors valuing Treasuries through this framework are betting on the timing of AI's productivity impact, not just its magnitude.

## The convexity: an embedded call option on AI

Because revenue scales as GDP^1.07 — a power function with exponent above one — the fundamental value of debt is a *convex* function of productivity growth. A +1pp shock raises value by ~108%; a −1pp shock only lowers it by ~87%. The asymmetry means bondholders gain from *uncertainty* about productivity, not just from higher expected growth.

| Growth uncertainty (σ) | Convexity gain | % of D₀ | Implied Δy |
| --- | --- | --- | --- |
| ±0.1pp | +$0.03T | +0.1% | −2bp |
| ±0.2pp | +$0.11T | +0.4% | −6bp |
| ±0.5pp | +$0.71T | +2.2% | −38bp |

A mean-preserving spread in growth expectations of ±0.5pp is worth $0.71T in convexity value alone — even if AI doesn't raise *expected* growth at all, an increase in *uncertainty* about its productivity impact still lifts Treasury prices. Treasuries embed a long call option on AI; the call has positive value even when the strike is out of the money.

## What could go wrong: the political-economy risk

The whole framework runs on the 1.07 revenue elasticity, which depends entirely on the progressive bracket structure. Two directions of risk:

**Tax cuts.** If AI-driven surpluses materialize, Congress may cut rates, flatten brackets, or index brackets to wage growth (which would eliminate real bracket creep). The 2017 TCJA already lowered rates and widened brackets; the 2025 extension debate centered on making those provisions permanent. The historical precedent is clear — EGTRRA (2001) and JGTRRA (2003) eliminated the projected late-1990s Clinton-era surpluses within a couple of years.

**Tax hikes.** Less discussed: if rising debt forces Congress to raise taxes — higher marginal rates, a VAT, a wealth tax, a carbon tax — the effective revenue elasticity could *rise* above 1.07, amplifying the AI bet's payoff to bondholders. This scenario makes the long-AI position even more favorable.

**Asymmetric political economy.** When growth generates surpluses, pressure to cut taxes is strong. When growth disappoints, pressure to raise taxes is weak. The effective revenue elasticity over a full business cycle is therefore probably *below* the statutory 1.07: Congress captures the upside but does not offset the downside. Bondholders betting on AI growth are also betting that Congress will *not* fully dissipate the windfall through tax cuts.

A conservative robustness check (Table 8 of the paper) lowers the revenue elasticity from 1.07 to 1.0 after year 10. The result barely moves: +0.1pp delivers $1.3T in both cases; +0.5pp falls only from $6.5T to $6.1T. Most of the bet is robust to bracket-creep erosion in the second decade.

It's worth noting how this connects to broader U.S. tax-code dynamics. As [[buy-borrow-die]] shows, the existing tax code already allows the wealthiest beneficiaries of asset appreciation to opt out of the income-tax system entirely; if AI-driven gains accrue disproportionately to capital owners (via stock appreciation rather than wages), the actual revenue elasticity could undershoot the 1.07 figure even *without* explicit tax cuts. The model assumes a representative-agent income distribution; reality may not deliver one.

## Why this matters

Reframing Treasuries as a productivity claim has four substantive consequences:

1. **The empirical puzzle dissolves.** Falling yields on AI news become price-consistent rather than evidence of disbelief. The Andrews-Farboodi finding is exactly what you should observe if the productivity-beta framework is right.
2. **Debt sustainability is more growth-sensitive than the standard `r − g` framing suggests.** Growth enters twice: through cash flows (via revenue elasticity) and through discount rates. A 0.5pp productivity acceleration is a much bigger fiscal event than the textbook framing implies, and dwarfs any plausible legislated change to discretionary spending.
3. **Treasury investors are implicitly making a political bet.** The framework's load-bearing assumption is that progressive bracket structure persists. Historically it hasn't, when faced with surpluses. This is an underexplored channel of fiscal-policy risk in long-duration sovereign debt valuation.
4. **Timing matters as much as magnitude.** The Jones-Tonetti exercise shows that two scenarios with the *same* terminal GDP gain (15% by 2055) can deliver wildly different bond payoffs ($6.5T vs $1.5T) depending on whether the growth is front- or back-loaded. Implicit Treasury bets on AI are bets on AI's productivity timeline, not just its existence.

## Sources

- Lustig, Hanno, Howard Kung, and James Paron (2026). "U.S. Treasury Investors' Massive Bet on AI." *The Two Cents.* <https://thetwocents.substack.com/p/us-treasury-investors-massive-bet> — [[2026-04-23-treasury-investors-ai-bet|local copy]]
- Kung, Howard, Hanno Lustig, and James Paron (2026). "U.S. Treasury Investors Are Long in AI." Working paper. <https://www.dropbox.com/scl/fi/r4wo4iu96lh754rwsi3g3/bonds_long_ai.pdf> — [[2026-04-23-bonds-long-ai-paper|local copy]]

## Related papers

- Andrews, Isaiah, and Maryam Farboodi (2025). "Pricing Transformative AI." MIT working paper.
- Chow, Trevor, Basil Halperin, and J. Zachary Mazlish (2025). "Transformative AI, Existential Risk, and Real Interest Rates." Working paper.
- Gómez-Cram, Roberto, Howard Kung, and Hanno Lustig (2025). "Can U.S. Treasury Markets Add and Subtract?" NBER WP 33604. <https://www.nber.org/papers/w33604>
- Gómez-Cram, Roberto, Howard Kung, Hanno Lustig, and David Zeke (2025). "Fiscal Redistribution Risk in Treasury Markets." NBER WP 33769. <https://www.nber.org/papers/w33769>
- Jiang, Zhengyang, Hanno Lustig, Stijn Van Nieuwerburgh, and Mindy Z. Xiaolan (2022). "Measuring U.S. Fiscal Capacity Using Discounted Cash Flow Analysis." *Brookings Papers on Economic Activity* 53(2), 157–229.
- Jiang, Zhengyang, Hanno Lustig, Stijn Van Nieuwerburgh, and Mindy Z. Xiaolan (2024). "The U.S. Public Debt Valuation Puzzle." *Econometrica* 92(4), 1177–1215.
- Jones, Charles I., and Christopher Tonetti (2026). "Past Automation and Future A.I.: How Weak Links Tame the Growth Explosion." Stanford working paper.
- Miller, Max, James D. Paron, and Jessica A. Wachter (2025). "Sovereign Default and the Decline in Interest Rates." NBER WP 34021.
