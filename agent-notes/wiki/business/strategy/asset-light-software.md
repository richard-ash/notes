---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-10-05-asset-light-software.md
compiled_at: 2026-10-05
model: claude-fable-5-1
confidence: medium
---

# Asset-Light Software

Will Manidis (Science.io) and John Kennedy (Mesa) argue, in a January 2024 essay that Manidis reposted to X in October 2026, that software businesses are shifting from **fixed cost to variable cost**. Every line item that used to require hiring (developers, sales reps, customer success, ops) can now be "selectively ignored, automated, delegated, or consumed as a service," and generative AI accelerates the trend by substituting for junior white-collar labor. The result is an *asset-light* software company: high margin, cash-flow-first, founder-controlled, and poorly served by venture capital. The essay predates the agentic-coding boom, which makes it a useful fixed point for judging what the 2026 theses in [[software-industry-barbell]] and [[minimum-viable-saleable-software]] added.

## The fixed-cost playbook and why it saturated

The authors' founding-era advice (late 2010s) was uniform: raise venture money to incur fixed costs that pay back over time, grow fast, raise again. Their two companies sold into very different markets (school districts; unstructured healthcare data) yet made identical investments and felt identical pressures. They quote Robert Smith of Vista Equity Partners, who built a $100B+ buyout firm on the observation that "all software companies taste like chicken": 80% of what any software company does is the same.

That sameness is the lever. If the work is standard, each cost bucket becomes an ecosystem of vendors and can be bought rather than staffed. The authors cite SaaS Capital's benchmark for the median bootstrapped B2B SaaS company, which spends roughly 90% of ARR on costs:

| Cost bucket | Share of ARR | Asset-light substitute the authors name |
| --- | --- | --- |
| Go-to-market | 25% | Resellers with installed bases (AWS Marketplace) instead of a sales team |
| R&D | 24% | A Django app from a Replit bounty for $650; white-labeling AWS/Microsoft BI tooling |
| G&A and misc. | 15% | Virtual assistants instead of headcount |
| Hosting and implementation | 13% | Consumption-priced infrastructure |
| Customer retention | 10% | Zapier/Intercom-style tooling, itself moving to pay-per-task pricing |

Their observation that the tooling layer is itself shifting from per-seat-per-year to **per-task consumption pricing** is the supply-side precondition for everything else: a company whose inputs are variable can run itself as a variable-cost business. The demand-side mirror, charging *your own* customers per outcome, is Taylor's argument in [[outcome-based-pricing]].

## Three theories of an AI-driven SaaS future

### Content creation is to generative AI what distribution was to the internet

The internet gave programmatic, global, zero-marginal-cost *distribution*; that is what turned shrink-wrapped software into SaaS and reorganized social life. Generative AI gives programmatic, global, diminishing-marginal-cost *creation*. The authors call this "an industrial revolution for white-collar work," by analogy to captured energy letting machines rather than hands make goods. The analogy is load-bearing for the rest of the essay: if creation is now cheap, the scarce thing moves elsewhere, which is the same conservation-of-attractive-profits logic discussed under [[scarce-assets]].

### A Perez-style technological revolution, restarted

Using Carlota Perez's *Technological Revolutions and Financial Capital* (2002), the authors map the internet cycle as an installation period (the extended 1990s: browsers as interface; search, e-commerce, social as categories), a slump (dot-com crash through the Great Recession), and a deployment period (roughly 2009 to 2022: Salesforce maturing, AWS, marketplace models, and as the "last new products" narrow vertical SaaS and consumption-priced infrastructure like Snowflake).

Their claim is that ChatGPT was a new big bang and that early 2024 sat in a fresh **installation period**: $27B into generative-AI startups in 2023, chat congealing as the default interface, a race to build general and narrow models. They call the coming slump "inevitable," since unit economics were "hidden under the comfortable blankets of venture capital"; the example given is GitHub Copilot at $100M ARR reportedly losing about $20 per user per month on compute. The investable conclusion is that fortunes go to whoever can "speed-run" the arc into deployment.

### Sustaining for products, disruptive for costs

Applying Christensen's taxonomy, the authors split generative AI in two:

- **For software products it is a sustaining innovation.** Commodity intelligence via API makes existing software more personalized, automated, and sticky. It reinforces incumbents' positions rather than resetting the market.
- **For the cost of white-collar work it is a disruptive innovation.** Most knowledge work is generating text (code, support emails, summaries, posts). "An army of infinite junior- to mid-level knowledge workers, accessible via an API" substitutes for the junior and mid-level employees who make up the base of every org pyramid.

