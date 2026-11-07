---
source: agent
compiled_from:
  - agent-notes/raw/economics/2024-03-optimal-urban-transportation-policy-chicago.md
compiled_at: 2026-11-06
model: claude-opus-5-5
confidence: medium
---

# Congestion Pricing

Congestion pricing charges drivers for the delay and pollution each car imposes on everyone else. The Pigouvian case for it is old. The open question is what a city should do alongside it: cut transit fares, run more buses and trains, or rebate the money. Almagro, Barbieri, Castillo, Hickok and Salz (NBER w32185, 2024, revised 2025) answer this for Chicago. Their result: road pricing and transit subsidy are complements. Done together, they gain almost twice what the two gain separately, because toll revenue lifts the transit budget constraint.

## The planner as a multi-product seller

The paper models the city government as a seller of several products: bus and train trips, priced by fare and with quality set by frequency, plus road use if it can toll. It maximizes welfare subject to a budget constraint, the transit deficit it is allowed to run. It does not control ride-hailing prices, and without road pricing it does not control the price of driving.

Their Proposition 1 breaks each optimal price into terms:

- **Marginal cost plus environmental externality** of one more *trip*, not one more vehicle. A bus that is running anyway costs nothing extra per passenger, so transit's marginal cost is about zero.
- **Congestion**: the delay one more trip imposes on other road users. This term is the classic Pigouvian toll.
- **Diversion**: a second-best correction for modes the planner can't price. If driving is underpriced, the planner lowers transit fares to pull people out of cars. The term vanishes once every other mode is priced correctly.
- **Budget distortions**, scaled by λ/(1+λ), where λ is the budget constraint's shadow price. A planner that must raise revenue behaves like a monopolist and charges a markup (Ramsey 1927). It also commits a **Spence (1975) distortion**: it sets frequency to suit the marginal rider rather than the average rider. And it starts weighing diversion by revenue instead of welfare. As λ → ∞ the planner becomes a pure revenue maximizer and stops caring about externalities.

The point of the framework is that cross-subsidy can remove the budget distortions completely. If road tolls produce a surplus, λ falls to zero and transit can be priced as if money were free. The authors call this an efficiency rationale for the London and New York designs that earmark toll revenue for transit.

## Chicago data

Markets are origin × destination × hour: 77 community areas, 48 hour-of-week periods, January 2020. The authors join four sources:

- CTA farecard records with inferred alighting stops (cash trips, 12%, scaled in).
- The City of Chicago's public universe of taxi and ride-hailing trips, with prices.
- Veraset phone-location data (~40% of US devices) to count all motorized trips. **Car trips are the residual**: phone trips minus transit and for-hire trips, since there is no official count of car trips.
- Google Maps travel times for every mode in every market, including modes not chosen.

Mode shares: car 69.9%, transit 22.9% (buses a bit over half), ride-hailing 6.3%, taxi 0.9% (dropped). Car use is an inverted U in income. Middle-income residents drive most, so they lose most from a toll. Buses run nearly empty: median utilization stays under 20% even at rush hour, and under 5% of buses are full at the busiest times. That near-empty bus is why the marginal cost of a passenger is zero, and the counterfactuals rest on it.

Estimated parameters:

| Parameter | Estimate |
|---|---|
| Value of time, bottom to top income quintile | $8 to $57 per hour (metro mean wage $29) |
| Congestion elasticity of travel time to vehicle flow | 0.08–0.09 buses, 0.13–0.17 cars |
| Bus headway variability (ω²) | 0.194; trains 0 |
| Marginal value of public funds at constrained optimum | 1.37 |

Travel-time endogeneity is handled with straight-line distance over citywide free-flow speed. Ride-hailing price endogeneity is handled with Chicago's downtown peak-hour ride-hailing surcharge, which implies a price elasticity of −1.42. Carbon is priced at the EPA's 2022 proposed $190/tonne, and local pollutants follow Holland et al. (2016).

## Counterfactuals

Weekly figures, point estimates (Table 3):

| | Status quo | Transit (no budget) | Transit, budget | Road pricing | Transit + road pricing |
|---|---|---|---|---|---|
| Bus / train fare | $1.09 / $1.33 | −$0.61 / −$0.81 | $1.46 / $1.90 | unchanged | ≈ $0 / ≈ $0 |
| Road tax | 0 | 0 | 0 | $0.36/km | $0.34/km |
| Bus / train frequency | — | +33% / +43% | +10% / +22% | unchanged | +34% / +43% |
| Car trips (M) | 21.33 | 20.12 | 21.33 | 18.62 | 17.88 |
| Δ Welfare ($M) | — | 3.89 | 0.62 | 3.80 | **6.97** |
| Δ Consumer surplus, no rebate ($M) | — | 26.87 | 0.95 | −32.32 | −7.84 |

What each column shows:

- **Unconstrained transit** would pay people to ride, since a negative fare is pure diversion away from underpriced cars. It runs a $21.67M/week bigger deficit. Emissions barely fall because the extra buses and trains offset the cars taken off the road.
- **Budget-constrained transit** gains almost nothing ($0.62M). Frequency still goes up, but fares have to rise to pay for it, so the markup and Spence terms dominate. The authors read the gap between this optimum and today's CTA (lower fares, lower frequency) as pressure to keep fares affordable: their budget optimum is regressive.
- **Road pricing alone** sets a toll that roughly doubles the per-km cost of driving, about $15.20 a day for the average car commuter. About a third of the toll is environmental and two-thirds is congestion. The welfare gain is real but travelers lose. Even with every dollar rebated, consumer surplus falls $0.39M a week. A downtown cordon charge, at its optimal $8.75, captures only $1.24M, a third of the per-km gain.
- **The combination** runs a toll surplus that funds free transit with frequency up by a third or more, and still has money left over. Rebating the remainder turns consumer surplus positive, up to +$4.34M a week. That is the only scenario in which travelers as a group come out ahead.

Prices are robust to the inputs: a 10% change in any parameter moves fares by under 3¢ and the toll by under 2¢/km. Optimal frequencies are less stable, moving about 5% for the same shock.

## Distribution

Without rebates most of these policies are regressive. Faster transit and less congestion are worth more to people whose time is worth more. Measured as a share of consumer surplus, road pricing is highly regressive. A flat per-resident rebate reverses this and leaves the lowest quintile better off. Even in the best package, though, middle-income residents end up worse off: they drive the most and get the least out of a transit upgrade.

## Granularity: frequency matters, toll design mostly doesn't

- Varying the toll by time, by place, or both (CBD rush hour up to $0.63/km) adds at most 1.3% to welfare. Carbon damage doesn't depend on where or when you drive, and the congestion and diversion terms vary in opposite directions across space and time, so they largely cancel.
- Reallocating transit frequency is worth a lot. Nearly doubling service on high-utilization routes and cutting low-utilization routes about 20% raises the budget-constrained gain from $0.62M to $3.39M, more than five times as much. The authors read this as misallocation in the status quo. It is still only about half of what the toll-plus-transit package delivers.

## Implications

- **The fare-free vs. frequency argument is a false choice, and it only resolves with a new revenue source.** Free-transit advocates and frequency advocates are each half right. Without new money the model says fares should go *up* to pay for more service. With toll revenue the city can have both. A city that drops fares without new money is spending its constrained budget on the wrong margin.
- **The political problem is the middle quintile.** Road pricing's efficiency gain shows up mostly as lower externalities, which voters don't see, while drivers see the toll. Middle-income drivers lose even under the best package with rebates. That fits how hard congestion charges have been to pass, and suggests a pitch built on "the toll buys you a bus every four minutes" rather than on the toll itself.
- **Charge by distance; skip the fine-tuning.** A per-km charge beats a cordon threefold, yet time-and-place variation adds about 1%. The big decision is the instrument, and simple versions capture almost all the gain.
- **Ride-hailing is already roughly Pigouvian.** In a side counterfactual, the status-quo ride-hailing price is only 1% below optimal. The platforms' markup happens to roughly equal the externality charge, which is why the authors leave ride-hailing untolled.
- **Frequency vs. coverage, two cities.** [[optimal-transit-networks|Kreindler et al.'s Jakarta study]] finds the bus network too concentrated downtown and recommends spreading service into uncovered areas. Chicago, with routes held fixed, finds the opposite reallocation pays: move buses *toward* the busiest routes. The two results answer different questions (adding new coverage vs. reshuffling capacity across existing routes) and rest on different conditions (short downtown waits in Jakarta, mostly empty buses in Chicago). Both find the status quo misallocates. Both also rely on the Mohring effect: more riders support more frequency, which lowers per-passenger cost.
- **What the model leaves out.** Residents and firms are held in place. The paper cites estimates that sorting moves road-pricing welfare by −20% to +18%. Time-of-day shifting is folded into the outside option, and outbound and return trips are modeled separately. New rail lines are excluded on purpose because US transit construction is so expensive (Brooks and Liscow 2023). The levers here are the cheap ones. Unlike road widening, which [[induced-demand]] warns fills back up, a toll takes road space by price.

## Temporal notes

- The baseline is January 2020, a pre-pandemic winter month. CTA ridership has not returned to 2019 levels, so buses are likely emptier than in the data. That strengthens the zero-marginal-cost premise, but the demand estimates may be off for post-remote-work travel patterns.
- New York's Manhattan charge, "recently approved" in the paper's framing, started in January 2025 as a cordon charge ($9 peak for cars). The Chicago results suggest a cordon recovers about a third of a distance-based charge's gain.
- Roughly a third of the optimal toll comes from pricing carbon at the EPA's 2022 proposed $190/tonne. In 2025 the federal government stopped using a social cost of carbon in policy analysis. The paper's sensitivity check (a 10% carbon-cost change moves the toll by under 2¢/km) suggests the congestion part of the case holds without it.

## Sources

- Almagro, Barbieri, Castillo, Hickok & Salz (2024, rev. 2025). "Optimal Urban Transportation Policy: Evidence from Chicago." NBER Working Paper No. 32185. <https://www.nber.org/papers/w32185> — [[2024-03-optimal-urban-transportation-policy-chicago|local copy]]
