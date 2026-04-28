---
source: agent
compiled_from:
  - agent-notes/raw/business/marketing/2014-05-17-distribution-marketing-sales.md
  - agent-notes/raw/business/marketing/2017-06-09-distribution-horowitz.md
compiled_at: 2026-04-27
model: claude-opus-4-7
confidence: medium
---

# Distribution Strategy

A framework for how startups and operators should think about getting products to customers — drawn from Tren Griffin's curation of Peter Thiel, Marc Andreessen, Jeff Bezos, Fred Wilson, Bill Gurley, and Larry Ellison, plus Ben Horowitz's operational framework for designing a channel around product and target. Central thesis (Thiel): **poor distribution, not poor product, is the number one cause of business failure.** Most companies that "build it and they will come" never come. Horowitz's complementary thesis: when distribution does fail, it usually fails because founders chose a channel from temperament rather than deriving one from the product and customer in front of them.

## Distribution as a moat

Distribution is not just a cost of doing business — it can be the durable advantage. Griffin highlights McDonald's, Starbucks, Amazon, and Costco as companies whose [[competitive-moats|moats]] derive substantially from physical and logistical distribution systems rather than from product differentiation. The product is fine; the *delivery* is unmatched. This is a key class of moat that engineering-led founders systematically undervalue.

## The engineer's blind spot

Thiel and Andreessen converge on a specific founder pathology: technically excellent teams assuming customers will line up for a great product. When pushed, these founders try "everything but the kitchen sink" — sales, BD, advertising, viral marketing — without committing to any single channel. Andreessen frames this as the "no distribution strategy / viral marketing strategy" failure mode: refusing to acknowledge that a real channel must be picked and made to work.

Griffin's prescription: send engineers and managers on actual sales calls, or have them spend a day in the call center. The empathy gap closes fast, and product insights surface in the process.

## Channel as a function of product and target

Horowitz proposes the design discipline: **`f(p, t) = c`** — channel is the *output* of a function whose inputs are the product and the target. Founders who reverse this — picking a channel because they admire Drew Houston's viral-growth story or because they personally dislike enterprise sellers — are imposing personality preferences on a problem with a structural answer. With multiple products or multiple targets, you may need multiple channels.

Horowitz formalizes two product dimensions:

- **Delivery:** (A) online (Github, Dropbox, Workday) or (B) physical / in-person (smart watch, security camera).
- **Onboarding assistance:** (A) none (Github, Slack), (B) minor (Okta), or (C) major / professional services required (Palantir, Pivotal, Oracle Financials).

A given product's classification depends on the *customer*. A small business buying Slack is `[A, A]`. A large enterprise buying the same Slack — needing migration, integration, compliance — is `[A, C]`. Horowitz notes this is the typical trajectory for products that begin with viral departmental adoption and end up enterprise-wide.

He classifies targets by *decision-making process*, not org size:

- **I. Individual** — consumer or single corporate decision maker.
- **II. Small group** — small engineering team (Trello, ATS).
- **III. Small company (<1000)** — multiple stakeholders, clear deciders (Zenefits).
- **IV. Large group** — multiple decision makers with different economic and technical motivations.
- **V. Multiple groups simultaneously** — e.g., sales *and* marketing must both agree (marketing automation).
- **VI. Entire large company** — long, multi-stakeholder process (Workday-class purchase).

The non-obvious move is treating decision-making process as the primary axis. A business that buys like a consumer *is* a consumer for distribution purposes. The reverse follows: **you cannot change the customer's buying process — you can only design a channel that meets it.** Targets IV-VI are especially hard because the customer themselves doesn't know who will sign off; an HR system might be bought once a decade, and no playbook exists. Much of the field rep's actual job is helping the customer *construct* the buying process.

The channel-design rules that fall out:

