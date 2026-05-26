---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-05-21-evans-ai-eats-the-world-spring.md
compiled_at: 2026-05-26
model: claude-opus-4-7
confidence: medium
---

# AI eats the world

Benedict Evans's recurring state-of-AI presentation, structured around three pillars: **Capital, Deployment, Change**. This article tracks his macro thesis on the generative AI platform shift — the capex bubble, the slow grind of enterprise deployment, and the open question of who captures the value.

Evans's framing builds on his prior thesis that generative AI is the next "Imagenet moment" ([[generative-ai-as-pattern-generation]]). The Spring 2026 version of the deck argues that the most likely equilibrium is **commodity models at the bottom of the stack with innovation and value capture moving up to applications** — by close analogy to how the mobile networks became a trillion-dollar utility while the value flowed to Apple, Google, and the app economy on top of them.

## Pillar 1: Capital

### A platform shift always resets the industry

Evans's frame: every 10–15 years (Mainframes → PCs → Web → Smartphones → Generative AI) a platform shift triggers three movements at once — innovation switches over, new gatekeepers emerge inside tech, and outsiders have to decide whether this is a tool, a revenue line, or an existential threat. The canonical evidence is Microsoft's collapse from ~95% of global computer unit sales in the late 1990s to a small minority once smartphones reset the platform.

### The capex explosion

The big four hyperscalers (Meta, AWS, Alphabet, Microsoft) have committed to **$700bn of capex in 2026**. For scale, that exceeds global Telecoms (~$300bn) and approaches the entire Oil & Gas industry (~$1tr). Evans pairs this with the executive justification — Pichai: *"The risk of under-investing is significantly greater than the risk of over-investing"*; Zuckerberg: *"The very worst case would be that we have just pre-built for a couple of years."*

Capex/sales ratios have climbed accordingly: Meta now spends >50% of revenue on capex, Microsoft ~40%, Alphabet ~30%, Amazon ~20%. These businesses were once asset-light and self-funding; they are no longer. "Here comes the structure" — companies are scrambling to manage the balance sheet, and OpenAI's reported deals to build 30GW+ of capacity at $1.4tr (or 1GW/week of new construction at $20bn/GW = ~$1tr annually) involve "Other People's Balance Sheets, circular revenue and a lot of plate-spinning."

### Supply-side bottlenecks

The capex doesn't translate cleanly into compute. Evans lists three converging constraints:
1. **GPUs and memory** — Nvidia's quarterly revenue has gone from <$5bn in 2020 to >$60bn in 2026, and they still can't get TSMC to expand capacity fast enough.
2. **Multi-year power backlog** — except in China.
3. **Community / political backlash** — data centre siting fights.

> "It's been almost impossible to build capacity fast enough since ChatGPT launched." — Kevin Scott, Microsoft CTO

US data centre construction (excluding the compute itself) has now overtaken office construction. Monthly global semiconductor billings have broken out of their 35-year band of $25–50bn to over $125bn by March 2026. Whether this is a permanent regime shift or yet another semiconductor cycle is the open question.

### The mobile-networks analogy and the commodity thesis

This is the load-bearing analogy of the deck. Mobile networks faced the same demand-supply imbalance circa 2010 and moved through it to an equilibrium of flat-rate capped bundles + Wi-Fi/edge offload. Bits = tokens, marginal cost ≈ 0, capacity is finite. The supply/demand imbalance today lets labs price at ROI, but **long-term pricing power is unlikely**.

The deeper claim: *commodity infra rarely captures value up the stack*. Global mobile data traffic grew ~8x from 2010 to 2025 (250 → 2,000 EB), but the MSCI global telco stock index was flat over the same period. Telcos built the substrate; Apple, Google, and the entire app economy captured the value.

Evans argues frontier LLMs are heading the same way. The benchmark scores of OpenAI, Anthropic, Google, Meta, and the Chinese labs cluster tightly in the 55–70 range by 2026, and switching providers is a configuration change. **No network effects.** This is the same conclusion Garicano and Saa-Requejo reach via industrial-organization analysis in [[ai-value-capture]] (output-market competition + upstream concentration + intelligence-not-the-bottleneck) — Evans gets there from the historical analogy of platform shifts and capital-light vs capital-intensive business structures.

Quote that contradicts the thesis, and that Evans presents to mark the disagreement:

> "We see a future where intelligence is a utility like electricity or water and people buy it from us on a meter." — Sam Altman

Evans's response is essentially: yes, and the utilities are not where the trillion-dollar businesses live.

### Provisional thesis on the model layer

Evans offers five "right questions, possibly wrong answers":

