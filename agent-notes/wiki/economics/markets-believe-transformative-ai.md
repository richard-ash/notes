---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-05-06-markets-believe-transformative-ai.md
compiled_at: 2026-05-06
model: claude-opus-4-7
confidence: high
---

# Do markets believe in transformative AI?

Isaiah Andrews and Maryam Farboodi run the canonical event study: across 17 major frontier-model releases from OpenAI, Anthropic, Google DeepMind, xAI, and DeepSeek in 2023-4, US Treasury yields, TIPS, and corporate bonds **fall** by 10+ basis points at long maturities around each release, and the decline persists for ~15 trading days. The pattern is statistically significant on direction (median change) but not on magnitude (median absolute change) — markets are not reacting *more* on these days, they are reacting *consistently downward*. Interpreted through a complete-market, representative-agent consumption-based asset pricing model, this implies that on average each release led investors to revise downward either (i) expected consumption growth, or (iii) the probability of extreme "doom" (existential risk) or "bliss" (post-scarcity) outcomes — but not (ii) consumption growth uncertainty, since the forward curve **level** shifts and the **slope** does not. Cumulated over 15 releases, the implied effect is roughly 3.12 percentage points off either annual growth expectations (under log utility) or the annual P(doom/bliss). This reading puts Andrews and Farboodi in direct dialogue with the alternative fiscal-channel reading in [[treasury-productivity-beta]]: same yield decline, opposite verdict on what markets believe.

## The empirical fact

Across 17 model release dates (Bard, ChatGPT 4, Claude 1-3.5 Sonnet, Grok 1-2, Gemini Pro 1.0-2.0, DeepSeek V2-V3, o1, plus a few intermediate releases), Andrews and Farboodi document:

- **Long-maturity Treasury yields fall ~10+ bp.** Median changes are statistically significant for 20- and 30-year nominal Treasuries (p = 0.054 and 0.038 at ±15 days) and 30-year TIPS (p = 0.038). Effects are not significant at 1- and 5-year maturities.
- **Corporate bond yields fall in tandem.** ICE BofA corporate bond yields show significant declines at every maturity bucket from 3-5 years up to 15+ years.
- **Corporate spreads do not move.** The decline is fully explained by the Treasury baseline, not by changes in credit risk.
- **The dollar depreciates.** Consistent with falling US rates pulling capital flows.
- **Effects begin 2-5 days *before* official release** and persist 15+ days after — consistent with documented pre-release access for outside experts.
- **No change in yield change *magnitude*.** Median absolute changes are not statistically distinguishable from placebo. So markets aren't surprised *more* on AI release days; they're being moved *in a consistent direction*.

This last point is the one Andrews and Farboodi flag as unexpected. If markets were taking transformative AI seriously, they would have predicted larger-than-average yield *moves* on release dates without a strong directional prior. Instead they got a clear *direction* without a magnitude effect — markets were responding consistently the same way each time.

The robustness battery is unusually thorough for an event study with only 17 events: dropping any one date preserves significance at most horizons, dropping two or three preserves direction; placebo distributions drawn from FOMC meetings, tech earnings, CPI/jobs/retail-sales releases, and Treasury auction dates all reject the null; controlling for the Citigroup Surprise Index, VIX, and SF Fed news sentiment leaves results directionally similar.

## Why "doom" and "bliss" are the same thing in asset prices

The cleanest theoretical contribution is the observation that, under a complete-market representative-agent model with time-separable utility, **existential risk and post-scarcity are observationally equivalent**.

The setup follows Jones (2024) and Chow, Halperin, and Mazlish (2024): each agent has utility

E_0 [ Σ β^t (1{t ≤ T} u(C_t) + 1{t > T} U*_t) ]

where T is a random terminal date after which a "doom" or "bliss" event occurs, U*_t is the post-T flow utility, and crucially u' → 0 as c → ∞ (a standard assumption that follows from concavity of u). Andrews and Farboodi normalize U*_t = 0.

The stochastic discount factor is then:

M_{t,t+h} = β^h · u'(C_{t+h})/u'(C_t) · 1{t+h ≤ T}

The extreme scenarios — humanity going extinct (doom) or aggregate consumption diverging to infinity (bliss) — both enter through exactly one channel: the indicator 1{t+h ≤ T}. Both annihilate the marginal utility of future consumption. Doom does it because there is no consumer to consume; bliss does it because consumption is so abundant that an extra unit is worthless. From the SDF's point of view, these are the same event, so **no asset price can disentangle them**.

