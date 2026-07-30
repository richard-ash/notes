---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-06-04-imas-trammell-what-remains-scarce.md
compiled_at: 2026-07-30
model: claude-opus-5[1m]
confidence: medium
---

# Labor share under automation

Roughly 60% of everything the economy produces has been paid out to humans as wages for as long as national accounts have existed, and the other 30–40% to owners of machines, land, and corporate claims. That constancy is one of the Kaldor facts. The central question of AGI economics is whether it survives.

Alex Imas (Chicago / Google DeepMind) and Phil Trammell (Epoch / Stanford), in conversation with Dwarkesh Patel, argue that the intuitive answer — a machine economy is a closed loop that leaves humans a shrinking sliver — is *not* obviously right, and that the actual determinant is a demand-side parameter nobody has measured.

## The Kaldor fact is more surprising than it looks

Imas stresses that ~60% surviving the entire Industrial Revolution is genuinely strange, strange enough that some economists suspect it is an accounting artifact. There is a live controversy over whether labor share has fallen in the last 20–30 years; Imas notes Atkinson's finding that holding the accounting conventions constant across decades, labor share has not fallen at all.

Trammell's explanation is that **nothing has ever been fully automated**. The right measure is the *network-adjusted factor share*: not how much of the final assembly step is done by capital, but how much labor is embedded down the entire supply chain, including the labor that built the machines that automate the final step. Computer and electronic products in the US have a network-adjusted capital share of about 50% — stable, and nowhere near one.

Both agree the qualitative shift now coming is that **some goods will have network-adjusted capital share equal to one**: the whole supply chain automated, with no step where anyone intrinsically wants a human involved. This is the first time in economic history that becomes possible, which is why the historical record's reassurance is weaker than it appears.

## Why the implication is ambiguous

Split the economy into a human-intrinsic sector (the ballerina) and everything else. Fully automate everything else. Two forces then run in opposite directions:

- **Satiation.** The quantity of non-ballerina goods goes to infinity, but if marginal utility in that stuff falls to zero *faster* than quantity rises, spending reallocates to the ballerina and labor share rises. This is the [[ai-and-relational-scarcity]] / [[structural-change]] channel: income effects push consumption toward what stays scarce.
- **Increasing variety.** If automation keeps inventing genuinely *new* categories of capital-produced goods faster than we satiate in the old ones, we never reach the diminishing-marginal-utility point. You can have all the relational goods you want and labor share still goes to zero.

Trammell's illustration is a Mongolian economist in 1400 holding varieties fixed in both categories. They would predict satiation in yurts, yogurt, and horse-transport, and conclude that everyone's income would end up going to singers. Instead the non-singer category expanded without bound and the singer share stayed negligible. That is Trammell's central (though hedged) prediction for AGI too.

**The transistor precedent cuts the same way.** Transistor count has grown perhaps a quadrillion-fold, yet Chad Jones finds the share of the economy spent on computing has been *falling*. Imas offers the pessimistic reading of Moore's law: every 18 months the value of computation halves — we run out of uses for compute so fast that price declines are what sustain the law rather than the reverse.

What makes AI possibly different is that this may have just stopped being true. An H100 costs more to rent today than three years ago, despite vastly more and better compute existing, because smarter models raised the *opportunity cost* of a compute-hour. That is the increasing-variety mechanism visible in a price. If demand for compute never satiates, compute's share of the economy keeps rising — and that is exactly the world where labor share goes to zero.

## The missing data

Imas's strongest practical claim: **we cannot answer any of this because the data does not exist.** No consumer demand elasticities, no tracking of which jobs are being created or destroyed, and an O\*NET task database that is rarely updated and low quality. He calls for a "Manhattan Project for data."

The specific measurement he wants for the relational sector is a conjoint analysis: present the same good produced entirely by machine versus with one task left to a human, and elicit incentive-compatible willingness to pay. Without that elasticity, the relational-sector story is a scenario, not a forecast.

His methodological recommendation follows: stop making point forecasts. A Fradkin–Jabarian–Koh survey found economists disagreeing about AI labor-market effects in every direction. Better to work backwards — assume labor share is zero, ask what model generates it; assume labor share is constant, ask the same — and use the resulting scenario map to decide what data to collect. (For aggregation, he prefers prediction markets over individual expert forecasts; compare [[reference-class-forecasting]].)

## The greedy-optimizer channel

The most novel argument in the conversation is that labor share may be determined not by average preferences but by the preferences of whoever fails to satiate.