1. **Chat is a terrible UX.**
2. **General use needs 'apps'.**
3. **Labs can't build (or generate) all the apps.**
4. **Models are commodities and have no network effects.**
5. **Models will just be infra; innovation will move up the stack.**

If correct, this means the capex war doesn't determine the value-capture war. Software (capital-light, network effects, monopolies, high margin) and LLMs (capital-intensive, no network effects, commodity, low margin) end up in different boxes on the same diagram.

## Pillar 2: Deployment

### Mile wide, inch deep

ChatGPT has ~900m weekly active users, **but only 5% are paying**. Consumer use is currently "a mile wide and an inch deep": even the top 5% of users sent only 4,000–5,000 prompts in 2025; the top 20% sent <1,000 — less than three per day. For 80%+ of users, ChatGPT is not yet a daily essential.

Daily-use rates are higher in younger cohorts (Gallup, March 2026: ~30% daily use among 14–29-year-olds in the US) but the gap between "tried it last week" and "depend on it daily" is the deployment problem.

### Enterprise — same pattern, slower

US workplace AI use grew rapidly from June 2023 to December 2025, but with a sharp split: Tech, Finance, and Professional services lead; Healthcare, Retail, Manufacturing, and Government lag. Across functions (Bain, Q4 2023 → Q3 2025), **Development/Pilot rates have hit 60–70% across most business functions, but Production rates remain a fraction of that.** Everyone has a pilot. Few have a production system.

> "Imagine you were an accountant seeing the first software spreadsheets. Now imagine you were a lawyer: 'very cool, but…'"

### How new technologies deploy

Evans's three-step progression for new general-purpose technologies:
1. **Absorb** — do the old things better with the new tech.
2. **Innovate** — do things only possible with the new tech.
3. **Disrupt** — redefine the question.

Step 1 dominates the early years. The Atlanta Fed CFO survey (December 2025) shows the easy-to-deploy, hard-to-measure gains (productivity, better insights, better customer service) are running ahead of the hard-to-deploy, easy-to-measure ones (cost-saving, new revenue).

### What's working first

Annualised enterprise AI spending (a16z, March 2026) ranks coding ~$4bn first, then legal, support, medical & health admin, search, text, real estate, finance. The functional pattern: **Analytics & productivity | Marketing | Customer support | Back-office processes | Coding** — anywhere with bounded outputs and existing measurement infrastructure.

Coding is the standout case. Zuckerberg: *"We're seeing more and more examples where one or two people are building something in a week that would have previously taken dozens of people months."* This connects to [[agentic-engineering]] (the discipline emerging around AI-assisted coding) and [[ai-coding-harnesses]] (the tool-call loop that makes it work).

But Evans cautions: **writing code isn't the hard part**. The hard part is knowing what the code should be doing and where it fits into the market. Enterprises run hundreds of horizontal systems of record (ERP, CRM, HCM), improvised workflows (Email, Excel, shared folders), and vertical apps. Cheap code production rearranges what gets bundled and unbundled, but it doesn't tell you the answer.

> "For half of my jobs I tell clients who use Excel to switch to a database, and the other half are the other way around." — Anon

### The deployment infrastructure

The systems integrators are eating well. Accenture's reported new quarterly generative AI contracts climbed from near zero in Feb 2023 to ~$2,500m by Aug 2025. Automation takes a lot of manual labour: PE roll-ups and GTM partnerships with outsourcers and strategy consultants are the actual delivery vehicle. The startup wave (Y Combinator batches are now majority-AI) exists to unbundle Google, Excel, email, Oracle… and ChatGPT itself.

## Pillar 3: Change

> "It's tough to make predictions, especially about the future." — Yogi Berra
> Imagine asking "What will be changed by the internet?" in 1997.

### The automation envelope

The new general-purpose technology adds **probabilistic systems on top of deterministic systems**.

- **Old**: anything we can describe in logical steps can be automated.
- **New**: anything with enough training data, or anything where verification is scalable.

Evans's four questions for any industry:
1. Is this just price elasticity & consumer surplus?
2. Which tasks become free? What does that enable?
3. Was that cost base your moat?
4. What was impossible that's now cheap?

### Job vs task

Sometimes automation collapses a job into a button. Otis's 1950 "Autotronic" automatic elevator eliminated ~100,000 elevator-attendant jobs in the US within three decades. The whole job *was* the task.

More often the job changes. Accountants and auditors grew from <0.5% of US employment in 1910 to ~1.2% by 2000 *despite* mechanical adding machines, then computers, then spreadsheets. CPA hiring rose 10x from 1970 to 2020. The task got cheaper; the job expanded.

