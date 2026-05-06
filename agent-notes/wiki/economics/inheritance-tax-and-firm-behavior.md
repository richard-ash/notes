---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-04-06-sweden-inheritance-tax-abolition.md
compiled_at: 2026-05-05
model: claude-opus-4-7
confidence: medium
---

# Inheritance tax and firm behavior

Most policy debate over inheritance and gift taxes argues about the *static* question — "who keeps the wealth at death?" Andric, Genedy and Nordqvist (2026) reframe the question as *dynamic*: how does the *anticipation* of an inheritance tax shape decisions made decades before any succession event? Their empirical answer, drawn from Sweden's 2004/2005 abolition of the gift and inheritance tax, is that the tax was not just transferring wealth at death — it was reshaping how owner-managed firms were *run* in the meantime.

## The natural experiment

Sweden's parliament abolished the inheritance tax effective January 1, 2005 (decision made December 2004). Pre-abolition rates for close relatives were 10–30% marginal; for distant relatives or non-relatives, historically up to 50–60%. The base was the recipient's net acquisition.

The authors exploit this as a natural experiment using yearly population data from Statistics Sweden (the LISA individual registry plus RAMS firm financials), covering ~37,000 owner-managed Swedish firms, tracked 2001–2007.

The identification trick is the choice of control group. The treated group is owner-managed firms whose owner-manager has **children aged 12–30** as of 2003 — old enough that succession conversations are starting, young enough that the children's careers are not locked in. The control group is firms whose owner-managers have **no children at all**. The argument: childless owner-managers will *have* to sell or close eventually regardless of the tax regime, so the inheritance tax abolition is irrelevant to their strategic decisions. The two groups are then matched on owner-manager age via Coarsened Exact Matching (CEM) to net out life-cycle confounds. Difference-in-differences with firm fixed effects.

## What changed when the tax went away

By 2007 (three years post-abolition), treated firms had grown faster than control firms across every dimension measured (all numbers are difference-in-differences in 2007 vs 2003 baseline):

| Outcome | Treated minus control |
|---|---|
| Net sales (log) | +8 pp |
| Total assets (log) | +4 pp |
| Fixed assets (log) | +4 pp |
| Current assets (log) | +6 pp |
| Equity (log) | +7 pp |
| Debt-to-equity ratio | −0.29 |
| Operating margin (EBIT) | +0.4 pp in 2004–2005, dissipates by 2007 |
| Sales per employee | +52 (in absolute SEK thousand) |
| Corporate taxes paid (log) | +10 pp |
| Total salaries paid (log) | +12 pp |

The pre-trends are flat — no detectable treatment-control divergence in 2001–2003 — and the wedge opens cleanly in 2004 onwards.

## The mechanism the authors propose

The story is about *capital extraction discipline*. Pre-abolition, owner-managers anticipating succession had to pre-fund the heir's future tax bill by extracting cash from the firm — typically via dividends — into personal savings. That cash leaves the firm and stops being available for reinvestment.

Post-abolition, the same owner-manager can leave the cash inside the firm, reinvest it, grow the asset base, hire more, and hand the firm over intact. The financial signature is exactly what the authors find: equity rises, leverage falls, fixed *and* current assets accumulate, and productivity (sales per employee) climbs.

Andric et al. argue this is also a *temporal-horizon* shift. When the tax was in place, owner-managers behaved more like the childless control group — running the firm for their own career. Once succession became financially feasible, they extended their planning horizon to a transgenerational one and started behaving like family-firm dynasts.

## The fiscal jiu-jitsu

The most policy-relevant finding is on tax revenue. Sweden gave up the one-time inheritance tax on these firms. But:

- Corporate taxes paid by treated firms grew **10 pp faster** than control by 2007.
- Total salaries (and thus payroll/social contributions) grew **12 pp faster**.

The authors phrase this carefully: *"the reform could have altered the timing and structure of taxation rather than eliminating it entirely."* In other words, the inheritance tax was not pure incremental revenue — some of it was substituting *for* corporate and payroll tax revenue that would have existed had the firm been allowed to grow.

This is structurally similar to the [[copyright-and-innovation|Tabarrok-curve]] argument: a policy that looks redistributive on its face can sit past its revenue-maximizing point if it suppresses the underlying activity it taxes. The mechanism is different (capital extraction vs. innovation incentive) but the meta-pattern — "the tax destroys part of the base it taxes" — is the same.