Take two people equally rich today. One satiates in capital and also enjoys human-intrinsic services. The other doesn't satiate in capital at all — they want to explore the universe, build mass drivers on the moon, turn their head into a galaxy brain. If both are rational, the non-satiating one has the higher savings rate, so **in the long run they own most of the wealth, and the economy-wide capital share converges to the capital share of *their* spending, which is one.**

You do not need to invent this preference. Zuckerberg could direct Meta to convert its earnings into dividends and consume them; instead he compounds and builds data centers. Musk is the wealthiest person alive and largely indifferent to whether his future engineers are human. Imas concedes the point conditional on the premise but pushes back on the premise: intrinsic preference for pure accumulation is not how preferences usually work — hedonic and status motives satiate, as Rousseau and Augustine both noticed — and the observed historical pattern is accumulate-then-spend.

Trammell's rebuttal is that the exceptions *do* exist today and have simply been erased by **dissipation shocks**: the titan dies, heirs steward the capital worse than the economy grows, or the fortune goes to a foundation that spends it. Remove the shock — through longevity, or through trusts genuinely aligned to accumulation — and a handful of non-satiating agents is enough, because their share compounds faster than everyone else's.

Trammell adds instrumental routes to near-unsatiable demand that don't require the intrinsic taste: arms races over political, philosophical, or religious influence; and classical-utilitarian philanthropy, where more wealth means more happy beings created (Bostrom's astronomical waste).

**The AI extension.** Selection favors entities that grow. An autonomous AI (or an AI-composed firm) that reinvests everything outcompetes one that spends on human-intrinsic goods, and Imas says he has no prior at all that such an entity would prefer to transact with humans. The limit case is a von Neumann probe — a pure greedy optimizer whose marginal valuation of a solar system is high precisely because it converts into more solar systems.

Trammell flags that this becomes partly an accounting question: GDP counts final consumption and investment goods, so whether a self-owning probe shows up as economic activity at all depends on conventions we have not written. His answer to "is high labor share possible in a von Neumann probe world?" is a deadpan *yes — the way we usually count it.*

Note the direction of the argument: it says the future's production mix is set by whoever compounds fastest, which is a stronger and stranger claim than ordinary inequality worries. It is [[cumulative-advantage]] applied to preferences rather than to products, and it sits underneath the asset-side story in [[scarce-assets]].

## Why demand collapse is unlikely

Imas wrote a piece responding to Citrini's viral scenario in which AI automates white-collar work, removes those salaries from circulation, and produces a recession. His method was to assume negative growth and derive the necessary conditions. They turn out to be very demanding:

1. Income and wealth reallocate from labor-earners to capital owners (plausible), **and**
2. Capital owners' demand is *hard-bounded* — not merely diminishing, but a genuine ceiling where they say "I don't want to spend any more," **and**
3. That unspent money does not re-enter as investment.

Condition 3 is where it breaks. A world with a singularity in which nobody wants to fund another data center or fab is incoherent. The Depression produced demand collapse *without* a expanding technological frontier; here the frontier is expanding, and generating negative growth out of abundance is very hard.

There is a subtlety Trammell raises against the reassuring version of this. Historically, investment had to be *titrated through human labor* — funding a factory meant hiring people to build it, which is why the investment boom since 1820 kept employment and labor share high. In a robotic economy only consumption remains human-mediated; investment does not route through humans at all. So "the rich will invest instead of consuming" is no longer automatically a wage story.

## Relative prices, not output

A recurring correction Trammell makes: macro models that treat output as a single substance allocable one-for-one to consumption or capital will get this world wrong. What is coming is **investment-specific technical change** — the price of capital goods falling relative to consumption goods.

The consequence is that "the returns to capital must fall if labor share is high" is not straightforward. The capital stock can grow explosively while the *price* of capital goods falls even faster. Measured in robots, the interest rate could be 10,000% (one robot becomes a hundred next year) while the number of ballerinas stays fixed. The marginal utility of a ballerina performance is unchanged; the marginal utility of a robot collapses; so *in units of robots* we want ballerinas far more than we do now. Prices adjust — that is the whole point — and the standard single-output framing hides it.

## The messy middle

Molly Kinder's "messy middle" is the scenario where AI destroys enough jobs to be a political crisis without creating enough wealth to buy off the displaced.

There is a trivial sense in which the money must be there: whatever a firm saves by not paying humans still exists somewhere. The problems are **allocative** (the government cannot identify who was displaced by AI specifically) and **political** (a $200k/yr laid-off Meta engineer cannot be made whole with a $200k check while lower-paid people are still working). Andy Hall's observation that a 2 percentage point rise in unemployment flips the political winds is the operative constraint; COVID showed fiscal response can be fast, but only when the shock reads as an emergency.

