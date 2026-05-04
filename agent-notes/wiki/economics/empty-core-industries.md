---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-05-04-why-airlines-are-always-going-bankrupt.md
compiled_at: 2026-05-04
model: claude-opus-4-7
confidence: high
---

# Empty-core industries

**Empty-core industries** are sectors that, in cooperative game theory terms, have *no stable competitive equilibrium*: every possible allocation of firms to demand can be profitably undercut by some coalition of producers and customers, so the market cycles endlessly between oversupply and undersupply, with the firms operating it unable to cover their cost of capital. Oks (2026) argues that the airline industry is the canonical contemporary example, and that its perpetual bankruptcy is a structural feature of its cost-and-demand geometry rather than a story about bad management or external shocks.

## The core, in cooperative game theory

[Cooperative game theory](https://en.wikipedia.org/wiki/Cooperative_game_theory) studies strategic interaction when agents *can* form binding agreements. Its central question is *which arrangements among players are stable* — meaning no subset of players could break away and do better on their own. The **core** of a game is the set of outcomes that no coalition of players can improve upon by breaking off and dealing among themselves.

- If an outcome is **in the core**, it's stable: no side deal makes any subgroup strictly better off.
- If the core is **empty**, every arrangement is vulnerable to defection by some coalition. The market has no resting point. It cycles, destabilizes, and — without outside intervention — eventually breaks down.

This is a different lens from the more familiar non-cooperative analyses (Nash equilibrium, [[entrepreneurial-profit|Schumpeterian profit decay]], the prisoner's dilemma). It's about whether *any* allocation can persist against side-deals, not just whether a given configuration is best-response stable.

## Telser's structural conditions

The economist Lester Telser worked out in the 1970s–'80s the conditions under which an industry has an empty core. Per Oks's reading, an industry suffers empty-core syndrome when *all four* of the following hold:

1. **High fixed costs, low marginal costs** — most of the production cost is incurred before any unit is sold; once capacity exists, the cost of using it is small.
2. **Sharp economies of scale** — average cost falls steeply with output up to a sizable minimum efficient scale.
3. **Lumpy supply relative to demand** — the *minimum efficient scale* of one firm is large relative to total market demand, so the market can support only a small number of efficient firms (and you can't have half a firm).
4. **Undifferentiated product + volatile demand** — buyers see firms as substitutes, so price competition is the dominant axis, and demand swings amplify the consequences of any miscount in capacity.

The first three are about the **integer problem**: if total demand divided by minimum efficient scale equals, say, 2.5, then two firms is too few (excess profit invites entry) and three firms is too many (someone bleeds money on fixed costs and must exit). Whichever side of the integer the market lands on, some coalition can profitably reorganize against the existing arrangement. The market never settles.

The fourth condition — undifferentiated product plus volatile demand — turns the cycle from a slow oscillation into a recurring crisis. An industry barely sustainable with three firms becomes catastrophically oversupplied the moment demand softens, and the inability to differentiate means firms can't escape the price competition by retreating to a defensible niche.

## Why most industries don't have this problem

In most industries, minimum efficient scale is small relative to total demand, so the rounding error from one extra firm is invisible. Soap, for example, has real economies of scale, but the market supports thousands of efficient firms and products differentiate through brand and recipe; demand is steady. The market settles into a stable, competitive, durably profitable equilibrium.

Empty-core syndrome only kicks in at the corner where **scale is sharp, scale is large relative to the market, products are undifferentiated, and demand is volatile**. Famous historical examples:

- **19th-century railroads** — vast capital expenditure on track, rolling stock, depots; near-zero marginal cost of carrying an additional ton across the line. Two competing Chicago–New York lines spent the 1870s–80s alternately forming pools and rate-fixing agreements, watching them collapse into ruinous price wars, going bankrupt, reorganizing, and repeating.
- **Ocean shipping** — same dynamic; the source-paper literature on shipping conferences and rate cartels traces the same arc.

## The airline industry as the contemporary case study

Oks works through the airline cost stack to show every Telser condition is met:

- **Fixed costs everywhere**: a widebody is in the low hundreds of millions; gate slots and landing rights are fixed; even labor is effectively fixed because the [Railway Labor Act of 1926](https://en.wikipedia.org/wiki/Railway_Labor_Act) (extended to airlines in 1936) keeps collective bargaining agreements in force until replaced. Even fuel acts fixed because spiking fuel prices are unfriendly enough that airlines hedge aggressively.
- **Lumpy supply**: a stylized SF–Tokyo route with 800 daily passengers and three airlines flying widebodies (250–300 seats) puts 750–900 seats into the market — close to demand, healthy fares. But the slack invites a fourth entrant. Now 1,000–1,200 seats chase 800 passengers; someone bleeds and exits; fares recover; another entrant sees the unmet demand and re-enters.
- **Undifferentiated product, volatile demand**: shocks (9/11, 2008, COVID, oil crises) trigger waves of bankruptcy because the variable cost of flying a half-empty plane is barely lower than a full one, so capacity persists into the demand collapse and fares cliff.

The numbers Oks cites: from deregulation in 1978 through 2025, the U.S. airline industry's *cumulative* net profit is roughly **negative $37 billion** (2026 dollars). The IATA's 2026 global outlook projects ROIC of 6.8% against WACC of 8.2% — the industry "collectively does not generate earnings that cover its cost of capital." Buffett's line: "if a farsighted capitalist had been present at Kitty Hawk, he would have done his successors a huge favor by shooting Orville down."

### Why shocks and management aren't the explanation

Oks rules out the two intuitive alternatives:

- **Shocks alone don't explain it.** Hotels are also exposed to recessions, terrorism, pandemics, with cost loaded into the property — but the hotel industry doesn't go through synchronized waves of bankruptcy. Shocks tip airlines over the edge; they don't cause the structural fragility.
- **Bad management doesn't explain it either.** The 2000s/2010s consensus — that legacy carriers were chronic money-losers and budget carriers were the future — has now collapsed. Spirit liquidated in May 2026; JetBlue and Frontier are at bankruptcy risk; even Southwest hasn't been profitable since the pandemic and is fending off Elliott Management. No airline has found a replicable formula for profitability under genuine competition.

And — telling — none of the *adjacent* aviation businesses have this problem. Engine and avionics manufacturers, MRO suppliers, gate and ground service vendors all generate normal returns on capital. The empty-core pathology is specific to running passenger seats.

## Chapter 11 as the relief valve, not the cure

In the U.S., bankruptcy protection is "practically the only mechanism by which an airline can renegotiate its rigid cost structure" — aircraft leases, pension obligations, collective bargaining agreements. Airlines rarely liquidate; they emerge from Chapter 11 with a *lower* cost basis and immediately undercut competitors, dragging the industry's competitive floor down rather than restoring an equilibrium that covers cost of capital. United's 2002 bankruptcy alone offloaded ~$6.6B in pension liabilities onto the federal Pension Benefit Guaranty Corporation. Bankruptcy doesn't cure the empty core; it just resets the floor for the next round of ruinous competition.

## The escape routes: become uncompetitive, or stop being an airline

If competition can't be profitable, the only stable equilibria are uncompetitive ones. Oks identifies three escape strategies airlines actually use, all of which amount to suppressing competition in different forms:

### 1. Statutory cartelization (the U.S. up to 1978)

The Civil Aeronautics Board (1938–1978) was effectively a government-approved cartel: it told airlines which routes to fly, when, at what fares, set to allow reasonable returns. Not a single trunk-line carrier was admitted between 1938 and 1978. The airline industry under the CAB was profitable, comfortable, and slightly boring — competing on cabin glamour rather than price. The 1978 Airline Deregulation Act dismantled this and immediately produced the bankruptcy waves of the 1980s, 2000s, and 2020s.

### 2. Private cartelization

When statutory cartels are taken away, the firms reach for private substitutes:

- **International alliances** — Star, SkyTeam, Oneworld, with codesharing and antitrust-immunized joint ventures, allow nominal competitors to coordinate scheduling, share revenues, and refrain from undercutting on high-value trans-oceanic routes.
- **Hub-and-spoke / fortress hubs** — by concentrating operations at a few major airports, airlines turn those airports into local monopolies. American carries ~90% of Charlotte and 82% of DFW; United dominates SFO; Delta carries everything at Atlanta. The map of U.S. domestic aviation is "a feudal map of fortress hubs," with each major carrier earning monopoly margins in its strongholds that subsidize the unprofitable competitive routes elsewhere.

### 3. Stop being an airline (the Delta strategy)

The most interesting response is to treat the planes as a loss-leading distribution channel for a more profitable adjacent business. Frequent flyer programs, invented post-deregulation as loyalty tools, have become free-floating financial businesses where mile values bear no relationship to seat costs.

Delta's American Express partnership exemplifies this. Delta-branded Amex cards see annual spending equal to ~1% of U.S. GDP. In 2025, the partnership produced ~$8B in revenue for Delta — *more than its entire profit*, meaning the airline business itself runs at a loss and the credit-card partnership is the actual product. Delta is profitable to the extent that it has stopped being an airline.

Ryanair plays a mixed strategy: it has the lowest fixed costs of any major carrier (achieved by patronizing low-volume regional airports — Stansted, Charleroi — which give discounts on gate slots and landing rights), it monopolizes hundreds of intra-European routes through those secondary airports, it extracts subsidies from regional governments, and it earns a large share of profit from ancillary fees rather than the seat itself. Oks's verdict: "Ryanair is profitable *roughly to the degree that it chooses not to compete*."

### 4. (Looming) State ownership

The Trump administration's 2025 offer of a 90% federal stake in Spirit — the first time the U.S. government would have owned a passenger airline outright — represents the third strategy: when private cartelization can't quite reach profitability, the empty-core question becomes "who holds the bag," and the answer drifts toward the public balance sheet. The Spirit talks collapsed and the airline shut down in May 2026, but the proposal itself is the tell.

## Implications

A few things follow from taking the empty-core analysis seriously:

- **Antitrust is harder than it looks.** "Restraints of trade" in empty-core industries are doing real economic work: they're choosing, even if arbitrarily, among allocations that would otherwise be inherently unstable and frequently unprofitable. Breaking them up doesn't restore competitive equilibrium because *there is no competitive equilibrium to restore*. This connects to [[competitive-moats]]: in empty-core industries, the only durable moat is *not competing*, and the firms that survive are the ones that build hub monopolies, alliance treaties, or adjacent-business loss-leader structures.
- **Consumer surplus and producer loss can coexist for decades.** Real U.S. airfares have fallen by roughly half since deregulation; air travel has become mass transit. The brunt of empty-core unprofitability falls on equity holders (wiped out repeatedly) and on workers (contracts rewritten in bankruptcy). Whether deregulation was net-good depends on how you weight those distributions; Oks tentatively concludes it was, given the alternative of stagnant cartel pricing.
- **Some businesses shouldn't exist as standalone profitable concerns.** "We need aviation to exist as an industry, but we're unable to have it survive as a profitable concern." The natural endpoints are anticompetitive consolidation, the loss-leader-for-something-else model, or direct state ownership.
- **The empty-core lens generalizes.** Wherever you find sharp scale + lumpy supply + undifferentiated product + volatile demand — historically railroads and ocean shipping, currently airlines — expect chronic instability and the same parade of cartels, mergers, bankruptcies, and adjacent-revenue strategies. Cloud-infrastructure and frontier-model AI economics arguably exhibit some of these features (extreme fixed costs, low marginal cost, scale advantages, weak product differentiation between hyperscalers), making the empty-core frame potentially relevant to [[ai-platform-moats]].

## Sources

- Oks, David (2026). "Why airlines are always going bankrupt." <https://davidoks.blog/p/why-airlines-are-always-going-bankrupt> — [[2026-05-04-why-airlines-are-always-going-bankrupt|local copy]]