It also intersects [[treasury-productivity-beta|productivity beta]] logic: when tax revenue elasticity to firm size is above one, faster firm growth disproportionately offsets revenue lost from a transfer tax.

## The capital extraction channel as a general phenomenon

The paper's framing — that inheritance tax forces *forward* capital extraction — generalizes. [[buy-borrow-die]] documents the opposite endpoint of the wealth-transfer-tax design space in the U.S.: a system that taxes inheritance only weakly and offers step-up in basis, which encourages the wealthy to *retain* assets and borrow against them rather than realize gains.

The two papers together suggest a continuum:
- **High inheritance tax + low income/capital gains tax** (Sweden pre-2005, UK historically): forces capital extraction *before* death via dividends to pre-fund the bill. Concentrates extraction in productive operating firms.
- **Low inheritance tax + step-up in basis** (US): rewards holding assets indefinitely and never realizing. Concentrates avoidance in passive holdings.

Neither equilibrium is obviously revenue-maximizing or growth-maximizing. The Swedish data suggests the *form* of the wealth tax shapes which firms get starved of reinvestment capital.

## What to be skeptical of

The paper is from the SSE Center for Family Enterprise — a research group whose institutional mission is the study of family firms. The framing is sympathetic to the abolition. A few things a careful reader should note:

1. **The control group's cleanness is doing a lot of work.** Childless owner-managers may differ from owner-managers with children in many unobserved ways — risk tolerance, time preference, willingness to plan long-term, even firm-type (capital-intensive vs services). CEM matches only on age. Robustness checks adding gender are mentioned but not fully reported.

2. **The operating margin effect dissipates by 2007.** Sales-per-employee productivity holds up; profitability does not. This is glossed over in the conclusion, but it raises a question: is the growth real efficiency-driven scaling, or is it scale-driven sales growth at flatter margins that happens to coincide with reinvested capital?

3. **Three years is short.** "Transgenerational value creation" is a 30-year claim being supported with three years of post-reform data.

4. **No M&A or exit data.** A firm that "grows" in net sales by 8 pp but ultimately gets sold to a foreign acquirer is a different policy outcome than one that survives intergenerationally. The authors flag this as future work.

5. **The 2008 financial crisis is the next data point.** The window cuts at 2007 — right before the global financial crisis. Whether treated firms' lower leverage protected them or whether the higher fixed-asset accumulation made them more vulnerable is exactly the kind of dynamic that would test the "long-term horizon" claim, and it isn't here.

That said, the result that capital extraction obligations distort firm capital structure is mechanically obvious — equity goes up, debt-to-equity falls, capital stays inside the firm — and the magnitudes are sensible. The harder claim — that this translates into faster real growth and offsetting tax revenue — is the part that depends on the identification assumptions.

## Why this matters beyond Sweden

The question keeps coming back. Norway's 2022 wealth tax hike triggered a wave of relocations to Switzerland. The UK is debating non-dom and inheritance reforms. Australia and New Zealand have already abolished inheritance taxes. The Swedish dataset is unusual in offering population-level firm financials that span an exogenous policy change with no obvious parallel reform — which is rare.

The authors' headline framing — that inheritance tax shapes not only *whether* firms survive but *how* they are run — is a useful reframe of the debate. Policy discussions tend to focus on either (a) wealth concentration (the egalitarian frame) or (b) capital flight of the very rich (the libertarian frame). The Andric et al. finding is that there is a third channel that affects neither billionaires nor oligarchs but the median ~6.6 MSEK Swedish founder-led firm: a steady extraction of capital out of mid-sized productive operating businesses, year after year, into personal savings accounts where it sits unproductive instead of being reinvested.

If that channel is real and the magnitudes generalize, then the question becomes whether the inheritance tax is even doing the redistributive work it's defended on — or whether it's mostly destroying the operating capital base of the firms it touches, with the actual dynastic-wealth concentration happening through the very different channels (passive holdings, private equity, [[buy-borrow-die]]) it doesn't reach.

## Sources

- Andric, M., Genedy, M., & Nordqvist, M. (2026). "The Impact of Abolishing the Gift and Inheritance Tax on Firm Strategic Decisions and Outcomes: The Case of Sweden." *Stockholm School of Economics — House of Innovation White Paper, April 6, 2026.* <https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6528658> — [[2026-04-06-sweden-inheritance-tax-abolition|local copy]]
