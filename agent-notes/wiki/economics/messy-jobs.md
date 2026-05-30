---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-04-24-task-is-not-the-job.md
compiled_at: 2026-05-30
model: claude-opus-4-7
confidence: medium
---

# Messy jobs (Garicano on bundles and authority)

Luis Garicano's supply-side answer to the Amodei/Suleyman thesis that AI will eliminate half of entry-level white-collar work in 1–5 years, drawing on his forthcoming book *Messy Jobs* with Jin Li and Yanhui Wu. Where Imas's [[ai-and-relational-scarcity|relational scarcity]] argument answers the demand-side question (*where does spending go?*), Garicano answers the supply-side question (*what do firms actually buy, and what do organisations need to do?*). His claim: firms do not buy isolated tasks, they buy bundles; organisations do not just process information, they allocate authority and settle conflicts. AI helps with all of this. It does not follow that it replaces the humans who do it.

## The framing move: labour markets price jobs, not tasks

Most discussion of AI and employment starts from task exposure — measure what fraction of an occupation's tasks AI can perform, predict displacement proportionally. Garicano rejects the inference at the framing layer. A job is a bundle of tasks, and the question is not whether AI can perform a component but whether that component can be cheaply separated from the rest of the bundle.

- **Weak bundle:** separation is cheap. AI takes the component. The human role narrows. Labour loses share.
- **Strong bundle:** separation is expensive. AI helps with part of the work. The human still sells the full service and keeps the larger share of the revenue.

