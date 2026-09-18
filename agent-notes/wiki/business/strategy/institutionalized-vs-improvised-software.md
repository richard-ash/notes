---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-09-03-evans-ai-tools-and-transformation.md
compiled_at: 2026-09-17
model: claude-fable-5-1
confidence: medium
---

# Institutionalized vs. improvised software

Benedict Evans's September 2026 essay "AI, tools and transformation" rebuts the Silicon Valley intuition that AI turns everyone into a tool-builder — that once anyone can ask a model to make (or simply *do*) the software they need, apps as a category are dead. Evans argues this misreads three things: how most people think about their work, where software actually comes from, and how companies actually change. The durable framework he offers instead is a **spectrum from institutionalized to improvised software**, along which AI moves the thresholds without changing the underlying question.

This article is compiled from a single opinionated essay; the claims below are Evans's unless marked otherwise.

## The setup: hundreds of apps and still full of drudgery

The typical big American company runs hundreds or thousands of pieces of software: "big iron" horizontal systems of record (SAP, Workday), hundreds of vertical SaaS apps, and hundreds more scripts, automations and databases, "right down to the 10 meg spreadsheet running a department." It often doesn't know what it has, what's used, or what it pays for. And it remains full of boring, repetitive tasks.

The tempting inference: the old joke says an engineer spends an hour building a tool to automate a ten-minute task. With AI the tool takes five minutes, needs no engineer and no code, and the model can skip the tool and just do the task. Software becomes dynamic, generative and spontaneous; massively more tasks get automated with massively less software. Evans concedes this is intoxicating if you are a tool-builder — and everyone in Silicon Valley is — but says it fails on three counts.

## Why "everyone becomes a builder" fails

**1. Most people are not tool-builders.** A great matrimonial lawyer spends the day thinking about cases and clients, not about what great discovery software would do; a great enterprise salesperson thinks about product, clients and competitors, not sales-enablement tooling. Excel tries to bridge this with templates and onboarding (everything in File/New is a suggestion), but Evans notes that every one of those templates still became a company — and he reads "Claude for X" the same way: helpful, not the answer. The task to be automated sits in plain sight and the person who has it doesn't see it. That gap is what the *forward-deployed engineer* exists to close: a builder who knows what AI can do walks around a law firm or an architecture practice and sees the opportunities lying on the table. (Evans compares it to every tech person's teenage internship: "um, daddy, did you realise you could just do it like this?")

**2. Even builders can't see most of it.** The deeper problem is that most of what got automated over the last few decades wasn't obvious even to tool-builders, and didn't have an obvious solution. The common first reaction to things we now use daily was "why would I want that?" The problem is often bundled or hidden inside something else; even when visible, fixing it usually means redefining or unbundling it, and most successful software companies were preceded by half a dozen failed attempts at the same problem. None of this is solved by making code cheaper to write: "The hard part is knowing that you need a tool for this in the first place, and then knowing what the tool should do."

**3. Adoption is an organizational decision, not a personal one.** Many automatable workflows touch 50 or 500 people across five departments, three systems of record and four regulatory regimes. An individual with a better idea for accounts payable can't change how everyone does it. "That has to be a purchase, and a decision, and an 18-month sales process."

## The spectrum: institutionalized to improvised

Evans's central frame is that software is bought, chosen or created along a spectrum from **top-down to bottom-up** — the company buys SAP; the user makes a spreadsheet — which is equally a spectrum from **institutionalized to improvised**.

- **Institutionalized** tasks live in dedicated tools (SAP, Carta, Rippling). Many people at the vendor and the customer have worked out the correct way to do the task, and it matters that everyone does it the same way with the same tools.
- **Improvised** tasks are the edge cases, exceptions and one-off questions those tools can't handle. Users solve them bottom-up in a fuzzy space of freeform substrates: Excel, email, shared folders, Tableau, PowerPoint, CSVs, screenshots, PDFs and conference calls.

The flow between the two is what generates the hundreds of apps. Once an improvised task is done all the time, the same way, by lots of people, with revenue and risk attached, the company has to institutionalize it — it needs audit, security, maintenance and accountability. In Evans's image, you pave the [desire path](https://en.wikipedia.org/wiki/Desire_path) and pay someone to set it in stone. But you may not realize the path is there (hundreds of people losing an hour a day), and working out the right way to pave it is hard.