- **Targets I-II + `[A, A]` / `[A, B]`:** marketing, viral, optional telesales. Tractable.
- **Targets I-II + `[A, C]` / `[B, C]`:** "God help you" — cost of sale exceeds deal size. Structural mismatch; the business should not exist in this configuration.
- **Target III:** human in the loop required even for self-serve products, to navigate stakeholders and frame buying criteria. `[A, C]` / `[B, C]` still typically uneconomic.
- **Targets IV-VI:** field sales reps walking hallways. With an `[A, C]` product the rep is essential — the customer expects one and will not trust a complex technical decision without one.

Horowitz's case studies illustrate the framework: **Dropbox** won targets I-II with a brilliant `[A, A]` product and viral distribution, then *had* to build a direct sales force for `[A, C]` enterprise customers — its mature reality is multiple channels, not one. **Box** built the field sales channel Dropbox initially refused to, capturing IV-VI from the start. **Workday** could have sold by phone but chose a high-end sales force because target VI demands it. **Zenefits** matched target III efficiently with telesales.

The corresponding sales-force shapes are distinct disciplines: **viral marketing** (product design that enhances forwarding), **inside sales** (telesales), and **direct sales** (field reps on customer sites). They are not interchangeable, and a company often needs several, deployed against different (p, t) pairs.

This is the operational counterpart to Griffin's "engineer's blind spot": don't pick a channel from temperament — derive it from the product and target you actually have.

## The distribution spectrum and the dead zone

Thiel maps customer acquisition along a spectrum based on transaction size:

- **Right end (high-touch enterprise):** large ticket items justify a human-driven sale. Field sales, account executives, long cycles.
- **Left end (mass market):** small ticket items justify advertising, mass marketing, and self-serve channels.
- **The middle (the dead zone):** small businesses and mid-market customers that are too small for field sales but too distrustful or fragmented for mass advertising. Many great products die here because **no distribution channel reaches them economically.**

Crack the dead zone — typically by inventing a novel low-cost channel — and Thiel argues you may have "a terminal monopoly business." This sits alongside Griffin's "stuck in the middle" warning: medium-sized businesses lack the scale economies of giants and the differentiation focus of niche players.

## Organic vs. paid acquisition

Fred Wilson's heuristic: **early-stage companies should acquire customers for free.** Spending kicks in only after the product has demonstrated organic pull. Bezos's reformulation: in the old world, 30% product / 70% shouting; in the new world, that inverts — a great product gets talked about for free.

Bill Gurley adds the harder economic claim: organic users have higher NPV, higher conversion, lower churn, and higher satisfaction than paid-acquired users. The implication is that paid spend is not just more expensive up-front; it produces a structurally inferior customer cohort. This connects to [[capital-discipline|capital discipline]] — companies that scale paid acquisition before organic pull is proven tend to obscure unit-economic problems with growth, then collapse when the funding cycle turns.

The corollary is that most early-stage paid-acquisition spending isn't buying growth; it's buying *the appearance of growth* for the next fundraise.

## The LTV trap

Griffin reports a 2014 cycle (still recurring in every cycle since) in which marketing teams used lifetime-value (LTV) models to justify essentially unbounded spending. The argument: if LTV exceeds CAC, every dollar of marketing is positive ROI. The problem: LTV is a *projection*, churn is *correlated* with the channel that acquired the user, and cohort assumptions break under scale. Paying CAC against an inflated LTV and then watching the cohort underperform is a common path to running out of cash.

Griffin's framing: spend is a "Goldilocks" determination. Too little leaves a network-effects market for a competitor to win when it tips. Too much, and you die of cash exhaustion before reaching escape velocity. There is no general answer; only a per-business judgment informed by cohort data, market dynamics, and runway.

## Cheap brand impressions

Rich Barton's law (as formulated by Griffin): **the number of cheap brand impressions rises with the square of the amount of controversial or interesting metadata produced.** Zillow exemplifies this — releasing per-zip-code real estate data that the press repeats endlessly, with each repetition serving as a free brand impression for Zillow.

