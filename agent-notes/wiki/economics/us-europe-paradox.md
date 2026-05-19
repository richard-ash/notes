---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-05-11-krugman-us-europe-paradox-model.md
compiled_at: 2026-05-13
model: claude-opus-4-7
confidence: high
---

# The US-Europe paradox

Two charts about US/Europe relative performance since 2000 sit in apparent tension. Conventional headline measures of real GDP per capita have favored the US: cumulative growth runs meaningfully ahead. But European GDP per capita measured at PPP has been roughly flat as a share of the US level — Europe has not "fallen behind" in living-standards terms. Paul Krugman labels this the **US-Europe paradox** and supplies a stylized two-country, two-sector model showing it is not a paradox at all: US dominance of a sector with fast productivity growth raises measured US real GDP without raising US relative income or relative welfare. The model isolates a measurement-driven divergence that is mechanistically distinct from — and complementary to — the Balassa-Samuelson PPP story Bergeaud documented in his [[ppp-and-productivity-comparison|pedagogical thread on constant vs. rolling PPP]].

## The two facts

Conventional real GDP per capita growth: US has pulled away from Europe over roughly 25 years, with a cumulative gap that is the workhorse statistic in the "Europe in decline" narrative.

Relative GDP per capita at PPP: Europe is roughly where it was in 2000 relative to the US — no decline.

Both numbers are calculated from real data and are correct. They diverge because they answer different questions. Krugman's model shows that this divergence has a clean structural source: **sectoral concentration of productivity growth interacts with how we measure real GDP via chained constant-price indices**, and the gap between chained real GDP growth and current-price relative GDP is exactly what you should expect when one country dominates a fast-growing sector.

## Krugman's stylized model

Two countries: **US** and **EU**, with equal labor forces (the only factor of production). Two goods, both costlessly tradable:

- **T** (tech): the sector with fast productivity growth
- **N** (nontech): the sector with no productivity growth

Preferences are **Cobb-Douglas** with constant expenditure share **𝜏 < 1/2** on T. This is the critical functional-form assumption: it pins down spending shares as constant in nominal terms regardless of relative prices.

Productivity in N is equal across the two countries and constant. Productivity in T grows at rate **𝜌** in whichever country produces it.

The US has a comparative advantage in T — Krugman is agnostic about why, but cites industrial-cluster externalities. So in equilibrium, all T is produced in the US, and the EU produces only N. The US splits its labor between T and N.

### Wage equalization

The first key result: **wages are equal across the two countries, and current-price GDP is equal**.

The mechanism is not Balassa-Samuelson and not labor mobility. It is simple goods-market arbitrage: because N is tradable and produced with the same productivity in both countries, the world price of N must equal labor cost / N-productivity in each country. Both countries produce N, so both prices clear at the same level — which means both wages must be equal. With equal labor forces and equal wages, nominal GDP is equal in both countries.

This shuts down the entire "relative current-price GDP" channel by construction. No matter how productive T becomes, neither country pulls ahead in nominal terms.

### Sector shares

By Cobb-Douglas preferences, world spending on T is share 𝜏 of world income. Since all T is produced in the US, T revenue is 𝜏 of world GDP. The US accounts for half of world GDP (equal wages, equal labor), so T is **2𝜏** of US GDP. The rest of US production is N. EU production is entirely N (worth (1-2𝜏) of world GDP).

### Chained-index real GDP growth

This is where the headline divergence appears. Real GDP growth measured by chained constant prices (the standard national-accounts methodology) is approximately the GDP-share-weighted sum of sectoral productivity growth:

- US: T grows at 𝜌, T is 2𝜏 of US GDP → **measured US real GDP growth = 2𝜏𝜌**
- EU: no productivity growth in N, no T sector → **measured EU real GDP growth = 0**

Add some N productivity growth and EU growth would be positive, but the US would still be ahead by 2𝜏𝜌. This is the "US has been growing faster" headline statistic, reproduced exactly.

### Real wages

The third key result: real wages rise at rate **𝜏𝜌 in *both* countries**.

Mechanism: T productivity growth pushes the world T price down at rate 𝜌 (assuming competitive output markets — quantity rises at 𝜌, revenue is constant, so price falls at 𝜌). The N price is constant. The Cobb-Douglas CPI is a 𝜏-weighted geometric mean, so it falls at rate 𝜏𝜌. Nominal wages are constant. Real wages = nominal wage / CPI rises at 𝜏𝜌.

