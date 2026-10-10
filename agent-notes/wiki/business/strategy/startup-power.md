---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-09-01-making-startups-powerful.md
compiled_at: 2026-10-09
model: claude-fable-5-1
confidence: medium
---

# Startup Power

Paul Graham's September 2026 essay "Making Startups Powerful" describes the heuristic he finds most useful in YC office hours: instead of asking how a company could make more money, ask what would make it more *powerful*. Graham's claim is that the money question yields incremental improvements, while the power question sometimes makes a company orders of magnitude more valuable, because it forces you to consider transforming the idea rather than optimizing it.

"Power" here is not a vague aspiration. Nearly every lever Graham lists is a specific structural position relative to other companies: owning the customer instead of supplying a component, being the marketplace instead of a service, being the ecosystem others build on, selling to buyers who decide on merit rather than on procurement politics. The essay reads as a founder-facing catalogue of the same positions that strategy writers describe from the outside in [[competitive-moats]], [[aggregation-theory]] and [[network-effects]] — with the crucial difference that Graham is prescribing how a company with no power yet can acquire some.

## The master heuristic and its constraint

Graham offers two framings that bracket all the specific levers.

**Where is the idea being held back by other companies?** Most of the transformations, he observes, turn out to be escapes: a component supplier escapes the box another company built around it by owning the customer relationship; a startup selling into bureaucracies escapes them by selling earlier in the customer's life or by competing with the customer directly. He proposes "in what ways is the current idea being held back by other companies?" as a generative question for making an idea bigger.

**Every lever must make things better for the customer.** Graham is explicit that you cannot add network effects, route money through yourself, or go full stack "just because you'd like to" — there is no uptake unless the result is better for the customer. A newly founded startup is too weak to force anything on anyone, which is why, in his view, startups are on the whole good for the world: the only path to power runs through making customers' lives better. He suggests running this constraint backwards as an idea generator: picture the perfect world from the customer's point of view and ask which component of it the startup could become.

The second framing is what distinguishes the essay from a cynical playbook. The same positions (marketplace, platform, rake) are described in [[marketplace-rake]] and [[multi-sided-markets]] as things an incumbent can abuse; Graham's point is that a startup can only reach them by being useful first.

## The levers

### Go upstream: own the relationship, the money, the stage, the data

Graham's one-line summary is "upstream is almost always good, whether it's with money or user relationship or customer stage or data." Four distinct moves fall under it.

- **Own the customer relationship and make money flow through you.** The component supplier who lives in a box built by another company is the weak position; the company the money passes through is the strong one. This is the founder-side view of Thompson's aggregation thesis in [[aggregation-theory]]: suppliers get commoditized and the customer relationship becomes the scarce asset. Graham's AI-era footnote is that *tokens* flowing through you usually means money flows through you too, which in theory makes the model companies your component suppliers — the same weakness Evans diagnoses from the model side in [[ai-platform-moats]], where the consumer relationship sits elsewhere. Graham immediately adds the caveat that the question is how easily the model companies could engulf you or your customers, which is precisely the "up the stack" move that [[commodity-trap]] argues the labs are forced to make.
- **Sell to customers at the earliest point in their life.** Graham calls it strange but true that selling to earlier-stage companies makes you more powerful, even though they have less money: if you sign them at the very beginning and charge on usage, your revenue grows at startup rates. Stripe is the model — it signs companies at the first possible moment, and because payments infrastructure that "ain't broke" never gets replaced, those customers never churn. Footnote 7 contains the reframing: replace "what size customers should we target?" with "at what point in their life should we acquire customers?" and targeting bigger companies reveals itself as merely targeting the same company later. Thinking in quarters makes customers look like fixed sizes; thinking in decades shows their trajectories. This is the growth-rate-over-absolute-numbers logic of [[exponential-growth-billionaire-math]] and [[superlinear-returns]] applied to customer selection: the fastest growth rate comes from selling to the customers who grow and decide fastest.
- **Get the data early.** Rippling's goal was to be both the operating system for employee data and most of the applications on it, without knowing in advance what that would look like. So it started with onboarding software, because that is where employee data begins; and because more was at stake than the onboarding market, the product was far better than it needed to be and spread fast. This is a close cousin of Barton's playbook in [[data-content-loops]], and Rippling reappears as the SMB all-in-one exemplar in [[software-industry-barbell]].
- **Sell to customers who decide fast.** Graham's argument is not just about speed. Customers who decide fast decide on quality, and startups usually make the best product, so fast-deciding customers convert product quality directly into revenue. Enterprise sales to 500-person companies is "notoriously not a domain where the best product wins." Hospitals and school districts are "like walking through mud," and his standing question for founders selling to them is whether some subset of the market decides faster. The ideal is a product batchmates can Collison-install today. The a16z screen in [[design-partners]] makes the same point from the other side: launch into the highest-urgency, fastest-moving segment.

