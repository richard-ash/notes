---
source: agent
compiled_from:
  - agent-notes/raw/business/entrepreneurship/2026-09-23-how-venture-rounds-happen.md
  - agent-notes/raw/business/entrepreneurship/2026-09-28-only-reason-to-raise-venture-capital.md
  - agent-notes/raw/business/entrepreneurship/2026-10-05-when-to-raise-venture-capital.md
  - agent-notes/raw/business/entrepreneurship/2026-10-20-how-to-use-metrics-in-a-fundraise.md
  - agent-notes/raw/business/entrepreneurship/2026-10-27-how-to-pitch-really-damn-well.md
compiled_at: 2026-10-27
model: claude-fable-5-1
confidence: medium
---

# Startup Fundraising

Whether to raise venture capital, when to raise it, and how rounds actually get closed, as distinct from how they are announced. The anchor source is a serialized guide, *How to Raise Venture Capital*, posted on X in September and October 2026 by Harris (@harris), a former YC partner now at Magid. Chapter 2 ("How Rounds Happen") is taxonomy: it sorts every closed round into one of three paths and argues that the one founders should aim for, the pre-empt, is manufactured rather than spontaneous. Chapter 3 ("The Only Reason to Raise Venture Capital") is the gate in front of all of that: a single test for whether to raise at all, and a catalogue of the reasons that fail it. Chapter 4 ("When to Raise") takes up timing. It rejects both standard answers, a metrics threshold and "raise when you can," and offers a framework Harris calls the Decisive Moment. A later installment, "How to Use Metrics in a Fundraise" (unnumbered in the post), supplies part of what Chapter 4 deferred. It treats metrics as the evidence that makes the narrative credible rather than as a trigger, reduces "knowing your numbers" to consistency and detail, declares benchmarks a mirage, and tells founders to lead with the metric nearest the investor's biggest blocker. It defers gathering market data from investors to "the next chapter." The pitch installment, "How to Pitch Really Damn Well" (27 October 2026, also unnumbered), is about the narrative those metrics ground: a pitch exists to argue the company becomes enormous and to make dismissing it feel unsafe, built on three or four load-bearing claims tested in casual investor meetings before the raise and framed as a contrarian bet with a path to consensus. It is not the market-data chapter. That chapter, the chapters on navigating hyperbolic-growth rounds, and the one on the take-it-or-run-a-process decision once a term sheet lands are still unpublished; all of these should integrate into this article as they appear.

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

- **It is not yet operational.** "Ready just after the money hits" and three elements "in balance" can't be checked in advance. Harris concedes this and defers measurement to a later chapter. The metrics installment below supplies part of it, namely what evidence to have ready and what disqualifies a founder regardless of timing. The market-reading half is deferred again.
- **Survivorship.** Scale is the right call in hindsight, and the promise-end Series As that failed don't appear. Harris's own example cuts the other way too: the prepared-mind method got Sequoia interested in a market he now says wasn't worth it. The method works on investors whether or not the thesis is true, which is why it belongs behind Chapter 3's gate and can't replace it.
- **Regime dependence.** The slide toward promise is described as a product of the AI boom. The chapter doesn't say whether it survives a contraction, and in 2022–23 efficiency metrics came back as gates quickly. The chapter also opens the question of "how much" and leaves it. Its description of fewer, larger rounds is the market's behavior, while Chapter 3's advice is still to size the round to the constraint, so a founder who times the moment well should expect to be offered more than the constraint needs.

## Metrics in a raise: signal, not gate

The metrics installment (posted 20 October 2026) opens by restating Chapter 4's conclusion and then taking the other half of it seriously. No metric produces a round. Rounds close when investors believe the company is on the path to something massive, and Harris says that belief is "primarily emotional." But metrics are what ground the narrative and make it credible, and not knowing them is disqualifying "in a way few other mistakes are," because it tells the investor the founder can't judge whether the business has product-market fit.

### Knowing your numbers

Harris reduces "knowing your metrics" to two properties.

**Consistency** is what lets an investor read a pattern as a trend. Six months at 40% monthly growth is a trend, if an early one. Months that alternate between shrinking and growing are hard to read even when they average to the same figure. If the numbers are inconsistent, his advice is to volunteer a genuine structural explanation rather than wait to be asked.

**Detail** is what lets an investor trust that the numbers mean what the founder says they mean:

