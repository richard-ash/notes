---
source: agent
compiled_from:
  - agent-notes/raw/business/finance/2026-06-18-opportunities-and-expectations-pvgo.md
compiled_at: 2026-09-23
model: claude-fable-5-1
confidence: high
---

# Present Value of Growth Opportunities (PVGO)

The present value of growth opportunities is the part of a stock's price that is *not* explained by the company's current earnings continuing forever. Stewart Myers coined the term in 1977; the underlying decomposition goes back to Miller and Modigliani (1961). Price splits into two pieces:

1. **Steady-state value** — current earnings capitalized as a perpetuity at the cost of capital. Buffett's "bird in the hand."
2. **PVGO** — the value of the *option* to make future investments that earn more than the cost of capital. The "two in the bush."

Two words in the name do real work. "Growth" means value creation, not revenue growth: an investment that earns exactly its cost of capital adds nothing to PVGO no matter how much it grows the top line (the same discipline that runs through [[capital-allocation]]). "Opportunities" means these are options — the right, not the obligation, to invest — which is why PVGO is a real-options concept rather than a forecast.

Mauboussin and Callahan's June 2026 Counterpoint Global report treats **PVGO as a percentage of price** as a direct readout of expectations: a low share says the market expects little future value creation, a high share says it expects a lot. The report tests whether that readout predicts returns at the market level and the company level, and whether it beats the Fama-French value factor.

## The P/E heuristic