The same fall in T prices benefits consumers in both countries equally. Americans don't end up materially richer than Europeans because the productivity gain in T is **passed through to global consumers via lower T prices**, not captured by American workers via higher relative wages.

## Why current-price GDP doesn't move

The cleanest piece of intuition in the model: as T productivity rises, the **quantity** of T produced rises at rate 𝜌, the **price** of T falls at rate 𝜌, and total T revenue is constant at 𝜏 × world income. Current-price nominal GDP doesn't move because price and quantity changes exactly cancel — that is the Cobb-Douglas assumption doing its work.

The chained-index real GDP measure, by contrast, holds prices constant and reads off the quantity expansion as growth. So the US "grows" by 2𝜏𝜌 in real terms while its nominal share of world GDP stays at 50%.

This is what produces the apparent paradox: chained real GDP and current-price GDP can move differently when there is concentrated sectoral productivity growth, even with no measurement error and no real divergence in welfare.

## What the model abstracts away — and what survives

The model is deliberately spare. Several assumptions are doing significant work:

1. **N is costlessly tradable.** This is the assumption that wages equalize without labor mobility. In reality, much of N is services (healthcare, education, retail, restaurants) that are essentially non-tradable. Once N is non-tradable, the [[ppp-and-productivity-comparison|Balassa-Samuelson]] mechanism kicks in: faster US tradable productivity raises US wages, which raises US non-tradable prices, and the US becomes "expensive" in PPP terms.
2. **Cobb-Douglas preferences.** Expenditure shares are constant. With more realistic non-homothetic preferences (e.g., the income-elastic services demand in [[structural-change|structural-change]]), the spending share on each sector would shift with productivity, and the nominal-GDP equality result would break.
3. **Complete specialization in T.** All T in the US; none in the EU. In reality both have T sectors, just with different mixes.
4. **Equal labor forces.** Drops out of the wage-equalization logic, but the per-capita comparison still requires it for the relative-GDP statement to be clean.

The durable contribution survives the abstractions: **when one country has a larger share of GDP in a fast-productivity-growth sector, its chained-index real GDP will grow faster than its trading partner's, even if the productivity gain is fully passed through to global consumers and the country's relative income is unchanged**. That is a measurement-and-aggregation fact, not an assumption.

## Relationship to Bergeaud's PPP framework

This is the same observation Bergeaud documented but with a different mechanism. Bergeaud's [[ppp-and-productivity-comparison|thread]] emphasizes that **constant PPP** (fixed-basket) and **rolling PPP** (current-basket) GDP-per-hour answer different questions — productive capacity vs. living standards — and the Balassa-Samuelson mechanism makes the US "expensive" in rolling PPP terms exactly because US tradable productivity is higher.

Krugman's model strips out PPP entirely. Both countries face the same prices (free trade), and current-price GDP is identical. The divergence is purely between chained-real and current-nominal GDP measurement *within each country*, not between PPP-basket choices across countries.

So there are at least two distinct mechanisms producing the same surface observation:

| Mechanism | Source of divergence | What's "really" happening |
|---|---|---|
| **Bergeaud (Balassa-Samuelson)** | PPP-basket choice across countries; non-tradable services prices rise with tradable productivity | US is genuinely more productive; rolling PPP absorbs the gap by capitalizing the productivity gain into service prices |
| **Krugman (sectoral chained-index)** | Chained vs. current-price real GDP within each country; sectoral concentration weighted by quantity expansion | T productivity gain is passed through to consumers globally; nobody "gains" relatively, but the country with the T sector shows up with higher measured growth |

These are partially in tension. Bergeaud says US workers really are better off — the rolling PPP just doesn't show it. Krugman says US workers are equally better off as EU workers — the chained real GDP measure just makes the US look like it's pulling ahead. In Krugman's model, real wages rise *equally* in both countries (𝜏𝜌 each), so there is no welfare divergence to obscure.

In practice both mechanisms are probably at work. Bergeaud's framework is closer to the real world where services are non-tradable and wages don't fully equalize across continents. Krugman's framework is closer to the part of the world economy that *is* in tradable goods (chips, software, tech hardware) where Cobb-Douglas-style arbitrage is a decent approximation.

