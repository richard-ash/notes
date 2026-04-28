---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2013-04-18-rake-too-far-platform-pricing.md
compiled_at: 2026-04-27
model: claude-opus-4-7
confidence: high
---

# Marketplace Rake

The **rake** — borrowed from poker, where it names the dealer's per-hand cut — is the percentage of gross merchandise sales (GMS) that a marketplace or platform retains as revenue. Bill Gurley's 2013 essay "A Rake Too Far" makes a counterintuitive case: for a platform whose long-term value is winner-take-all dominance, *charging too much* is more dangerous than charging too little. The rake is friction; friction is strategically expensive even when it looks like profit.

## The core argument

It seems tautological that higher rakes produce more revenue. Gurley's claim is that this confuses short-run extraction with long-run capture. The rake gets baked into the landed price the consumer pays, so an excessive rake makes the platform structurally uncompetitive against any cheaper alternative — including disintermediation. It also gives suppliers a permanent reason to look elsewhere.

The healthy formula, Gurley argues, is **high volume × modest rake**, where the value of being in the network plainly exceeds the transactional cost of being in it. Below that threshold, suppliers feel obliged to stay and consumers don't see prices loaded with platform overhead. Above it, the platform creates what Gurley calls "a pricing umbrella that can be exploited by others in the ecosystem, perhaps by someone with a more disruptive business model" — restating Bezos's "your margin is my opportunity" as a structural prediction. This is the same dynamic that runs through [[competitive-moats|the broader moat literature]]: visible high margins draw entry, and platforms whose advantage is supposed to be the network itself can't simultaneously enjoy monopoly-style pricing without inviting attack.

Peter Drucker's "Five Deadly Business Sins" puts worship of premium pricing first. Gurley's reformulation: there is a real difference between what you *can* extract and what you *should* extract.

## A spectrum of rakes (circa 2013)

Gurley's table sketches the range:

- **Very low (≈3–5%):** OpenTable, HomeAway — platforms that pulled supply onto a network by being cheap to join.
- **Low–mid (≈10%):** eBay (≈9.6% in 2011), Booking.com's original agency model.
- **Mid (≈12%):** Amazon Marketplace (range 6–15% by category).
- **High (≈30%):** Apple App Store, iTunes media, Facebook payments, Shutterstock contributor splits (suppliers retain only 30%).
- **Effective ≈70%:** Groupon Daily Deals — a 38% rake stacked on top of the 50% discount Groupon asks the merchant to underwrite, leaving the supplier with ~30 cents on the dollar of consumer-paid revenue.

The Groupon case is the cleanest illustration of why "rake on the rake" matters: nominal headline percentages understate the real economic burden when the platform also forces other concessions.

## The Booking.com playbook

Gurley's exemplar of rake-as-strategy is Booking.com's rise in late-1990s European travel. Expedia and Travelocity favored the **merchant model** — packaging vacations as bundles, where a 30%+ rake was achievable. Booking.com used a **10% agency model**, lower-rake and with better cash-flow terms for hotels. That pricing made it the path of least resistance for nearly every small European hotelier, which produced the supplier breadth that compounded into selection advantage, which compounded into consumer pull, which carried Priceline Group to a $35B market cap (in 2013 dollars).

The non-obvious second move: once supplier breadth was secured, Booking layered an **opt-in auction for placement** on top of the base rake. Suppliers who wanted more volume bid up their effective commission for better ranking. Average rake rose without any supplier being repriced against their will, and — critically — when prices went up, suppliers blamed competitors rather than the platform. Gurley calls this "one of my favorite marketplace business model tweaks" and notes that Google AdWords runs on the same principle. The pattern:

1. Establish broad supplier participation with a low base rake.
2. Layer a competitive market for promotion or placement on top.
3. Let suppliers self-select into higher effective rates.

This separates the *base tax* from the *opt-in expansion mechanism*, which is structurally different from raising the headline rate.

## The oDesk decision

A second case from Gurley's own portfolio: in 2006, oDesk's competitors (Freelancer, Rent-a-Coder) were charging the industry-standard 30% commission. Benchmark and oDesk dropped to 10%, accepting an immediate ~67% cut in current-period revenue. By 2009, oDesk had passed every competitor and become larger than the next several combined.

The decision is a clean demonstration of the trade-off Gurley frames throughout the essay: short-run revenue versus long-run market position. It also reveals the type of investor and founder fit the strategy demands — both sides have to be willing to absorb the near-term hit.

## Apple, Facebook, and the cost of a "30%"

Half the essay is a retrospective on the App Store and Facebook's developer platform, both of which charged a 30% rake. Software's near-zero marginal cost lets developers tolerate this in the short run, but Gurley argues it produced two strategic costs Apple and Facebook didn't fully internalize:

- **Effective rake exceeded headline rake.** Many of the same Facebook game companies were also large advertisers, so the real cost of being competitive on the platform was much higher than 30%. Zynga's 2012 renegotiation — escaping the requirement to share 30% even on revenue earned *off* Facebook — marked the inflection where the gaming industry's enthusiasm for the platform broke. Zynga's later trajectory is now read by shareholders through *how successfully it reduced* its Facebook dependency.
- **Strategic partnerships became impossible.** Gurley's most interesting Apple claim is counterfactual: Amazon and Facebook *should have been* iOS's biggest allies. Both were natural complements; Google was the common threat. But Apple's 30% on App Store revenue, on media, and (most painfully) on in-app digital goods made it impossible for Amazon's Kindle bookstore or Facebook's developer-monetization business to coexist on the platform. Both punted, and both went on to support Android in ways that materially strengthened Apple's only real competitor. The Amazon case is sharper still: by demanding 30% on content, Apple priced itself into a competitor — Kindle Fire — built explicitly on the thesis that consumers shouldn't pay fat margins on both hardware *and* content.