- Honest representation. Concealed or massaged numbers "will get discovered," and the discovery destroys trust. His three classic offenders are cumulative charts that only go up, gross merchandise value reported as revenue, and margin figures that quietly leave out compute.
- Absolutes and growth rates across monthly, quarterly, and annual windows.
- For every number, how it is calculated, what data supports it, and what assumptions are baked in, ideally with the sensitivity. If a user is someone who logs in monthly, know the number under a daily definition.
- Most of it by heart. For the rest, "I'm not sure about that one, I'll get back to you today" builds credibility. A made-up answer, discovered later, "ends processes."

### What good looks like now

Harris wrote YC's Series A guide, and says that at the time he and colleagues built a benchmark table from data on successful raises: ranges for revenue, growth, and retention, correlated with round sizes. He calls that exercise quixotic then and useless now. "Benchmarks are a mirage." Ask any VC for the revenue and growth rates of their firm's last five deals and the result is a near-random scatter plot. Investors nonetheless know good when they see it, and he offers three properties of what they see.

| | Harris's claim | Consequence |
|---|---|---|
| **Good is explosive** | Investors pattern-match on explosive trajectories. The old "triple-triple-double" cadence isn't enough, and neither is a large revenue figure with middling growth. AI companies have reset what fast looks like, so investors care more about growth narratives than levels. | The slope matters more than the intercept. |
| **Good is relative to the queue** | Numbers are judged against the other companies in that investor's pipeline right now. | Timing is partly about who else is pitching that month. Learn what each investor passed on, what they missed, and how you compare. The real benchmark source is investors themselves, gathered in casual meetings, not a Carta blog post. |
| **Good is consistent with your story** | There is no magic threshold for CAC, LTV, AUM, or DAU. The number that matters most is the one that proves *your* specific story is coming true. | Pick the metric that bears on the thesis, not the one a stage template asks for. |

### Why trends beat snapshots

Harris's model of what metrics do is that they are inputs into the investor's mental picture of whether the business becomes gigantic. At the earliest stage there are few data points, so the decision runs on promise and vision. Later there is deep data to anchor on. Wherever a round sits, it is priced on how convincingly the data the founder has now validates the vision already sold. Three failure cases follow:

- **Insufficient data.** A product launched two months ago with great early numbers supports a promise-based raise (a seed, a bridge, or support for a later round), but two months is not a trend and won't be priced as one. The exception is growth so explosive it has captured all the attention in the world. His example is Instinct, which the post doesn't elaborate on.
- **Inconsistent data.** High average growth over months that alternate negative, flat, and positive reads as a founder who doesn't understand the levers of the business well enough to pull them predictably.
- **Too much unflattering history.** Years of flat growth, or a lot of capital raised, before a recent take-off. Founders underestimate how hard it is to get investors to trust the last four months over the previous four years, and claiming a pivot doesn't erase the history. "The burden of proof rises with every month of history."

### Investor psychology: the blocker metric

Harris's preferred way to choose metrics is to look at the business through the eyes of a great investor. He characterizes the best as optimists who have learned skepticism. Pessimists wash out because they never find a future worth betting on. Such an investor first builds a picture of the company's future state and the world it creates, since that is the only kind of company worth investing in, and then enumerates the blockers between here and there. The founder's job is to show how each blocker gets cleared, and **the first metric to focus on is the one closest to the biggest blocker.** For a deeply technical product that may be solving the problem or hiring the team, which isn't a metric at all. For a company that has never sold to enterprises and must, it is enterprise sales. The externally visible evidence has to make someone "sit back and say wow." His closing line: "Make wow. Raise money."

### Reading the chapter

The chapter is the operational half of Chapter 4's "signal, not gate." Several points connect to earlier chapters and to other articles:

- **The blocker metric is Chapter 3's test seen from the other side.** Chapter 3 asks the founder to name the input capital buys and the growth it unlocks. The blocker metric asks what the investor thinks stands between the company and its future state, and demands evidence it can be cleared. The two coincide when the biggest blocker is the capital constraint itself. When they diverge (the blocker is "can this team sell to enterprises," say), the raise has a prerequisite the money won't fix, and the founder should expect to be asked for proof before the round rather than after.
- **"Relative to the queue" is a mechanism behind Chapter 4's timing.** It makes the decisive moment partly a matter of who else is competing for attention, not only of the company and the investor. It also explains why Chapter 2's cold start is punished: a cold pitch lands in a queue the founder hasn't seen, against companies the founder knows nothing about, while the warm process lets the founder learn the queue first. The deferral of "gathering market data from investors" to the next installment suggests that is where the measurement Chapter 4 promised will land.
- **Sensitivity analysis is the credibility move.** Chen's advice in [[startup-growth-metrics]] is to decompose growth into new, reactivated, and churned before investors do it for you. Harris's "know the number under the daily definition" is the same move applied to definitions rather than components. In both cases the founder pre-empts the analyst's first question, and having done so is evidence about the founder, which is what Chapter 4 says investors are mostly buying.
- **The three offenders are each a known accounting or unit-economics trap.** GMV reported as revenue is the gross-versus-net question in [[revenue-recognition]] and the take-rate question in [[marketplace-rake]]. Compute left out of margin is the 2026 form of Gurley's gross-margin factor in [[revenue-quality]], with the cost structure described in [[token-pricing]]. Cumulative charts are the oldest trick, and the reason Chen's growth accounting exists. Harris's point is not that these are wrong to show. It is that undisclosed versions end the relationship, since every one of them is checked in diligence.
- **"I'll get back to you today"** works by the same mechanism as the discipline in [[credibility-based-selling]]. A visible admission of ignorance buys trust for everything else the founder says, while a fabricated answer puts every other number under suspicion. It is also a test the investor is partly running on purpose.
- **Optimists who learn skepticism** is Harris's sketch of investor calibration. [[probability-neglect]] describes the base-rate neglect that makes founders attempt things that look irrational. Venture requires an investor willing to share that neglect on a few bets while holding the base rate for the rest, and "pessimists wash out" is the selection effect that produces such people.

Three caveats, the last two not in the source:

- **Harris concedes the regime.** "Good is explosive" is explicitly a product of AI-era revenue curves, and the chapter doesn't say what good looks like when those curves stop. The regime dependence noted under Chapter 4 applies here too.
- **"Benchmarks are a mirage" and "good is relative to the queue" are in tension.** If the queue sets the bar, there is a benchmark. It is just local, moving, and unpublished. Harris's practical advice, to get the comparison set from investors directly, fits that reading, and it makes "no benchmarks" mean "no public benchmarks you can plan against."
- **The unflattering-history rule strengthens Chapter 3's gate.** Every round taken before a real constraint lengthens the history the next round has to explain, and a flat stretch after a raise is the worst version of that. The chapter also leaves open how a long-lived company should present itself, beyond the warning that the pivot story alone won't carry it.

## The pitch: a story that makes dismissal unsafe

The pitch installment (posted 27 October 2026, also unnumbered) is about the narrative that the metrics installment said metrics exist to ground. Harris's frame is that startups are stories and founders are storytellers, adjusting the narrative to the audience while, "and this is critical," staying honest. The chapter covers the story told to investors.

### Two jobs and one mechanism

Harris says an investor pitch has exactly two purposes: convince the investor the company will be worth billions ("trillions?"), and scare them that they are at risk of missing it. Both follow from what he says an investor is actually doing in every early meeting. The investor's binding constraint is time, not money. No firm can meet and diligence every company raising, so the job in each meeting is **elimination**: dropping companies that don't merit more time. Investors also know that a tiny number of companies generate essentially all venture returns, and their nightmare is crossing one of those off. The founder's goal in every meeting therefore reduces to one sentence: "make them feel it is unsafe to dismiss you right up until they decide that you're the big one."

The shorthand investors use for future greatness is enormous growth. If you have it, build the story around it. If you don't yet, build the pitch to demonstrate convincingly that you soon will.

### World building

The best founders, in Harris's account, are worldbuilders. They can picture a future that doesn't exist yet and transmit the excitement of it, and then convince the investor that their team, technology, and execution will close the gap between here and there. Once an investor has been taken into that world, extraordinary claims about the company become justifiable. Harris adds that investors read the ability as a **recruiting signal**, since a founder who can pull an investor into a world can do the same with the people they need to hire.

The failure mode is the opposite instinct. A founder immersed in operations will want to walk the investor through the complicated, clever things they have done "to optimize margins or something," and Harris says that will generally lose them, at least in a first pitch. The job is instead to show how the current work leads "inexorably" to altering something foundational about the world. The founder already believes this in their gut. They have about fifteen minutes, sometimes less, to get someone else to believe it in theirs.

### The vertebrae

Harris calls walking into pitches with an untested narrative dangerous, and a good way to waste the time and social capital it took to get the meeting. Before the earliest meetings, a founder should identify the three or four points that best support the argument that the company will "absolutely become enormous." These are the vertebrae, the load-bearing claims. The selection rule is specific: choose them so that **if an investor believes any one of them, they will be afraid to write you off.**

Then test them. Harris treats the investor meetings in the six to twelve months before a raise as a laboratory. Watch which points produce leaned-in questions, which the investor repeats back, which they still remember a quarter later. "What excites them is your data." Record the reactions and use them to revise the narrative, so that by the time the formal raise starts every vertebra has been load-tested against real skepticism.