### Induce network effects, then generalize

Graham treats finding network effects as a challenge to attempt on every company, including ones where they seem unlikely (footnote 3 notes YC itself turned out to be one). When it works it can change the category: a service becomes a marketplace. The full app store is the deluxe version; failing that, let users share something (opt-in benchmarking against other users; in AI, opt-in training on user interactions, so that opted-in users get a better model than the vanilla one).

The sharper move is to generalize the idea so that network effects appear. His worked example: a startup letting agents pay for things should be asked whether agents could pay *each other*. If so, it is a marketplace, and marketplaces are valuable enough that it would be worth spending serious time inventing what agents would pay each other for, tilting the company toward it, and even acting as market maker to bootstrap liquidity. Griffin's taxonomy in [[network-effects]] and the chicken-and-egg prescriptions in [[multi-sided-markets]] are the strategy-side literature on what Graham is pointing at; his contribution is the instruction to go looking for the marketplace inside an idea that does not look like one.

### Become the platform: app stores, standards, extensibility, APIs

An app store makes every other company's effort to build valuable things make you more valuable, ideally combined with owning the customer and the money. Footnote 2 adds a smaller version for companies too young for an app store: propose the standard for how products in a new field interact. Graham's observation is that everyone is so hungry for standards that the first one proposed tends to win regardless of who proposed it, so a tiny early entrant should not be shy.

Extensibility is the continuum below a full app store, and Graham argues that not restricting or charging for extensions tends to produce a bigger ecosystem (footnote 6 speculates this flexibility could be what finally displaces Apple, which will certainly stay restrictive about integration). The far end is exposing the product through an API. Companies resist this because they dislike losing control of how their software is used, but Graham suspects that rigidity is usually a mistake, and especially so now that agents are replacing human users and nobody knows what they will want to do. His advice for a "larval startup" with nothing to lose: err on the side of APIs. This dovetails with [[agents-as-aggregators]], where Thompson argues suppliers who try to charge agents for access will simply be routed around.

### Go full stack, or eat the customer from the inside

Instead of selling technology to companies doing *x*, use it to do *x* yourself in competition with them. Graham describes the transformation as almost physical: the idea stretches to engulf what had been the customer, and once you own the outer surface its shape changes too. The gradual variant is to do the customer's hardest work for them until, in the limit, you are doing all the brainwork and they are running errands — at which point the real customer is *their* customer and the original one is "a kind of hand puppet." Footnote 8 ties this to customer selection: in a normal industry, slow-adopting customers are an opportunity because you can go full stack around them; what makes hospitals and school districts grim is that you generally cannot, though there are routes around schools directly to students.

Xu's "verticalize to an outcome" advice in [[commit-and-go-deep]] and Taylor's case in [[outcome-based-pricing]] describe the same move from the YC and vendor sides, and [[low-margin-ai-winners]] quantifies why doing a thin-margin operator's coordination work for them is so attractive.

### Listen for tails that could wag the dog

