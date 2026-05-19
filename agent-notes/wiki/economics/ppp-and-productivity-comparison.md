---
source: agent
compiled_from:
  - agent-notes/raw/economics/2025-12-18-bergeaud-ppp-productivity-thread.md
compiled_at: 2026-05-13
model: claude-opus-4-7
confidence: high
---

# PPP and cross-country productivity comparison

When commentators compare US and European living standards, they almost always quote a number in "PPP-adjusted" terms — and the answer changes depending on which PPP they use. Antonin Bergeaud's December 2025 pedagogical thread walks through why this matters: **GDP per hour at constant PPP and GDP per hour at rolling PPP answer two genuinely different questions**, and the gap between them is itself the Balassa-Samuelson mechanism showing up in the data. Reading the gap correctly turns the "Europe is fine when you correct for prices" story on its head — a cheaper Europe is the mirror image of slower productivity growth, not evidence that everything is well.

## What a PPP actually measures

Exchange rates convert currencies but ignore that the same coffee, beer, or childcare costs different amounts in different countries. Purchasing power parities (PPPs) are designed to fix this by pricing a comparable basket of goods and services in each country, so that the resulting "PPP dollar" buys roughly the same bundle of stuff regardless of where it is spent.

A PPP of, say, 0.5 between France and the US means that for the reference basket, France is half as expensive as the US — a given dollar in France goes twice as far. When commentators say "PPP France/USA has fallen over the last 20 years," they mean that France has gotten relatively cheaper than the US, or equivalently, that the US has gotten relatively more expensive.

The catch is that the basket reflects spending structures and is influenced by the evolution of *relative* prices. If one country's spending shifts toward expensive items, or if the items in the basket get more expensive there, the price level rises with it. Bergeaud's central observation is that this isn't noise — it's signal about what's happening to productivity in different sectors.

## The Balassa-Samuelson mechanism: services drive the price level

The "price level" of a country is overwhelmingly driven by **non-tradables**: health, education, personal services, housing, restaurants, childcare. These are precisely the categories where the US has stood out for decades.

The mechanism is the classic Balassa-Samuelson story (Bergeaud doesn't name it, but it's what he is describing):

1. A country is more productive than its peers in **tradable sectors** exposed to international competition (industry, technology, digital).
2. Tradable productivity gains lift wages in those sectors.
3. Because labor markets clear across sectors, wages rise economy-wide — including in **non-tradable sectors** (haircuts, healthcare, childcare) that haven't experienced any productivity gain.
4. Non-tradables are produced locally with a lot of labor, so their prices rise with wages.
5. The country becomes "expensive" in price-level terms — not because something has gone wrong, but because productive workers in tradables have bid up the wages of barbers and teachers and nurses.

In equilibrium, faster tradable-sector productivity growth produces a higher overall price level. The "expensive country" and the "productive country" are the same country.

This is the same mechanism that underlies [[structural-change|structural change]] toward services — high-income economies spend more on labor-intrinsic services — and the same labor-residual logic that drives [[ai-and-relational-scarcity|relational scarcity]] under AI: when commodities get cheaper, what remains expensive is whatever requires human labor that can't be productivity-shocked away.

## Two questions, two PPPs

The choice between **constant PPP** and **rolling (current) PPP** is the choice between asking two different questions.

**Constant PPP** fixes relative prices to a reference year and then compares countries in volumes at those fixed prices. The thought experiment: *if we valued French and American output with the same price system, who produces more per hour?* In a one-good world, this is literally "number of goods produced per hour." In the real multi-good world, it is "aggregate volume per hour" valued at a common price vector.

Constant PPP answers the **productivity** question: how much real stuff does one hour of work generate?

**Rolling PPP** (sometimes called current PPP) updates the PPP year by year, so the comparison incorporates the evolution of relative price levels. As the US gets more expensive relative to France, the rolling PPP shifts to reflect that.

Rolling PPP answers the **living standards / purchasing power** question: how much consumption can one hour of work finance, given local prices?

These two questions are related but they do not coincide, and they react differently to relative price changes between countries.

Bergeaud explicitly identifies this as the methodological divide between two prominent data series:

- The **WID series** (World Inequality Database) uses rolling PPPs → measures living standards.
- The **longtermproductivity.com** series uses constant PPPs → measures productive capacity.

When two analysts look at the same US/Europe data and reach opposite conclusions about whether Europe is "catching up," they are usually disagreeing about which PPP series to trust, which means they are silently disagreeing about which question they are answering.

## The smartphone-and-haircut example

Bergeaud's worked example makes the divergence concrete. Imagine each country produces two things: **smartphones** (tradables, disciplined by world prices) and **haircuts** (non-tradables, priced by local wages).

- **2010:** One hour of work in either country buys one smartphone + one haircut. PPP is essentially 1.
- **2010–2025:** The US gains productivity in tradables. One hour of US work now buys two smartphones + one haircut. Meanwhile, faster US wage growth means a haircut in the US is now much more expensive in absolute terms than a French haircut.

What does each PPP series report?

- **Constant PPP** (fix prices to 2010): the US gap shows up clearly — Americans produce two smartphones to the French one per hour, haircuts unchanged in the price yardstick. Productivity gap is visible.
- **Rolling PPP**: the US price level has risen (because haircuts got expensive), so the rolling PPP partially offsets the productivity gain — Americans produce more, but their dollars buy proportionally less, so living-standards comparisons compress.

This is *not* a paradox or a measurement error. Both numbers are correct, and they answer different questions. The compression of the rolling-PPP gap is the Balassa-Samuelson mechanism doing its job: faster productivity → higher wages → more expensive local services → higher price level → rolling PPP "absorbs" some of the productivity gap.

## Bergeaud's punchline: cheap Europe is the diagnosis, not the cure

The standard sympathetic reading of European economic performance goes: "Yes, the US has higher headline GDP, but once you correct for prices, our living standards are comparable. Europe is fine."

Bergeaud's argument is that this reading inverts the causality. If European service prices have risen less than American ones, it is **partly because European productivity in tradables has grown less**. The Balassa-Samuelson mechanism doesn't fire if the underlying productivity shock doesn't happen. A cheaper Europe is the *mirror image* of slower income dynamics — the same fact described from two sides.

Worse, you can choose to contain prices through institutions, regulation, subsidies, or demand-support policies. But if the underlying productivity growth is missing, the constraint reappears elsewhere — strained public finances, difficulty raising wages, weak investment, external dependence. Pricing is a thermometer; suppressing the thermometer doesn't cool the room.

This is opinionated, and Bergeaud is staking out a clear position in an ongoing French/European debate. But the methodological core — that constant vs. rolling PPP answer different questions and that the gap between them is informative — is uncontroversial and is the durable contribution of the thread.

## Implications for reading productivity statistics

Three practical takeaways:

1. **Don't trust headline "PPP-adjusted GDP" comparisons without checking which PPP.** Different choices of base year, different rolling-vs-constant conventions, and different basket weights can swing US/Europe comparisons by tens of percentage points.

2. **The constant-PPP series is what matters for capacity questions** — competitiveness, ability to fund the welfare state, sovereign borrowing capacity. This is also the series that asset markets implicitly price ([[treasury-productivity-beta|treasury-productivity-beta]] argues that long Treasury yields are productivity-beta-positive *in real productive-capacity terms*, not consumption-living-standards terms).

3. **The rolling-PPP series is what matters for welfare comparisons** — how well do households actually live. But "people live well in Europe given current prices" is compatible with "Europe is losing the productivity race," because both are true simultaneously when Balassa-Samuelson is at work.

The reference year for constant PPP does affect *levels*, but not *trend*. Bergeaud is careful to flag this caveat: a 2017-base constant PPP and a 2010-base constant PPP will give different absolute gap numbers, but they tell the same directional story about who is converging or diverging.

## Sources
- Bergeaud, Antonin (2025-12-18). "Pedagogical thread on PPP, productivity, and US/Europe comparisons." X (Twitter) thread. <https://x.com/a_bergeaud/status/2001792997260734865> — [[2025-12-18-bergeaud-ppp-productivity-thread|local copy]]
