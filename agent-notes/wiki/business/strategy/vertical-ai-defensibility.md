---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-10-28-rabois-vertical-ai-survival.md
compiled_at: 2026-10-31
model: claude-fable-5-1
confidence: medium
---

# Vertical AI Defensibility

How a vertical AI application survives the frontier labs. The anchor source is Keith Rabois (managing director, Khosla Ventures) on the *Verticals* podcast with Luke Sophinos and Nic Poulos, October 2026. Rabois's test is not growth but **durability**: "what could this be in 2030, and work backwards. Is this going to be a sustainable, independent, successful company in 2030?" He argues that many of the fastest-growing vertical AI companies would not pass, and lays out the properties that let one pass.

Rabois is an investor in most of the companies he cites (Spellbook, Rogo, Basis, State Affairs, Ramp, Profound, and the HR company transcribed as "Comp"), so the specific performance claims below are a portfolio insider's and should be read as one weighted input. The frameworks are the durable part. Several company names are garbled in the auto-transcript (Rego/Rogu/Rogue Wave for Rogo, Rubicon probably also Rogo); this article normalizes them.

## Two screens

Rabois opens with two filters that Khosla applies before investing in a vertical AI company.

**Autopilot over copilot.** Products that move toward doing the work ("autopilot") are "probably more defensible and more durable long-term" than products that assist a human doing it ("copilot"). The implied mechanism is that a copilot's value scales with the underlying model, which the lab controls, while an autopilot owns the outcome and the workflow around it. Compare [[agents-as-aggregators]], where Thompson reads Microsoft's Copilot-to-Autopilot shift as a bid to be the aggregator, and [[outcome-based-pricing]], which is what an autopilot can charge for and a copilot cannot.

**Bet on models improving, not flatlining.** Channelling Sam Altman: a vertical AI company whose value grows as frontier models improve may be a good investment; one that implicitly assumes models stop improving so it can "build on top" is not. This is the same test Graham poses in [[startup-power]]: model companies become your component suppliers "if they don't engulf you."

Rabois's own examples strain the first screen. He describes Rogo, used (he says) by 29 of the top 30 investment banks, as giving junior analysts "superpowers" and turning "an average analyst into a super analyst," which is a copilot. He resolves this by calling Rogo a *Zero to One* special case: a very defined market, dominated, rather than a growth story like Harvey or Legora. The honest reading is that market definition and dominance can substitute for autopilot, at least for a while.

## The middle of the distribution

Rabois's model of where AI wins is a distribution curve: "AI is excellent in the middle of all curve distributions." Novel situations (a road never driven, a contract never seen) still favor humans; the bulk does not. Waymo is "probably 5 to 10x safer" than humans on most roads, and "automatic AI is going to make less mistakes than the average American lawyer." Customers should pay for unique judgment at the tails and not for the middle.

His contracts case: "there's no reason 90-some-odd percent of contracts in the United States require a human lawyer." The SAFE note is the precedent. It takes three minutes to understand and thirty to master, and it replaced $20,000 financings for $500,000 seed rounds with a few bullet points; Rabois thinks most contracts should become SAFE-shaped, with AI showing the options and trade-offs and negotiating against the counterparty's AI. Two thousand contracts go into one Knicks home game, and only a handful are bespoke. Spellbook (Khosla portfolio) is moving to "autonomous contracting," and Rabois says a Fortune 100 customer estimates $21M saved in outside-counsel fees over three years. Harvey, by contrast, he reads from outside as building "a one-click button that allows a CEO to see the entire world of law and regulation," starting with large-company GCs. Both can be large; the visions are distinct.

The empirical caution: [[clinical-ai-vs-frontier-llms]] found frontier models beating purpose-built clinical tools on blinded clinician review. If "the right answer in the middle of the distribution" is where the lab's model is strongest, that layer is the lab's, and the vertical company's defensible layer has to be something else. Rabois's remaining sections are a list of what that something else can be.

## The Cursor lesson: in the path of the frontier, build your own model

