---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-07-09-evans-token-pricing.md
compiled_at: 2026-07-09
model: claude-opus-4-8
confidence: medium
---

# Token pricing

Benedict Evans's July 2026 essay on where the price of an AI token settles once today's supply crunch eases. It is the economic deep-dive underneath the commodity-models pillar of [[ai-eats-the-world]]: the deck asserts frontier models become commodity infrastructure; this essay works through *why*, what would have to change for a different outcome, and — crucially — how little anyone can actually know right now.

Evans's one-line answer: **token price is a function of supply and demand, priced somewhere between the seller's marginal cost and the buyer's ROI — but we don't know what supply, demand, marginal cost, or ROI will be.** Every dynamic he can currently see points toward frontier models becoming low-margin commodity infrastructure with the value captured up the stack; every path to the *opposite* outcome (pricing power, value capture, winner-take-all) "requires something to change" that we can't yet see.

## The situation is transitory and unstable

Two things are certain: we're in a supply crunch, and it's unstable. Everything is in play.

- **Supply side:** $1tr+ of data-centre capex is in the pipeline (plus semiconductor capex behind it), inference efficiency is improving fast, and new models vary wildly in token-efficiency.
- **Demand side:** the market has been capacity-constrained since 2022, but the *acute* crunch of early 2026 was driven by product-market fit in essentially **one use case — software development** — which is a small field. The warning: if a consumer use case with hundreds of millions of DAUs found PMF, today's infrastructure couldn't serve it at any price. We don't know what the next use case to scale is, when it arrives, or its token appetite.

### The margin picture

Inference reportedly runs at **40–50% gross margins** today, including depreciation of the servers (but nobody knows the true asset life — 5 years? 7?). That figure **excludes training**, which currently costs far more than revenue. The structural claim: inference is marginal cost, training is fixed cost, so at high enough revenue you reach profitability — *if* training costs behave. On the buyer side, it's unclear how much of the recent surge has a CFO-quantifiable ROI, so we don't know what people will actually pay. (swyx and Shaughnessy dig into the subsidy/loss-making side of this in [[ai-lab-economics]]; the capex-to-return chain is the "AI capex required-return" framework in [[wiki/business/finance/index|Business > Finance]].)

## Two ways to forecast — both weak

**Bottom-up modelling** (chips × performance × data-center throughput × power × price discipline × use cases) gets you a number, but Evans compares it to building a five-year broadband forecast in 1998: the spreadsheet is pretty, maybe right for this year, useless for the long-run market structure. Too many unknown variables.

**Top-down** (how do things like this tend to play out?) is the more honest frame, and it turns on one curve: **intelligence vs. cost-per-intelligence**. Where that curve goes drives everything, and Evans organizes the whole question into four sub-questions.

## The four questions that decide the outcome

1. **How many people pay to be at the frontier (top-right of the curve)?** Some use cases already run fine on a small/old/open model for ~free on-device; some genuinely do better with the newest, most expensive frontier model; most are in between. So how much demand actually climbs the cost curve *and has ROI for it*, versus being served by "good enough" commoditised models? The Panglossian view — ROI rises with more expensive models because results are better — applies *where, exactly*?
2. **Does the frontier keep moving significantly?** The core science question: does the frontier keep improving, keep needing more compute, and keep doing so fast enough to stay ahead of downward pricing pressure from efficiency and capacity gains? Does the expensive head of the curve remain a thing at all?
3. **Is there still fierce competition among frontier models?** Today ~5 companies use mostly the same science and data and get mostly the same results, with **no known network effect or winner-take-all mechanism**. A different outcome needs the field to shrink, or models to *diverge* (clear per-domain leads) — either of which could create pricing power. Does that happen?
4. **How much value does the model itself capture?** Even where you need the big expensive model underneath, how much has to be wrapped in tooling, proprietary data, GTM, support — everything a traditional software company does? Can the model be the whole product, or is it always *infrastructure you build a product on*? At the extreme: could the model invent and operate all that wrapping itself, and charge by seat/outcome? Or do the highest-value use cases necessarily live inside hundreds of new companies that pick and choose models?

None of these is a binary — all are questions of degree that vary by use case. The two poles: **two or three giant minds** running half of everything with massive pricing power, versus **LLMs as databases** — millions of them, big and small, where the value is in what you build on top (every SaaS company is a "database wrapper"). One future: Anthropic (or an unknown company) wins the whole thing and sets its own terms. The other: routers run real-time auctions across hundreds of low-margin model-farms and a benchmark company clips a fee on every call.

## Why the uncertainty is different this time

Evans invokes the S-curve: early in any big technology it's clear this is huge but nothing else is clear (the internet in the mid-1990s, mobile in 2008–09). But this uncertainty is *worse* than usual, because **we have no theoretical understanding of why these models work so well, so we don't know how much better they can get.** In 1995 we knew there were <100m expensive PCs and telcos couldn't wire everyone for fibre next year; in 2010 we knew the next iPhone wouldn't have retinal projection. We knew the physical limits. With LLMs we don't — next month a new approach could cut inference compute 90%, or double demand, or both.