If current earnings persist, the steady-state P/E is simply 1 ÷ cost of equity. At the 8.75 percent cost of equity the authors use (close to Damodaran's June 2026 estimate), that is 11.4×. Any P/E above that is either PVGO, unsustainable current earnings, or a mix of the two — Leibowitz calls the same split "earnings power" versus "franchise value."

The S&P 500 traded at 21.9× consensus 2026 earnings on June 12, 2026. By this heuristic roughly 48 percent of the index price was PVGO (10.5 turns out of 21.9). The report's own year-end series, computed differently, says only that end-2025 was "well above" the long-run average.

The heuristic is only as good as the discount rate. Dropping the cost of equity from 8.75 to 7 percent moves the steady-state P/E from 11.4× to 14.3× and shrinks the implied PVGO share materially. Danbolt, Hirst and Jones (2002) found exactly this input sensitivity when re-testing Kester's 1984 company-level method.

## PVGO as a market-level gauge

**Method.** Trailing four-quarter S&P 500 operating earnings ÷ cost of equity (Damodaran's equity risk premium plus the risk-free rate), subtracted from the index price at each year-end, 1961–2025.

**Findings.**
- PVGO averaged 35 percent of price; steady state 65 percent.
- Near-zero PVGO in 1974 and 2011; very high in 1999 and 2001. End-2025 well above average.
- Subsequent 10-year total shareholder return (TSR) correlates at r = −0.26 with the starting PVGO share. Bottom-quartile starting points delivered 11.6 percent annualized, top-quartile 7.6 percent, the middle quartiles 11.2 percent.

The authors' verdict is that the signal is usable only at extremes and is "a poor tool for timing in general." They note that Javier Estrada (2022) found a much cleaner, monotonic relationship over 1872–2021 and that they could not replicate it — a useful flag that the strength of the result depends on data and method choices.

## PVGO at the company level

**Method.** Trailing 12-month NOPAT (adjusted for intangible investment, as in the authors' capital-allocation work) ÷ weighted average cost of capital, minus net debt, gives steady-state equity value. PVGO is whatever market equity value remains. Worked example: NOPAT $100 at 8 percent = $1,250, less $250 net debt = $1,000 steady-state; a $1,500 market cap implies $500 PVGO, or 33 percent.

**Findings, U.S. companies with market cap ≥ $1 billion (2024 dollars), 1990–2024:**
- Median next-5-year TSR was 8.7 percent for the lowest-PVGO quintile and 5.0 percent for the highest.
- The relationship is not monotonic: the *second* quintile had the highest median TSR. Again, extremes carry the signal.
- Splitting stocks into halves, the low-minus-high spread in five-year annualized TSR was positive in about 90 percent of formation years and averaged 2.6 percentage points.

Negative PVGO is possible and meaningful. It says the market values the company below its capitalized current earnings, which can mean current earnings are seen as unsustainable, that future investment is expected to destroy value, or both. The residual cannot distinguish these.

## Four company narratives

Company-level histories use a third variant of the method: consensus next-four-quarter earnings capitalized at the cost of equity, compared to the share price.

- **NVIDIA.** Despite being the largest company in the world by market cap, its PVGO share is *below* its early-2000s average and close to its end-2016 level. The stock's rise has largely tracked realized earnings and cash-flow growth rather than rising expectations.
- **Microsoft.** PVGO share went from 85 percent in 1999 to −53 percent in 2012 while the stock sat flat for a decade and sales and profits kept growing. It has rebounded since but remains well below the 1999 peak.
- **Amazon.** PVGO exceeded 100 percent of price through 2001 because the company was losing money (negative steady-state value). It has drifted lower ever since even as sales, profits and the stock compounded rapidly. Year-end 2025 was the lowest reading since the 1997 IPO.
- **JPMorgan Chase.** Same shape as the tech giants at much lower amplitude: a peak around 40 percent, substantially negative after the 2008–09 financial crisis.

The lesson the authors draw, without stating it as advice, is that a rising stock price and rising expectations are different things. Amazon and NVIDIA are cases of expectations being *met and absorbed into earnings*, so the PVGO share fell while the price rose. Microsoft 2000–2012 is the mirror image: earnings caught up to a price that had run far ahead, and the expectations component was ground down to below zero before the stock could move again.

## PVGO versus the value factor

The Fama-French value factor (HML) sorts on book-to-price, controlling for size, and goes long high book-to-price, short low. It is also an expectations measure, and it has worked poorly since the early 2000s. Lev and Srivastava (2022) attribute the failure to the shift from tangible to intangible investment, which makes book value an increasingly irrelevant anchor.

Over 1990–2024, the low-minus-high PVGO sort delivered five-year returns averaging 230 basis points above the value factor, and did so more consistently year to year.

The reason is structural rather than magical. PVGO anchors on capitalized, intangible-adjusted NOPAT — an income-statement measure that survives the intangibles shift — whereas HML anchors on the balance sheet, which does not. PVGO is effectively a value factor rebuilt on earnings power instead of book value.

## Implications

- **It reads the market, it does not forecast.** The PVGO share tells you what expectations are embedded in a price. Judging whether those expectations are achievable is a separate step — the base-rate discipline in [[reference-class-forecasting]], which Mauboussin and Callahan apply to AI revenue projections in a companion report, is the natural complement.
- **Growth-opportunity bias.** Shefrin (2014) and Gong et al. (2022) document that investors systematically overpay for PVGO. The persistent low-beats-high spread is consistent with that bias being priced in and slowly corrected.
- **Scale versus value creation.** Because PVGO only credits investment that clears the cost of capital, it is the market-price analogue of Damodaran's argument in [[scaling-vs-profitability]] that scale and profitability have different determinants. A company can scale enormously and add nothing to PVGO.
- **The AI capex bet, priced.** An S&P 500 PVGO share well above its 35 percent average at end-2025 is the equity-market expression of the required-return chain in [[ai-capex-required-returns]]: the upper rungs of that chain are, in the Geometric Investor's phrase, "paid in expectations," and PVGO is the line item where those expectations sit. [[markets-believe-transformative-ai]] shows the bond-market side of the same expectation.
- **Qualitative cousin.** Gurley's "optionality" factor in [[revenue-quality]] is the narrative version of PVGO: a business whose current revenue carries embedded options on adjacent markets should command a higher PVGO share, and deserves it only if those options earn above the cost of capital.

## Sources

- Mauboussin, Michael J. and Dan Callahan (2026). "Opportunities and Expectations: The Present Value of Growth Opportunities in Valuation." Morgan Stanley Counterpoint Global Insights (Consilient Observer), June 18, 2026. <https://www.morganstanley.com/im/en-us/financial-advisor/insights/consilient-observer/opportunities-and-expectations.html> — [[2026-06-18-opportunities-and-expectations-pvgo|local copy]]