"You definitely need to build probably your own model if you're in the path of a frontier model. You're going to have to have a faster and better and deeper data loop."

Cursor is his worked example. He calls its acquisition "heroic" (everyone made money) but says its future as an independent company was "pretty bleak." It had the talent and the data, pioneering scalable self-coding and accounting for something like 30% of Anthropic's usage by his loose estimate. Building frontier-competitive models would have cost on the order of a billion dollars, and against a large acquisition offer the risk/reward did not pencil. Had they started earlier, the price would have been lower and the evidence stronger. "Cursor could have survived, but not once they really didn't invest enough, fast enough, deeply enough in their own model." (The host notes Cursor's Composer model launched only about six months before the acquisition and had already taken meaningful usage share.)

This is the sharpest claim in the episode and the one most in tension with the rest of the wiki. [[pacing-the-frontier]] and [[ai-coding-harnesses]] argue the harness, not the model, is becoming the moat; [[commodity-trap]] argues the labs escape inference commoditization by climbing into exactly the products Cursor built. Rabois's position is narrower than either: if your product sits directly on the lab's roadmap (coding is the canonical case), neither harness nor data saves you without your own model. Everything below is about not being on that roadmap.

## Six properties that hold against a frontier model

Rabois lists what gives a vertical company "lots of potential" against a model: "compounding loops, non-accessible data, cutting by small cells and slivers, corner cases." Two more, the last mile and breadth, come later in the conversation.

1. **A compounding data loop where returns do not diminish.** Self-driving is the clean case: roads times conditions is effectively unbounded, so whoever has the most data keeps pulling away. Coding may show diminishing returns for second and third movers; Rabois is unsure. Loops are "really hard" to keep running fast.

2. **Public-but-not-accessible data.** His distinction: "it's public but not accessible, which is a difference." State Affairs (Khosla portfolio) monitors state legislation for Fortune 1000 companies; in Wisconsin, hearing content exists only if someone attends and writes it down. Rogo's investment-banking data is likewise largely out of the public domain. This is the Rich Barton playbook from [[data-content-loops]] (aggregate withheld industry data) relocated to the AI era, where the withheld data is what the lab's model has never seen.

3. **Slicing by cells.** NBA contracts, consumer-packaged-goods contracts, and space-launch contracts behave differently; the vertical company that cuts its data finely enough has data density the general model lacks. Rabois concedes "you have to keep slicing and slicing."

4. **Corner cases.** Law is his example of a vertical where the tails matter enough that the middle-of-the-distribution model is not the product.

5. **The last mile: standing behind the answer.** In law and medicine, "getting 99% of the way there may not be the same product as the full solution." The product is the answer plus the malpractice coverage, the license, and the regulatory liability. Accounting shows all the dimensions at once: closing the books is tractable and a lab "if it had context, could do that"; audit requires a third party by definition; tax carries "a noose around your neck if you're wrong." Will a frontier lab file your taxes and eat the penalties? Khosla funded both Basis (sells book-closing to most of the top 150 accounting firms; an accountant shortage means firms take more clients with fewer staff) and an AI-native accounting firm built on Basis that holds the licenses to do tax and audit.

6. **Breadth: own the whole job.** Comp (as transcribed) "replaces humans in HR with AI," launched in Brazil with large public companies and is entering the US. Rabois: "if you can only do a sliver... you're not doing the proper job to be done, and you might be a little bit more dependent on the frontier" than you want. Whereas "there's no way Anthropic's like replacing HR departments." Breadth is defensible precisely because it is unattractive to the lab.

A seventh, more speculative one: **a harness tuned to jagged intelligence.** If frontier models keep having uneven edges (one better for memoir, another for poetry), then "a harness-ish thing that's tuned to whatever the task is, using different models under the hood, might have a long way to run." Rabois does not know whether jaggedness persists; he credits Harvey's benchmarking program with both pursuing this and cutting through the marketing clutter. This is the Rabois version of the harness/model modularization argument in [[pacing-the-frontier]].

## Department-scale automation and AI-native services