Imas thinks the genuinely bad version is the **drip**, not the crash. His case study is telephone operators, 1920–1940: fully automatable for two decades before the transition completed, and the QJE work on it shows operators were reabsorbed — at lower salaries, largely underemployed. No mass unemployment statistic, no emergency framing, no fiscal response, just two decades of quiet downward mobility.

Both nonetheless think the scenario requires an unlikely conjunction:

- Automation must be *piecemeal by profession* — you can replace all software engineers but the same capability can't also replace accountants and analysts. Imas's model of intelligence says the breadth required for software engineering already spans most white-collar work.
- The replacement capital must cost *just barely less* than the labor it replaces, so there is saving but no abundance.

Both conditions must hold at once for there to be displacement without a growing pie.

## Current evidence: no white-collar bloodbath

As of mid-2026 the data shows very little. Imas points to Yale's Budget Lab: you have to squint. Even in software engineering — the most exposed sector — the only signal is junior developers hired *below trend*, not a level shift, with senior demand if anything rising. Anecdotes about CS graduates struggling are anecdotes; layoffs get relabeled as AI layoffs.

He flags a specific hazard in that relabeling: **AI adoption as a public coordination device**. If not laying people off reads as failing to adopt AI, firms cascade into layoffs to signal modernity — leaving the firm worse off than before. (The organizational pathology is documented at length in [[ai-mania]].)

The standard explanation for the absence of displacement is elasticity of demand. Automate nine of ten tasks in a job, the survivor specializes, the product gets cheaper, and if demand is elastic enough, hiring *rises*. Imas cautions that people invoke Jevons paradox as though it were a market law rather than a condition on elasticity. Coal in Britain, yes; software, plausibly. But oil, insulin, and food are not elastic — you eat enough and you're done. We could grow far more food with the share of the economy agriculture once commanded; we don't.

## O-ring reliability, in both directions

The O-ring model (one failed component destroys the whole product) explains why automation is slower than capability suggests: Gans and Goldfarb's result is that if you can automate nine-tenths of a job but only at lower quality, you may not want to automate any of it.

Patel's observation is that the same logic **reverses** at higher capability. Once production flows are organized around AI labor — communicating in neuralese, running thousands of times faster — a human's one-tenth becomes the component that drags down quality and speed. Even where comparative advantage says hire the human, transaction and reliability costs may make it infeasible to integrate one.

This is the mirror image of the bundle argument in [[messy-jobs]]: Garicano argues jobs survive because firms buy bundles that are expensive to separate; here the bundle re-forms around machines and *excludes* humans on the same integration logic. Note that it is a claim about production flows, not about consumer preference — it says nothing about the relational sector, where being human is the point.

Trammell treats the regulatory layer keeping humans in the loop — licensure, liability, judges, jurors, legislators — as **transitional**. What we require to come from a human has been reorganized many times, and once an AI-run political system is more efficient it will tend to outcompete the alternatives. This is a much more radical position than the residual-decision-rights argument in [[messy-jobs]], which holds that the institutional machinery of reputation and liability took centuries to build for humans and cannot be quickly rebuilt for machines.

## Designing the redistribution

Imas's framing: separate **how revenue is raised**, **what is taxed**, and **how it is distributed**. These are independent choices and conflating them produces bad arguments. The instruments differ on two axes — implementation complexity, and how quickly they start helping.

- **Negative income tax** — works the day it becomes law; provides an immediate floor.
- **UBI** — Imas's objection is political economy, not cost. Today we are endowed with labor convertible into income. If that ends and basic needs come from a check, the power-sharing arrangement between citizen and elected official becomes dangerous — it starts to matter enormously who holds office. (Patel's challenge — wouldn't that apply to any transfer program? — is fair and gets no clean answer.)
- **Universal basic capital** — the appealing property is that a share is *property*, not a benefit; you are simply a shareholder. Two problems: it generates nothing for years, so it cannot answer a six-month crisis; and it requires solving the **targeting problem** — what goes in the portfolio? If Anthropic goes to zero and an unknown robotics company takes over, universal basic capital delivers nothing. UBC is only as good as the indexing problem below.
- **Wealth tax** — Imas doubts a 0.5% wealth tax is a politically sustainable equilibrium. The income tax started low, for a war, and ratcheted to ~40% federal marginal (50%+ in some states). Expect the same drift.
- **Consumption tax (VAT)** — Trammell's preferred combination is raising broad-based revenue and using it to *buy* equity that is then distributed, rather than expropriating a specific firm. (The privatize-Social-Security proposal was structurally this: hand everyone a basket of stocks.) He explicitly worries about a populist alternative that expropriates whichever company happens to be famous.
- **Land value tax** — explicitly rejected as insufficient. Land is currently valuable because it's near other humans; strip out the relational component and it isn't the main factor of production in the future. A Georgist tax would not raise enough to fund any of these programs.

