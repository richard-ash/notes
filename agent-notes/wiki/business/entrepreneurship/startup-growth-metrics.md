---
source: agent
compiled_from:
  - agent-notes/raw/business/entrepreneurship/2026-04-16-investor-metrics-deck.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: medium
---

# Startup Growth Metrics

An investor-grade framework for decomposing, evaluating, and stress-testing startup growth — drawn from Andrew Chen's 80-slide deck that landed him the General Partner role at Andreessen Horowitz in 2018.

## Growth Accounting

The foundational move is to stop staring at an aggregate MAU curve and decompose it:

**Net MAU = New users + Reactivated users − Inactive users**

This equation reveals what a top-line graph hides. A startup can show growth while its inactive cohort quietly approaches a crossover point. Chen warns: "When your New + Reactivated equals your Inactive users each period, you hit peak MAUs" — after which the curve plateaus or declines regardless of acquisition spend.

The implication for founders: present growth in decomposed form before investors do it for you. Hiding behind a blended curve is itself a signal.

## Acquisition Loops

Chen categorizes acquisition into four channel types, ranked by scalability and defensibility:

1. **UGC-SEO loops** — user-generated content feeds search indexing, which drives new users who create more content (Yelp, Reddit, Glassdoor). High defensibility once the flywheel spins.
2. **Paid marketing loops** — ad spend drives signups whose LTV funds more ad spend. Scalable but fragile to CAC inflation and platform risk.
3. **Viral loops** — each user invites or exposes others, measured by a viral coefficient. Powerful when k > 1 but rare outside social products.
4. **Linear channels** — PR, conferences, partnerships. Useful for early traction but do not compound.

### Red flags in acquisition

- **Channel concentration** — heavy reliance on a single platform is brittle. Chen cites Branchout's collapse from 14M to sub-1M DAU within months after Facebook algorithm changes.
- **Quality inflation** — new low-quality channels juicing signup numbers ahead of a fundraise.
- **Inconsistent ad spend** — spiky paid acquisition that appears only in the months before a raise signals optimization for optics rather than fundamentals.

## Engagement Loops

Acquisition means nothing without retention. Chen identifies three engagement archetypes:

- **Social feedback loops** — require sufficient network density and low-friction content creation (likes, comments, shares pulling users back).
- **Seed-planting models** — the user plants a seed during onboarding (a Zillow home alert, a Credit Karma credit-score tracker), and the product triggers future visits via personalized notifications.
- **Real-life triggers** — usage tied to physical-world moments ("I'm lost" → open maps). These are defensible because the trigger is external and habitual.

### Measuring engagement quality

- **Cohort retention curves** — D1 / D7 / D30 retention, with the critical question being whether the curve flattens (users retained long-term) or asymptotes toward zero. A curve that flattens above ~20% generally signals product-market fit.
- **Notification analysis** — volume, click-through rates, and opt-out rates. High volume with low CTR is a red flag (the product is nagging, not engaging).
- **Frequency distribution** — how users progress from single use-case to multi use-case engagement. Expanding use cases per user is a strong signal.

Chen shares a telling Uber anecdote: early on, "only unhappy riders rated the app," producing an average of 1.7 stars. Once Uber prompted all riders post-trip, ratings jumped to 4.7 — a change worth millions of incremental downloads. The lesson: measurement artifacts can mask true engagement.

## Building Forecasts

Chen argues against single-line projections and for scenario-based models that combine:

- Acquisition growth potential with specific, documented optimization opportunities
- Engagement cohort curves with realistic activation improvements
- Platform dependency risks and their downside scenarios

The goal is not prediction accuracy but structured conversation: "What has to be true for this business to work?" grounded in product mechanics rather than pattern recognition.

## The Meta-Lesson

Chen emphasizes that "startups aren't spreadsheets." Metrics are symptoms of underlying product dynamics — loop quality, retention mechanics, channel defensibility. An investor who only reads the numbers misses the engine; a founder who only tells the story without the numbers lacks credibility. The framework bridges both.

## Sources
- Chen, Andrew (2018). "The Red Flags and Magic Numbers That Investors Look For in Your Startup's Metrics." <https://andrewchen.com/investor-metrics-deck/> — [[2026-04-16-investor-metrics-deck|local copy]]
