---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-11-06-how-do-building-codes-affect-the-price-of-housing.md
compiled_at: 2026-11-06
model: claude-fable-5-1
confidence: medium
---

# Building code costs

Regulation makes housing expensive by two routes. Land-use rules limit how much can be built (see [[commercial-zoning-costs]] for the commercial side and [[abundance-agenda]] for the politics). Building codes raise what each unit costs to produce. Brian Potter's November 2026 survey in *Construction Physics* collects the studies that try to put a number on the second route. (His essay on technology as search is in [[technological-evolution]].) His tentative answer: changes to US model codes have added roughly 0.5% to 1% a year to construction cost, most of it from a small number of provisions, and the benefits are too thinly measured to say whether the code as a whole is worth what it costs.

Confidence is `medium`. This is one author's literature survey, compiled here without reading the underlying studies, and Potter calls his own conclusions tentative. Most of the studies he cites come from organisations with a stake in the answer. The tables below use the data behind the article's embedded charts, which is kept in an appendix to the local copy.

## How the code gets made

Codes are mostly adopted by states. Almost none write their own. They start from a model code published by a private body, chiefly the International Code Council (ICC), whose codes are used almost only in the US despite the name. The two that matter most for housing are the International Residential Code (IRC) for one- and two-family homes and the International Building Code (IBC) for larger buildings. Model codes are revised every three years. States adopt new editions less often (Georgia updates most codes every six years), cities and counties can add stricter rules, a few cities such as New York write their own, and manufactured homes fall under a federal code.

| Code | Publisher | Covers | States using it |
|---|---|---|---|
| International Building Code | ICC | Commercial and multifamily | 50 |
| International Residential Code | ICC | 1–2 family homes, townhouses | 49 |
| International Mechanical Code | ICC | Mechanical | 47 |
| International Plumbing Code | ICC | Plumbing | 37 |
| Uniform Plumbing Code | IAPMO | Plumbing | 18–20 |
| Uniform Mechanical Code | IAPMO | Mechanical | ~4 |
| National Electrical Code | NFPA | Electrical | 50 |

So there are three layers: the model edition, the state's adopted version with its amendments and its lag, and local additions. Every study below prices the model code. What binds a project is the adopted one, and the two can differ in either direction. The 2009 IRC required fire sprinklers in new houses, and almost every state struck the provision when adopting it, which Potter credits to lobbying by the National Association of Home Builders (NAHB). Going the other way, [[ai-technical-drafting]] records a Massachusetts amendment that requires a second egress the base IRC does not.

## The counterfactual is not zero

Potter's first caution is that no code would not mean no rules. Insurers and mortgage lenders already impose their own standards (Factory Mutual's insurance standards, the UK's Professional Consultant's Certificate), and these would bind harder as public rules loosened. The professional liability of engineers and architects would set a floor too. This is why the studies measure each edition against the one before it. It also means their numbers are the cost of a change, and repealing a provision saves less than its estimated cost wherever an insurer or lender would ask for the same thing. The second half of that sentence is this article's inference, not Potter's.

## What the changes cost

| Source | Scope | Method | Finding |
|---|---|---|---|
| NAHB per-edition reports | IRC changes since the 2006 edition | Engineering estimate of every change, on same-size reference houses in different climate zones | About $40,000 added to a house that cost about $440,000 to build in 2024, or roughly 0.5% a year |
| Eriksen, Besiktepe and Martani (2026) | 140 IBC revisions, 2012 to 2021, on a three-story apartment building | 36 revisions raise cost somewhere, 16 of them for this building type, 104 are cost neutral | Costs up 9.9%, or about 0.8% a year |
| NAHB builder surveys | "The last 10 years of code changes" | Builders' own estimates | 8.3% of construction cost (2011), 9.2% (2016), 9.9% (2021), 12.7% (2026), or about 1% a year |

Four things to hold against those numbers:

- **Editions do not only add cost.** The 2015 IRC raised or lowered cost depending on the house, and the 2024 IRC lowered it in every climate zone, partly by thinning the required vapor barrier.
- **The NAHB total appears to include the 2009 sprinkler requirement**, which states did not adopt. The code as enacted has cost less than the model code as written.
- **Eriksen's 9.9% at 0.8% a year implies about twelve years.** That fits four three-year editions measured against a 2009 baseline. The source does not state the span, so this is a reading.
- **NAHB's survey runs at about double NAHB's own engineering estimates, and the survey figure keeps rising.** The survey may be picking up electrical codes and local amendments that the IRC reports leave out, or it may be picking up bias. Potter calls the potential for bias "strong" because the answers are perceptions.

## Concentrated twice

