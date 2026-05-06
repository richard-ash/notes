---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2016-10-22-dozen-things-multi-sided-markets.md
compiled_at: 2026-05-06
model: claude-opus-4-7
confidence: high
---

# Multi-Sided Markets

A **multi-sided market** (often called a "platform") is a business that brings together two or more interdependent groups of users who need each other and lets them transact directly. The defining structural feature, as Tren Griffin summarizes, is that "the sides interact directly" — Uber riders meet drivers, eBay buyers meet sellers, LinkedIn recruiters meet candidates, App Store consumers meet developers. This contrasts with the **single-sided / linear value chain** described in *Platform Revolution* — "a step-by-step arrangement for creating and transferring value with producers at one end and consumers at the other" — where a market-maker buys, holds inventory, and resells.

The economic significance of the distinction is non-linearity: a correctly structured multi-sided market can scale value faster than costs. Esko Kilpi's framing: "Network effect-based value can increase exponentially at the same time as costs grow linearly, if at all." Tom Goodwin's much-quoted version of the implication: "Uber owns no vehicles. Facebook creates no content. Alibaba has no inventory. And Airbnb owns no real estate." Less capital tied up, more upside compounding through [[network-effects|network effects]].

## Why most attempts fail

Hundreds of would-be platforms launch each year. The reason VCs and founders keep trying despite the high failure rate, Griffin argues, is asymmetric payoff: it is *magnitude* of correctness, not *frequency*, that determines returns. One Apple, Amazon, or Facebook pays for many dozens of failed attempts. But "getting all the elements just right at just the right time" is genuinely hard — every multi-sided market that succeeds has solved a sequence of distinct structural problems, any one of which can kill the business.

The four structural problems, in approximate order of operation:

1. **Is there a coordination problem worth solving?**
2. **Can a side or sides be subsidized into existence?** (the chicken-and-egg problem)
3. **Do the sides actually complement each other?**
4. **Where is the profit pool?**

Each is treated separately below.

## The coordination test

A platform is only valuable if the sides cannot easily find each other on their own. The deeper economic claim — Hayek's coordination problem, restated — is that markets exist to discover prices and allocations among participants who hold different and changing knowledge under uncertainty. Multi-sided platforms add scaffolding (reputation, search, dispute resolution, escrow) that makes that discovery feasible at fragmentation levels where it otherwise fails.

The diagnostic question Griffin offers: *if Boeing needs a rivet supplier, once it finds one, does it need a marketplace?* No — and that is the test. Bilateral, repeat, low-variance procurement does not need a platform. The high-fragmentation, high-variance, hard-to-search markets are where platforms create surplus: Airbnb (idiosyncratic supply, occasional demand), Uber (real-time geographic matching), UpWork/ProFinder (skill heterogeneity), Etsy (long-tail taste). If the matching problem is easy or solved by a phone call, no platform will compound.

This is why **B2B vertical platforms** so often disappoint: the coordination problem they're solving is too small, repeat-business reduces it further, and switching costs eventually pull supply and demand directly into bilateral relationships once each side knows whom they want to deal with.

## Demand- vs. supply-side scale economics

Griffin distinguishes the two flywheels every platform leans on:

- **Demand-side economies of scale** (= [[network-effects|network effects]]): value to users rises with the number of users — positively (social networks, marketplaces) or negatively (congestion, spam, fraud).
- **Supply-side economies of scale**: average cost per unit falls with production volume.

The fashionable claim in 2016 was that supply-side scale "no longer matters" because network effects had eclipsed it. Griffin pushes back: the strongest moats stack both. AWS combines a developer/customer ecosystem (demand-side) with web-scale infrastructure unit costs (supply-side) that smaller competitors cannot match. Amazon retail does the same with reviews and Prime selection on one side and fulfillment density on the other. **A moat can never be too strong** because it is always under attack — adding supply-side scale on top of network effects is belt and suspenders, not redundancy.

This connects to the broader [[competitive-moats|moat taxonomy]]: network effects and supply-side scale are two of the structural sources of durable advantage; brand, regulation, and IP are the others. Without one of these, financial returns drift to the cost of capital.

## The chicken-and-egg problem and the loss-leader solution

