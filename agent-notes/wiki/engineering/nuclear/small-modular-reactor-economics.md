---
source: agent
compiled_from:
  - agent-notes/raw/engineering/nuclear/2026-07-30-smr-technoeconomic-competitiveness.md
compiled_at: 2026-11-06
model: claude-opus-5-5
confidence: medium
---

# Small Modular Reactor Economics

A **small modular reactor (SMR)** is a fission reactor of roughly 5–300 MWe built mostly in a factory and shipped as modules, so that cost falls with repetition the way it does for manufactured goods rather than rising the way it has for one-off gigawatt plants. Dozens of designs exist; none had been built commercially in the U.S. when this paper was written. The open economic question is not whether an SMR can make power but **which buyer pays enough for the first ones** — the first-of-a-kind (FOAK) units that carry the full cost of an unbuilt supply chain, before learning brings the nth-of-a-kind (NOAK) price down.

The licensing and press conversation assumes the buyer is the electricity market. Garrouste, Kochunas, Vanatta and Craig (University of Michigan, *Nature Communications*, 2026) model every plausible U.S. buyer site by site and conclude the opposite: grid power is the one market where SMRs lose, and the early market is industrial hydrogen — but only while the federal clean-hydrogen credit lasts.

## The model

Two optimizations, both in Pyomo with CPLEX:

- **Industrial sites** — a per-site mixed-integer program that picks the number and type of SMRs and electrolyzers to fully displace a facility's fossil energy at least annual cost. Sites: all 34 U.S. ammonia plants, 9 blast-furnace steel mills, 47 refineries (process hydrogen — hydrogen as a feedstock), and the 955 highest-emitting natural-gas process-heat facilities (86.7 GWt, 124 MMtCO₂/yr; plastics, chemicals, corn milling, lime, pulp and paper). Heat is binned by temperature; a design can only serve heat at or below its steam temperature, and anything hotter must come from burning SMR-made hydrogen. Surplus capacity sells power at state average wholesale prices.
- **Wholesale power** — a price-taker program dispatching each design hour by hour against 2024 state-level prices projected by NREL's Cambium, with minimum-load and ramp limits.

Five generic designs, with vendor FOAK costs taken from the same group's earlier work (Vanatta et al., *Joule* 2023):

| Design | MWe | Outlet °C | Overnight $/kWe | LCOE $/MWh |
|---|---|---|---|---|
| iPWR (integrated light-water) | 77 | 302 | 5,535 | 57 |
| HTGR (gas-cooled) | 164 | 950 | 7,500 | 78 |
| PBR-HTGR (pebble bed) | 80 | 750 | 4,569 | 52 |
| iMSR (integrated molten salt) | 141 | 700 | 4,091 | 46 |
| Micro (gas-cooled microreactor) | 6.7 | 630 | 10,902 | 117 |

The iPWR and pebble-bed parameters match NuScale's 77 MWe module and X-energy's Xe-100 (80 MWe / 200 MWt); the paper does not name vendors. Every base-case capital cost is cut 30% for the Advanced Energy Project credit (§48C). NOAK is modeled as a flat 20% reduction from FOAK, from a 13% learning rate over four units. The §45V hydrogen credit — $3/kg for ten years — is added *after* optimization, so each site's subsidy-free economics can be read off directly.

## What pays

| Scenario | Profitable capacity | What it serves |
|---|---|---|
| FOAK, no H₂ credit | 4 GWe, 33 sites, IRR 5–10% | process heat only |
| NOAK, no H₂ credit | +7.8 GWe, IRR 8–12% | process heat (iMSR dominant) |
| FOAK, with H₂ credit | 91 GWe — 94% of today's U.S. nuclear fleet; IRR 9–38% | 57 heat, 24 ammonia, 7 steel, 3 refining |
| NOAK, with H₂ credit | +172 GWe; total 263 GWe, 121 MMtCO₂/yr avoided | mostly heat via hydrogen |
| Capital cost +117–156%, with H₂ credit | 28 GWe, 41 sites | hydrogen only; zero heat sites |
| Capital cost +117–156%, no H₂ credit | none | — |

Three findings hold across every scenario:

1. **Grid power never pays.** The cheapest design's LCOE ($46/MWh) is at least 36% above the highest state average wholesale price (~$34/MWh). Even NOAK costs leave SMRs only "close to profitability."
2. **Process heat is the only subsidy-free market**, and it is small (4 GWe at FOAK). The most profitable of those sites sit in California, Connecticut and New York, three states that restrict new nuclear construction.
3. **Hydrogen is the big market, and it is the credit's market.** The authors' capital-cost *profitability margin* — how far capital cost can rise before a site stops paying — runs around 300% for ammonia, above 50% for most refineries, about 20% for steel, and under 10% for the few positive heat sites. Ammonia and refining survive a doubling of capital cost; steel and heat do not survive a 10–50% overrun.

## The subsidy picks the technology

The model's largest single block of capacity is a thermodynamic detour. With the credit in place, 56 of the 57 GWe of FOAK process-heat capacity makes heat by turning reactor output into electricity, electricity into hydrogen, and hydrogen back into heat by burning it — even at sites where the reactor's own steam was hot enough to serve the load directly. The authors call this "an artifact of the H2 PTC structure that prioritizes hydrogen production over thermodynamic and economic efficiency." The credit pays per kilogram of hydrogen, so the optimizer manufactures kilograms.