### Make them contrarian, then make them right

The chapter's last layer is investor psychology. Every investor, Harris says, wants to be a contrarian. It is cool ("the equivalent of wearing a black leather jacket"), and it is what they tell themselves and their LPs makes the fund differentiated. But almost nobody wants to stay contrarian forever. The financially successful contrarian stakes a position against prevailing wisdom and then finds ways to build consensus around it. The ones who never manage the second half are "simply, curmudgeons."

A founder exploits this by making the investment feel like an arch-contrarian position. Harris calls that the easy part. The hard part is convincing the investor, and then the world, that more capital will show up once the company starts growing and "their secret starts getting out." That requires founder and investor to believe together that at each stage of the funding cycle there will be enough people inside the contrarian tent to feel they are getting a good deal, and that soon more people will see it. Thread that needle and investors "will jump at the opportunity to fund."

He closes with the regime argument that runs through the guide. Companies are founded and scaled faster than ever, investors are unsure which metrics and benchmarks to judge them by, and all of them have watched generational companies slip through their fingers. Structuring the vertebrae to present the company as a massive contrarian bet captures both the excitement and the fear of investors in the AI era.

### Reading the chapter

The chapter looks like advice on persuasion, but most of it is a model of the investor's payoff, and the advice falls out of the model.

- **The target is regret, not expected value.** Harris's elimination model has an asymmetric loss function. A false positive costs a few more hours of diligence, while a false negative on one of the handful of companies that return the fund is unrecoverable. The power law behind that is the one in [[scaling-vs-profitability]], where the top 1% of deals produce most of the returns, and it is why "scare them" is accuracy about the investor's own position rather than manipulation. The pitch does not have to raise the probability the investor assigns to success. It has to raise the cost of being wrong about it. The [[cialdini-influence|scarcity]] principle is the generic version of this lever, and Chapter 2's written term sheet is the same lever in its most concrete form.
- **Vertebrae are an OR, not an AND.** A logical argument chains claims so that the conclusion needs all of them. Harris's selection rule reverses that: each vertebra must be sufficient by itself to block elimination, so the story survives an investor rejecting any two or three of them. That is also why they are tested one at a time, and why the right test statistic is which ones get repeated back, not whether the whole deck landed.
- **A vertebra is a claim; the blocker metric is its evidence.** The metrics installment said the narrative is grounded by metrics and that the first metric to show is the one nearest the investor's biggest blocker. Each vertebra should pair with such a metric, or with the admission that the evidence is not a metric yet (the team, a solved technical problem). The two installments also mirror each other on data: the founder's metrics are evidence for the investor, and the investor's reactions are evidence for the founder.
- **The pre-raise conversations now have three jobs.** Chapter 2 used the six-to-twelve-month window for groundwork and strategically managed information, Chapter 4 for preparing investors' minds and reading the queue, and this chapter for load-testing the story. They are the same meetings, which makes the window the most overloaded part of the guide and raises a tension the source doesn't address: a vertebra that fails in a test meeting is also remembered by the investor whose mind you were preparing. The consistent reading is that testing is cheapest early and with investors lower on the list, and that revising a story told in casual settings reads as learning, whereas the metrics chapter's consistency rule applies to numbers in a pitch. Nothing was pitched, so nothing was contradicted.
- **World building is making an illegible benefit legible.** [[legibility-asymmetry]] argues that transformative innovations have legible costs and illegible benefits, because the benefits depend on practices that don't yet exist. Harris's complaint about founders walking investors through margin optimizations is that asymmetry in miniature: operations are legible, the future state is not, and the founder's job is to carry the listener into the world where the benefit is obvious. It is also what [[definite-optimism]] asks for from the other direction. Thiel's test is whether a team can state the mechanism of its advantage rather than the odds, and a built world is that mechanism told as a story. Winston's claim in [[public-speaking]] that humans are storytelling animals, and his rule to go shorter, is the delivery-side version of the fifteen-minute constraint.
- **The recruiting signal closes a loop with Chapter 4.** If founder and team are "the only fixed point" left in a promise-weighted market, then the pitch is partly an audition, and the audition is for the skill that also wins hires. Graham's "imagination" in [[founder-evaluation]] is the closest named quality. One consequence is that the chapter's advice does not vary with stage. Later rounds in the current regime are still founder-weighted, so the world still has to be built at the B.
- **Contrarian-then-right is a two-period pricing argument.** An investor's return needs a low price now and a high price later. The contrarian half supplies the first: the market has not yet priced what the investor sees. The consensus half supplies the second: a mechanism by which the market catches up, at each round, with enough new believers to re-price the company. Harris's "secret getting out" is Thiel's secret from [[business-frameworks]] run forward in time, and in Neumann's terms ([[startup-uncertainty]]) it is the uncertainty window that incumbents and consensus investors cannot act in, converted into a moat before it closes. The staircase of believers is the herding described in [[cumulative-advantage]], here designed rather than merely exploited, and Anthropic's move from rejected to chased in Chapter 2 is what the second half looks like when it works. The hard part is hard because it is the only part the business has to earn. Feeling contrarian can be manufactured. A re-pricing mechanism cannot.
- **Elimination is why cold starts are punished.** Chapter 2 said cold pitches get the worst terms, and this chapter supplies the mechanism. A cold meeting is an elimination round with no prepared mind, no tested vertebrae, and no view of the queue, so the investor's default action, dropping the company, meets no resistance.

