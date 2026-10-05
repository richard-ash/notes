---
source: agent
compiled_from:
  - agent-notes/raw/business/entrepreneurship/2026-09-23-how-venture-rounds-happen.md
  - agent-notes/raw/business/entrepreneurship/2026-09-28-only-reason-to-raise-venture-capital.md
  - agent-notes/raw/business/entrepreneurship/2026-10-05-when-to-raise-venture-capital.md
compiled_at: 2026-10-05
model: claude-fable-5-1
confidence: medium
---

# Startup Fundraising

Whether to raise venture capital, when to raise it, and how rounds actually get closed, as distinct from how they are announced. The anchor source is a serialized guide, *How to Raise Venture Capital*, posted on X in September and October 2026 by Harris (@harris), a former YC partner now at Magid. Chapter 2 ("How Rounds Happen") is taxonomy: it sorts every closed round into one of three paths and argues that the one founders should aim for, the pre-empt, is manufactured rather than spontaneous. Chapter 3 ("The Only Reason to Raise Venture Capital") is the gate in front of all of that: a single test for whether to raise at all, and a catalogue of the reasons that fail it. Chapter 4 ("When to Raise") takes up timing. It rejects both standard answers, a metrics threshold and "raise when you can," and offers a framework Harris calls the Decisive Moment. Chapter 4 defers how to measure and act on that framework to a later installment. The chapters on navigating hyperbolic-growth rounds and on the take-it-or-run-a-process decision once a term sheet lands are also still unpublished; all of these should integrate into this article as they appear.

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

## When to raise: the decisive moment

Harris calls timing the hardest question in the guide and the one founders ask him most. He says both standard answers are wrong in ways that cost founders money.

**The metrics table.** "Get to $1 million in ARR, grow 20% month over month, and the round takes care of itself." Harris calls this "pure fiction." His check is to ask any investor what numbers they tell founders to hit, then ask what their own portfolio companies had actually hit when they were funded. The lists won't match, because no particular number causes a round to close. He has seen rounds of several hundred million dollars come together at $200k of revenue, and companies fail to raise at more than $10 million of ARR. Investors are paid to find outliers, and an outlier is a company that doesn't fit the table.

**"Raise when you can."** Accurate and useless. The only way to learn that you can raise is to raise, so the rule gives no help on the day of the decision. It is also the hot-market reasoning Chapter 3 already rejected.

His own first answer is deliberately unhelpful: "you're ready to raise just after the money hits your bank account." Readiness can only be observed afterwards. The example is Scale AI's Series A, which Accel's Dan Levine led weeks after Alexandr Wang and Lucy Guo founded the company. Scale was still in YC, had just pivoted, and had a few early contracts. No metrics table would have called it ready. Harris says Levine acted on belief in the market and the founders, a view of the future, and gut, and had to ignore a number of logical objections to do it.

### Why the old timeline broke

The older model placed each round on an axis from Promise to Metrics. A company starts as a team and a story. Over time it produces data, and eventually a trend an investor can underwrite. Seeds sat at the promise end and Series Bs at the metrics end. Where a given round landed depended on the company's age, how much it had raised, and how well the founder told the story. Harris says the whole distribution has slid toward promise in the last few years, while rounds have become less frequent and much larger. He gives two causes.

- **AI broke the yardstick.** Revenue went from zero to $10 million in 18 months, then zero to $100 million, then zero to $1 billion in under two years. One such company can be explained away. After several, investors can no longer tell normal from exceptional, and a wrong call is now both more expensive and more public.
- **Technology stopped being a durable differentiator.** Harris claims nearly every revolutionary piece of software shipped in the past year was copied within months, that open-source Chinese models trail OpenAI and Anthropic by months, and that even capital-intensive fields crowd quickly (he points at the number of small modular reactor companies).

