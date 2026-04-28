---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2019-01-18-schumpeter-on-strategy.md
compiled_at: 2026-04-27
model: claude-opus-4-7
confidence: medium
---

# Entrepreneurial Profit

Joseph Schumpeter's model of how some entrepreneurs earn returns above the cost of capital — and why most don't. VC Jerry Neumann's recapitulation of the relevant chapter from Schumpeter's *Theory of Economic Development* (1911/1934) argues that this single model is the underlying generator of most of mainstream business strategy: Porter's generic strategies, sustainable competitive advantage, blue oceans, and the BCG growth-share matrix all fall out of it as corollaries.

## The three-part argument

**1. At equilibrium, profit is competed away.** "Profit" here is *surplus* profit — anything above the risk-adjusted cost of capital (which Schumpeter treats as a real input cost, not a residual). If a firm produces the same output from the same inputs as competitors, prices and costs equalize and surplus disappears. Critically, the founder is also an input: as manager, they earn the wage their job commands, no more. There is no automatic premium for being the boss.

The empirical version: Scott Shane's *The Illusions of Entrepreneurship* shows that across the middle eight income deciles, entrepreneur income equals employee income for the same work. Median revenue of an owner-managed firm is ~$90K, 81% of founders have no growth ambition, and most start firms in already-crowded industries with no claimed competitive advantage. Shane's diagnosis of motive: "Most people start businesses simply because they don't like working for someone else."

**2. Surplus profit comes from innovation only.** Schumpeter's model permits exactly two routes to entrepreneurial profit: get the *same* output for *less* input (efficiency innovation), or get *more/better* output for the *same* input (value innovation). Anyone earning surplus profit is doing one of these or both. Anyone not innovating is, by definition, not earning entrepreneurial profit — they're earning a wage.

**3. The profit decays.** Once an innovation is visible, imitators enter and bid the surplus away. The entrepreneur's lifetime profit is the area under a decay curve: the *height* is the size of the innovation, the *width* is how long imitation takes. Both matter; total realized value is the integral.

Neumann's stylized diagram has three notional shapes: the height of the spike (size of innovation), the rate of decay (speed of imitation), and the area under the curve (lifetime entrepreneurial profit). All of mainstream strategy can be read as ways to enlarge one of those three.

## Why this generates most of business strategy

Once you accept the model, mainstream strategy follows mechanically. Neumann walks through the correspondences:

| Strategy concept | Schumpeterian translation |
|---|---|
| Porter's **cost leadership** | The efficiency-innovation route — same outputs from cheaper inputs |
| Porter's **differentiation** | The value-innovation route — better outputs from same inputs |
| Porter's **focus** | A precondition for getting to one of the other two within a sector |
| **Sustainable competitive advantage / moat** | Slowing the decay curve so the area under it grows |
| **Experience curve** ("learning by doing") | Continuously refining the innovation faster than imitators can catch up |
| **Blue ocean / positioning** | Choosing a slot of the attribute space where no one else competes — temporary monopoly until imitators arrive |
| **Regulatory moats** (IP, licensing, brand-as-IP) | Legal slowing of imitation |
| **BCG growth-share matrix** | Portfolio management of innovations at different points on their decay curves — pour cash from cows into stars, kill dogs |

This connects directly to the [[competitive-moats|moat taxonomy]] (network effects, focus, operational specialization, scalable infrastructure): every moat is, in this model, a mechanism for slowing the decay of an innovation's surplus. It also clarifies what [[strategy-execution|Vermeulen's "coherent set of choices"]] is *for* — coherent choices are the way a real strategy enlarges one of the three dimensions (height of spike, slowness of decay, or sequencing of multiple curves at the corporate level).

The framing also subsumes [[aggregation-theory|Aggregation Theory]] and [[data-content-loops|data content loops]]: both describe specific, durable mechanisms by which a particular kind of innovation (zero-distribution-cost demand aggregation; SEO-fueled industry indexing) produces a slowly-decaying excess-profit curve. Calling them "moats" is the moat-taxonomy view; calling them "innovations whose imitation is slow" is the Schumpeterian view. Same phenomenon.

## Two fundamentally different kinds of startups

Neumann's most operational observation: the word "startup" papers over two phenomena that share almost no economic structure.

**Type 1 — job replacement.** Most "entrepreneurs." Started because the founder doesn't want to work for someone else. Earns roughly the same income they'd earn as an employee doing the same work. No innovation, no surplus profit, no scale ambition. Valuable to *the founder* (autonomy, self-actualization) but not, on average, a vehicle for excess economic value creation.

**Type 2 — Schumpeterian.** Started to capture entrepreneurial profit via innovation. Responsible for most net new jobs, fundamentally new products, and aggregate productivity growth. Valuable to *society* — and these are the startups VCs back, policymakers want more of, and the press writes hagiographies about.