The market-size argument runs through Ramp. Its goal was always "the app that a CFO has on his or her phone and controls everything that the finance organization needs to do." Six or seven years ago that was implausible; Rabois says it now feels like next year's release: FP&A, close, procurement, policy enforcement, "token spend, token management, token ROI versus human ROI," all in the app. "The future organization should need just one CFO, which is legally required as a Delaware corp." Apply the same frame to Harvey across all law and regulation and the business is enormous.

The hosts offer a two-bucket taxonomy. Bucket one is the industry-specific GPT or agent (Harvey, Rogo at the surface level), which is where nearly all the zero-to-$100M-in-18-months stories live. Bucket two is AI-native services: "we're going to handle this from A to Z for you." Rabois agrees descriptively but says Khosla orients on 2030, where bucket one needs one of the properties above and bucket two is the form that department-scale automation naturally takes. Asked whether a niche vertical the labs ignore ("they'd rather make money off it via API credits") is enough on its own, he answers "maybe" and points to the accounting pair as a both-and.

Read against the wiki: this is the heavy end of Vernal's [[software-industry-barbell]] (one AI-native system per buying center or industry) with the mechanism filled in. The lab does not follow you into HR or audit because the job is wide, liability-bearing, and labor-shaped rather than model-shaped. It is also the implementation-layer thesis of [[ai-value-capture]] stated as an operating plan, and the department-as-product version of [[asset-light-software]].

## Tesla's wedge, not Google's checkbook

Durability still has to be reached from traction. Rabois contrasts two playbooks. Waymo had Google's money and mapped every road for years at a loss, and it is working. Tesla had no spare billions, so it built a car good enough to be driven everywhere and collected data at roughly zero marginal cost until it could ship the feature. "Most startups need to follow Tesla's playbook." That means a **wedge**: a product that gets into the market and generates scale, data, and accumulating advantage on its own economics. The alternative is to be one of the very few founders who can raise hundreds of millions "pseudo one-shot," which depends on the founder's credibility and on a macro environment willing to fund it.

## Go-to-market: top-down plus brand, and why he changed his mind on enterprise

Rabois used to refuse enterprise investing out of self-awareness: he had built PayPal- and Square-shaped businesses on marketing and product instead of salespeople and knew nothing about enterprise sales. "I had this allergy to salespeople, which led to an allergy to enterprise." He has "changed my view completely" because the AI-era motion is different.

**Top-down sales.** The founder-CEO goes to the customer's CEO, board member, or one level below and creates the sale; an AE moves paper across the line. It works because AI is on every board agenda: "anytime you're on the agenda for a board meeting or CEO priority list, you can do top-down sales." The corollary is sharp. If you are not in the CEO's top three priorities, top-down is "probably your enemy": the last thing you want is the CEO noticing a million-dollar line item for a startup. He expects this to fade once the AI wave crests and organizations feel they have made their bets. This extends his January 2026 claim in [[ai-native-company-building]] that top-down is a real but temporary anomaly, now with the mechanism (board-agenda salience) and an expiry condition.

**Brand marketing, meaning storytelling.** The second half of the motion is becoming the default name. Legal AI is, he says, the hottest technology topic on X in 2026 (benchmark fights, Harvey, Legora, Spellbook, vertical podcasts), and half of a podcast audience recognizes startup names that in the old enterprise era "would have been like zero" recognizable. "If you're in investment banking, there's no chance now that you don't know what Rogo is." Brand outlasts the top-down window because it does not depend on board salience, and it is not necessarily paid: Harvey's benchmarks are his example of creative, unpaid brand. See [[credibility-based-selling]] for the mechanism by which public expertise substitutes for a sales motion.

**Founder profile.** One founder (not necessarily the CEO) must have the cachet to hold their own with senior executives, and the team must be able to tell a story that cuts through. The AE-cohort ramp model (hire N reps, predict revenue by cohort) still works for some companies (he names Profound) but is not the pattern he wants to fund.