PayPal began as security software for handheld devices; PayPal itself was a demo. When eBay sellers started using it to take payments, the founders took a couple of months to acknowledge that this was now the business. So when founders build something peripheral, Graham asks whether it could be the real product, and he treats users "misusing" a product as a strong signal: it means they want something badly enough to use a non-solution as a solution. The related growth point is that PayPal helped users make money, which Graham says makes a company powerful twice over, since such users adopt fast and pay a lot — a property he attributes to most of YC's most successful companies and to YC itself. This is the strategic complement to the "noticed, not invented" ideation in [[organic-startup-ideation]].

### Play the long game and be generous

Both levers rest on the same observation: most of the people a startup deals with are not playing long. Competing startups are run by opportunists hoping to be acquired; big-company counterparts are executives thinking about this quarter. So tradeoffs that pay off in ten years are systematically underpriced, and the classic one is selling as cheaply as you need to in order to get all the users before worrying about margin. Footnote 4 adds the limit: selling at a loss can be worthwhile, but give away too much and you lose the signal customers send by paying — "if your product is a $10 bill that you sell for $5, your growth rate isn't telling you anything useful."

Generosity is the same bet stated as O'Reilly's maxim, create more value than you capture. Graham frames the choice as two worldviews: squeezing customers yields at most 2x, while discovering something new to make for them can yield 10x or 100x. Open sourcing is the canonical case — give the product away, become the standard and earn trust, and end up with a small piece of a much bigger pie. Footnote 5 is a sociological aside: the O'Reilly stance is more common among founders because founders remember weakness, whereas hired CEOs take the company's power for granted and switch to squeezing. Gurley's rake argument in [[marketplace-rake]] and Spolsky's framework in [[commoditize-your-complement]] supply the mechanics for why giving things away can be the dominant strategy rather than charity.

### Avoid mafia markets, or come in from the side

Because startups win by making the best product, they are strongest on level playing fields and weakest in markets run by what Graham calls mafia — record labels and PBMs are his examples, and footnote 9 offers "full of lawyers" as the tell. There the best product does not win, and a startup may exist only as long as the incumbents allow. Graham thinks they can be defeated, but only by coming in from the side and making them irrelevant, so that beating them is an ancillary benefit of winning in another dimension rather than the plan. This is consistent with Neumann's point in [[startup-uncertainty]] that disruption works when incumbents cannot imitate without breaking their own relationships.

### Just y

The last source of weakness is internal. Graham reports that a surprising share of his advice contains the word "just": *you don't need to x, just y*. Ideas that evolved from earlier ideas carry parts they no longer need, and in very early startups the complexity is often fear, the company "unconsciously cowering" by attempting something less ambitious than it could. "Just y" is usually "just stand up straight."

## Synthesis

Read together, the levers sort into three kinds of power. **Positional** power is being upstream: owning the relationship, the money, the customer's earliest stage, or the data. **Structural** power is having others build on you: network effects, marketplaces, standards, APIs, ecosystems. **Temporal** power is outlasting short-term counterparts by pricing the long game correctly. Graham's customer constraint applies to all three, and it is the reason the essay cannot be reduced to "become a monopoly": a startup can only arrive at any of these positions by being chosen.

Two implications the essay leaves implicit:

- **The customer-selection advice is the most actionable and the most stage-dependent.** The Stripe pattern (install early, charge on usage, never churn) presupposes a product that sits on infrastructure the customer will not revisit. For a product customers *do* revisit, selling to early-stage companies still buys fast decisions but not lifetime lock-in; the no-churn assumption in footnote 7 is doing the real work.
- **The hospitals-and-school-districts warning is about sequencing, not avoidance.** Graham's advice to founders in those markets is to find the fastest-deciding subset first, or to route around the institution to the end user, not to abandon the domain. Combined with the "come in from the side" prescription for mafia markets, the essay implies that public-sector and healthcare founders should pick an entry point where product quality is actually the decision criterion and let the institutional market be a later consequence.

## Sources

- Graham, Paul (2026). "Making Startups Powerful." <https://paulgraham.com/powerful.html> — [[2026-09-01-making-startups-powerful|local copy]]