The general principle: many companies sit on a byproduct dataset or analysis that the public would consume for free. Releasing it converts a cost center into a customer-acquisition channel. This is structurally different from advertising — instead of paying to interrupt attention, you produce content that *is itself* the attention. Kwok's [[data-content-loops|deeper analysis of the Barton playbook]] generalizes this — across Expedia, Zillow, and Glassdoor, the same data that powers brand impressions is also the kernel for a per-entity SEO land grab and the basis for an eventual demand-side network effect.

## Loss leaders and multi-sided seeding

Thiel's PayPal anecdote: advertising was too expensive, BD failed, so PayPal paid users to sign up — literally giving away money. This worked because PayPal was a multi-sided market (payers and payees) with a chicken-and-egg coordination problem. Without seeding one side, neither side joins.

The general lesson: in markets with strong network effects, the early CAC may legitimately exceed marginal economics, because what's being purchased isn't a customer — it's the seed of a flywheel. The risk is that founders without genuine network effects use this argument to justify burning cash that will never compound.

## Sales as a craft

Thiel's claim about salespeople parallels the well-known one about engineers: top performers are dramatically more valuable than average ones, with a long tail of below-average performers in between. Great salespeople are rare and underpriced — a top performer's compensation is high but typically below their marginal contribution. Ellison's complement: in a great company, *everybody* sells, including engineers who must often participate in technical sales.

Ellison's other observation cuts the other way: no salesperson can rescue a product the user already dislikes. **Quality is a precondition for distribution effectiveness, not a substitute for it.** Distribution amplifies whatever the product actually delivers.

Horowitz adds the channel-shape dimension: viral marketing, inside sales, and direct sales are *different jobs*, and a real distribution strategy may require building and managing more than one in parallel. Relying on a product's inherent virality is fine for some segments but is "not a complete channel strategy" — it leaves larger customer segments unaddressed.

## Connections

[[competitive-moats]] — distribution systems are one of the four moat classes Griffin identifies; this article elaborates the distribution-specific dynamics.

[[aggregation-theory]] — Thompson's framework explains how zero-cost digital distribution inverts the value chain: aggregators that own the demand side commoditize supply. This is what made the "dead zone" of distribution narrower for digital products but wider for many physical/SMB markets.

[[capital-discipline]] — Stitch Fix's playbook of restraint is the operational counterpart to Wilson and Gurley's warnings about paid-acquisition overreach.

[[cultural-imprinting]] — Simler's mechanism explains *why* mass-market advertising works (or doesn't) at the left end of the distribution spectrum: it requires shared awareness, which fragmented digital channels struggle to produce.

## Temporal notes

Published in 2014. Three durable shifts since then:

- **The dead zone has narrowed for digital-first products** but widened for SMB software requiring relationship-based selling. Self-serve PLG (product-led growth) channels — barely a category in 2014 — now span much of the former mid-market gap.
- **The LTV trap has recurred at larger scale.** The 2020–2022 venture cycle saw growth-at-all-costs companies (Casper, Peloton, many DTC brands) collapse in exactly the pattern Gurley described, validating the original warning.
- **Network-effect "winner take most" markets are now widely understood,** which was less obvious in 2014. The Thiel/Griffin point about needing to grow fast in tipping markets is now received wisdom.
- **AI-era distribution.** Foundation model and AI-product distribution increasingly runs through existing platform aggregators (App Store, ChatGPT GPT Store, browser defaults), making distribution risk *more* concentrated, not less.

## Sources

- Griffin, Tren (2014). "A Dozen Things I've Learned About Marketing, Distribution and Sales." *25iq*, May 17, 2014. <https://25iq.com/2014/05/17/a-dozen-things-ive-learned-about-marketing-distribution-and-sales/> — [[2014-05-17-distribution-marketing-sales|local copy]]
- Horowitz, Ben (2017). "Distribution." *a16z*, June 9, 2017. <https://a16z.com/distribution/> — [[2017-06-09-distribution-horowitz|local copy]]