This is a continuous, organic cycle of bundling and unbundling. Every SaaS app does something you *could* do in SAP, Excel or email — "Carta is a $4bn company that manages one spreadsheet for your CFO" — and tasks move in both directions. Evans quotes a consultant whose jobs were half telling Excel users to move to a database and half the reverse. The SaaS shift was the previous order-of-magnitude increase in how much software companies had, with a new operating model and cycle time, and it killed incumbents who couldn't make the jump — the real rationale, he says, for the "SaaSpocalypse."

The threshold depends on scale. PwC hiring 3–4,000 graduates a year uses institutionalized software; a firm hiring five uses email, a shared folder and Google Sheets; as it grows it moves to Notion or an SME HCM. Meanwhile a small team inside PwC tracks candidates in Google Sheets because Workday is too inflexible — and the unbundling starts again.

## Where AI lands on the spectrum

AI rolls across all of it: existing apps expand, many new vertical apps appear, and the freeform substrates (Excel, Sheets, Tableau, email) gain new capabilities. The chatbot itself is a **new freeform space sitting next to Excel and email**, taking tasks from them and from apps, and also losing tasks to apps.

The small firm hiring ten graduates might now stay in Google Sheets longer because AI makes it more scalable, or use Sheets as a data store for Gemini, or ask whether to have Claude build something or move to Notion — and then discover a new SaaS app aimed at exactly that plus a problem it hadn't thought of. Evans's summary: "AI doesn't change the question: it creates new choices and moves the thresholds."

## "Give everyone Copilot" is 1983 and 1997 again

Evans reads the last three years of enterprise AI deployment through this lens. Every big company gave everyone Copilot (or ChatGPT or Claude); a small group uses it heavily (some with real productivity gains), a larger group a couple of times a week, and most of the company barely at all. That is partly training and change management, but mostly the same problem as giving everyone a PC and Lotus 1-2-3 in 1983 or a browser in 1997: *how does this map to the tasks people actually have this week?* Giving everyone Lotus wasn't how you transformed invoice processing; giving everyone a browser wasn't how you rebuilt supply-chain management or ran e-commerce.

The conventional next step is pilots — trials of bought and built products that automate previously unautomatable processes. Roughly half work, which Evans says is normal: that's why they're pilots. But this is an old-fashioned CIO conversation (use cases, lighthouses, heroes, quick wins), and the CEO and board see the mismatch: hundreds of workflows, five or ten pilots — "that doesn't seem to scale?" Giving everyone ChatGPT scales in theory, except most people aren't finding ways to use it.

## Three questions every transformative technology forces

Yes, you should give everyone the tool, and yes, KPMG can tell you about training and change management. But Evans argues that isn't how a company thinks about transforming itself around a generational technology. Each one forces three kinds of question:

1. **How do we buy, build and deploy this?** Pilots? The bundled product from Microsoft/Google/Oracle, build in-house, pay someone to build, or buy from a startup?
2. **How far does this change our operations?** What does email mean for us? What do spreadsheets mean for us? The answer differs radically between an insurance company and a law firm.
3. **Does this change our economics?** New competitive pressure, or an existential threat?

None of these are answered by "Claude for X." Evans notes the irony that all three generate new demand for professional services — the business models AI most obviously threatens. Deploying an LLM voice-analytics tool in a call center? Call Accenture. Startup wanting fast enterprise go-to-market? Call the Big Four. The big labs now run their own "deploycos"; Evans's joke is that if a "machine learning scientist" was a statistician who lives in San Francisco, a "forward deployed engineer" is anyone OpenAI hired from a systems integrator. Frustrated selling AI into law firms? Start an "AI-enabled" law firm and find out whether that is real leverage or the equivalent of a "PC-enabled law firm" in the 1980s. And a board weighing existential threat against revenue opportunity will call Bain, BCG, McKinsey or an M&A banker — that is what they do.

## First old work faster, then new things