He notes the upside for him personally: the old enterprise investors' playbooks are not the ones winning, so "we're all back to zero and we're all learning." This is consistent with [[institutionalized-vs-improvised-software]] on adoption being an org-wide, top-down purchase decision, with the twist that AI temporarily put that decision on the CEO's own desk.

## Capital: milestones, fund size, ownership

**All parties end.** Rabois's specific prediction: any trouble with Anthropic's IPO, in timing or trading valuation, "even a blip for them will be felt as an earthquake for everybody else," because current pricing puts an extra zero on expected value ("if an outcome could be trillions, we can pay billions"). Remove the zero and the zeros disappear fast. Compare the capital overhang in [[pacing-the-frontier]] and the pricing-not-valuing argument in [[scaling-vs-profitability]].

**When front-loading is rational.** Khosla asks founders for their two-to-five inflection milestones and sequences financing around validating them. Where the slope is a step function with no milestone below it, a $20M to $100M first check is the correct, deliberate conclusion: anything less cannot reach any milestone. Most front-loaded raises are not doing that analysis. See [[startup-fundraising]] for the when-to-raise gate this sharpens.

**Fund size dictates strategy.** LPs measure dollars returned on dollars invested more than IRR, so a 100x on $1M is irrelevant to a large fund; the fund must "move the needle by billions." Strategy, fund size, and LP base have to align the way a company's market, segment, value proposition, and pricing do.

**Ownership depends on how you compete.** A consigliere investor whose scarce input is high-quality time needs ownership to cover that opportunity cost; a momentum investor does not, and for them ownership can be a red herring. Rabois places himself in the first camp: "the scarcity is not how many dollars I can invest."

## Rapid-fire positions

- **AI roll-ups: bearish.** "More business fundamental value is created on growth than cost reduction." Roll-up pitches are mostly about using AI to cut costs, which improves cash flow but not enterprise value. His counter-example is Ramp, accelerating for seven straight quarters at over 100% annualized, which at his last check made it the only private equity with Nvidia's growth-plus-breakeven profile. A roll-up using AI to propel growth, with evidence, would interest him; that is not 90% of what he hears.
- **Vertical SaaS incumbents (Toast, ServiceTitan-shaped): bearish.** Expect "a new wave of companies in every vertical built from the ground up, a little bit like mobile." Few web-era incumbents made the mobile transition; the apps on your home screen were mostly not internet companies. Agrees with [[software-industry-barbell]] and with [[ai-native-company-building]] on integration count no longer being a moat.
- **Deep tech: very bullish.** His definition is clean: deep tech is when the primary risk is "can this actually be built?" and demand is not in doubt if it is. Market risk ("will they buy it at a price we like?") is ordinary startup risk.
- **Podcasts: bullish** for a unique voice that cuts through; Stratechery, newly sponsored by Stripe, is his model of durable original thinking.

## What this adds

Rabois's framework is a checklist for the question Richard Hamming would ask of any vertical AI company: *why doesn't the lab do this?* His acceptable answers are that the data is withheld or sliced too finely, that the tails matter, that someone has to carry the liability, or that the job is wide and labor-shaped. His unacceptable answer is "the models will stop improving." The Cursor case sets the price of being on the roadmap anyway: roughly a billion dollars of your own model, started early.

Two tensions are worth holding. First, Rabois's own best example of dominance (Rogo) is a copilot, which suggests the autopilot screen is about trajectory rather than current form. Second, the "middle of the distribution" is where frontier models are empirically strongest, so the vertical company's product must be the thing wrapped around the answer, not the answer. Both tensions point the same way as the department-scale thesis: own the outcome and the liability, and let the model be a supplier.

## Sources

- Keith Rabois with Luke Sophinos and Nic Poulos (2026, October 28). "Most AI Startups Won't Survive (Here's How to Build One That Does) | Keith Rabois." *Verticals: A Weekly Biz Show On Vertical AI.* <https://www.youtube.com/watch?v=_8wcKJFxIa4> — [[2026-10-28-rabois-vertical-ai-survival|local copy]]