This is a sharper epistemic caveat than the "no-one knows / what happened last time everything changed?" posture in [[ai-eats-the-world]]: there, uncertainty is about *deployment*; here it's about the *technology's own ceiling*.

## The analogy discipline

"All conversations about AI end in a hunt for metaphors." Evans grades the common ones — and then disowns the whole method.

- **Fiber (Dotcom overbuild).** Superficially like today's infra build-out, but wrong twice: fiber was built *far ahead* of demand (AI compute is *far behind*), and fiber was mostly **fixed cost** (digging holes) while AI compute is **marginal cost** (you must keep buying more compute as demand grows).
- **Mobile data (the best fit).** Marginal-cost capacity; a demand surge ~15 years ago that overwhelmed capacity and forced pricing to be rebundled; and selling *bits* is opaquely like selling *tokens* — an abstract unit of marginal cost that maps to neither value nor use case and has to be wrapped in bundles. The punchline: cellular traffic rose several orders of magnitude into a **$1tr-revenue / $200bn-capex** industry, yet **the stocks went nowhere and all the value was captured up the stack**. This is the load-bearing precedent for the commodity-infrastructure thesis.
- **Semiconductor manufacturing.** Unlike cellular, it shares AI's *escalating cost and complexity*. **Rock's Law** — cutting-edge fab cost doubles every four years — drove the field from dozens of players to a handful to effectively one (TSMC). So: could AI get so hard and expensive that only a couple of firms can do it, even *without* network effects? Yet even TSMC, a de facto frontier monopoly with nice margins, captures little of the broader tech economy's value — net income $53bn last year, less than half of Apple's.
- **Altman's own two:** OpenAI as **Windows** (high-margin, capital-light, network-effect monopoly) *and* as an **electricity utility** (natural monopoly but low-margin, regulated, pure commodity) — mutually contradictory. Plus **cloud** (three players, good margins, differentiated, but limited value-capture).

**The meta-point: analogies have no predictive value.** You can't prove an outcome by arguing how much something resembles the analogy. The cautionary case is the "Android beats iOS because open Wintel beat closed Mac" argument that many smart people got wrong 15 years ago — the same category error as doomers arguing "AI is *like* nuclear weapons." Bits, tokens, and transistors are all different; AI will be different too. What the examples *do* prove empirically: something can be world-changing, expensive, and full of sophisticated science and yet have a **wide range of possible equilibria** — high-margin or low-margin, concentrated or fragmented. There is no single inevitable path, and "you don't understand exponentials!" doesn't collapse that range.

## What would have to change for labs to escape commodity status

Every non-commodity outcome requires something to change that we don't yet see. Evans's candidate "maybes":

- Frontier competition slackens — *but* in the last six months Zuckerberg and Musk jumped **from zero back onto the leaderboards**, i.e. competition intensified.
- Network effects emerge (none known today).
- Chatbots grow into products that don't need software wrapping (Evans is on record thinking chat is a poor interface — [[ai-eats-the-world]]).
- One lab out-executes on sheer product dynamism (as Microsoft/Google/Facebook/Apple each did *before* winner-take-all locked in).

### The two *dei ex machina*: Trump and China

The market may not stay free. China is reportedly considering **regulating open source**; some people near Trump have floated the same (though with Meta abandoning Llama, the US has no leading open model anyway); and **export controls** could expand and systematise. Regulation cuts both ways for the thesis — many read Anthropic's and OpenAI's regulation pleas as **regulatory capture**. This is the same geopolitical lever Shaughnessy identifies as the "kill switch" in [[ai-lab-economics]]: **China going closed-source would flip the whole picture from bearish to bullish** for Western labs' pricing power, because the free-Chinese-open-weights escape valve is a large part of what caps it.

## Bottom line

As the supply crunch eases, current dynamics point to frontier models becoming **commodity infrastructure with the value built on top** — and a different outcome needs something to happen that isn't yet visible. Note the epistemic stance: this is a *default extrapolation of present dynamics*, explicitly not a confident forecast. Evans's repeated "we don't know" is the actual thesis.

## Related

- [[ai-eats-the-world]] — Evans's parent macro deck; this essay is the economic engine under its commodity-models pillar and the mobile-networks analogy.
- [[ai-lab-economics]] — swyx on the model-lab/agent-lab split and subscription subsidies; Shaughnessy's subsidy-unwind bear case, whose China kill-switch matches Evans's *deus ex machina*.
- [[open-source-in-the-enterprise]] — Zhang's maturity-curve reading of when demand climbs vs. descends Evans's intelligence/cost curve (new use cases buy frontier intelligence; mature ones flip to small, fine-tuned, self-hosted open weights).
- [[prompt-caching]] — one concrete lever on the "inference efficiency improving fast" supply-side variable.

## Sources
- Benedict Evans (July 9, 2026). "Ways to think about token pricing." <https://www.ben-evans.com/benedictevans/2026/7/9/ways-to-think-about-token-pricing> — [[2026-07-09-evans-token-pricing|local copy]]
</content>
