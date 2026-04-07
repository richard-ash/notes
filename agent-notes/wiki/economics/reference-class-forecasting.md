---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-02-10-bayes-and-base-rates.md
compiled_at: 2026-04-06
model: claude-opus-4-6
confidence: high
---

# Reference Class Forecasting

Reference class forecasting is the practice of anchoring predictions about a specific case to the empirical base rate of a relevant reference class — the historical distribution of outcomes for similar cases — and then updating that prior as new evidence arrives. The technique operationalizes [[bayesian-reasoning|Bayesian reasoning]] for real-world planning and investment analysis.

## The core idea

Rather than building a forecast from the inside out (asking "what do we expect *this* project or company to achieve?"), reference class forecasting starts from the outside in: "what has the full population of similar cases actually achieved?" The inside view is then used to adjust the base rate up or down based on case-specific evidence.

Phil Tetlock's research on superforecasters — the top 2% of participants in the Good Judgment Project — found that exceptional forecasters don't formally apply Bayes' Theorem but embody its core insight: hold beliefs lightly and update them incrementally in proportion to the weight of new evidence. Starting from a base rate and updating is more reliable than starting from a narrative.

## Application to corporate growth forecasts

Mauboussin and Callahan (2026) apply this framework to AI company revenue projections using 75 years of Compustat/FactSet data on U.S. public companies (1950–2024).

### OpenAI

- **Forecast:** $3.7B (2024) to $145B (2029) — 108% CAGR over 5 years.
- **Reference class:** Companies with $2–5B in starting sales (~18,900 firm-period observations). Mean 5-year CAGR = 7.0%, standard deviation = 10.6%.
- **Result:** No company in this reference class has ever achieved 108% CAGR. The forecast is a ~9.5 standard deviation event under a normal approximation — effectively zero probability.
- **Updating factors:** ChatGPT reached 100M users in 2 months (vs. 9 months for TikTok, 28 months for Instagram). 2025 revenue expected at ~$13B (~250% YoY growth). But free cash flow was negative $9B in 2025 and expected to be negative $17B in 2026, with stock-based compensation exceeding 45% of sales.
- **Rolling forward:** Even using the 2025–2030 window ($13B to $200B, 72.7% CAGR), no company with starting sales above $6.5B has ever achieved that growth rate in the dataset (16,400+ firm-periods).

### Oracle Cloud

- **Forecast:** $10B (FY ending May 2025) to $166B (FY 2030) — 75% CAGR.
- **Reference class:** Companies with $8–12B in starting sales (~4,400 firm-period observations). Mean 5-year CAGR = 5.7%, standard deviation = 9.6%.
- **Result:** No company with $5.6B+ in starting sales has ever achieved 75% CAGR for five years.

### Key statistical note

The distribution of historical sales growth rates is not normal — it is leptokurtic (more peaked than normal, with fatter tails). This means the standard-deviation math slightly overstates the improbability, but the qualitative conclusion holds: these forecasts would be unprecedented.

## Application to mega-projects

The same base-rate logic applies to the infrastructure buildout required to deliver on AI growth forecasts. Bent Flyvbjerg's database of 16,000 large projects across 136 countries shows:

| Metric | Success rate |
|--------|-------------|
| On budget (or better) | 47.9% |
| On budget and on time | 8.5% |
| On budget, on time, and on benefits | 0.5% |

AI data centers face specific bottlenecks — access to power, specialized hardware (GPUs), and cooling requirements — that compound the base-rate risk. The Stargate Project alone anticipates up to $500B in AI infrastructure spending through 2029.

Flyvbjerg and Gardner advocate for **reference-class forecasting** as an explicit planning tool and a "think slow, act fast" approach: invest heavily in upfront planning to identify risks, then execute rapidly. They also note that modular designs have higher success rates than bespoke ones.

## Strategic signaling as a confound

Mauboussin and Callahan observe that some of the aggressive forecasts may serve a strategic purpose beyond genuine prediction. Drawing on Michael Porter's framework for capacity expansion decisions, they note the logic of **preemptive strategy**: committing major resources early to deter competitors and new entrants from investing.

This carries its own base-rate risk. Prior investment booms — notably the telecom buildout of the late 1990s — produced overcapacity and corporate bankruptcies. And preemptive strategies are especially fragile when competitors include both well-capitalized incumbents (Alphabet, Amazon, Meta) and well-funded startups (Anthropic, OpenAI, xAI) who may not be deterred.

As of the second half of 2025, global AI diffusion (share of people who have used a GenAI product) was only 16%, suggesting the market is still early but the gap between infrastructure investment and current adoption is wide.

## Practical takeaways

1. **Start with the outside view.** Before assessing any specific forecast, find the base rate for the relevant reference class. Even an imperfect reference class disciplines optimism.
2. **Update, don't replace.** Case-specific evidence (adoption speed, early revenue) should adjust the base rate, not override it entirely.
3. **Growth ≠ value.** Revenue growth only creates value when return on invested capital exceeds the cost of capital. Massive negative free cash flow and high SBC are material considerations.
4. **Execution risk compounds.** The probability of delivering on revenue forecasts must be multiplied by the probability of the underlying infrastructure being completed on time and on budget — and that second probability is historically very low.

## Sources

- Mauboussin, Michael J. and Dan Callahan (2026). "Bayes and Base Rates: How History Can Guide Our Assessment of the Future." Morgan Stanley Counterpoint Global Insights (Consilient Observer), February 10, 2026. — [[2026-02-10-bayes-and-base-rates|local copy]]