A reader who has internalized both gets the right takeaway: **the headline US growth advantage since 2000 is partly a measurement artifact of sectoral concentration (Krugman), and partly real productivity that is hidden by rolling-PPP basket recalculation (Bergeaud) — but in neither case does it imply Europe is "falling behind" in welfare terms**, which is what the PPP-stable chart actually shows.

## Relationship to Garicano-Kooi's two-Europes thesis

Krugman's model has only "EU" as a single block — which is precisely the granularity problem Garicano and Kooi identify in [[two-europes-divergence|two-europes-divergence]]. The aggregate "EU" hides the eastern catch-up half (Poland, Baltics, Romania, Bulgaria) converging from 27–34% to 53–69% of US per-capita GDP and the western/southern rear (France, Italy, Spain) slipping from 86%/93% to 71%/68%. Both Krugman's model and Bergeaud's PPP arithmetic operate at the aggregate level where the diverging halves average out to "stable EU/US ratio."

This means Krugman's "paradox" is being driven in significant part by which Europe you count. The eastern accession countries are genuinely catching up via institutional and capital-stock convergence; the western rear is slipping in chained-real terms for exactly the reasons in Krugman's model (no T sector concentration) plus the political-economy reasons Garicano-Kooi document (Olsonian distributional coalitions blocking domestic reform). The aggregate stability is a statistical artifact of averaging convergence and divergence within the same currency union.

## Why this matters for the AI productivity debate

If T in Krugman's model is read as "AI / frontier tech / cloud / semiconductors," the predictions of the model become directly testable claims about the next decade:

1. **US chained-real GDP will pull further ahead of EU's**, in proportion to the US T-sector share times the AI productivity growth rate.
2. **Current-price relative GDP will not move much** — the AI gain will be passed through to global consumers as lower prices for AI-using outputs.
3. **Real wages will rise approximately equally** in the US and Europe, because the global T price will fall and CPI will fall in both countries.

If observed, those three results would *not* mean Europe is "falling behind" in welfare. They would mean exactly what Krugman's model predicts: sectoral concentration in a fast-growing sector produces a chained-index measurement gap that doesn't translate into welfare divergence.

This sits alongside the asset-market debate: [[markets-believe-transformative-ai|Andrews-Farboodi]] document Treasury yields falling on frontier-model release days, which [[treasury-productivity-beta|Manyam reads as a positive productivity beta]] (markets endorsing US AI capacity) and Andrews-Farboodi read as skepticism of transformative AI. Krugman's model is silent on this — it implies higher US measured growth from AI but says nothing about the level of 𝜌 itself, which is what the asset-market debate is really about. The two debates can be settled independently.

## Krugman's positioning

This is a "technical note" Krugman flags as something he wants to refer back to. It is also a continuation of his ongoing argument that the "Europe in decline" narrative — popularized by Aghion, Draghi's 2024 competitiveness report, and others — is based on misreading conventional GDP growth statistics. Krugman has been arguing in his Substack series that PPP-adjusted relative living standards are the right comparison and that on that comparison Europe has not declined.

The model gives him a clean economics-professor-style derivation of the "chart-A diverges, chart-B doesn't" observation. It does not, however, address the dynamic concern: even if welfare hasn't diverged, the *concentration of T productivity in the US* may have second-order effects (fiscal capacity, sovereign-debt servicing, strategic autonomy, defense capability) that the Cobb-Douglas one-period model abstracts away. Garicano and Kooi's two-Europes work and Draghi's competitiveness report both make this dynamic case. Krugman's model is a clean defense against the *static* version of the decline narrative; it is not a defense against the dynamic version.

Worth flagging because Krugman's note is sometimes read as definitively settling the European decline debate — it doesn't. It cleanly demonstrates that one specific argument for European decline (the chained-real-GDP divergence) is consistent with no divergence in static welfare. The dynamic/strategic version of the concern is on different ground.

## Sources
- Krugman, Paul (2026-05-11). "Modeling the US-Europe Paradox (Very Wonkish)." Substack. <https://paulkrugman.substack.com/p/modeling-the-us-europe-paradox-very> — [[2026-05-11-krugman-us-europe-paradox-model|local copy]]