In both analyses a handful of provisions carry most of the cost. Eriksen and co-authors attribute $180,000 of roughly $400,000 in added cost to a single 2018 IBC requirement: watching the site for fire during non-working hours while the building is under construction. NAHB counts 89 cost-increasing IRC changes between 2009 and 2024, and about 60% of the total comes from ten of them. The chart data lists the largest:

| Edition | Section | Change | NAHB estimate |
|---|---|---|---|
| 2015 | R322 | Slab foundations in Zone A flood hazard areas | $13,465 |
| 2021 | R202 | Windborne debris region expanded | $6,685 |
| 2009 | R313 | Fire sprinklers in one- and two-family dwellings | $6,349 |
| 2018 | R322.3.6 | Flood-resistant or breakaway stairs and ramps | $5,142 |
| 2021 | R326 | Habitable attics count as a story | $4,851 |
| 2018 | R301.2.2.1 | Updated seismic design category maps | $4,779 |
| 2009 | R322.2 | Flood areas reclassified from A Zones to Coastal A Zones | $4,360 |
| 2015 | N1101, N1106 | Energy Rating Index alternate method | $2,892 |

Six of the eight are flood, wind or earthquake rules. That is not a point Potter makes, and it changes how the headline rate should be read. These provisions cost nothing for a house outside the hazard zone and a great deal for one inside it, so the cost is concentrated in a few places as well as in a few provisions. An average across climate zones overstates the burden on most houses and understates it on a coastal one. The figures are what each provision costs where it applies, so they do not add up to the $40,000 average. The hazard rules are also the provisions with the best measured returns (next section), so the most expensive part of the code is plausibly its most defensible part.

Sprinklers show how soft the individual estimates are. NAHB's 2009 figure is $6,349. NIST's 2005 projection was $635 to a little over $2,000. The National Fire Protection Association (NFPA) looked at houses actually built with sprinklers and found under $2,000 to over $20,000 in 2013. NFPA also found costs substantially lower where a state required sprinklers statewide, which Potter reads as installer experience or scale. The implication is that a provision's cost depends on how widely it is adopted. A line-item estimate made before adoption misses that, and the patchwork of state amendments is itself a cost. It is the same learning-curve logic that [[technology-in-the-2020s]] records for batteries and solar.

## The benefit side

Potter's main complaint is that most of this literature counts only costs. The cost-benefit studies he finds:

| Provision | Study | Benefit-cost ratio |
|---|---|---|
| Home fire sprinklers | NIST (2007) | 2.4 to 6, mostly averted deaths |
| Flood-zone elevation (National Flood Insurance Program) | FEMA (2020) | Often above 1, depending on discount rate and foundation type |
| Flood requirements vs. 1990s baseline | National Institute of Building Sciences (2019) | About 6 ($550 million against $90 million) |
| Wind requirements vs. 1990s baseline | Same | About 10 ($5.6 billion against $0.54 billion) |
| Earthquake requirements vs. 1990s baseline | Same | Nearly 12 ($7 billion against $0.6 billion) |
| Residential energy code (IECC), by edition | Pacific Northwest National Laboratory (PNNL) | 1.9 to about 12 |
| 2021 IECC | NAHB | Below 1 |
| 2021 IECC | Consultant for the Institute for Market Transformation | Close to PNNL's |
| Second stair and corridor in multistory apartments | Center for Building in North America (2025) | Adds 6–13% to building cost for little or no safety gain |

The same group argues that elevator costs are inflated by a rule that cabs fit a full-sized stretcher, with questionable safety benefit.

PNNL's edition-by-edition numbers show where the energy-code fight is:

| IECC edition | Added cost per dwelling | Energy savings per year | PNNL ratio | Simple payback |
|---|---|---|---|---|
| 2009 | About $970 | $168 | 3.4 | 5.8 years |
| 2012 | About $1,820 | $332 | 3.6 | 5.5 years |
| 2015 | About $11–13 | About $6.80 | 10–12 | Under 2 years |
| 2018 | About $50 | $24 | 9.5 | 2.1 years |
| 2021 | About $2,010 | $191 | 1.9 | 10.5 years |
| 2024 | About $400 | $163 | 8.0 | 2.5 years |

The payback column is this article's arithmetic (cost divided by annual savings), not PNNL's. The 2021 edition is the most expensive and has the weakest return even on PNNL's numbers. It is also the one NAHB chose to contest. Potter says the two disagree mostly on up-front cost, and at a ratio of 1.9 a cost estimate about twice PNNL's is enough to push the answer below 1. The 2015 and 2018 editions changed almost nothing, so their high ratios say little.

