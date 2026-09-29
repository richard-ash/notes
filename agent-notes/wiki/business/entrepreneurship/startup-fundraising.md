---
source: agent
compiled_from:
  - agent-notes/raw/business/entrepreneurship/2026-09-23-how-venture-rounds-happen.md
  - agent-notes/raw/business/entrepreneurship/2026-09-28-only-reason-to-raise-venture-capital.md
compiled_at: 2026-09-29
model: claude-fable-5-1
confidence: medium
---

# Startup Fundraising

Whether to raise venture capital, and how rounds actually get closed, as distinct from how they are announced. The anchor source is a serialized guide, *How to Raise Venture Capital*, posted on X by Harris (@harris) in September 2026. Chapter 2 ("How Rounds Happen") is taxonomy: it sorts every closed round into one of three paths and argues that the one founders should aim for, the pre-empt, is manufactured rather than spontaneous. Chapter 3 ("The Only Reason to Raise Venture Capital") is the gate in front of all of that: a single test for whether to raise at all, and a catalogue of the reasons that fail it. Later chapters of the guide (navigating hyperbolic-growth rounds, and the take-it-or-run-a-process decision once a term sheet lands) are referenced but not yet published; they should integrate into this article as they appear.

## Whether to raise: the one good reason

Harris opens Chapter 3 with the cost side, which founders tend to skip. A raise consumes a large amount of founder time and, if it works, dilutes equity and control. Something has to pay for that.

His diagnosis of why founders raise anyway is cultural. The press covers big rounds, announcements collect likes, and a round is the only thing the industry gets to celebrate between founding and exit, so it gets celebrated loudly and treated as a trophy. Harris argues a round is a tool, not a trophy, and that confusing the two produces a specific and fatal skill. Founders who treat raising as the scoreboard get very good at it, and so become "the best in the world at incinerating money": burn is how you earn the next round, and the next round is how you score. The only number that should matter, he says, is terminal value, meaning what the company is worth at the end.

Against that he sets one test. **Raise when capital is the fundamental limit on your growth.** The specifics vary; the shape does not. There is growth on the other side of the money, and money is what unlocks it. His examples are hires you can't yet afford, salaries high enough to stop a frontier lab poaching your best engineers, GPUs, inventory, robots, and Meta ads.

### The reasons that fail the test

| Stated reason | Harris's verdict |
|---|---|
| "It looks fun." | It isn't. Seed and A may have been easy, but eventually a raise "will punch you in the face." |
| "We don't know what else to do." | Raising as a rallying milestone after growth stalls doesn't fix the business, adds distraction, and adds investors to the list of people watching it stall. Investors will probably balk anyway. |
| "Our competitor raised." | Customers buy the best product, not the funding announcement. The exception: enterprise deals lost because buyers doubt you'll outlast a better-funded rival. That one counts *because* it collapses back into the one good reason. |
| "Our investors think we should." | Insiders may want a markup or a follow-on alongside a fancy firm; new investors always want a piece. Fine if it happens to coincide with a real capital constraint; otherwise stay the course. |
| "The market is hot and we can." | The 2021 cohort that raised huge rounds because it could is now full of zombies: big piles of slowly burning cash, valuations they'll never justify, executives who can't walk away from the promises they made, and investors with no incentive to admit defeat. Harris calls this much worse than raising less at a sensible price. |
| "Hedge against a downturn." | Requires timing macro cycles, which nobody can do. "If you could, you should run a hedge fund." |

Inside the competitor entry sits a sharper corollary. Some founders try to raise from every "good" investor to starve rivals of capital. Harris says it backfires. There is always more capital for good founders, and a huge round makes the category look hot, so every investor left out goes hunting for your competitor. "Congrats, you have personally catalyzed your rival's fundraise."

### Reading the test

The bad reasons have something in common. Each is driven by a party or pressure outside the company's growth function: the press (the trophy), boredom or a stall, a competitor's signal, investors' marks, the market's mood, fear of the macro cycle. The good reason is the only one that lives inside the business, since it requires naming a specific input that converts capital into growth. A practical version of the test is whether the founder can finish the sentence "this money buys ___, which produces ___ growth that we can't get otherwise." If they can't, the round is serving someone else's scoreboard.