Three caveats, the first partly conceded by the source:

- **"Scare them" and "be honest" need reconciling, and the chapter asserts both without doing it.** The consistent reading is that the fear has to come from the vertebrae being true, not from manufactured urgency. Fear built on a false claim is discovered in diligence and, per the metrics installment, ends the process. Chapter 2's rule that only a written term sheet counts polices the same thing from the investor's side.
- **The method optimizes for survival against skepticism, not for truth.** Load-tested vertebrae are claims investors failed to kill, which is correlated with being right but is not the same thing. Harris's own Chapter 4 example is the warning: the prepared-mind method got Sequoia interested in a market he now says wasn't worthwhile. The vertebrae belong behind Chapter 3's gate, like everything else in the guide.
- **Regime dependence, again.** The closing argument is that narrative weight rises because benchmarks have stopped working, which is the metrics chapter's "benchmarks are a mirage" seen from the story side. In a contraction where efficiency metrics return as gates, the vertebrae would presumably need to be metrics rather than claims, and the chapter doesn't say how the method changes.

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
- Know your absolutes and growth rates by month, quarter, and year, how each is computed, and how it moves if the definition changes. If you can't answer, say you'll get back to them that day, and do.
- Never show cumulative-only charts, GMV as revenue, or margins that exclude compute without saying so.
- Lead with the metric closest to the investor's biggest blocker, and make it one that proves your thesis rather than one from a stage template.
- Learn what is in each investor's queue, what they passed on, and what they missed. That is the only benchmark that exists.
- Keep a running read of what investors currently believe about your market, and pick the moment yourself.
- Build investor relationships before capital is needed, and send them information on a cadence you control.
- Find the likely skeptics early and argue the thesis with them in casual settings, months before any pitch.
- Build the pitch to do two things only: show the company becomes enormous, and make dismissing it feel unsafe. Cut what does neither.
- Lead with the world your work produces, not the operations that produce it. Save the clever margin work for diligence.
- Pick three or four load-bearing claims, each sufficient on its own to stop an investor writing you off, and pair each with the evidence nearest its blocker.
- Test those claims in the pre-raise meetings. Record which ones draw leaned-in questions, get repeated back, and are remembered a quarter later, and rewrite the story from that record.
- Frame the bet as contrarian now, and show the mechanism by which more investors come inside the tent at each later round.
- Treat any offer that is not a written term sheet as interest, and say so. Ask for the paper.
- Never let one investor set the timeline. Keep the parallel process alive until a term sheet exists.
- Trigger the first offer before the broad pitch; the floor and the momentum are the point.
- Protect runway through burn discipline so that the cold-start path is never the only one open.

## Sources
- Harris (2026). "How to Raise Venture Capital Chapter 2: How Rounds Happen." <https://x.com/harris/status/2102736808983277578> — [[2026-09-23-how-venture-rounds-happen|local copy]]
- Harris (2026). "The Only Reason to Raise Venture Capital" (*How to Raise Venture Capital*, Chapter 3). <https://x.com/harris/status/2104563809977290917> — [[2026-09-28-only-reason-to-raise-venture-capital|local copy]]
- Harris (2026). "How to raise venture capital, chapter 4: When to Raise." <https://x.com/harris/status/2107132880333742484> — [[2026-10-05-when-to-raise-venture-capital|local copy]]
- Harris (2026). "How to use metrics in a fundraise" (*How to Raise Venture Capital*). <https://x.com/harris/status/2112554470852964710> — [[2026-10-20-how-to-use-metrics-in-a-fundraise|local copy]]
- Harris (2026). "How to pitch really damn well" (*How to Raise Venture Capital*). <https://x.com/harris/status/2115066843614347265> — [[2026-10-27-how-to-pitch-really-damn-well|local copy]]