One cost is missing from the energy ledger altogether. [[indoor-air-quality-cognitive-function]] traces how sealing buildings for efficiency roughly halved home air-exchange rates, and argues the cognitive cost of low ventilation may exceed the energy saved. The energy-code studies count energy bills. That connection is this vault's, not Potter's.

## Who ran the study

Where two parties studied the same provision, each found what suited it: the homebuilders' association puts the 2021 energy code below break-even, while a Department of Energy lab and an efficiency nonprofit's consultant put it near 2. The other studies come from bodies with a mission attached as well. NFPA publishes fire codes and the Center for Building in North America argues for code reform. Potter flags only NAHB as "probably somewhat biased". Extending the caution to the rest is this article's reading. It is a reason to discount each number for its author's incentive, not a reason to throw any of them out.

The code that results does not track the ratios either. Sprinklers carry a federal estimate of 2.4 to 6 and were struck almost everywhere. The second stair has, on Potter's reading, "almost certainly" higher costs than benefits and is only now being reformed state by state. That pattern fits [[political-economy-of-reform]], where organised interests and veto points decide what passes more than social returns do. There is a caveat on the sprinkler case: if NIST's 2007 ratios rest on cost figures like its 2005 projections, then the costs NFPA later observed, several times higher in places, would cut the ratio a long way in the dearest markets.

## What the method cannot see

Every cost study here prices the difference between one edition and the next. A provision that predates the editions studied never appears as a change, so it is never priced. The two-stair rule is one of these. It is the provision Potter singles out as the clearest net loss, and at 6–13% of building cost it is of the same order as the whole of Eriksen's 9.9% for a decade of revisions. The 0.5% to 1% a year is therefore the rate at which known cost is being added. It says nothing about how much cost is already embedded in the code, which could be much larger and has not been measured.

## Quality nobody counts

The Census Bureau's constant-quality index for new houses adjusts for bedrooms, bathrooms, wall material and heating system, but not for safety features the code requires. The Bureau of Labor Statistics does count mandated safety equipment as quality in its new-vehicle index. Potter's point is that if code benefits exceed code costs, some of construction's famously flat productivity is a measurement artifact.

A rough size for the effect, which Potter does not give: code changes add 0.5% to 1% a year to cost, and the index records all of it as price. If benefits about equal costs, measured productivity growth in new housing is understated by about that much each year. Where benefits are a multiple of cost (the hazard rules) the understatement is larger, and where they fall short of cost (the second stair) the lost productivity is real. [[ppp-and-productivity-comparison]] and [[us-europe-paradox]] are the cross-country version of the same lesson, that a productivity story is only as good as its price index.

## From cost to price

Potter's title asks about price, and the studies measure cost. How much of a code cost reaches the buyer depends on the market. This is standard incidence reasoning, not something the article argues. Where building is easy, price sits near construction cost and code costs pass through (the Dallas and Austin cases in [[abundance-agenda]]). Where land-use rules cap supply, price is set by scarcity, and a code cost comes out of land value or decides whether a marginal project gets built at all. So code reform should lower prices most in the places that already build, and in supply-capped metros it mostly changes which projects pencil. [[public-problem-solving-capital]] puts building codes and plan-check in the last of its four layers of housing reform, after approvals, zoning and fees. That memo scores the layer as about 10% cleared in California and treats the layers as conjunctive: until all four are cleared, little gets built.

## The AI project

Potter closes by proposing "a provision-by-provision cost-benefit analysis of the entire building code" as a job for AI models. His own survey suggests which half of that is tractable.

- **Costs are the cheap half.** NAHB's method is line-item estimating on reference buildings, repeated per provision and per climate zone. That is the routine analytic labor [[ai-economics-research]] expects to get cheap, and a model that can draft a permit set from sketches ([[ai-technical-drafting]]) can plausibly price what a provision adds to one.
- **Benefits are limited by data.** A benefit estimate needs losses by provision: fire deaths, flood claims, energy bills. Potter's phrase for what exists is "pretty thin". More analysis does not create loss data.
- **Volume is where a model earns its keep.** A useful version would price provisions already in the code and not only the changes, and it would price the adopted code in each state and not the model code. No study in the survey does either, and the reason is volume.

## Open questions

- What does the code as adopted cost? Every study prices the model code, and states both strike provisions and add them.
- Is the construction fire watch worth $180,000 a building? It is the largest single item in the IBC study, and the survey cites no benefit estimate for it.
- Does cost fall with adoption for provisions other than sprinklers? If so, the per-edition estimates are too high for anything that becomes universal.

## Sources

- Potter, Brian (2026). "How Do Building Codes Affect the Price of Housing?" *Construction Physics*. <https://www.construction-physics.com/p/how-do-building-codes-affect-the> — [[2026-11-06-how-do-building-codes-affect-the-price-of-housing|local copy]]