With metrics and technology both unreliable, the founder and team are "the only fixed point" left. Backing exceptional founders always drove seed rounds. Harris says it now drives nearly every round, sometimes through the C or D. Metrics survive as a *signal*: evidence that the founder is who investors hope and that the future the founder describes is starting to arrive. They no longer work as a *gate*, or as a proxy for enterprise value.

### The three elements

The framework borrows from the photographer Henri Cartier-Bresson. A great street photograph looks like luck to someone who doesn't shoot. Harris says it comes from planning, positioning, and action: the photographer picked the camera and film that morning, found a spot where something might happen, waited, and released the shutter as the cyclist crossed the frame. He means the comparison literally. There is "no critical path to a round," and no sequence of numbers or flattering investor emails triggers a term sheet. The best founders track the market continuously, keep updating their model of where they sit in it and what investors currently think, notice when the odds have moved in their favor, and then choose the moment. "The round is not something you wait for. It's a shot you take."

| Element | Founder's control | What it is |
|---|---|---|
| The right business | Largely yours | A story that validates your view of how the world is changing, as opposed to an income statement or a corporate charter. Venture capital only fits companies that must scale far ahead of what cash flow can fund *and* have a shot at becoming "almost inconceivably large." Harris calls this the camera in your hand. |
| The right reason to raise | Partly yours, partly the market's | "The narrative core of the raise": the interface between what you are building and what the market wants to see. It shifts as both change. |
| An investor with a prepared mind | Almost none | You can't create one or force belief. You can find likely investors early and shape their thinking through conversation in low-pressure settings, months before any pitch. |

Harris's evidence for the third element is his own seed round. Greg McAdoo, his first gatekeeper at Sequoia, told him flatly that tutoring was too small a market. They weren't in a pitch. They were standing in a circle of people at YC one evening, in what Harris calls a silly side conversation, and he replied that it was a $6 billion market at minimum. McAdoo's "wait, what?" opened a series of conversations with him and his partners. Harris argues that a formal pitch on the size of the tutoring market would never have got the meeting, and that if it had, the listener's skeptical half would have been running throughout. "Prepared minds are built in casual conversations." He adds that the market "kinda wasn't" worthwhile and that his company didn't win it. (The chapter doesn't name the company. It is presumably Tutorspree, the tutoring marketplace Aaron Harris co-founded before joining YC.)

### Reading the framework

Each element restates something from an earlier chapter. The first is the condition for venture capital fitting the company at all. The second is Chapter 3's test seen from the market's side. The third is the groundwork behind Chapter 2's engineered pre-empt. What Chapter 4 adds is that the three have to coincide, and that noticing when they do is the founder's job. In the terms used below, the decisive moment is the founder controlling the clock.

The second element sits uneasily with Chapter 3. There the good reason was defined from inside the business: capital is the binding constraint on growth. Here the reason is a narrative tied to "what the market wants to see," which read alone drifts back toward the scoreboard Chapter 3 warned against. The consistent reading is two filters in sequence. The reason must first be true of the business, and then be expressible in terms the market currently cares about. A real constraint the market can't yet read is a cue to wait or to do more preparing. A legible story with no constraint behind it is the trophy round.

Several points connect to existing articles:

- **Path 1 broke the yardstick for path 2.** Chapter 2's hyperbolic-growth companies are few, but they are the ones whose numbers destroyed the calibration for everyone else. A company at $2 million of ARR is no longer measured against a table. It is measured against the memory of zero-to-$100-million.
- **Signal, not gate.** The growth accounting and cohort retention in [[startup-growth-metrics]] are still what a founder shows, and still the "strategically managed information" of Chapter 2. The question the evidence answers has changed, from "has this company cleared the bar for a Series A" to "is this founder's account of the future coming true." The practical consequence is to choose the metrics that bear on the thesis, not the ones that match a stage template.
- **Founder judgment moves up the stack.** If Harris is right, the frameworks in [[founder-evaluation]], written for first institutional capital, now apply to B and C rounds. That article also records Rabois and Khosla's view that seed consensus is close to noise and forms around known people ("two people leaving Cursor"). An inference Harris doesn't draw is that the least reliable judgment in venture now governs the largest cheques, and that a founder-weighted market favors founders investors already know. For everyone else the third element carries the weight, since the only way to be judged as a person is to be known before the pitch.
- **The metrics table is a justification regime.** [[startup-uncertainty]] argues that a plan fully defensible on known market size and unit economics is, by construction, a plan with no moat, and [[competitive-moats]] that no structural moat is reliably available to a startup at day one. Harris reaches the same place from the investor's chair: technology doesn't hold (compare [[pacing-the-frontier]] on capability no longer translating into a moat), and the Scale round he admires was made by setting the defensible analysis aside.
- **The prepared mind changes owner.** Pasteur's "chance favors the prepared mind" is Chance III in [[four-kinds-of-luck]], where the prepared mind belongs to the person who gets lucky. Harris gives it to the counterparty: the founder's work is to prepare someone else's mind, so that the eventual pitch lands as recognition. The McAdoo story has the same structure as the claim in [[networking-as-relationship-building]] that the channel has to exist before the ask, and as pre-syndication in [[multi-stakeholder-selling]]. A venture partnership is a multi-stakeholder buyer, and McAdoo first, then his partners, is a skeptic converted one-on-one who then carries the case inside.
- **Naval's threshold.** In [[credibility-based-selling]] Naval raises when his own excitement about the fundamentals crosses a threshold. Both he and Harris reject the calendar and the metrics table, and both make the founder the one who chooses. They differ on the instrument. Naval reads himself; Harris reads the market and the investors. Naval's threshold covers roughly the first two elements, and Harris's addition is that conviction with no prepared investor on the other side is still a cold start.

Three caveats, none of them raised in the source except the first:

- **It is not yet operational.** "Ready just after the money hits" and three elements "in balance" can't be checked in advance. Harris concedes this and defers measurement to a later chapter.
- **Survivorship.** Scale is the right call in hindsight, and the promise-end Series As that failed don't appear. Harris's own example cuts the other way too: the prepared-mind method got Sequoia interested in a market he now says wasn't worth it. The method works on investors whether or not the thesis is true, which is why it belongs behind Chapter 3's gate and can't replace it.
- **Regime dependence.** The slide toward promise is described as a product of the AI boom. The chapter doesn't say whether it survives a contraction, and in 2022–23 efficiency metrics came back as gates quickly. The chapter also opens the question of "how much" and leaves it. Its description of fewer, larger rounds is the market's behavior, while Chapter 3's advice is still to size the round to the constraint, so a founder who times the moment well should expect to be offered more than the constraint needs.

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
- Don't wait on a metrics threshold. No number triggers a round; show the metrics that support the thesis, as evidence for it.
- Keep a running read of what investors currently believe about your market, and pick the moment yourself.
- Build investor relationships before capital is needed, and send them information on a cadence you control.
- Find the likely skeptics early and argue the thesis with them in casual settings, months before any pitch.
- Treat any offer that is not a written term sheet as interest, and say so. Ask for the paper.
- Never let one investor set the timeline. Keep the parallel process alive until a term sheet exists.
- Trigger the first offer before the broad pitch; the floor and the momentum are the point.
- Protect runway through burn discipline so that the cold-start path is never the only one open.

## Sources
- Harris (2026). "How to Raise Venture Capital Chapter 2: How Rounds Happen." <https://x.com/harris/status/2102736808983277578> — [[2026-09-23-how-venture-rounds-happen|local copy]]
- Harris (2026). "The Only Reason to Raise Venture Capital" (*How to Raise Venture Capital*, Chapter 3). <https://x.com/harris/status/2104563809977290917> — [[2026-09-28-only-reason-to-raise-venture-capital|local copy]]
- Harris (2026). "How to raise venture capital, chapter 4: When to Raise." <https://x.com/harris/status/2107132880333742484> — [[2026-10-05-when-to-raise-venture-capital|local copy]]