This is the rigorous version of an idea that floats around the AI discourse: "doom" and "singularity" beliefs both compress the relevant time horizon, and their asset-price footprints are identical. Andrews and Farboodi formalize the equivalence and use it as a principled reason why their analysis won't try to separate them.

The further implications fall out naturally:
- An increase in expected consumption growth → lower expected future marginal utility → higher real yields.
- A closer expected arrival of T (whether doom or bliss) → higher P(t+h > T) → higher yields (the bond is more likely to mature into a state where it doesn't matter, so it must offer a higher rate to be held).
- An increase in *uncertainty* about future consumption → precautionary saving → lower yields.

So the headline finding — yields *falling* on AI news — implies markets are revising *some combination* of: lower growth, higher uncertainty, lower P(doom or bliss).

## Forward curve level vs slope: pinning down the channel

Adopting CRRA utility u(C) = C^{1-γ}/(1-γ) and assuming log-normal AI growth shocks, Andrews and Farboodi derive a tractable expression for log forward yields. The key decomposition:

- The **slope** of the forward yield curve (with respect to maturity) tracks changes in growth *uncertainty* σ_t², scaled by −γ²/2. Uncertainty changes show up as slope shifts because consumption growth impacts compound over time — the variance of cumulative log-growth grows linearly in the horizon.
- The **intercept** captures both the change in the mean growth rate μ_t (scaled by γ) and the change in P(T not arriving in a given year), log(1−δ_t).

Empirically, regressing the difference-in-differences in log forward yields on (h − k) for horizons h ∈ {5,...,10}:

| Coefficient | Estimate | Placebo percentile |
|---|---|---|
| Slope | +0.0015 log points | 60.5th |
| Intercept | −0.208 log points | **1.5th** |

The slope is statistically indistinguishable from zero. **The yield decline is entirely a level shift.** Therefore, under the simplified model, growth uncertainty is *not* the channel: markets did not become more uncertain about AI's consumption-growth impact on these dates.

Backing out the level shift implies, depending on the relative weight of the two surviving channels:

| Scenario | Implied effect (per release, average) | Cumulated over 15 releases |
|---|---|---|
| All from P(doom/bliss): δ_t falls by | 0.208 pp | 3.12 pp |
| All from growth: μ_t falls by (γ = 1) | 0.208 pp | 3.12 pp |
| All from growth: μ_t falls by (γ = 2) | 0.104 pp | 1.56 pp |
| All from growth: μ_t falls by (γ = 5) | 0.041 pp | 0.62 pp |

These are economically large effects for plausible CRRA values. The observed yield response is consistent with markets becoming *less* convinced of transformative AI on each release — either because each release's marginal information dampens expected growth, or because each release narrows the implied P(extreme outcome).

## The Metaculus tiebreaker on "disappointing progress"

If yields are falling because markets are revising growth expectations downward, an obvious question is: did the releases *disappoint*? Were they good for AI capability progress but bad for the consumption-growth implications, or vice versa?

Andrews and Farboodi pull AI-progress forecasts from Metaculus around the same event dates. Two questions:

1. **Weak AGI** (Winograd Schema 90%+, SAT math 75th percentile, Turing test, Montezuma's Revenge from <100 hours play, single unified system): the median forecast date *moves earlier* around model releases, statistically significantly. The 25th percentile shifts earlier *before* the release; the median shifts after.
2. **First AGI** (more demanding criteria): no significant shift; if anything, the forecast *recedes* slightly.

End-of-2024 forecast medians: weak AGI in March 2027, AGI in August 2033 — a six-year gap.

The takeaway: at least the Metaculus crowd was *positively surprised* about near-term AI progress around these releases. So the bond-yield decline is not a "disappointing progress" story. It's harder to read into AGI itself, but the more demanding question shows no movement, which Andrews and Farboodi suggest may indicate that participants thought model releases were informative about weak AGI specifically but not about the deeper progress required for AGI.

This complicates the simplest reading. If progress was positively surprised but yields went down, then under the simplified model investors must be revising P(doom/bliss) down rather than expected growth down — they updated *toward* a more incremental, less explosive trajectory. Or alternatively: the consumption-based asset pricing model is wrong, and the yield drop reflects something the model can't capture (institutional risk-management flows, term premium changes, fiscal channels).

## Where this sits relative to the productivity-beta reframe

The same yield-decline observation gets a different interpretation in [[treasury-productivity-beta]]: Howard Kung, Hanno Lustig, and James Paron argue that Treasuries are implicitly long productivity growth via the fiscal channel (revenue elasticity of 1.07 vs near-zero spending elasticity), so falling yields on positive AI news is the *expected* response, not a puzzle. Andrews and Farboodi's complete-market consumption-based reading and the Kung-Lustig-Paron fiscal reading produce diametrically opposite conclusions from the same event-study facts:

| | Andrews-Farboodi | Kung-Lustig-Paron |
|---|---|---|
| Treasuries are | risk-free assets | levered claim on GDP |
| Yields fall because | growth expectations or P(extreme) fall | future surpluses rise (PV of debt rises) |
| Implication | markets are skeptical of transformative AI | markets are pricing in transformative AI |
| Convexity in growth | no — symmetric | yes — embedded long call on AI |

Andrews and Farboodi flag this as a caveat: their first listed alternative interpretation is that Treasuries are not a reasonable risk-free proxy. Their counter — corporate bond yields also fall, and corporate spreads don't widen, so the Treasury-default-risk story would require corporate risk premia to move in tandem — partially addresses but does not eliminate the Kung-Lustig-Paron channel. Kung-Lustig-Paron's response, conversely, is that the consumption-based representative-agent model is exactly the kind of fully-optimizing complete-market benchmark that fails when applied to sovereign debt with a non-trivial default option.

The two readings can both be right at different horizons: short-run, Andrews-Farboodi's complete-market intuition gives one answer; long-run, the fiscal channel dominates. Which is closer to how marginal investors actually price these bonds is unresolved.

## Caveats Andrews and Farboodi flag

The paper is unusually candid about its own limitations:

1. **Treasuries may not be risk-free.** Inflation risk and US default risk could mean falling yields reflect lower risk premia, not changed growth/scenario beliefs. Their corporate-spread evidence weakens but does not eliminate this channel — the [[treasury-productivity-beta]] fiscal reading lives in this caveat.
2. **Event dates may be non-representative.** The selected release dates could capture downward updates while AI news on other dates pushed yields up. Hard to argue this prima facie since all major model releases from the universe of frontier labs are included, but cannot be ruled out empirically.
3. **The model may be misleading.** Complete markets, representative agents, time-separable expected utility — none of these are strictly true. Asset-manager risk-management constraints, market frictions, behavioral effects, and segmented-market dynamics could all generate the observed yield decline through channels orthogonal to investor beliefs about AI.

The third caveat is the most serious: the model has to do a lot of work to translate "yields fell" into "markets revised P(doom/bliss) down by 0.208 pp per release," and any deviation from the benchmark could in principle reverse the sign of the implied belief update. Andrews and Farboodi's response is essentially that *something* large is moving in one of the deepest financial markets in the world around these dates, and even an alternative explanation would be of interest in its own right.

## Why this paper matters

Three contributions worth tracking:

1. **The empirical fact is now the load-bearing stylized fact in the AI–macro debate.** The 10+ basis point Treasury yield decline around frontier model releases is what every subsequent paper in this space cites, including [[treasury-productivity-beta]] and the Chow-Halperin-Mazlish theoretical work on transformative AI and real interest rates.
2. **The "doom = bliss" equivalence is a clarifying theoretical move.** It explains why empirical work on AI risk premia cannot, even in principle, distinguish the two extreme scenarios using asset prices alone — and why papers that try to should be read with skepticism.
3. **The level-vs-slope decomposition rules out the uncertainty channel.** This is more useful than the headline level estimate because it constrains the space of stories: whatever explains the yield decline, it is *not* "investors got more uncertain about AI's growth impact." That removes a popular narrative in one regression.

The headline result — that markets, viewed through this lens, look *skeptical* of transformative AI — is in tension with both the Metaculus crowd's positive update on near-term progress and with the productivity-beta reading. Reconciling these requires either rejecting the consumption-based model, accepting that bond markets are dominated by something other than belief-updating about AI, or concluding that markets believe in *progress* but not in *transformation* (i.e., that AI gets better but doesn't move long-run consumption growth or extreme-outcome probabilities). The first interpretation is what [[treasury-productivity-beta]] formalizes; the third is the most parsimonious reading consistent with both the bond data and the Metaculus data.

## Sources

- Andrews, Isaiah, and Maryam Farboodi (2025). "Do Markets Believe in Transformative AI?" NBER Working Paper No. 34243. <https://www.nber.org/papers/w34243> — [[2026-05-06-markets-believe-transformative-ai|local copy]]