Treating the round as a scoreboard is a textbook case of Goodhart's law. Capital raised and valuation are proxies for terminal value, and making them the target cuts the link. The "incinerating money" line is what that decoupling looks like in the operating plan.

The starve-the-competitor corollary is the mirror image of a mechanism in Chapter 2. There, investors pricing off each other rather than off fundamentals is what lets a founder turn one written offer into momentum ([[cumulative-advantage|rich-get-richer]]). The same herding means a vacuum round works as a public comparable for the whole category, and the capital it was meant to deny flows to whoever is next in line.

The zombie entry is the concrete form of the "indigestion, not starvation" argument in [[capital-discipline]] and of Gurley's unicorn-era critique quoted there. It also fits Damodaran's point in [[scaling-vs-profitability]] that VCs price rather than value: a 2021 price set by market appetite eventually has to be cleared by a valuation, and when it can't be, the price becomes a liability rather than a reward. (Harris doesn't spell out the mechanics. Down-round dynamics and the preference stack a large round leaves behind are the usual reasons the executives "can't walk away.") The obvious rebuttal is that many 2021 over-raisers survived the 2022–23 downturn *because* of those cash piles, which is exactly the hedge argument. Harris's zombie paragraph is his implicit answer: surviving without a path to justify the price isn't a win, and it may be worse than a clean failure or a smaller company at a sensible valuation.

Harris's examples of legitimate constraints are distinctly 2026: compute, and talent competition with frontier labs. One implication, not stated in the source, is that AI companies pass the test more often than classic SaaS did. GPUs are a real variable input that scales with usage, and lab salaries set a floor on the cost of engineering talent, so money turns into capacity more directly than it did when the marginal cost of software was near zero.

## Two mechanisms, three paths

Harris starts from a reduction: money reaches a startup in only two ways. Either the founder asks and gets it, or an investor offers and the founder accepts. In practice those two mechanisms resolve into three paths to a closed round.

**1. Externally obvious hyperbolic growth.** Growth so fast that outsiders can see it, so investors compete to fund it without being asked. Harris cites the OpenAI and Anthropic growth rounds, where investors "pummeled them with cash at increasingly astronomical valuations." The diagnostic is precise: multiple investors chasing you with *term sheets*, unprompted, without concern for valuation. Vanishingly few companies are here, and Harris notes that even Anthropic was rejected by dozens of top firms across multiple early rounds. Being in this category does not make the round safe; there are, he says, many ways to ruin a good thing.

**2. Process-driven fundraising.** The overwhelming majority of rounds. The ideal outcome is what funding announcements call a "pre-empt": an investor who already has a relationship with the company offers terms before the founder formally "starts" the process. Investors do this to win by being first, and usually believe it was their idea. Harris's central claim is that in the best fundraises he has seen, the founder orchestrated the offer.

**3. Cold-start pitching.** Beginning a pitch process with no prior groundwork or relationships. Harris calls it the hardest and "honestly worst" way to raise. Founders end up here when runway or another existential threat forces the timing. In the AI era especially, he says, it tends to produce poor terms or none.

## The pre-empt, demystified

The chapter's most useful content is its deflation of the pre-empt mythology.

- **It is recent.** Pre-emptive behavior was rare before 2020 and has become common across many round sizes for attractive AI and deeptech companies.
- **It has a hard definition.** "A real pre-emptive offer is a written term sheet. Full stop." Anything short of that, however enthusiastic, is an expression of interest. Harris warns that verbal pre-empts bedazzle founders while functioning as an attempt to open a one-on-one process on the investor's timeline instead of the founder's.
- **It is engineered.** Pre-empts look magical from outside but are almost always the product of groundwork: cultivating investor relationships and strategically managing what information investors receive, well before capital is needed. Most pre-emption is therefore still a process, just a warm one rather than a cold one.
- **It compounds.** A founder who triggers an offer before pitching broadly gains optionality (a floor under the round) and momentum that carries through the rest of the raise, the same [[cumulative-advantage|rich-get-richer]] dynamic that makes investors price off each other rather than off fundamentals. Harris frames nearly everything else in the guide as instrumentation for reaching this point.

