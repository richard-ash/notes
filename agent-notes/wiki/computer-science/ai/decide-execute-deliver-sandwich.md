---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-06-10-why-ai-hasnt-replaced-software-engineers.md
compiled_at: 2026-06-12
model: claude-opus-4-8[1m]
confidence: medium
---

# The decide-execute-deliver sandwich

Arvind Narayanan's argument (first essay in a *Normal Tech* series, June 2026) for why AI has not caused — and will not cause — mass layoffs of software engineers, even though software is the profession where AI capabilities are furthest along and adoption fastest. The load-bearing model: knowledge work is a **decide-execute-deliver sandwich**, and AI compresses only the middle layer. The two outer layers resist automation for reasons that are *not* about capability and so won't be overcome by better models.

This is the empirically-grounded, software-specific counterpart to [[ai-and-the-future-of-work]] (Andreessen's broad macro optimism) — and it converges on the same career conclusion from a different direction: the durable human value is judgment and accountability, not execution.

## The sandwich model

Software engineering work has three conceptual layers (not temporal phases — engineers switch among them constantly):

1. **Decide** — problem framing, requirements specification, planning. Deciding *what* to build.
2. **Execute** — design and implementation. Writing the code. *This is the layer AI compresses.*
3. **Deliver** — testing, verification, integration, maintenance, and being *accountable* for what ships.

Underpinning all three is **deep understanding** of the codebase, the business, and the environment — a prerequisite, not a fourth layer.

The central claim: **AI has nearly fully compressed Execute but left Decide and Deliver largely untouched.** So even a hypothetical future where the execution layer becomes instant and perfect is only a small change from today's status quo. The reasons the outer layers resist AI are structural, not capability-limited:

- **Decide resists automation** because specifying correct behavior requires reasoning about user needs, market signals, organizational priorities, and regulatory constraints. As AI absorbs more decisions, the layer doesn't get *thinner* — once a decision is delegable to AI it stops being a competitive advantage, and the value of human decision-making **migrates upward**. Software complexity keeps growing, so there's no ceiling to this escalator.
- **Deliver resists automation** because someone has to be accountable. Today's AI is too unreliable to ship mission-critical code unsupervised. And even if the technical barrier disappeared, society can *choose* to keep humans accountable via norms, law, and liability — a more resilient safety lever than slowing capability development (the core thesis of Narayanan & Kapoor's *AI as Normal Technology*).

The engineer's future role becomes analogous to a **crane operator**: AI does the cognitive heavy lifting, the human supervises and keeps it under control. Notably, this supervision is *not* cheap — see the exhaustion paradox below.

This pattern generalizes to most knowledge work (radiology, legal, etc.) since complex decision-making and accountability are universal; software is just furthest along.

### Empirical support

- **"Writing Code vs. Shipping Code"** (NBER, 100,000 GitHub developers): AI agents produced an **8× increase in lines of code written** but only **30% more releases**. Execute is compressed almost completely; the Decide/Deliver bottlenecks hold throughput nearly flat. (In a mobile-app sub-study, usage of the resulting apps didn't rise at all — consumer software competes for a fixed pool of attention, unlike enterprise software where there's room to software-mediate previously-manual processes.)
- **Writing code was never the bottleneck.** A 2019 Microsoft study of 6,000 developers found coding is only 9–61% of dev time depending on the study. A wave of late-2025 practitioner blog posts independently rediscovered this once agents made the execute layer cheap: automating code-writing barely moved overall productivity.

## AI washing: the layoff stories don't survive scrutiny

Narayanan's empirical core is that the headline "AI replaced engineers" layoff stories are **AI washing** — financial restructuring rebranded as AI for better optics. In *every* story examined, the same narrative violation appeared:

- **Block** (Feb 2026, 4,000 cut): Dorsey cited AI "enabling smaller, flatter teams." Reality: post-pandemic 3× overhiring and financial pressure. A Cash App data scientist reported "very limited gains in productivity" and that AI was "shoved down everyone's throats."
- **Snap** (Apr 2026, ~1,000 cut): Spiegel cited AI (and "65% of code is AI-generated"). Reality: an activist-investor cost-cutting campaign; Snap had posted a net loss every year since its 2017 IPO. The cuts (e.g. 150 across the AR division) didn't match the across-the-board pattern AI displacement would predict.
- **Intuit** (May 2026, 3,000 cut): press framed it as AI restructuring. The CEO uniquely *pushed back*: "none of it had to do with AI" — the cuts targeted coordination-heavy roles and excess management layers.

Survey and disclosure evidence that AI washing is economy-wide:
- **59%** of US hiring managers admit they emphasize AI to explain layoffs because it plays better with stakeholders than citing financial constraints.
- Forrester: 9 of 10 companies preparing "AI-driven" layoffs have no vetted AI app ready — "they haven't even started."
- HBR survey (1,000+ execs): **21%** made large headcount cuts "in anticipation of" AI vs only **2%** from actual AI implementation — a 10× gap between hype and reality.
- **NY WARN Act AI checkbox** (first US state to add one, 2025): of 160+ filings in year one, only one company (Nespresso) checked it — ~0.2% of ~25,000 laid-off workers.