The abatement-cost numbers, which leave the credit out because a transfer is not a gain to society, show what that detour costs. Hydrogen for refining and steel mostly abates CO₂ below the EPA's ~$230/t social cost of carbon at FOAK, and 90% of hydrogen sites clear it at NOAK. Process heat never does: at least ~$500/t at FOAK and a median of $885/t at NOAK. So most of the headline 263 GWe is deployment the credit buys at two to four times the social cost of the carbon it removes.

The authors nonetheless recommend extending §45V past its deadline. That follows from their numbers only on a learning argument they make explicitly: a first wave of hydrogen-serving reactors builds the supply chain, workforce and construction practice that bring capital cost down for everything after, including the grid. The recommendation is a bet that this spillover is worth more than the above-social-cost abatement; the paper does not quantify the spillover, and Vanatta, Stewart and Craig's separate *Nature Energy* (2025) paper on module manufacturing learning is the place that question is treated.

## Vendor numbers and the outside view

Every base-case result rests on vendor-supplied FOAK costs. The paper's own sensitivity cites Merrow, Phillips and Myers's 1981 RAND study of pioneer process plants: plants at the R&D stage, where SMRs sit, estimate only about 49% of what they end up costing. The authors apply +117% to most designs and +156% to the iPWR, in line with recent U.S. light-water builds (Vogtle 3 and 4 finished at more than double their original budget). The iPWR case already has a real data point: NuScale's Utah project, the first U.S. SMR order, saw its target power price rise from $58 to $89/MWh before it was cancelled in November 2023 (see [[technology-in-the-2020s]]).

Read through [[reference-class-forecasting]], the escalated case is the base rate and the vendor case is the inside view. On that reading the paper's robust result is narrow: **ammonia and refinery hydrogen, with the credit, and nothing else.** Process heat, the one subsidy-free market, disappears entirely once costs escalate. The authors draw the same line in their discussion — the full opportunity depends on "the ability of SMR vendors to build on budget."

## First licensed wins

The paper's most strategic argument is about path dependence rather than cost. U.S. nuclear converged on the pressurized water reactor not because it was best on paper but because it came first (out of the naval propulsion program) and every later plant inherited its supply chain and trained workforce. The authors expect the same: the first SMR designs licensed will be deployed "en masse," and learning will make whichever design that is the default for industry, "any SMR design with potentially less-than-optimal technological performance" included. On techno-economics alone their model would pick the molten-salt design, which has the lowest starting capital cost; history suggests the licensing queue will pick instead.

This sharpens the critique in [[subcritical-reactors]]: new reactor architectures mostly answer nuclear's political problem (fear of runaway reactions), while the binding constraint is cost. Garrouste et al. imply something further — that cost leadership itself is less a property of a design than of being first through licensing.

## What the model leaves out

- **Data centers.** The authors exclude large-load customers because their deals run through private power-purchase and behind-the-meter agreements that are hard to model, and note they "could provide an alternate pathway to achieve NOAK capital costs." Since late 2024 that has been where actual SMR orders have come from — hyperscaler offtake and equity deals rather than refineries or ammonia plants (see [[technology-in-the-2020s]] and the AI-capex framing of nuclear as a long-duration bet in [[ai-capex-required-returns]]). The paper's map is of the markets that *should* pay on public prices; the market that has paid so far is one that values firm, clean power above the wholesale price.
- **Capacity revenue.** The power model counts energy sales only and argues capacity and ancillary payments are small for baseload units. That was defensible on 2024 prices. PJM's capacity auctions then cleared at about $270/MW-day for 2025/26 and at the $329 cap for 2026/27, roughly $11–14/MWh for a unit running all year — about the size of the gap between the cheapest SMR's LCOE and the highest state energy price. Whether that closes the grid case depends on which state, but it weakens the paper's flattest conclusion.
- **Siting on retired coal plants**, which other DOE work estimates could cut SMR capital cost 15–35% by reusing turbines, switchyards and grid connections — roughly the paper's NOAK discount, available at FOAK.
- **Non-cost limits on the competitor.** Natural gas with carbon capture beats SMRs for hydrogen without the credit at FOAK cost, but the comparison ignores pipeline access, CO₂ transport and storage availability.
- **Hydrogen demand units.** Plant-level hydrogen demand is given in million metric tons for ammonia (an average of "268 MMtH₂" per plant) but in tonnes for steel. The MMt figures cannot be literal, since total U.S. hydrogen output is about 10 million tonnes a year, so plant-level demand magnitudes in the text should be checked against the code repository before reuse.

## Temporal notes

- **The hydrogen credit's deadline.** The abstract says the §45V credit "expires in 2033" while the body says construction must start by 2028. The abstract reflects the original 2022 Inflation Reduction Act; the body reflects the July 2025 budget law (the One Big Beautiful Bill Act), which ended §45V for facilities beginning construction after December 31, 2027. As of this note, the body's date is the law. An industrial SMR-hydrogen project would have to begin construction by the end of 2027 to qualify, which for designs still in licensing makes every with-credit scenario above close to unreachable unless Congress extends the credit — the extension the authors recommend.
- **§48C is not automatic.** The base case cuts all capital costs 30% for the §48C Advanced Energy Project credit, but §48C is a capped, competitively allocated credit (about $10 billion under the IRA, awarded in rounds), not an entitlement every project can claim. Without it, every base-case cost is about 43% higher, which pushes results toward the escalated scenarios.

## Sources

- Garrouste, M., Kochunas, B., Vanatta, M. & Craig, M. T. (2026). "Technoeconomic competitiveness of small modular reactors across U.S. power and industrial sectors." *Nature Communications* 17:9399. <https://doi.org/10.1038/s41467-026-76077-3> — [[2026-07-30-smr-technoeconomic-competitiveness|local copy]]