And sometimes the task becoming free unlocks something new. Grocery barcodes (1974) didn't just make checkout faster — they made automated inventory management possible, which let stores stock 5x more SKUs (~10,000 → 50,000+). The interesting change isn't the task; it's what the task being free unlocks.

### Was the cost base your moat?

The killer question, and Evans's strategic frame. Many industries (music: CDs; news: printing; telecoms: cables; retail: stores) were protected by physical-cost moats that incidentally also enabled the value-creation job. The internet removed those moats. Now: which industries were protected by a *cognitive* cost base that AI can automate to zero?

> "Anything 'boring' will now be automated. What industries need boring work? What can you split apart?"

This connects directly to [[task-automation-vs-paradigm-replacement]] — the Roodman/Bessen framing that the productivity gains from automation are bounded inside existing paradigms, and the larger effects come from what the cheap input enables.

### Infinite interns

> "AI gives you infinite interns."

Evans's leverage prompt: what if you had a million interns? Or one intern who was a million times faster?

The shift from "listen to every call and tell me if the customer sounds strange" (the old, sampling-based intern job) to "listen to a million calls every day — what do you notice?" (the impossible-now-cheap variant) is where new questions live. The change from the previous platform isn't "do more of what we did" — it's "ask things you couldn't ask before."

> "Show me the data Bob's talking about on this call."
> "What were the top concerns on customer calls in the last six months?"
> "What pricing changes would improve our churn?"

### First-principles content understanding

Zuckerberg's framing of what Meta gets from a frontier model:

> "Instead of just looking at statistical patterns of what types of people engage with what content, we're going to be able to develop a 1st-principles understanding of what you care about and what each piece of content is about."

Evans's wry version: Amazon, Google, and Meta don't know what the products in their catalogues *are*, or why people buy them. Now they might. What does recommendation look like when it goes from correlation to comprehension?

### Reality check

It's still early. Bain (September 2025) found that "Always search" still dominates US consumer search preference across all age cohorts; "Always GenAI" is a minority even among under-30s. Generative search is currently additive, not substitutive.

This matches the broader pattern in [[ai-and-the-future-of-work]]: rapid headline metrics, slow real-world replacement.

## Welcome to the beginning

### "This is totally different" — but it always is

Evans's closing move is to put the current moment in historical perspective. The combined private market values of OpenAI + Anthropic are comparable in 2026 dollars to the market cap at IPO of all US venture-backed companies from 1995–2000. The capital intensity is unprecedented, the valuations are unprecedented, and — by Evans's read — that is itself a recurring feature, not a unique one.

The dot-com graveyard is full of company names that looked like the future: AOL, Yahoo, Pointcast, Flash, VRML. The mobile-internet graveyard is full of i-mode, J2ME, WAP, JOYN, DVB-H. The generative-AI shortlist of unknowns: browsers? MCP? voice? app stores? wearables? GEO?

> All AI questions have one of two answers: "No-one knows" or "What happened the last time that everything changed?"

The Goldman frame ("nobody knows anything") and the historical-rhyme frame are Evans's two recommended postures. The substitution-versus-coexistence empirical record is mixed: Uber displaced NYC taxis decisively after 2015; Airbnb grew but didn't displace US hotels. *"Sometimes software eats the world, and sometimes it only nibbles."*

### The Philippines question

The 8%-of-GDP, 2m-employee Philippine IT-BPM industry sits at the sharp end of the job-or-task question. It's built on skill/income arbitrage for processes that AI can now do. Whether it's a job (durable, expanding into new work) or a task (a button waiting to be pressed) is the empirical test that will play out over the next few years.

### Inventing new questions

> "What if I don't have to buy a CD?" versus "what if I can get all the music there is?"

The first question gave you Napster. The second gave you Spotify, and total global recorded music revenue eventually exceeded the CD-era peak in 2025 dollars. The framing of the question determined which industry survived. Evans's strategic instruction is to **presume radical uncertainty** and ask the second-order questions:

- What can you and your competitors do with this?
- Can this unlock or break something crucial in your business model?

## Temporal notes

This is the Spring 2026 edition of an annually-updated deck. The frame (three pillars, Capital/Deployment/Change) has been stable since 2023; the data and specific claims update with each release. Future editions can integrate into this article.

## Sources

- Benedict Evans (May 2026). "AI eats the world (Spring 2026)." <https://static1.squarespace.com/static/50363cf324ac8e905e7df861/t/6a0f426de2690d76bb0707a6/1779384941828/2026-Spring-AI.pdf> — [[2026-05-21-evans-ai-eats-the-world-spring|local copy]]
