---
source: agent
compiled_from:
  - agent-notes/raw/economics/2023-06-optimal-transit-networks-jakarta.md
compiled_at: 2026-04-06
model: claude-opus-4-6
confidence: high
---

# Optimal Transit Network Design

Designing a public transit network with a fixed fleet of buses requires balancing three competing dimensions: **directness** (more point-to-point routes vs. hub-and-spoke transfers), **intensity** (more frequent service on fewer routes), and **reach** (covering more origins and destinations). The relative importance of each dimension depends on how commuters weigh travel time on the bus, waiting time at stops, and the hassle of transfers — preference parameters that are difficult to estimate because they require exogenous variation in system-level attributes.

## The TransJakarta natural experiment

Kreindler, Gaduh, Graff, Hanna, and Olken (2023) exploit a rare opportunity: the staggered launch of 93 new routes on TransJakarta — the world's largest Bus Rapid Transit (BRT) system — between 2016 and 2020. Jakarta's metropolitan area (population ~18 million) is served by over 139 TransJakarta routes operating on 120+ miles of dedicated BRT corridors plus non-BRT feeder routes, with a flat fare of IDR 3,500 (~$0.25). Daily ridership peaked around 1 million in early 2020.

The staggered rollout created three distinct types of "events" for different origin-destination (o,d) pairs, each varying a different dimension of service quality:

1. **Event 1 — New direct route, no speed change.** A pair previously connected only by transfer gets a direct route, but total time on the bus is unchanged. Isolates the value of directness.
2. **Event 2 — New direct route + faster.** The new direct route is also faster than the best existing transfer option. Captures directness and speed jointly.
3. **Event 3 — Additional overlapping route.** A new route overlaps with existing direct service between o and d, adding buses and reducing wait times without changing travel time or directness.

The analysis draws on three granular datasets: 500+ million smart card taps from TransJakarta, GPS tracking of every bus every 5–10 seconds (~1,800 buses, ~16,000 trips/day), and anonymized smartphone location data covering 35 million weekday trips from 2.3 million devices (Veraset, March 2018–March 2020).

## Key empirical findings

Using difference-in-differences estimation with origin×destination, origin×time, and destination×time fixed effects:

- **Directness matters:** A new direct BRT route (Event 1) increases ridership by 0.16 log points (~19 additional riders/week per treated o,d pair).
- **Speed matters more on top of directness:** Event 2 increases ridership by 0.27 log points, with travel time falling 0.29 log points.
- **Wait times matter:** Event 3 increases ridership by 0.09 log points, driven by a 0.32 log point increase in bus arrival rates. The implied elasticity of ridership w.r.t. wait times is −0.29 for BRT and −1.05 for non-BRT.
- **Mode substitution, not new trips:** Smartphone data shows no increase in aggregate trip volumes between affected locations. Ridership gains come entirely from commuters switching away from motorcycles, cars, and taxis — not from generating new travel. This is consistent with the [[induced-demand]] literature, though in reverse: improving transit quality draws existing trips onto the bus rather than creating new trips.

Event-study graphs show sharp jumps at the moment of route launch with no pre-trends, supporting the causal interpretation.

## The Mohring effect

The finding that ridership responds to wait times is evidence for the **Mohring effect** — the positive externality where higher ridership justifies more frequent service, which in turn further reduces wait times and attracts more riders. For non-BRT routes, the implied elasticity exceeds −1, raising the possibility of multiple equilibria: a low-ridership/high-wait-time regime and a high-ridership/low-wait-time regime could both be stable. This has policy implications: a one-time subsidy to boost frequency on underperforming non-BRT routes could tip them into the high-ridership equilibrium permanently.

## Structural model of commuter route choice

The authors develop a novel discrete choice model where the idiosyncratic heterogeneity comes from **exponentially distributed random wait times** (following Poisson bus arrivals) rather than the standard logit error. Daganzo (1979) calls this a "negative exponential distribution model." The model has four appealing properties:

1. **Invariant to route aggregation** — splitting an identical route in two doesn't create spurious utility gains (avoids the "red-bus, blue-bus" problem).
2. **Empirically validated** — GPS data confirms bus wait times are approximately exponentially distributed.
3. **Realistic predictions** — overlapping routes reduce effective wait times; commuters sometimes skip the first bus to wait for a better option.
4. **Tractable** — closed-form expressions for expected utility and choice probabilities.

The model adds **partial inattention**: commuters may fail to notice route options whose travel time on the bus is much longer than the fastest option. In a higher nest, commuters choose between the TransJakarta network (integrating over the distribution of wait times) and private transport (motorcycles, cars, ojek) via a logit.

### Estimated preference parameters

| Parameter | Estimate |
|---|---|
| Wait time cost relative to travel time (BRT) | 2.4× |
| Wait time cost relative to travel time (non-BRT) | 4.2× |
| Transfer penalty (beyond wait + travel time) | None (zero) |
| Inattention threshold | 34–44% slower than fastest option |

The absence of a standalone transfer penalty is notable: commuters dislike transfers only because they add wait time and travel time, not because of any inherent switching cost.

## Optimal network design

### The computational challenge

With 418 grid cells and 1,536 possible route edges, the configuration space is ~2^1,536 (~10^500) — far too large for exhaustive search. The authors reformulate the problem: instead of finding the single welfare-maximizing network, they model the social planner as making a discrete choice over all possible networks (multinomial logit with a precision parameter β), then sample from this distribution using **Metropolis-Hastings / simulated annealing**. Properties of optimal networks are estimated as expectations over sampled networks.

### How the optimal network differs from the actual network

| Characteristic | Actual TransJakarta | Typical optimal network |
|---|---|---|
| Grid cell coverage | 42% | ~66% |
| Trip pairs with bus access | 73% | 91% |
| City-center bus frequency | Very high | Somewhat lower |
| Geographic distribution | Concentrated in center | More dispersed |

The central finding is that **the current network is too concentrated**: it packs too many buses into the city center where wait times are already very short, at the expense of geographic reach. Even though commuters are highly sensitive to wait times, the marginal benefit of further reducing already-short center-city waits is small compared to the welfare gain of extending coverage to underserved areas.

### Comparative statics

The framework enables linking micro preference parameters to macro network properties:
- **Doubling wait time cost** → networks connect 41% fewer o,d pairs (more concentrated, higher frequency)
- **Adding a 15-minute transfer penalty** → direct connections rise from 12% to 16% of connected pairs
- These results reveal which preference parameters most influence optimal network shape, and where estimation precision matters most.

## Implications

The paper's three-step methodology — reduced-form causal estimates → structural preference parameters → computational network optimization — provides a template for transit planning in rapidly growing LMIC cities. The key insight for planners: **coverage is likely being underweighted relative to frequency** in many transit systems. When wait times in the center are already low, the next bus is better deployed on a route that brings new areas into the network.

The Metropolis-Hastings sampling framework for characterizing optimal networks is itself a methodological contribution, applicable to any high-dimensional discrete optimization problem where the planner's objective violates the complementarity properties needed for standard approaches.

## Sources

- Kreindler, Gaduh, Graff, Hanna, and Olken (2023). "Optimal Public Transportation Networks: Evidence from the World's Largest Bus Rapid Transit System in Jakarta." NBER Working Paper No. 31369. <http://www.nber.org/papers/w31369> — [[2023-06-optimal-transit-networks-jakarta|local copy]]