The pattern: a high rake doesn't only tax current participants, it forecloses future ones. The platform's most valuable potential partners are precisely those whose business models can't survive the rake.

## Why this is harder than it looks

Several reasons platforms over-rake despite the strategic argument:

- **VCs structurally encourage extraction.** Gurley notes that most investors push entrepreneurs to maximize what they can capture per transaction. The rake-too-low strategy requires an investor base that will tolerate near-term revenue suppression, which is genuinely rare.
- **Software rakes look free.** Because marginal cost is near zero, software developers don't viscerally feel a 30% rake the way a hotel does. This obscures the friction's strategic cost — until a competing platform offers a different deal.
- **Initial success masks the problem.** Apple's 30% rake worked for years and helped make Apple the world's most valuable company. The cost was opportunity cost — partnerships and ecosystem moves that didn't happen — which is invisible on the income statement.
- **Asking both sides to pay is overconfident.** Gurley flags Apple charging 30% on apps *and* 30% on media as a sign of overreach — extracting value on every axis where you have leverage signals that you've stopped thinking of the network as a partner ecosystem.

## Connections to the broader framework

The rake essay is in some sense a pricing-specific corollary of [[aggregation-theory|Aggregation Theory]]. Thompson's framework explains why aggregators win: zero distribution and transaction costs let user-experience leaders attract users, who attract suppliers, who improve the experience. A high rake directly undermines two layers of this flywheel — it raises the consumer's landed price (degrading the user-experience wedge) and it taxes suppliers (giving them a permanent reason to look for an alternative).

Likewise, marketplace rake interacts with [[network-effects|network effects and critical mass]]. A platform's network-effect moat is most fragile *before* critical mass — exactly the period when revenue pressure tempts founders to raise rates. Gurley's case studies (Booking, oDesk, Taobao vs. eBay) all show a low-rake disruptor seeding the network when it's small, locking in supplier breadth, and only then layering monetization. The MySpace-vs-Facebook contrast in Griffin's network-effects essay generalizes the same point at a different layer: monetize before the moat is structural and you forfeit the moat.

The Bezos quote "your margin is my opportunity" is the connective tissue between this article and [[competitive-moats]]: high margins are not a moat, they are an *advertisement* of where to attack. A network's moat lives in its participation, not its pricing.

For consumer-distribution platforms specifically, [[distribution-strategy]] applies the same logic to channels: high-friction distribution invites someone to reach the same customer cheaper, just as high-rake marketplaces invite someone to broker the same transaction cheaper.

## A heuristic

A condensed reading of Gurley's prescriptions:

1. **Start low to seed supply.** Whatever the industry standard rake is, ask whether half of it would dramatically expand supplier participation. If yes, that is likely the right starting rake — even at the cost of current-period revenue.
2. **Add monetization as an opt-in market, not a tax.** Move incremental revenue into mechanisms suppliers choose to participate in (placement auctions, promoted listings, premium tiers) rather than raising the base.
3. **Ask whether the rake forecloses partnerships you'd want.** If yes, the headline rate is too high regardless of what current participants will pay.
4. **Watch the effective rake, not the headline.** When the platform has multiple monetization layers (ads, placement fees, mandatory discounts), what does a typical successful supplier actually keep? That number — not the published commission — is what determines whether suppliers will stay or build alternatives.

## Temporal notes

This source is from 2013. The intervening thirteen years have largely confirmed the argument:

- **Apple's 30%** has become the central antitrust pressure point against the company. The Epic v. Apple litigation, the EU Digital Markets Act, and the resulting allowance of third-party app stores and alternative payments in the EU all stem directly from the rake Gurley flagged. Spotify, Epic, and Match have spent a decade making Gurley's argument in court. The "developer tax" critique has become mainstream.
- **Booking.com's dominance** has held; agency-model rakes won European hotel distribution definitively, with merchant-model challengers either converting or ceding share.
- **Taobao vs. eBay**, which Gurley appended after publication, became the canonical cross-border example. Alibaba's IPO ($25B in 2014, then the largest in history) cemented this as one of the largest pricing-strategy victories ever recorded.
- **The auction-on-top model** spread far beyond Booking and Google. Amazon Sponsored Products, the Uber/Lyft surge mechanism, App Store Search Ads, and effectively every modern marketplace now layers an opt-in placement auction on top of a base commission.
- **30% has cracked at the edges.** Apple cut its small-developer rate to 15% (under 1M revenue) in 2020; the EU now mandates lower rates and alternative billing. Epic Games Store entered with a 12% rake explicitly arguing that 30% was uncompetitive. The headline number has lost its inevitability.
- **Counterexample:** OnlyFans built a billion-dollar business at a 20% rake — high by Gurley's standards but defensible because it pairs with payment-rails, anti-piracy, and discovery work that platform participants visibly can't replicate. The rake debate has matured into a more nuanced question of *what services the platform actually performs* in exchange for its take.
- **Web3** built much of its rhetoric around "removing the platform tax," with mixed real-world results. The argument that lower rakes win in the long run is still operative; whether decentralized rails can deliver them economically is unsettled.

## Sources

- Gurley, Bill (2013). "A Rake Too Far: Optimal Platform Pricing Strategy." *Above the Crowd*. <https://abovethecrowd.com/2013/04/18/a-rake-too-far-optimal-platformpricing-strategy/> — [[2013-04-18-rake-too-far-platform-pricing|local copy]]