The operational obstacle every platform faces: *how do you get one side to participate before the other side exists?* Below [[network-effects#Critical mass|critical mass]], the network's "value depends on others using it" property is a tax rather than a flywheel — a side that arrives first finds nothing of value waiting for them.

Griffin's structural prescription has three parts that must all be true together for the bootstrap to work:

1. **One or more sides must be designated the loss leader.** Pricing one side below marginal cost — sometimes literally below zero (cash incentives, signing bonuses, free hardware) — is the only way to seed the side that will not show up unsubsidized. *Which* side gets subsidized doesn't actually matter much; *that* a side is clearly subsidized is what matters.
2. **The subsidized side has predictable characteristics.** Higher demand elasticity, harder to recruit, more important to the other side. For Uber, that's drivers — they are the rate-limiting resource. In US residential real estate, it's buyers (free representation, paid by the seller). In credit cards, it's cardholders (free cards, paid by interchange on the merchant side).
3. **The subsidy must use a low-marginal-cost good.** Giving away software, signal, or matching capacity is sustainable; giving away hardware or storage or physical inventory bleeds out before critical mass. This is why software platforms can subsidize aggressively and hardware platforms (e.g., consoles selling at a loss) operate on borrowed time until the software side compounds.

The combination — subsidize a price-elastic, hard-to-recruit side using a low-marginal-cost incentive — is the bootstrap recipe most successful platforms followed. Griffin echoes Chris Dixon's "come for the tool, stay for the network" pattern (also discussed in [[network-effects]]) as a related solution: launch the platform with single-player utility so the first side has reason to show up before the other side exists.

The chicken-and-egg trap is also temporal: cash and momentum run out. Get to critical mass too slowly and you die before the flywheel turns. Get there too fast and you may waste capital subsidizing past the inflection. Griffin notes you may also face competitors acting extremely aggressively or irrationally — this connects to Bill Gurley's "play the game that is on the field" framing, which is the same warning generalized.

## Sides as complements

Multi-sided markets work best when the offerings on either side are **complements** — goods or services where each makes the other more valuable. Cars and gasoline; chips and salsa; search results and search ads; smartphones and apps; social-network users and advertisers. When the sides are complements, the platform reduces customer acquisition cost on both sides simultaneously: each side's presence draws the other in, so marketing can ride the existing demand.

This is more than a definitional point. **If the sides are not complements, the platform is fighting human disinterest on both sides at once.** Marketplace ideas that pitch "supply-meets-demand" without checking whether the participants actually want to transact tend to fail — the platform shows up to a party where nobody wanted to meet anyone. The complement test is a cheap diagnostic worth running before any platform investment.

The complement framing also explains why monetizing the "other side" of an existing complement is the most reliable platform business model: if you've assembled an audience for X, monetize via the natural complement of X (search → ads, social → ads, video → ads, free email → ads). The product was a complement to the monetization mechanism the whole time.

## Profit pools and the holistic view

Griffin's closing point is the one most easily lost in the loss-leader excitement: **products and services at a given business cannot all be loss leaders.** Subsidies are a tactic for optimizing customer acquisition and lifetime value across the whole platform, not a standalone strategy. Somewhere in the system, a profit pool must exist — a side or layer that pays enough to cover the subsidies and the cost of capital plus a return.

Concretely:

- Apple subsidizes free OS upgrades and free iCloud tier; the profit pool is hardware margin and the App Store rake.
- Google subsidizes search and Gmail; the profit pool is advertising on commercial intent.
- Uber historically subsidized rides; the (eventual) profit pool is take rate on the matched transactions, plus expansion into Uber Eats and freight.

A platform that cannot answer the question "*which side, in steady state, monetizes?*" is not a platform — it is a marketing campaign masquerading as one. The fact that ride-hail, food delivery, and many on-demand services took a decade or more to demonstrate sustainable unit economics suggests how often founders skipped this question, treating "we'll figure out monetization later" as compatible with platform strategy. It generally isn't, because the rake choice (see [[marketplace-rake]]) interacts with the bootstrap dynamics — too high and you slow critical mass, too low and you never produce the profit pool.

This is also where multi-sided market strategy hits the broader [[strategy-execution|strategy-as-coherent-choices]] frame: subsidy, complement structure, side selection, rake, and acquisition channel must form a self-reinforcing set. Pulling on any one without the others is the most common failure mode.

## Why platforms are rare at scale

Putting the pieces together, a platform that succeeds has cleared all of:

1. A coordination problem real enough that participants cannot bypass the platform once matched.
2. A demand-side economy of scale strong enough to generate a moat once seeded.
3. A bootstrap mechanism (loss leader on the right side, with low marginal cost) that gets through critical mass before cash runs out.
4. Sides that are genuine complements, so user acquisition cost stays manageable on both sides.
5. A clear profit pool somewhere in the system that, in steady state, funds the subsidies and earns above the cost of capital.
6. Often, supply-side scale economics on top, so the moat is not solely a network-effects moat (which can be brittle, see [[network-effects]] on Friendster, MySpace, BlackBerry).

The reason successful platforms cluster at the top of the market-cap rankings — Apple, Microsoft, Google, Amazon, Facebook, Alibaba, Visa/Mastercard — is that clearing all six conditions is genuinely rare. The reason hundreds of platform attempts launch each year is the asymmetric payoff: clearing them once produces a category-defining business that prints capital indefinitely.

## Connections to other frames

- The **chicken-and-egg / critical-mass section** of [[network-effects]] is the same logic from the network-effects mental-model perspective; this article approaches it from the platform-design perspective.
- [[marketplace-rake]] is the pricing-side companion: once the platform exists, what take rate on the profit-pool side maximizes long-run value rather than short-run extraction. Gurley's case studies (Booking, oDesk) are textbook applications of "establish supply with low rake, monetize with opt-in placement auctions."
- [[aggregation-theory]] is the same family of ideas viewed through Ben Thompson's lens: zero-distribution-cost platforms commoditize supply and own demand. Aggregators are a subset of multi-sided markets — those whose moat sits on the demand side and whose supply is internet-distributable.
- [[ai-platform-moats]] is the negative case: Evans's argument that foundation-model companies look like platforms but lack the structural elements above (no real network effect, no real complement structure, no lock-in), so they will not compound the way Apple/Google did.
- [[startup-uncertainty]] explains *why* an entrant could ever win against an incumbent platform with these moats: the founding moment is Knightian-uncertain, and incumbents are structurally barred from acting in that uncertainty window. Most successful platforms today were founded into uncertainty windows the incumbents could not see or could not justify acting on.

## Temporal notes

The source is from 2016. The decade since has confirmed most of the framework while sharpening a few of the edges:

- **The "platforms eat verticals" thesis** played out broadly: Uber/Lyft and Didi consolidated ride-hail per geography; Airbnb consolidated short-term rentals; DoorDash/Uber Eats consolidated US food delivery; Shopify and Amazon consolidated e-commerce supply. The Tom Goodwin asset-light line ("Uber owns no vehicles…") became the dominant frame for thinking about technology businesses.
- **Subsidy-side strategy has become much more visible.** The decade-long "blitzscaling" period — characterized by burning capital on subsidy to seed critical mass — was, in retrospect, a real-world test of Griffin's loss-leader prescription. Some platforms graduated to profitable monetization (Uber Rides, DoorDash); others did not (WeWork, scooter sharing, Q-commerce, most metaverse experiments). The pattern that distinguished winners was the presence of a real coordination problem and a real complement structure under the subsidies — exactly Griffin's test.
- **AI changes the frame.** Foundation-model companies superficially look like platforms (they have developers and end users) but lack the multi-sided market structure: developers can switch APIs trivially, end users have no per-user lock-in, and there is no clear demand-side network effect at the model layer. This is the explicit subject of [[ai-platform-moats]]. The 2016 framework remains the right diagnostic — and it is what reveals that AI labs are mostly *single-sided* infrastructure businesses with platform aesthetics.
- **The complement structure of social platforms cracked.** Facebook's user-side and advertiser-side complement was strong from 2008 to roughly 2020; signal-loss from ATT/iOS privacy changes, regulatory pressure, and demographic decay weakened the advertiser side specifically because the user-side targeting fidelity that made the complement powerful was the regulatory pressure point. Multi-sided market moats are not as fixed as they look in steady state.
- **Hardware as profit pool, software as loss leader.** Apple's strategy through 2016 looked like the canonical "subsidize the side with low marginal cost" prescription — give away iOS updates, charge for hardware. Services revenue (App Store, iCloud, Music, TV+) has now grown into its own profit pool, and Apple has diversified into a multi-pool platform. The basic structural lesson holds.

## Sources

- Griffin, Tren (2016). "A Dozen Things I've Learned about Multi-sided Markets (Platforms)." *25iq*. <https://25iq.com/2016/10/22/a-dozen-things-ive-learned-about-multi-sided-markets-platforms/> — [[2016-10-22-dozen-things-multi-sided-markets|local copy]]