The catch they flag is that infinite junior employees produce infinite junior mistakes, so the binding problem becomes supervision at scale. Their proposed shape for the firm is the **marketing org** rather than the engineering pyramid: senior strategists and creatives managing automated systems the way HubSpot and Mailchimp let a small team run campaigns, with tools like Poolside doing for code what those did for email. The historical precedent offered is the spreadsheet: clerks and bookkeepers outnumbered analysts, auditors, and managers by a third before VisiCalc; twenty years later analysts and managers outnumbered clerks two and a half to one. "Every clerk becomes an analyst, every writer an editor, every developer an architect."

This is the 2024 statement of what [[ai-native-company-building]] (Hu, Rabois) later turns into an operating playbook, and the supervision problem they name is the verification-labor bottleneck that Leach quantifies in [[minimum-viable-saleable-software]]. The factor-share question underneath (does leverage moving "up the chain" preserve labor's share?) is the subject of [[labor-share-under-automation]].

## Software as a variable-cost business

The authors' summary line is "SaaS is dead. Long live SaaS." The product category persists; the cost structure inverts. "Every cost is a choice." Two consequences they draw:

- **Services businesses can spin up software lines.** If the marginal software product is cheap, a firm with customer relationships can add software to what it already sells, rather than a software firm hiring a services arm.
- **Private-equity operating discipline can be applied to building, not buying.** Vista-style playbooks presuppose a mature company to optimize; asset-light construction lets the same rigor apply from day one.

## Financing: Hank Hill, not Zuckerberg

The authors describe venture capital as "a narrow product for a narrow set of companies in a narrow set of market conditions": it monetizes conviction about enormous unsaturated markets and depends on someone writing a bigger check next. The software-business spectrum runs from eleven-figure companies down to "CPAs in Omaha building steady incomes from no-code tools," and financing is over-indexed to the top.

Their prediction is that lowering the barrier to starting a software business changes who starts one. "The future median software founder will aspire to be Hank Hill, not Mark Zuckerberg": steady cash flow over hypergrowth, sleeping at home over sleeping at the office, a niche served well over a global market. Such founders will prefer **non-dilutive and structured capital** (credit, warrants, loans), and venture will reject them as much as they reject it.

They also argue prestige VC "dug its own grave" on the numbers: most of the ~$1T Pitchbook tracked into private software equity since 2018 went in while public SaaS traded above 10× ARR; by early 2024 the public median was ~5×, with historical-mean reversion implying further to fall. "By some crude math, most dollars invested in private software equity could not be sold for fifty cents."

Three existing articles bracket this. Harris's gate in [[startup-fundraising]] (raise only when capital is the binding constraint on growth) implies that for an asset-light company the honest answer is usually *don't*. Lake's playbook in [[capital-discipline]] is a case study of a founder who chose profitability as the moat. Damodaran's matrix in [[scaling-vs-profitability]] explains why scale and profit have different determinants, which is another way of saying the Hank Hill founder is not a failed Zuckerberg but a different archetype. On the supply side of credit, [[private-credit]] documents direct lenders' growing software exposure, the counterparty the authors expect these founders to find.

## The smiling curve: hyperscalers versus vertical software

The authors place the asset-light operator at one end of Thompson's smiling curve (see [[aggregation-theory]]) and the hyperscalers at the other. Their never-run headline: "AWS + Azure + Google Cloud at $200 billion in annual revenue growing 20 percent per year."

Their definition of vertical market software is deliberately deflationary: *industry-specific templates and integrations on top of commodity data warehousing and workflow.* The vertical vendor's real expertise is the market's technology stack (which systems to integrate, which reports are standard, which privacy rules apply), plus a vertical brand. As costs go variable, hyperscalers can encroach: why pay for a niche supply-chain tool when Azure offers a "good enough" version, configurable by a business manager, pre-integrated with everything else you run, with vertical personalization generated by AI? The authors would not choose to compete against a hyperscaler making a focused vertical bet, and note many startups are forced to.

Their one concession to the vertical vendor is relational: "You can't automate taking a vice president to a steak dinner." Accumulated loyalty of a vertical client base is the defense. That is precisely the relational-task residue argued for in [[ai-and-relational-scarcity]] and [[messy-jobs]], and it is the GTM half of the winner formula in [[software-industry-barbell]].

The closing move is to look below the enterprise fight. The lower and middle market, and "countless public and private sector organizations frustrated with their software," will need *services* to reach the deployment period. This is the same market that [[low-margin-ai-winners]] identifies as where AI's value actually lands, and the same "friendlier face" posture that forward-deployed delivery models adopt.

## Where this sits among related theses

| Claim in the essay (Jan 2024) | Later article | Relationship |
| --- | --- | --- |
| Median founder becomes Hank Hill; VC mis-sized for them | [[software-industry-barbell]] (Vernal, Sept 2026) | Same light end of the barbell, same warning that it is not venture-addressable; Vernal adds the newspaper analogy and the heavy-end "own the buying center" prescription |
| Vertical SaaS = templates on commodity infra; hyperscalers encroach | [[software-industry-barbell]] | Disagreement on who wins the heavy end: Manidis and Kennedy expect hyperscalers to absorb verticals, Vernal expects one AI-native company per industry. Both agree the middle hollows |
| Buy a Django app for $650; every cost can be consumed as a service | [[minimum-viable-saleable-software]] (Leach, 2026) | Corrective: cheap is not free. Verification and maintenance labor keep a zone where buying beats building, so "every cost is a choice" has a floor |
| "Good enough" Azure configurable by a business manager | [[institutionalized-vs-improvised-software]] (Evans, 2026) | Evans's objection: most people are not builders, knowing what to build is the hard part, and institutional adoption is an org-wide purchase decision. The configurable hyperscaler product is the improvised end; the vertical vendor sells the institutionalized one |
| Steady-income solo software businesses | [[solopreneur-economy]] (Stripe data) | Empirical confirmation that solo businesses are forming faster and climbing the income distribution, powered by AI filling capability gaps |
| Pay-per-task tooling | [[outcome-based-pricing]] | The same pricing shift seen from the vendor's side |
| Perez installation frenzy; slump inevitable | [[ai-capex-required-returns]], [[pacing-the-frontier]] | The 2026 state of the capital cycle: the frenzy extended rather than slumped, with the required-return math and the labs' capital overhang now the live questions |
| Infra providers on the other side of the smile | [[commodity-trap]] | Narayanan and Kapur's infrastructure case studies argue builders *rarely* keep the value they create; the authors' hyperscaler headline assumes cloud is the exception, which the commodity-trap article grants for enterprise software but not for raw inference |

## Temporal notes

- **Written January 2024, reposted October 2026.** The Replit-bounty and virtual-assistant examples now read as quaint: by 2026 the equivalent is an agent building the Django app in an afternoon, which strengthens the fixed-to-variable argument and sharpens Leach's objection that the human verifier is the remaining fixed cost.
- **The slump did not arrive on schedule.** The authors called a crash "inevitable" from inside the installation period. As of the repost the capital cycle had extended rather than broken; see [[ai-capex-required-returns]] for the required-return accounting and [[pacing-the-frontier]] for the capital and pricing overhangs. The Perez frame is unfalsified but the timing was early.
- **The Copilot loss figure** comes from late-2023 reporting and should not be read as a current number; [[token-pricing]] covers where inference margins have since settled.
- **What the authors did next.** In the 2026 repost Manidis notes that Kennedy founded Lafayette Standard Co to "prosecute this thesis," with Manidis as a small investor. The essay is therefore now a founding memo for an operating company, not only a forecast.

## Implications

- **For a founder, the cost stack is a menu, not a template.** Start from the SaaS Capital buckets and ask of each: ignore, automate, delegate, or buy as a service? Only what survives that pass is headcount. The floor is Leach's verification labor.
- **Match the capital structure to the archetype before raising.** An asset-light company that takes venture money inherits the hypergrowth obligation that made the fixed-cost playbook necessary in the first place. Harris's binding-constraint test is the gate.
- **Vertical software must be more than templates on commodity infra.** If the authors' deflationary definition describes your product, a hyperscaler can generate it. The durable parts are the relationship, the brand, and the hard-won knowledge of the vertical's stack; see [[competitive-moats]] on which of those are real moats.
- **The under-served market is deployment, not models.** Public-sector and mid-market organizations frustrated with their software need someone to walk them into the deployment period. The authors frame that as a services opportunity; the barbell and low-margin-winners theses frame it as where the value actually accrues.

## Sources

- Manidis, Will and Kennedy, John (2024; reposted 2026). "Asset Light Software." Originally published January 16, 2024; reposted to X October 5, 2026 with a coda on Lafayette Standard Co. <https://x.com/WillManidis/status/2107139199463780637> — [[2026-10-05-asset-light-software|local copy]]
