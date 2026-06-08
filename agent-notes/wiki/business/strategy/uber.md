---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-06-03-khosrowshahi-uber-invest-like-the-best.md
compiled_at: 2026-06-08
model: claude-opus-4-7
confidence: medium
---

# Uber

A case study in operating a physical-world [[aggregation-theory|aggregator]] through a generational technology transition. As of mid-2026, Uber runs ~10M couriers and drivers, ~10B trips per year, $10B+ in free cash flow, and has 50M Uber One members growing at 50% YoY. CEO Dara Khosrowshahi — who joined in 2017 from Expedia at the depth of the Travis Kalanick-era crisis — describes a company whose strategic problem has shifted from "stop bleeding" to "win the trillion-dollar autonomous-vehicle marketplace by being the largest amalgamator of AV supply rather than the builder of any particular AV stack." The interview reads as a worked example of how an incumbent aggregator positions for a technology shift that could either dramatically expand its TAM (if it captures AV demand aggregation) or commoditize it (if AV operators bypass it).

## Supply-first marketplace philosophy

Khosrowshahi's central operating insight, brought from his Expedia → Uber transition, is that Uber inverts the demand-first orientation typical of consumer-internet companies. At Expedia, the company chased consumers to the site and built hotel/flight inventory in response to demand. **At Uber, supply comes first and demand follows.** The biggest growth lever is not acquiring more riders but securing more drivers, restaurants, couriers, and merchants — particularly in the long tail of sparse markets ("not the top 10 cities in a country but the next 50, the next 200").