This is the supply-side mirror of [[task-automation-vs-paradigm-replacement|Oks's paradigm-replacement thesis]] — Oks asks when the *paradigm* itself becomes obsolete (ATMs vs. iPhones for bank tellers); Garicano asks when the *bundle* becomes separable inside a still-living paradigm. They are compatible: paradigm replacement is what happens when the entire bundle becomes one weak component of a new one.

## The travel agent and accountant case studies

Two empirical anchors:

**Travel agents.** Stripe Economics (Tedeschi) shows travel agent employment is >60% below its dot-com peak. The booking-and-comparison tasks were a weak bundle; once they unbundled, they were gone. But the surviving agents moved upmarket — planning fees, luxury consortia, upgrades, personalized itineraries. Average weekly earnings at travel agencies rose from 87% of the private-sector average in 2000 to 99% in 2025. The machine took the weak part and left the strong one, raising hourly earnings of the residual.

**Accountants.** Frey and Osborne's famous 2013 paper put the probability of accountants and auditors being automated at 94%. A decade later, the BLS counts 1.6M accountants and auditors, median pay $81,680, projected to grow 5% through 2034. But the BLS category "bookkeeping, accounting, and auditing clerks" is projected to fall 6% over the same period. The clerical task is a weak bundle; the accountant's job — interpreting tax law for a specific client, signing audits the bank and SEC will rely on, carrying legal exposure — is a strong bundle.

The 2013 Frey-Osborne prediction was wrong not because AI underperformed expectations but because it answered the wrong question: it predicted task exposure, not bundle separability. This is a load-bearing failed-prediction case — the standard reference everyone cites for "94% of accountants will be automated" turned out to be off by an order of magnitude in the same direction the bundle theory predicts.

## Three traits that make a bundle strong

Garicano identifies three structural features that raise the cost of unbundling:

1. **Unpredictable demand.** If you could tell in advance which tasks a customer will need, you could pre-allocate each to the cheapest agent (human or AI). In practice, you can't. The customer service call that looks routine reveals a thorny account problem; AI handles the routine well and the delicate poorly, and constant handoffs are expensive. Yanhui Wu's Hangzhou fieldwork at a leading Chinese customer service firm with a two-year domain-specific model deployment: human agents are indispensable on (a) recognising what the customer is not explicitly saying and (b) avoiding interactions that end up on social media. Senior manager quote: "frequent switches between the AI and human modes — the coordination cost would be too high."

2. **Production spillovers.** Some tasks belong together because doing one makes you better at the other. A radiologist who has already spoken with the patient and reviewed the clinical record reads the scan better than one who sees only the image. Unbundling destroys the contextual signal that improves the bundled task's quality.

3. **Measurement problem.** Alchian and Demsetz: when several inputs jointly produce an output, their separate contributions are hard to disentangle. If AI drafts and a human signs and the product goes wrong, who is responsible? Banks, regulators, boards, and clients need someone to blame. The bundle holds because liability cannot be cheaply allocated across its components.

Where these conditions hold, AI raises productivity *inside* the bundle without replacing it. The nurse practitioner with AI diagnostic support handles cases that used to require a doctor; the entrepreneur with AI tools runs a company that used to require a team — neither is displaced.

## Authority and residual decision rights

Bundling, Garicano argues, understates the case. Organisations are not production functions. They are coalitions of people with legitimate but conflicting goals — marketing wants ads, engineers want tokens, lawyers want process, finance wants less of everything. Managers exist to settle conflicts and decide who loses. The question is whether AI can play that role.

His answer draws three pillars from organisational economics:

**Arrow on trust.** Information is not a commodity: you cannot inspect it before you buy it because once you have, you already have it. The people who hold information have reason to distort it, and what checks that distortion is not a better contract but trust — and trust cannot be traded. ("If you have to buy it, you already have some doubts about what you've bought.") Trust is the expectation that the counterparty will bear a reputational cost if it defects and will be around tomorrow to pay it. An AI agent has neither.

**Williamson on hold-up.** Once a party makes a relationship-specific investment, the counterparty can hold it up. Before xAI built Colossus in Memphis, it could walk away to any site; after billions were sunk, the city could demand concessions. A human manager carries a reputation across counterparties she will deal with again; an AI cannot be sued, cannot be replaced with fanfare to signal a reset.

**Hart-Moore on residual decision rights.** Every project involves thousands of unspecified situations. The construction contract says March delivery but doesn't say what happens when the electrician and the plumber both need the same wall on the same day. The manager exercises residual decision rights — authority over what contracts and processes do not specify. These rights are not a cognitive task. They are an institutional role with three requirements:

- **Hold tacit and relational knowledge** people will not share, because communicating it gives away their bargaining power
- **Bear consequences** — be sued, fired, or publicly blamed when things go wrong (Garicano's case: the Sonos CEO fired after the 2024 app launch failure)
- **Confer legitimacy on the decision** — the role of meetings, which are not information exchanges but rituals of procedural fairness; people accept decisions they dislike when the process looks legitimate and the decider is accountable

Garicano grants this could in principle be acquired by AI, but the institutional machinery — corporate registries, professional licensing, courts that can compel testimony — took centuries to build for humans. No equivalents exist for AI. Until they do, some human holds residual decision rights.

## The supply-side vs demand-side decomposition

Garicano's explicit reconciliation with Imas:

| Question | Imas (demand) | Garicano (supply) |
|---|---|---|
| Why do jobs survive? | Customers want human origin | Firms buy bundles, not tasks |
| Where does employment concentrate? | Relational sector (nurses, therapists, teachers, hospitality) | Strong-bundle AI-augmented work + political-organizational core of firms |
| What is scarce? | Human involvement as consumed good | Human authority as institutional role |
| What does AI do? | Cheapens commodities, raises relative price of relational goods | Increases productivity inside bundles without unbundling them |

The two answers are complementary, not competing. Imas describes the economy of *what customers want*; Garicano describes the economy of *what organizations need to do*. Garicano claims the second is larger — which is the substantive point of disagreement. Imas's list (boutique fitness instructors, bespoke tailors, spiritual guides) feels frightening if read as exhaustive; Garicano's complement (managers handling ambiguity, integrating context, bearing consequences) covers the hundreds of millions of office workers, consultants, engineers, and middle managers Imas leaves out.

## What this implies about junior career ladders

Garicano acknowledges the AI-Becker problem — the disruption of junior career ladders is real, since the bottom rungs of the strong bundle (drafting, summarising, routine analysis) are exactly what AI does best. He has written about this separately. The bundle/authority argument does not deny entry-level disruption; it denies the inference from entry-level disruption to *job-category extinction*. The accountant survives but enters the profession through a different door, because the door she used to enter through is now an AI.

This is in tension with Taylor's [[ai-and-org-design|hyper-generalist-with-AI-exoskeleton]] thesis — Taylor expects flatter org structures with fewer middle managers, Garicano expects the political-organizational core to grow as the share of the economy where humans add value. They are reading the same trend in opposite directions: Taylor sees AI as a substitute for middle-management coordination; Garicano sees AI as a complement that raises the value of the residual coordination humans must still perform. The disagreement is empirically resolvable but unresolved: it turns on whether unbundling the cognitive tasks of middle management is cheap or expensive in the conditions Garicano's three traits identify.

## Connections

- [[ai-and-relational-scarcity]] — Imas's demand-side companion piece, explicitly referenced by Garicano as "the demand side" answer he is supplying the supply side to; the bundle/authority argument is what Imas leaves out by focusing on terminal consumption
- [[task-automation-vs-paradigm-replacement]] — Oks's paradigm-shift framework; bundles can survive a paradigm shift only if they are reconstituted in the new paradigm (the surviving travel agent is a different bundle than the 1995 travel agent, not the same bundle augmented)
- [[ai-value-capture]] — Garicano-Saa-Requejo's companion piece on AI industrial organization; "intelligence is not the binding constraint in implementation" is the firm-level version of "the bundle is not the task" — both argue that the locus of friction is institutional/organizational, not cognitive
- [[ai-and-org-design]] — Taylor's hyper-generalist thesis is partially in tension; Garicano expects authority-bearing roles to grow, Taylor expects them to flatten
- [[ai-economics-research]] — Kiesling on what becomes scarce within economics: judgment, evaluation, institutional reasoning. Garicano applies the same price-theoretic intuition (when one input becomes cheap, its complements rise) to the firm rather than to a discipline; the institutional reasoning Kiesling identifies as scarce in economics research is what Garicano identifies as the residual decision rights bottleneck in organisations
- [[use-of-knowledge-in-society]] — Hayek's knowledge problem is the substrate Garicano builds on; both Arrow and Hart-Moore are descendents of Hayek's insight that local, tacit, contextual knowledge resists central aggregation. Garicano uses this to defeat the "Hayekian AI" optimist position that argues AI just makes the price system faster
- [[empty-core-industries]] — Telser's framework for industries without a stable competitive equilibrium; Garicano's measurement problem (Alchian-Demsetz on joint production) sits in the same lineage of why simple production-function models fail to predict actual market outcomes

## Open questions and weaknesses

1. **The bundle theory is observational on the historical cases (travel agents, accountants) but predictive on AI** — it doesn't yet say which currently-strong bundles will weaken first. The three traits are necessary conditions for bundle strength but not measurable in advance, so the framework gives qualitative confidence that *some* bundles will hold without saying which ones.
2. **The authority argument depends on legal-institutional inertia** — Garicano explicitly concedes AI could in principle acquire residual-decision-rights standing, the constraint is just that the institutional machinery doesn't yet exist. If a jurisdiction created such machinery (corporate AI agents with limited legal personhood, AI professional licensing, AI-specific liability allocation), the authority argument weakens. This is not a stable equilibrium so much as a transition cost.
3. **The Frey-Osborne miss is one data point** — the accountant case is the central piece of evidence but it's also load-bearing in many other arguments (Acemoglu, Autor, etc.). The bundle theory's distinctive contribution is the explanation *why* Frey-Osborne missed, not the fact that they did.
4. **"Junior career ladders" hand-wave** — Garicano admits the disruption is real and then defers it. The book's working paper apparently goes deeper but the essay leaves the most policy-relevant question (what does an accountant's entry-level training look like when AI does her first three years' work) unanswered.
5. **The "second economy is larger" claim is asserted, not measured.** Garicano's case for why the supply-side residual is bigger than Imas's relational sector relies on intuition pumps (the hundreds of millions of office workers and middle managers) rather than a quantitative decomposition. Reasonable, but the conclusion that the second economy is larger is the most contestable specific empirical claim in the piece.

## Sources

- Garicano, L. (2026-04-24). "The task is not the job." *Silicon Continent*. <https://www.siliconcontinent.com/p/why-desk-jobs-survive-and-amodei> — [[2026-04-24-task-is-not-the-job|local copy]]
