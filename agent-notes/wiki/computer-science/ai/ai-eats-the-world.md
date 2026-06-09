---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-05-21-evans-ai-eats-the-world-spring.md
  - agent-notes/raw/computer-science/ai/2026-05-31-evans-lenny-podcast-ai-rational-take.md
compiled_at: 2026-06-09
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

### Distribution as the moat when the product is a commodity

Elaborated on Lenny's Podcast (May 2026): if the field is basically commodity, **distribution and brand become the moat**. The structural analogy Evans reaches for is web browsers. The browser product is a thin wrapper around a rendering engine — input box, output box, and what else? The last innovation in browser design was tab browsing 20–25 years ago. Every now and then somebody tries to innovate in browser design and it never works because it's the platonic ideal, like trying to innovate in smartphone design (it's a glass rectangle). Microsoft used distribution to break in. *Then* it turned out winning browsers didn't matter anyway because the value was further up the stack.

The current map of who's pressing this lever:

- **Google** is using Search, Chrome, Android, and Workspace defaults to drive Gemini. To a normal person there's no perceived difference between Gemini and ChatGPT.
- **Meta** quietly sprayed an adequate-but-not-leading assistant across every surface (WhatsApp, Instagram, Messenger). Tech wrote it off; survey data put it up there with ChatGPT and Gemini in actual use.
- **OpenAI** late-2024 strategy was nicknamed "everything yesterday" — trying every wedge to build a flywheel before the distribution incumbents got there first.
- **Apple** is the last penny to drop. The whole second half of WWDC 2024 was the Apple Intelligence vision: tool-using, agentic, on-device, with no prompt injection or hallucinations, and a standardized intents API across 10,000 apps. Apple couldn't ship it — but neither did anyone else. Evans's open question: at WWDC 2025, do they ship that vision now powered by Gemini? In that world the model is the dumb commodity underneath; the feature, distribution, and on-device billion-installed-base advantage live above it.

This is the practical mechanism by which Evans's commodity-models thesis cashes out into a market structure: the labs without a distribution channel get squeezed.

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

### Why the frontier labs are themselves staffing consultants

In the May 2026 Lenny's Podcast interview Evans turned the "AI replaces consultants" naive prediction inside out. The cutting-edge labs (OpenAI, Anthropic, plus PE players) are the ones most aggressively hiring forward-deployed engineers and acquiring consultancies. His framing joke:

> "A forward deployed engineer is like an Accenture outsourced software developer who lives in San Francisco."

The mechanism is structural: companies do not have spare capacity sitting around to "completely reimagine all of the internal workflows of your company and work out which of them could be automated really quickly with AI." That is a project, and projects need five-to-ten people for one-to-two months just to scope before any building starts. Enterprises do not keep idle architects, idle ad agencies, or idle integrators on staff — they hire Bain/BCG/McKinsey for analysis, Accenture/Infosys for delivery, branding agencies for brand work. Forward-deployed engineers are the AI-lab-flavoured wrapper for that same demand.

The deeper point, which feeds Pillar 3's job-vs-task distinction: the slide deck is just the task. What you pay Bain for is to walk all over your enterprise, work out the politics of *why* you didn't already do the thing, talk to your customers about what they actually think rather than what's on the first page of Google. Claude can write the PowerPoint badly; that's not what the engagement was. Same in software: Claude Code can write the code, but who is the customer, what are the right features, how do you take it to market.

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

### The shifting AGI definition

Evans observes (May 2026 podcast) that the term AGI is doing what the term "AI" has always done — quietly receding to mean *whatever just stopped working as software*. He cites Larry Tesler:

> "AI is whatever machines can't do yet. Because once machines can do it, people say 'well, that's just software.'"

So jet airliners in the 1960s were "technology"; now they're not "tech." Machine-learning sentiment analysis was once AI; now people will say "oh, that's just sentiment analysis." Today AGI is being redefined to mean "can do a certain percentage of economically valuable work" — but an IBM mainframe in 1975 already could. The current debates about whether super-intelligence is more than AGI or less than AGI ("last year I thought super intelligence was really good but not as good as actual AGI, and now it's like oh no we've already got AGI but super-intelligence is really hard") rhyme with old arguments about whether crypto is blockchain or blockchain is crypto — there is no right answer because the terms are not referring to anything stable.

Evans's serious point: **you don't have to believe in AGI to believe this is a giant deal.** Even if the models stopped getting better tomorrow and you hit a brick wall, what already works gets rolled out over the next 10 years. The AGI question is a Rorschach test for vibes-forecasting. The deployment question is a real economic question with a real answer.

## The anti-AI backlash

Added from the May 2026 podcast. Evans's frame: the backlash is "a big fuzzy mess of different stuff," some real and some not, mirroring the structure of the earlier backlash against social media but compressed in time. Sorting it:

**The water claim is mostly fake.** Data centres use water for cooling, but it's mostly closed loop. Livermore Lab's end-2024 study put US data-centre water consumption at ~0.017% of US water consumption. The actual problem when it bites is small-town planning (one well, capped and routed to the data centre) — not a data-centre problem.

**Energy is real but bounded.** Data centres are ~5% of US energy and might grow ~1 percentage point per year for the next five years.

**Jobs data is genuinely inconclusive.** There's a slowdown in employment for 18-to-24-year-olds, but it shows up similarly across degree/no-degree and across AI-exposed/non-exposed fields. The model labs publish no daily-active-user data ("we don't have a daily active user number for ChatGPT — this is crazy"), so the empirical work has to back numbers out of BLS surveys and consultancy panels. Politically, this doesn't matter: if you're a student and you can't get a job, the cause attribution is academic.

**Creative-industry culture wars are real and local.** Cover artists for YA romance novels, novelists, podcasters (where 30–40% of new shows are now AI-generated) all have legitimate grievances about substitutability of specific outputs they used to be paid for.

**The "Facebook sells your data" pattern.** As with the social backlash, some claims are objectively false but the people who believe them are absolutely adamant. Jonathan Swift: "You can't reason somebody out of an idea they didn't reason themselves into."

### Every tech wave creates new ways to ruin people's lives

Evans grounds this with the UK Post Office / Horizon scandal. The Post Office rolled out a Fujitsu-built point-of-sale computer system 15 years ago that had bugs producing apparent cash shortfalls. The Post Office concluded its franchisees (often second-generation Indian immigrant pharmacists who ran the back-counter post office) were stealing. Hundreds went to prison; there were suicides and bankruptcies; meanwhile Post Office and Fujitsu staff testified in court that there were no bugs in the system. This is 1970s technology.

His point: every wave of technology comes with novel ways to ruin people's lives, either deliberately (Chinese mass surveillance) or by accident (Horizon). The deep-fake-nudes problem isn't refuted by "haven't you heard of Photoshop?" — a 15-year-old kid couldn't use Photoshop to make hardcore pornographic nudes of every girl in their high school and send them to the whole school in an afternoon, and now they can. The 1990s line about social media — "you can be the only gay kid in your village and find your tribe" — turned out to also mean you can be the only Nazi or pedophile in your village and find yours. AI will produce more of this. You have to be conscious of it and also kind of not panic about it.

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

### "It'll probably be okay" — but you have to dive in

Evans's closing prescription in the podcast is unfashionably calm. Yes, this will change things and there will be friction and dislocation. That's the constant — the last 200 years have run this loop on the back of mechanisation, electrification, telephony, computing, the web, and mobile. The jobs that go away in retrospect are mostly crap jobs; the new jobs are better. GDP keeps going up. The 1800 peasant did not know what a railway engineer was.

The only actionable answer to "what should I do?" is:

> "Don't stick your head in the sand and say I hate all of this stuff. That gives you a great feeling of moral superiority and you can go on Blue Sky and shout at everybody about how evil AI is. Great, I'm happy for you, but that's not going to help. What helps is you diving into this completely, submerging yourself in it, and coming out understanding what you can do with it, how this changes things, how you can be a great hire."

If a law firm is hiring 50 associates this year instead of 100, walking into the interview and saying "I think AI is bad and I'm never going to use it" is not the right mood. There is no career strategy that routes around the question. Evans's career rule for his own teenage son: you have a bunch of skills, there are jobs those skills make you good at, and there are jobs people will pay you for — try to get at least two of those to overlap, preferably all three.

The personal motto he offered for the lightning round, with characteristic British understatement: **"It'll probably be okay."**

## Temporal notes

This article integrates two complementary 2026 sources: the Spring 2026 deck (May 21) and the May 31 Lenny's Podcast interview with Evans. The deck is the canonical reference; the podcast is the spoken-word elaboration with extra material on distribution as the moat, the FDE-as-Accenture observation, the AGI-definition drift, and the anti-AI backlash analysis.

The frame (three pillars, Capital/Deployment/Change) has been stable since 2023; the data and specific claims update with each release. Future editions can integrate into this article.

## Sources

- Benedict Evans (May 2026). "AI eats the world (Spring 2026)." <https://static1.squarespace.com/static/50363cf324ac8e905e7df861/t/6a0f426de2690d76bb0707a6/1779384941828/2026-Spring-AI.pdf> — [[2026-05-21-evans-ai-eats-the-world-spring|local copy]]
- Benedict Evans & Lenny Rachitsky (May 31, 2026). "The most rational take on AI you'll hear this year." Lenny's Podcast. <https://www.youtube.com/watch?v=BD3vLtWhT5A> — [[2026-05-31-evans-lenny-podcast-ai-rational-take|local copy]]