## Indexing AGI

For both developing countries and ordinary citizens in rich ones, the mechanism by which you get a claim on AI's gains without producing AI is **owning the index**. Both guests think this beats the reflexive recommendations — retraining programs, jobs programs, build-a-data-center — though Trammell would not rely on it alone, since in long-timeline or messy-middle worlds retraining leaves real value on the table. Imas's counterpoint: a country is often poor *because* its education system is poor, so "become world-class at retraining people on AI" is not a promising strategy for exactly the countries that need it. The optimistic case is leapfrogging — mobile banking is more prevalent in Nigeria than in Germany.

The obstacle is that indexing may be getting harder. A very small fraction of the economy has accounted for most value created over the past century; before index funds, capturing it was near-impossible. Imas's provocative framing is that there may have been a **brief golden window** — from the invention of index funds until roughly five years ago — during which an ordinary person could actually own the economy's growth rate. Returns are now concentrating in private companies the average person cannot access. It also explains why the Rockefeller heirs don't own everything: if the greedy-optimizer selection argument is right, the missing ingredient wasn't the preference, it was the *instrument*.

Trammell is less worried: still well under 20% of the total market cap of non-tiny US companies is private, the big labs will likely go public before long, and AI may itself dissolve the disclosure frictions that keep firms private. His guess is that the long trend toward easier indexing resumes.

The deeper question underneath is Imas's:

> **Is AI going to be like electricity, or like social media?**

Electricity is a monopoly resource everyone uses, and ConEd has no notable political or social power — the downstream benefits accrued to *users*, not the producer. Social media was equally ubiquitous, but the rents went to the platform. Patel's inference: the more you believe AGI transforms the whole economy the way electricity did, the more it looks like electricity — every future S&P company is in the index *because* it leveraged AI, so buying the index gets you the gains again.

Whether that holds depends on forecasting questions that look purely technical: how far behind the frontier open models stay (six months? nine?), and whether recursive self-improvement or continual learning produce runaway concentration. As Imas puts it, every question here is connected to every other one — and those technical questions determine whether Uganda has any purchase on the returns to AGI. This is the same value-capture question [[ai-value-capture]] and [[commodity-trap]] answer from the supply side; here it is asked from the position of someone with no supply-side leverage at all, for whom the only lever is a portfolio.

Patel's conclusion is that he now hopes the labs get commoditized, or at minimum go public quickly: AI will be more popular and more likely to broaden prosperity if capturing its gains is as hard as capturing the gains of electrification. Trammell's caution is the tech-race cost — safety may want fewer frontier firms, each with buffer to slow down. But he thinks the trade-off is smaller than assumed: a wide capability gap is compatible with widely distributed *ownership*, if the leader is public. Imas adds a political argument in the other direction: concentrated labs are a tangible, identifiable target for government coercion, as the Defense Production Act threat against Anthropic showed. Diffuse the capability and the threat is much harder to make.

## What to watch

The conversation is structured as a scenario map rather than a forecast, and its useful output is a short list of load-bearing branch points:

1. **Does compute demand satiate?** Watch whether compute's share of GDP keeps rising. Falling share means the transistor precedent holds and the increasing-variety story wins. The H100 rental price is the current counter-evidence.
2. **Is the relational elasticity large?** Requires the conjoint data nobody has collected.
3. **Do the non-satiating actors keep compounding?** Watch whether dissipation shocks (mortality, heirs, foundations) weaken — longevity and accumulation-aligned trusts are the tells.
4. **Does indexing get easier or harder?** Private share of total market cap; whether the labs go public.
5. **Electricity or social media?** Open-model lag behind the frontier is the proxy.

Note that (1) and (2) determine the *size* of the human sector, (3) determines whose preferences set the production mix, and (4)–(5) determine whether the distributional problem is solvable with a portfolio or requires a tax. They are largely independent, which is why the space of outcomes is wide and why neither guest offers a point forecast.

## Sources

- Imas, A., Trammell, P. & Patel, D. (2026). "The better AI gets, the smaller its share of the economy might get." *Dwarkesh Podcast*. <https://www.dwarkesh.com/p/alex-imas-phil-trammell> — [[2026-06-04-imas-trammell-what-remains-scarce|local copy]]