The two share a surface form (a small new firm) and almost nothing else. Conflating them, Neumann argues, leads to bad analysis everywhere:

- **Press confusion.** Articles about "declining entrepreneurship" don't usually distinguish the two — and the trends often diverge. Type 1 fluctuates with labor markets and credit; Type 2 fluctuates with technology cycles, capital markets, and basic-research funding.
- **Policy confusion.** Encouraging Type 1 (let people work for themselves) and encouraging Type 2 (produce world-leading high-growth companies) require different levers. Neumann's separation:
  - **For Type 1:** less regulation, universal healthcare (decoupling insurance from employment), small-business credit infrastructure. Most people will start Type 1 firms if you simply *let* them — they don't need to be motivated.
  - **For Type 2:** basic research funding, affordable higher education (not just STEM) to reduce student-debt-induced risk aversion, better understanding of what makes these companies succeed.
- **Founder self-confusion.** Neumann notes he started a Type 1 firm (a venture fund) but spends his days around Type 2 founders, and sometimes catches himself confusing the two roles. He'd earn similar money as an employee at someone else's fund — the founding decision is about autonomy, not surplus capture.

This split clarifies what [[organic-startup-ideation|Paul Graham's "live in the future, build what's missing"]] is selecting for: it's a Type-2 ideation discipline. The "well" metaphor (narrow + deep demand, with a path out) is essentially "find a small high-spike innovation in a market structure where the decay curve will be slow." Graham's framework is silent on Type 1 because YC isn't financing Type 1.

It also reframes [[startup-ideation-framework|Lyon's seven-step ideation framework]]: most of its filters (market growth, willingness to pay, founder-market fit, capital efficiency) are mechanisms for finding Type-2-shaped opportunities. A Type-1 founder doesn't need most of them — they need a job they like.

## What the model does not give you

The Schumpeterian model is generative for *strategy*, but Neumann acknowledges (implicitly) that it has limits as a how-to:

- **It doesn't tell you which innovations are tractable.** The model says "innovate," but the hard problem is recognizing where the prepared mind plus the leading-edge field intersect. That's the territory of [[organic-startup-ideation|Graham's organic ideation]] and the [[four-kinds-of-luck|preparation-luck]] view of opportunity recognition.
- **It doesn't tell you how the surplus is distributed.** Neumann notes the area-under-curve gets "somehow split between" founders, employees, and financiers — but the actual division is governed by negotiation, market power, and labor-market dynamics that the model doesn't address. (In practice this is what cap tables, comp design, and VC term sheets fight over.)
- **It assumes one innovation per curve.** Real firms run portfolios of overlapping curves; the corporate-level BCG move (sequence innovations so the next spike begins before the last decays out) is mentioned but not formalized.
- **The decay rate is exogenous.** The model treats imitation speed as a property of the innovation; in reality firms invest heavily to *slow* it (the moat-building activity). Once you endogenize the decay rate, "competitive advantage" is itself an ongoing activity, not a static property of the innovation.

## The "entrepreneurial profit" lens vs. the "venture returns" lens

A useful translation exercise: VC return distributions are the empirical shadow of Schumpeter's curve.

- The fat power-law tail of fund returns is the height of the spike for the rare large innovations.
- The long-duration nature of those returns is the slowness of the decay curve (Google, Amazon, Apple all sit on innovations whose decay has been measured in decades).
- The fact that most funded startups return zero is the Schumpeterian prediction that imitators or non-innovators bid surplus to nothing — even with venture capital backing, a non-Schumpeterian startup is still a non-Schumpeterian startup.

This is why Neumann (a VC) finds the model so explanatory: it tells him that what he's actually buying when he writes a check is the right shape of decay curve. If the startup isn't innovating, no amount of capital makes the curve appear.

## Temporal notes

The essay is from 2019; the underlying Schumpeter is from 1911/1934. Two updates worth flagging:

- **The decay curves have gotten faster in some sectors and slower in others.** Software-distributed innovations decay quickly (anything app-shaped is copied within months). Network-effect-protected innovations (social, marketplaces, search) have decay measured in decades. AI foundation models present a current open question — see [[ai-platform-moats|Evans's argument]] that they may not have the decay-slowing structure of true platforms, in which case the entrepreneurial profit will be transient regardless of the spike's height.
- **The Type-1/Type-2 conflation is, if anything, worse.** "Solopreneur," "creator economy," and "indie hacker" framings have given Type 1 a glossier vocabulary without addressing the substantive distinction; "unicorn" and "decacorn" have done the same for the high end of Type 2. The middle of the distribution — small-but-genuinely-innovating firms — remains under-theorized in both popular and policy discourse.

## Sources

- Neumann, Jerry (2019). "Schumpeter on Strategy." *Reaction Wheel*, January 18, 2019. <https://reactionwheel.net/2019/01/schumpeter-on-strategy.html> — [[2019-01-18-schumpeter-on-strategy|local copy]]