Evans closes with the simpler version: every new technology is first used to do the existing work more and faster, and only later to make entirely new things. AI will automate broad classes of work inside existing workflows and companies — with far more trouble than "give everybody a model" — but in every previous platform shift the stuff that mattered was what wasn't possible before and no one imagined.

## Synthesis and connections

**A defence of vertical software that doesn't rest on cost.** [[minimum-viable-saleable-software]] (Leach) argues SaaS survives because LLMs made building cheap but not free — verification and maintenance labour remain. Evans's argument is stronger and independent of build cost: even at zero cost, the buyer still has to notice the desire path, define the tool, and get 500 people across five departments to adopt it. Cheap code moves where the bundling/unbundling threshold sits; it doesn't remove the reasons the threshold exists (audit, accountability, everyone doing it the same way).

**Same diagnosis as the "Copilot trap," different prescription.** Bret Taylor's [[ai-and-org-design]] makes the same observation — companies hand out Copilot and declare themselves "AI now" — and prescribes process owners with KPIs and end-to-end automation per process. Evans's framing explains why that prescription is hard: the process crosses systems of record and regulatory regimes, so it is a purchase decision with an 18-month sales cycle, not something an owner can will into existence. Taylor says *what* to do; Evans says *why* companies default to pilots instead.

**"Infrastructure, not tools" answers "most people are not tool-builders."** [[low-margin-ai-winners]] argues enterprise AI sold as a tool assumes a behaviour change that fails in change-resistant workforces, so agents should be embedded in the systems where work already happens. That is precisely the response to Evans's first objection: if the lawyer will never look at their day as a tooling problem, the automation has to arrive without asking them to.

**Expertise and the builder's eye are held by different people.** [[expertise-as-llm-leverage]] argues the scarce input to LLM use is domain expertise. Evans's forward-deployed-engineer point is the mirror image: the domain expert has the expertise but not the builder's instinct to see their work as automatable; the builder has the instinct but not the domain. Both imply the value is in the pairing — which is what an FDE engagement, or a domain-expert founder who can also build, actually is.

**The pilot data and the deployment pillar.** [[ai-eats-the-world]] carries Evans's own numbers on the pilot-to-production gap (development/pilot rates of 60–70% across functions, production a fraction of that) and his absorb → innovate → disrupt progression, which this essay's closing section restates. It also has the earlier version of the FDE joke and the structural reason labs hire consultants: enterprises keep no idle capacity for reimagining their workflows. [[commodity-trap]] (Narayanan & Kapur) describes the same lab behaviour from the value-capture side — climbing the stack into bespoke FDE deployment is how labs escape commodity inference.

**The internal-deployment case studies are FDE work inside tech firms.** [[company-wide-agent]] (Sierra) and [[enterprise-agentic-coding-adoption]] (Airbnb) are what "a builder walks around the company and sees the desire paths" looks like when the company is itself full of builders. Evans's argument predicts the pattern those reports show — engineering adopts first, everyone else needs a dedicated team to find and pave their paths — and implies the same playbook is far harder in a bank or a law firm.

**The organizational-behaviour view.** [[ai-mania]] (Ludic) is the practitioner's field report of the CEO/board headscratch Evans describes: leaders with no plan beyond pilots and heads-down survival. Evans's three questions are a more charitable framing of the same paralysis — the questions are genuinely hard, and the answers differ by industry.

**Implications.** (i) The "AI kills SaaS" bear case is weakest exactly where software is most institutionalized: audit, accountability and everyone-doing-it-the-same-way are organizational needs, not code-generation problems. (ii) The most exposed layer is the improvised middle — Sheets-plus-Gemini and chatbots will absorb the one-off and edge-case work that previously justified lightweight tools, and will delay the point at which a growing firm buys its first HCM. (iii) For a founder, Evans's FDE observation is a sourcing strategy — the durable opportunities are desire paths in non-tech firms that the people walking them can't see — but his second objection is the warning: seeing the path is not the same as knowing how to pave it, and most first attempts get the problem definition wrong.

## Sources
- Benedict Evans (2026). "AI, tools and transformation." <https://www.ben-evans.com/benedictevans/2026/9/3/ai-tools-and-transformation> — [[2026-09-03-evans-ai-tools-and-transformation|local copy]]
