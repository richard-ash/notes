---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-06-22-solopreneur-economy.md
compiled_at: 2026-06-30
model: claude-opus-4-8[1m]
confidence: medium
---

# The solopreneur economy

A data-driven argument from Stripe economist Ernie Tedeschi (writing on the Stripe Economics blog, June 2026) that solo-operated businesses — "solopreneurs," firms that generate revenue without hiring employees — are forming faster, reaching higher income thresholds, and increasingly powered by AI. The piece triangulates US Census Bureau Business Formation Statistics, cross-country registration records, and Stripe's own platform data to make three claims: (1) solopreneurship is outpacing employer-business formation and the surge isn't fraud; (2) both the count and the *share* of solopreneurs crossing meaningful revenue thresholds are rising; (3) AI is filling the capability gaps that historically forced founders to hire.

## A measurement artifact, then a real trend

The story opens with a methodological footnote that matters. Until 2022 the Census Bureau auto-reclassified any business above a revenue threshold as an "employer," on the assumption that you couldn't earn that much solo. By the early 2020s solo operators were visibly clearing those thresholds without hiring, so the Bureau raised them — and counts of high-revenue *nonemployer* businesses jumped. Part of the "rise of the solopreneur" is thus the statistical system catching up to a reality it had been suppressing. Tedeschi's argument is that beyond this correction, the underlying phenomenon is genuinely accelerating.

## The surge, and why it isn't fraud

New business applications (filings with state agencies and the IRS that precede actual activity) reaccelerated from late 2024. Crucially, the Bureau's **"high-propensity" applications** — those its internal model flags as likely to hire within eight quarters, based on industry, EIN request, and planned-wages indicators — stayed flat. The growth is concentrated in businesses that don't intend to become employers.

This rhymes with the 2020 pandemic spike, which research ([Dinlersoz et al. 2021](https://www.aeaweb.org/articles?id=10.1257/pandp.20211055)) attributed partly to the Paycheck Protection Program: PPP required little more than an EIN, incentivizing low-intent filings. Tedeschi marshals four arguments that the *current* wave is different:

- **No subsidy this time.** PPP stopped accepting applications in May 2021; the last forgiveness payout was 2024. There's no comparable financial incentive to file frivolously now.
- **Faster time-to-revenue.** If recent cohorts were padded with inactive shells, they'd take *longer* to reach material volume. The opposite holds: the share of Stripe businesses hitting $1M cumulative revenue within a year of going live was ~30% higher for the 2025 cohort than 2023, and ~3x higher than 2019. Fraud doesn't transact.
- **It's global.** Business registrations since 2017 are up ~40% (Australia), ~70% (Finland), ~80% (France), accelerating in 2025. Acceleration across different regulatory regimes points to a fundamental driver, not jurisdiction-specific fraud. France's granular data shows the surge is microentrepreneurs, not employer firms — the US pattern again.
- **Intent-signaling geographies.** Delaware incorporations (the venue for founders raising institutional capital or building formal governance) grew ~40% YoY from early 2025 and have stayed above pandemic peaks. Wyoming, another deliberate-structuring jurisdiction, is growing fastest. Bad actors filing passive LLCs don't pick these.

The pattern of evidence is deliberately constructed to rule out the "it's just fraud / it's just shells" objection — the same skeptical move you'd want for any too-good administrative-data trend.

## Up the income distribution, not just the count

The more striking claim is about quality, not quantity. By 2023 roughly **four million Americans** earned their primary income as solopreneurs grossing over $100,000 — up from the mid-two-millions in the early 2010s, before Stripe/Substack/Kajabi-style infrastructure matured. Census data thins out at higher thresholds (NES methodology changes frustrate longitudinal study), so Tedeschi builds a **proxy index** from ~115 solopreneur-focused platforms plus all solo Stripe Atlas businesses. Caveats are stated plainly: it understates the true population (most solo operators use general infrastructure), may include non-solo businesses, and can't see firms that later hired.

Within that proxy, growth is *steeper at higher thresholds* and accelerating since 2023: more than 2x as many solopreneurs cleared $1M in 2025 vs 2023, and close to 3x as many crossed $5M and $10M. Most importantly, the **share** of solopreneurs above these thresholds also doubled — evidence against the "lots of lottery tickets, a few lucky winners" reading and toward genuinely higher-quality cohorts.

## AI as the mechanism

Tedeschi's causal story for *why now* is AI, and it operates on two levels:

1. **Discovery and integration (the measurable floor).** AI-assisted sign-ups now make up nearly 4x the share of Stripe sign-ups as a year prior. Stripe splits these into *direct* signals (using its MCP, CLI, or Claimable Sandboxes to build integrations) and *passive* ones (referrals/traffic from LLMs like ChatGPT recommending Stripe). Census BTOS data shows industry-level AI adoption correlates positively with nonemployer-application growth (with outliers: manufacturing down, transportation/warehousing up).

2. **Capability substitution (the larger, harder-to-measure effect).** The deeper reason businesses were historically built by *teams* is that no single person holds every skill — market sizing, coding, pricing, marketing, sales. AI fills these gaps, so motivation alone can now carry a solo founder. Sam Altman's phrase for this is "revenge of the idea guys." Tedeschi argues the ~20% AI-attributable figure is a **floor, not a ceiling**, precisely because this capability-substitution channel is the part the sign-up telemetry can't see.

This is the labor-economics crux and connects directly to [[task-automation-vs-paradigm-replacement]]: rather than AI automating tasks *within* the firm, it changes the optimal *boundary* of the firm — making the one-person firm viable where a multi-person firm was previously required. It is the supply-side mirror of [[messy-jobs]]: where Garicano asks which job *bundles* resist unbundling, Tedeschi observes the founder bundle being re-internalized into one person plus AI. It also sits alongside [[ai-and-the-future-of-work]] and [[markets-believe-transformative-ai]] as a near-term empirical signal of AI's economic footprint, and is the macro backdrop to the entrepreneurship-side argument in [[ai-native-company-building]] that solo or tiny teams can now run real companies.

## Reading notes

- **It's a Stripe house publication.** Two of the three data sources are Stripe's own, and the proxy index is constructed by Stripe. The conclusions flatter Stripe's business (more solo founders = more Stripe customers). The cross-country Census-style corroboration is the part that travels furthest beyond Stripe's interests; the income-threshold proxy is the most self-interested and should be read as directional.
- **Correlation, not identification.** The AI-adoption-vs-formation-growth link is a cross-sector correlation with admitted outliers, and the 4x AI-sign-up figure measures *association* with AI tools, not causation. Tedeschi is careful about this ("untangling this effect is not always easy") — the strong causal claim rests on the unmeasurable capability-substitution argument.
- **What "share doubled" implies.** If the *share* (not just count) of solopreneurs clearing high revenue is rising, the marginal new solopreneur is more productive than the average past one. That's the most consequential claim for anyone forecasting how concentrated economic output becomes — it suggests a fatter right tail of one-person firms, which has implications for [[scarce-assets]] (what stays scarce when production de-bundles) and the income distribution generally.

## Sources
- Tedeschi, Ernie (2026, June 22). "The age of the solopreneur." Stripe Economics. <https://www.stripeeconomics.com/p/the-age-of-the-solopreneur> — [[2026-06-22-solopreneur-economy|local copy]]