**Layoffs are the wrong signal anyway.** Research shows AI's labor effect operates through **slower hiring, not increased separations**. Firing destroys the tacit knowledge and organizational capital needed to operate AI well, and is expensive (severance, morale, rehiring risk) when natural turnover achieves the same headcount adjustment in a few years. A Federal Reserve compilation finds US coder employment still *growing* post-ChatGPT, just ~3 pp/year slower than a no-AI counterfactual — and that likely understates the picture since the method misses self-employment, into which AI-enabled entrepreneurship may be diverting growth.

**Two *real* but different AI-driven losses:** (1) AI obviating *product demand* (Chegg, Stack Overflow) rather than doing the worker's job — like the telegraph operator made obsolete by new tech (of 270 jobs in the 1950 census, only the elevator operator was directly *automated* away); (2) companies that *sell* AI (IBM, SAP) reallocating headcount to their growth line — ordinary restructuring, not displacement.

## Vibe coding is not agentic engineering

Much confusion comes from "vibe coding" being used sloppily for a whole spectrum. The two ends are more dissimilar than similar:

- **True vibe coding**: user tells the agent what to do, doesn't supervise, doesn't review (may lack the skill to), doesn't evaluate output beyond noticing visible breakage.
- **[[agentic-engineering]]**: AI as a tool, human in control and **accountable** for output. This is how most professional engineers actually work, and it's [[ai-coding-harnesses|the dominant pattern]].

The **exhaustion paradox** recurs: agentic engineering is *surprisingly* time-consuming to supervise — Simon Willison reports being mentally exhausted by 11am from supervising agents (see also [[agentic-engineering]] and [[ai-code-review]]). The SWE-chat dataset (opted-in OSS developers) found only **44% of agent-produced code survives into commits**, vibe-coded commits introduce vulnerabilities at **9× the human-only rate**, and the most common user intent is *understanding existing code* (19%) over *generating new code* (13%). The jobs implication is solid even if the dataset is self-selected: **you can't ship production software by hiring unqualified vibe coders instead of engineers.**

## Why demand may actually *grow*

Narayanan argues software is highly **price-elastic** (cheaper → buy much more) while the **elasticity of substitution** between AI and engineers is low (AI doesn't replace them). Cheaper software therefore produces a *derived demand* for more engineers — the Jevons-paradox-style argument (loosely; the precise mechanism is elasticity, not Jevons). This is the same dynamic as the ATM/bank-teller parable in [[task-automation-vs-paradigm-replacement]]: automating a task within a paradigm grows the job count; only a *new paradigm* that makes the workflow irrelevant destroys it. Historically programmer employment went from ~zero in 1950 to millions; unlike agriculture (calorie demand is roughly fixed, so mechanization decimated labor), software demand has grown a millionfold and shows no ceiling — a modern car runs ~100M lines of code.

Caveats Narayanan flags:
- More software ≠ bigger Big Tech. Most engineers already work in-house at non-software firms; that share may grow. "AI rollups" (PE/VC buying Main Street businesses and rebuilding them AI-native with embedded engineers) may matter — or may be hype.
- The **democratization bet** (that domain experts, not engineers, will produce the software) — Narayanan bets *against* it, calling it the same vibe-coding/agentic-engineering conflation. FORTRAN, COBOL, and SQL each arrived with identical democratization hopes that never materialized; the barrier was never syntax, it's **skilled judgment under accountability**.

## Two long-running trends, not a sudden AI rupture

Narayanan stresses the sandwich-squishing predates AI:
- The BLS began tracking **programmers** (execution only) separately from **software engineers** (more of the sandwich) two decades ago. Programming has been *shrinking* and pays less — seen as grunt work. AI merely accelerates the long-standing devaluation of purely technical execution skill.
- **Fred Brooks's *No Silver Bullet* (1986)** is the 40-year-old articulation: software has **accidental complexity** (tooling clunkiness, reducible over time) and **essential complexity** (specifying correct behavior is intrinsically hard). AI only attacks accidental complexity, so — as Brooks predicted of every productivity tool, AI hopes included even then — it won't yield order-of-magnitude gains. This *is* the "Decide layer is thick" argument, made decades early.

## Connections and assessment

- **vs. [[ai-and-the-future-of-work]]**: Andreessen reaches "deepen judgment, don't be fungible" via macro optimism (AI offsets demographic collapse; task loss not job loss; E-shaped careers). Narayanan reaches a structurally identical conclusion via the sandwich model and hard layoff/employment data. The two are complementary: Andreessen on *why the macro is fine*, Narayanan on *the microstructural mechanism* and *debunking the layoff narrative*.
- **vs. [[ai-eats-the-world]]**: Evans's "value moves up the stack" maps onto Narayanan's "value of decision-making migrates upward."
- Confidence is **medium**: the model is opinionated and the supporting studies (SWE-chat self-selection, Fed counterfactual estimation, a not-yet-replicated NBER paper) carry the caveats Narayanan himself flags. The AI-washing debunking and the no-bottleneck-in-code-writing findings are the strongest, most factual parts. The forward-looking demand-grows claim is the most speculative.
- Narayanan promises a follow-up essay on why *individual* engineers' careers may still be rocky (firm type, geography, seniority, adaptation pace) even if aggregate demand holds — integrate it here when ingested.

## Sources
- Arvind Narayanan (2026-06-10). "Why AI hasn't replaced software engineers, and won't." *Normal Tech.* <https://www.normaltech.ai/p/why-ai-hasnt-replaced-software-engineers> — [[2026-06-10-why-ai-hasnt-replaced-software-engineers|local copy]]