## Reading the taxonomy: who controls the clock

The three paths look like a ranking by company quality, but read more cleanly as a ranking by *who controls timing*. In path 1, growth sets the clock and investors race it. In path 3, the runway sets the clock and the founder races it. Only in path 2 does the founder set the clock, and the entire guide is an argument for engineering your way into that path regardless of how strong the underlying business is.

That reading explains why the term-sheet test matters so much. A verbal pre-empt is an offer to move the founder from path 2 to a private version of path 3: one counterparty, their timeline, and the founder's parallel process quietly suspended. Parallelism is the founder's only structural leverage in a negotiation where the other side does this for a living, and a written term sheet is the only artifact that both preserves that leverage and creates the social proof that pulls other investors in. This is [[cialdini-influence|scarcity and social proof]] working for the founder rather than against them; a verbal offer delivers neither.

Two of Harris's asides connect to existing articles here:

- **Anthropic being rejected early and chased later** is the same company moving between paths as its growth became legible. That fits the argument in [[founder-evaluation]] that VC consensus at seed is close to noise: the category a company lands in is a function of stage and the visibility of its metrics, not of its eventual quality. It also fits Damodaran's point in [[scaling-vs-profitability]] that VCs price rather than value. Path 1 is what comparable-driven pricing looks like once the comparable metric is visible to everyone.
- **"Strategically manage information"** is doing quiet work in the pre-empt recipe. The material a founder drips to warm investors is the growth-accounting and retention evidence described in [[startup-growth-metrics]]; the guide's later emphasis on "data-driven pitches" presupposes that the founder has instrumented the business well enough to have something worth dripping.

## Relationship to capital discipline

Chapter 2 on its own could be read as optimizing for terms and momentum, in tension with the Stitch Fix playbook in [[capital-discipline]], which argues for raising less and later. Chapter 3 removes most of that tension. Harris takes the capital-discipline side on *whether* and *how much*: raise only against a real growth constraint, never because the market will let you, and never to buy a cushion for a downturn you can't time. Chapter 2's process advice governs only the *terms* on a raise that has already passed that gate.

The two chapters meet at path 3. Running out of money is what forces a cold start, so burn discipline is what keeps path 2 open. There is one residual tension. Chapter 2 advises protecting runway so a cold start is never the only option, while Chapter 3 forbids raising extra as a hedge. The way to reconcile them is that Harris wants runway protected by spending discipline and by starting investor relationships early, not by oversizing the round. The guide does not say raise more; it says raise only for growth, and never let the calendar choose your process for you.

The guide leaves unexplained why the cold-start penalty is sharper in the AI era. A plausible reading, not in the source, is that AI investors are saturated with inbound and rely on warm referrals as a filter, so a cold pitch signals that nobody who already knew the company wanted in.

## Practical rules implied by the guide

- Before any process, name the specific input the money buys and the growth it unlocks. If you can't, don't raise.
- Size the round to the constraint, not to the market's appetite, a competitor's headline, or a downturn hedge.
- Don't try to starve competitors by locking up every good investor; the leftover investors will fund your rival.
- Weigh insider and new-investor enthusiasm for a raise against their own incentives (markups, allocation).
- Build investor relationships before capital is needed, and send them information on a cadence you control.
- Treat any offer that is not a written term sheet as interest, and say so. Ask for the paper.
- Never let one investor set the timeline. Keep the parallel process alive until a term sheet exists.
- Trigger the first offer before the broad pitch; the floor and the momentum are the point.
- Protect runway through burn discipline so that the cold-start path is never the only one open.

## Sources
- Harris (2026). "How to Raise Venture Capital Chapter 2: How Rounds Happen." <https://x.com/harris/status/2102736808983277578> — [[2026-09-23-how-venture-rounds-happen|local copy]]
- Harris (2026). "The Only Reason to Raise Venture Capital" (*How to Raise Venture Capital*, Chapter 3). <https://x.com/harris/status/2104563809977290917> — [[2026-09-28-only-reason-to-raise-venture-capital|local copy]]