This is the operational restatement of the supply-side scale economics described in [[multi-sided-markets|Griffin's framework]] for platforms: where Uber is dense enough that finding a driver is cheap, riders show up. The strategic implication for Khosrowshahi is that anything that secures additional supply — fleet financing, AV partnerships, driver retention, merchant onboarding in tier-2 cities — directly buys future demand. This is consistent with Thompson's [[aggregation-theory|aggregation framing]], which identified Uber as one of the canonical post-Internet aggregators that modularized fleet management (independent drivers replacing owned fleets) and integrated with consumer demand. Khosrowshahi's contribution is to specify *which side* of the modularize/integrate move is the binding constraint in practice: it's the supply side, despite the demand side being where the brand and surplus live.

The supply-first philosophy also explains a quality concern Khosrowshahi names explicitly: a typical rider interacts with the app for 30 seconds; a driver has the app open 6–10 hours a day. A P95 bug a rider hits once a month, a driver hits every week. Putting employees behind the supply-side interface — Khosrowshahi bought an e-bike and delivered food in San Francisco during COVID — is the operational response. He frames this under a corporate value called "building with heart": the numerical engineer's instinct must be paired with felt empathy for the side of the marketplace that lives in the app.

## AV strategy: partnerships, not vertical integration

Khosrowshahi's AV thesis is structurally analogous to his read of the foundation-model market: **there will be no single winner**, just as there isn't in LLMs. Waymo, Wayve, Pony.ai, Wabi, Nuro, Lucid+Nuro joint products, Nvidia (now offering a software driver in addition to compute), and a growing list of OEMs investing in L4-ready systems will all exist. Uber's strategic bet is to be the **go-to-market layer for all of them** — over 30 active partnerships as of mid-2026 — rather than building its own digital driver.

The build-around-the-driver play involves the supporting infrastructure that any AV operator needs but can't easily build:

- **Demand aggregation** — Uber's existing rider base, by Khosrowshahi's data, makes AVs on the Uber network 30%+ busier than AVs operating off-network. At hardware costs of $60–70k per AV (the Lucid-Nuro midsize Uber has commissioned), that utilization differential moves ROI from marginal to attractive.
- **Depots and charging** — Uber is buying physical real estate for fleet operations in cities where the regulatory landscape is moving in the right direction.
- **Fleet financing** — A newly announced $1B financing line with Santander for EV and AV fleets, plus autonomous-vehicle insurance underwriting in development.
- **Data collection** — Uber drivers are continuously collecting street-level data that can be sold or used to train AV partners' models. This is a flywheel: the AV operator gets training data and demand, Uber gets supply and insurance underwriting profits.

This is structurally the same play [[aggregation-theory|aggregators]] have run in adjacent industries — Khosrowshahi explicitly draws the parallel to online travel agents who coexist with Marriott and Delta even when those hotels and airlines build direct channels, because the platform delivers incremental demand for capacity the hotel/airline must fill regardless. A Waymo with its own direct app may still want Uber demand because empty AV seats earn zero. The unit economics asymmetry — 70% utilization vs. 90% utilization is "night and day" for a hotel, and the same holds for a $70k AV — is what keeps incumbents on the platform even when they would prefer to disintermediate.

Khosrowshahi's stated premortem ("what kills this strategy?") within Uber's control is **access to supply**: if AV operators successfully build direct channels and the demand differential collapses, Uber's value-add evaporates. The competitive moves are therefore mostly supply-locking: every AV partnership signed, every depot leased, every financing line drawn down is insurance against that scenario. Outside Uber's control, his premortem is societal backlash — AVs are popular among Uber drivers in Austin and Atlanta because they are adding incremental demand, but the public-facing narrative of "AV displaces driver" could reverse the regulatory trajectory in cities like New York and Boston that are already slow-walking permits. The Middle East (Abu Dhabi, Dubai, Saudi Arabia) is moving fastest because regulators there are entrepreneurial; Europe is starting (commercial robotaxi pilots in London by year-end 2026); the US is bifurcating between AV-friendly states (California, Texas) and the slow lane.

This strategic posture is the polar opposite of [[waymo-autonomous-driving|Waymo's]] vertical integration model. Waymo builds the foundation model, the teacher/distilled-student architecture, the sensor stack, and a directly branded ride-hailing service. Khosrowshahi's claim is that the unit economics make it irrational for Waymo to *only* run direct: any depot-night where Waymos sit idle is foregone revenue Uber can fill. The two stances are not contradictory because they answer different questions (Waymo: how do we build the safest driver? Uber: how do we monetize whoever's driver wins?), but they imply different long-run profit pools. Brooks's [[ai-robotics-hype-cycles|long-tail skepticism]] cuts in Uber's favor here: if AV deployment really takes 5–15 more years to generalize beyond geofences, Uber's optionality of partnering with whoever solves which geographies first is worth more than betting on a single stack.

## The trillion-dollar TAM claim

Khosrowshahi sizes AVs as "another trillion-dollar marketplace" on top of Uber's existing trip volume. The argument rests on three components:

1. **Hardware cost curve.** AV hardware costs historically fall 30–40% per generation; AV software costs will fall on the same curve. At sub-$70k purpose-built vehicles, transportation cost-per-mile drops below the human-driver line.
2. **Demand elasticity.** As Uber lowered ride prices over its history, demand growth outpaced expectations. Original taxi-market sizing turned out to be "multiple times" too small. AVs apply the same elasticity at a steeper price drop.
3. **Vehicle utilization.** Each L4 vehicle drives 3–4× what a human does. Even if the unit count never matches today's car parc, the trip count can.

This expands the [[aggregation-theory|aggregation TAM]] for whoever owns demand. It also implies — without Khosrowshahi saying it explicitly — that the Chinese AV manufacturing base ("incredibly impressive in quality and cost, unrivaled") is the gating factor on hitting those price points in the Western hemisphere. Uber's commissioning of Lucid+Nuro is partly a hedge against US/EU AV hardware staying expensive; a Western "Foxconn for AVs" doesn't yet exist and Khosrowshahi flags it as needed.

## Drones: not yet, but in the 5-10 year window

On drone delivery, Khosrowshahi is more cautious than on AVs. The gating constraint is battery energy density: drones must lift their own batteries plus a payload, with sufficient range and recharge cycles. Joby has people-carrying drones working; food/grocery drones will "hit real scale over the next two to five years" but will cost more than human delivery initially. Two-year horizon: no. Five-to-ten years: "more and more normal." The strategic implication is that Uber Eats is not at near-term existential risk from drones, but the same partnership-driven amalgamator playbook applies once unit economics work.

## Uber One: the cross-platform membership flywheel

50M members growing 50% YoY, with Khosrowshahi explicitly modeling Uber One as the **Amazon Prime template** adapted to a variable-cost business. The framework:

- **The Netflix-style fixed-cost membership** (programming is a sunk cost, additional viewing is free to serve) is the easy case. Travel and entertainment loyalty programs work because the benefit is often an upgrade to a room or seat that was empty anyway — zero marginal cost.
- **The Amazon-style variable-cost membership** is harder. Each Prime delivery costs Amazon money; the more a member uses it, the less profitable that member is in the short term. Amazon walked through what Khosrowshahi calls the "valley of despair" — public-market losses, analyst incomprehension — because it understood the unit economics over a 3-4 year horizon, not the first year.
- **Uber One mirrors Amazon's bet.** The first year of an Uber One member loses money. Years 2-4 are profitable, and the program is solidly profitable in aggregate now. Khosrowshahi explicitly cites Amazon as the inspiration for tolerating the early losses.

The flywheel is amplified by Uber's **cross-platform structural advantage**: mobility customers get upsold to Eats (13% of Eats bookings originate from the mobility app), Eats customers get upsold to grocery, all of them get hotels. Uber One is the membership wrapper that monetizes the cross-platform retention. Khosrowshahi's positioning vs. competitors (DoorDash, Lyft as single-vertical players): "for the same price, you get more content than anyone else" — a direct Netflix analogue applied to local services.

The strategic insight here is that **single-vertical food-delivery players cannot match the membership value proposition** because their fixed-fee envelope can only cover one variable cost. Uber One's discounts on mobility, surge protection, free delivery, grocery fee waivers, and 10% hotel cashback all fit inside one subscription because the cross-vertical attach rate amortizes the cost. This is the cross-platform restatement of Spolsky's [[commoditize-your-complement|complement logic]]: making the price of *one* Uber service lower expands demand for *all* of them, because the membership wrapper makes adjacent services free or near-free at the margin.

## Cross-platform expansion: trains → hotels → the planned-trip stretch

Uber's content-and-retention loop — "the more services you have, the more you interact with them, the more you come back" — is the operating reason behind a series of category extensions:

- **Trains** (UK and Spain) — first non-mobility travel product; validated that "more content = more retention" at the cross-platform level.
- **Hotels** — via a deal with Khosrowshahi's old company Expedia, with Uber giving "the vast majority of the economics back to Uber One members." 10% off all hotels, 20% off 10,000 select hotels. The bet is not on hotel-booking economics per se but on locking in Uber One renewals and creating an in-market journey Uber can wrap.
- **Uber Reserve** (planned rides) — over $5B run-rate now, didn't exist five years ago. Pre-commit at 99%+ reliability, higher price, drivers accept ahead. This proved that Uber's *brand* — historically known for on-demand "push a button" — could stretch into pre-committed planning.

The premortem Khosrowshahi names for the hotel push is **brand-stretch failure**: Uber's identity is on-demand, and stretching it into "plan your vacation 2-3 months ahead" might not work. Uber Reserve is the proof-of-concept that pre-commit works for a few-hours horizon; hotels test whether it can stretch to weeks or months. He calls it "not a slam dunk." The strategic logic for trying it anyway is the in-market vision: a hotel booking should pre-book the airport ride, the hotel-to-restaurant ride, and (eventually) use the Uber app as a room key. The booking is the wedge; the in-market wrap is where the long-run value sits — and where the [[multi-sided-markets|coordination problem]] Uber already solves (real-time geographic matching) compounds with the new content.

This is also where the marketing thesis evolves. Khosrowshahi describes flipping his prior mental model — "marketing's job is to get people to the app, product's job is to surface the right service" — after his marketing team pushed back. The new model: marketing builds *storylines* (Uber Teens picking up your kid after a game, Reserve delivering hot coffee before the airport ride) that convey the *abstraction* — "Uber gives you your time back across a broad array of services" — rather than discrete product features. The agents-and-apps follow-up question Khosrowshahi answers: in seven years, inbound interaction (your speech to the app) will be largely unstructured AI; outbound (the picture of the car arriving) stays as a structured UI. This is consistent with [[agent-harness|Taylor's harness thesis]] applied to a consumer marketplace: the agent layer eats the input side, but the visual confirmation of physical-world fulfillment doesn't translate to text and isn't going anywhere.

## Capital allocation: organic growth > buybacks

Khosrowshahi's answer to "are you Amazon or Apple?" is "somewhere in between," with a stated preference toward growth. The hierarchy:

1. **Organic investment first.** Uber Eats grew from <$1B in gross bookings when he joined to $100B+ now; that took enormous organic investment that wouldn't have happened under buyback prioritization.
2. **AV ecosystem investment second.** Fleet financing commitments, AV partnerships, the Santander credit line, autonomous insurance underwriting. "We've got to be the ones developing the market." These commitments will be financialized via debt rather than equity, but Uber's commitment is what unlocks the financing.
3. **Buybacks third.** "Plenty of cash left over for buybacks," but explicitly behind innovation and organic growth. "If you're building the company right, you'll do both."

The compounding-math frame ("costs grow slower than revenue and good things happen over a long period of time") is straightforward investment-banking-trained discipline. The interesting part is what Khosrowshahi *doesn't* say: he doesn't try to defend buybacks-as-strategy, and he doesn't apologize for the Amazon-style capex tilt. The implied stance is that in a high-rate-of-change environment, the option value of organic-growth investments dominates the certainty of share-count reduction.

## AI inside the company: blew through budget, rebuild rather than optimize

Khosrowshahi describes Uber as "AI-native" in the sense of having used probabilistic ML for matching, ETA prediction, and fraud detection long before LLMs. The current LLM-era rollout has produced three observations:

1. **Adoption is bottoms-up and unpredictable.** Devs in India suddenly driving 10× the code commits they used to; autonomous-agent uptake spread across legal, marketing, debugging, on-call, and platform migrations in patterns no top-down forecast predicted. Khosrowshahi's posture: encourage usage, find the rebels, promote them. He explicitly does not want to be the single point of failure for AI strategy.
2. **The CEO push is to rebuild, not optimize.** Optimizing an existing process 20-30% with AI is "a decent first step" but easy. Rebuilding the process from first principles using AI as the substrate is "much harder" and is the bar Khosrowshahi is holding teams to. This connects to [[ai-and-org-design|Taylor's "atomic unit of AI productivity is a process, not a person"]] thesis: the leverage is on the process boundary, not the headcount inside it.
3. **Budget blew up in a quarter.** Uber's full-year AI budget was consumed in the first quarter. The response is a two-handed policy: continue encouraging adoption (to find the winning rebuilds), but meter headcount growth (the marginal AI cost partially substitutes for the marginal engineer cost) and triage workloads — frontier models (Claude, OpenAI's) for exploration, cheaper open-source or distilled models for scale. This is structurally the same framing as Thompson's opportunity-cost-of-compute argument in [[aggregation-theory|Aggregation Theory]]: compute is a fixed cost, allocation is the question, and the discipline is to use the expensive models where the marginal experimental value is highest and downshift to cheaper inference once the interaction proves out.

The framing matters for Uber specifically because its margin structure is thin (~$10B FCF on $100B+ trips). Khosrowshahi's stated reason for caring about efficiency is to "lower prices for riders and give more earnings to our earners" — i.e., to pump AI productivity gains back into the marketplace's price elasticity rather than retaining them as margin. This is a non-obvious strategic choice; the obvious alternative would be to keep the savings.

## Management practices: ground truth, troublemakers as mutations

Two practices Khosrowshahi credits to his mentor Barry Diller and his early years at Allen & Company:

### Going to the source

Diller's habit of demanding to talk to the analyst who built the LBO model, not the MD or VP, is the structural insight. As organizations scale, the CEO receives a thin, processed layer of information curated by well-meaning intermediaries. The average is widely shared and not informationally valuable; the **edge** (the P95 case, the 20% outlier, the unfiltered ground truth) is what gives leaders an actual decisional edge — and is exactly what processing strips out. Khosrowshahi's operational habit: be brutally frank himself ("what's good, what's bad, what's okay, where I don't know the answers"), which models the truth-telling behavior the team is then permitted to mirror back to him. This is structurally what Horowitz prescribes in [[truth-telling-leadership]]: the inverse relationship between trust and required communication, where lying compounds the trust deficit multiplicatively across an org.

### Troublemakers as mutations

The metaphor Khosrowshahi uses: companies are organisms, and organisms evolve by mutating. Large companies systematically chase mutations away because the structured org optimizes for getting-along — a single culture, a single process, a single information flow. The CEO's countermove is **build random interactions into the schedule** — meet people outside direct reports, talk to engineers and product leads several layers down, create channels where bad ideas can surface without filtering. "The signals are usually weak, but if a signal becomes strong enough, I move."

This is the operational complement to [[strategy-execution|Vermeulen's bottoms-up experimentation principle]] in *Strategy Execution* — strategy is a coherent set of choices implemented through bottom-up experimentation, and the experimentation requires a structural counter-pressure against the homogenization that natural process design produces. It's also a corollary to Khosrowshahi's stated leadership identity: "I'm a learning creature; the magic happens when you learn; learning has to come with pain." The troublemakers are the source of the pain that produces learning.

## The Khosrowshahi turnaround as a decomposition exercise

When Khosrowshahi joined Uber in 2017, the diagnostic he applied to the chaos was vector mathematics: a complex multi-dimensional problem can be decomposed into single-dimension problems that each have a tractable solution. The Uber-specific decomposition:

- **Board** — fighting for control rather than for the future of the company. Bring in Ron Sugar as chairman to broker peace.
- **Stakeholder trust** — lost with regulators and the public. Go on a listening tour, then act on what is heard, then communicate both internally and externally.
- **Management team** — talent in place but some legacy executives stuck in the prior culture. Move them out; retain core long-term operators like Andrew McDonald; bring in new senior management like Tony West.
- **Business itself** — fundamentally strong but going through competitive change.

Khosrowshahi attributes his low stress threshold to having lost everything once already (family fled Iran when he was 9; he watched his father's family business collapse and the spark not return). The framework he names is engineering-school: list the problems, define an approach to each, test and learn, accept non-linear progress. "Being stressed out — what's the point? Who cares?" The biographical chip-on-the-shoulder ("Iranian immigrant chip — never satisfied") drove the work ethic; the inherited trauma of his father's experience inoculated against letting work define him as a person.

## Strategic open questions

- **Does AV demand actually flow through Uber rather than around it?** Khosrowshahi's bet on coexistence assumes the Marriott/Delta utilization logic applies. If a single AV operator (Waymo, Tesla, a Chinese-manufactured fleet) achieves dominant scale, the OTA analogy may not hold — the dominant operator could potentially run a one-sided market with no need to amalgamate demand from rivals.
- **Can the brand stretch to planned trips?** Reserve is the proof-of-concept at hours; hotels is the test at weeks/months. Khosrowshahi explicitly calls it "not a slam dunk."
- **Does the membership unit economics survive AV pricing?** Uber One's free-delivery benefit is funded by Uber's take rate on driver-fulfilled trips. If AV margins are different (lower per-trip operating cost, higher capital cost), the membership cost structure needs to be re-derived.
- **Drone unit economics.** Khosrowshahi explicitly says drones cost more than human delivery initially; the cost-curve thesis is plausible but not yet demonstrated.
- **AI cost discipline at scale.** "Blew through the budget in a quarter" is a striking admission for a low-margin business. The metering on headcount and downshift-to-cheap-models policy is conventional, but the underlying compute opportunity-cost is the same problem [[aggregation-theory|Thompson highlights]] for hyperscalers — compute allocated to AI exploration is not available for production inference, and the choice surfaces real opportunity-cost tradeoffs.

## Connections

- [[aggregation-theory]] — Uber is the canonical physical-world aggregator in Thompson's framework. Khosrowshahi's supply-first operational philosophy specifies which side is the binding constraint in practice and how an aggregator positions for a technology shift (AV) that could either expand or commoditize its TAM.
- [[multi-sided-markets]] — Khosrowshahi's framing of supply-vs-demand priorities, cross-platform attach rates, and the membership flywheel are operational instances of Griffin's coordination/scale-economics/complement/profit-pool framework.
- [[waymo-autonomous-driving]] — Waymo is the structural counterpoint to Uber's strategy: vertical integration with a foundation-model → teacher → distilled-student architecture and a direct ride-hailing service. The two stances answer different questions and imply different profit pools; Khosrowshahi's bet is that even a winning Waymo wants to fill empty seats with Uber demand.
- [[ai-robotics-hype-cycles]] — Brooks's long-tail skepticism on AV deployment timelines reinforces Khosrowshahi's optionality play: if AV generalization takes 5-15 more years per geography, partnering with whoever solves which markets first beats betting on one stack.
- [[ai-and-org-design]] — Taylor's "atomic unit of AI productivity is a process, not a person" thesis is the same insight Khosrowshahi articulates as "rebuild from first principles, don't just optimize 20-30%."
- [[truth-telling-leadership]] — Horowitz's trust-communication inverse-relation is the structural reason Khosrowshahi's Barry-Diller-derived "go to the source" habit works: as the org scales, the CEO's information becomes processed and the edge gets stripped; ground-truth seeking is the counter-pressure.
- [[strategy-execution]] — Vermeulen's bottom-up experimentation prescription is the structural complement to Khosrowshahi's "troublemakers as mutations" practice and his deliberately bottoms-up AI adoption posture.
- [[commoditize-your-complement]] — Uber One's cross-platform membership is a worked example: making one Uber service cheaper expands demand for all of them, because the membership wrapper amortizes the discount across attach.
- [[coca-cola]] / [[snapchat]] — companion long-arc consumer brand case studies. All three illustrate durability sources outside the easily-copied product layer: distribution + brand for Coke, ecosystem + hardware for Snap, supply aggregation + membership cross-platform for Uber.

## Sources

- O'Shaughnessy, Patrick (host) and Khosrowshahi, Dara (2026). "Uber CEO on AI, Autonomous Vehicles, and the Future of Transportation." Invest Like the Best, June 3, 2026. <https://www.youtube.com/watch?v=ThMtheE5eO0> — [[2026-06-03-khosrowshahi-uber-invest-like-the-best|local copy]]
