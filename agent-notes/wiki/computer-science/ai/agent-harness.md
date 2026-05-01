---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-03-10-bret-taylor-sierra-cheeky-pint.md
compiled_at: 2026-04-30
model: claude-opus-4-7
confidence: medium
---

# Agent Harness as Business Interface

Bret Taylor's argument that AI agents will pull a new layer of software-business design into existence: alongside the web app (for humans) and the API (for programs), companies will need to expose an **agent harness** — a body of skills, documentation, rules, and context that lets agents extract real value from the product. This is the same idea that powers [[ai-coding-harnesses|coding agents]], generalized from the IDE to the SaaS dashboard.

## The web app + API model isn't enough

Taylor frames the historical interface stack of a SaaS product like Stripe:

- **Web app** — forms, fields, buttons, graphs, designed for human eyes and clicks.
- **REST/GraphQL API** — the manipulable surface for programs. Mostly exposes the highest-value business objects.

The API is where computers talk to computers. But Taylor argues the API alone is too thin for agents that need to perform multi-step, judgment-laden procedures on a customer's behalf. There are dozens of switches in the dashboard with no API equivalent. The data isn't browsable in agent-accessible ways. And critically, the API tells the agent *how to call*, not *when, why, or in what sequence*.

What's missing is the equivalent of "the greatest Stripe expert who knows how to extract maximum value from their account." That expert has tacit knowledge — when to enable local payment methods, what fraud rules apply to which merchants, what to do when a Russian-submarine-looking switch needs flipping — and that knowledge is exactly what an agent harness would encode.

Taylor's prediction: in two years, "Stripe's ability to work with the agent that manages commerce for a direct consumer e-commerce company" will be a basis on which Stripe is evaluated. Harness compatibility becomes a procurement criterion.

The dashboard side gets easier, in fact: a PM can add a new switch that "looks like a Russian submarine" without UI design work, as long as the harness describes when to use it. UX polish becomes optional for agent-mediated paths.

## Markdown beats elaborate scaffolding

Taylor and Collison spend most of the conversation circling the same surprising empirical finding: simple, terminal-friendly, human-readable substrates outperform the more sophisticated alternatives that the industry expected to win.

**Memory as markdown files.** OpenClaw's wildly insecure, three-name-changes-in-three-days hobby project remembers things by scribbling notes in markdown — like the movie Memento. This is somehow more useful than ChatGPT's or Gemini's polished blank-slate chats. Vector databases are random-access; you have to know what to look for. Markdown directories give you context-plus-random-access, which is closer to how real memory works. Taylor: "mimicking a code base is actually the best way to make a general-purpose agent work."

**Documentation as the durable artifact.** Pointing to OpenAI's harness-engineering blog post, Taylor wonders if the output of a Codex session should be a documentation artifact alongside the code. Code is transient; the PRD, the customer problem, and the intent are the durable assets. "It would be the greatest irony if software engineering agents made all of us just write documentation the whole time." See [[llm-knowledge-bases]] for Karpathy's parallel argument about personal knowledge bases.

**Unix tools as the lingua franca.** Every modern model already knows grep, sed, ls, and curl. Taylor: "The AIs really know how to use all the Unix tools. You got a lot of lift from that." Stripe is now building what amounts to "SSH into your Stripe account" — `tail` the payments log, pipe between commands — because the elegance of Unix happens to map directly onto how agents want to manipulate state.

The thread connecting all three observations: the most efficient agent substrate looks remarkably like a 1970s programmer's desktop, just because that substrate is what every model has been heavily trained on.

## Skepticism of MCP and multi-agent architectures

Taylor explicitly distances himself from two architectures that dominate Silicon Valley whiteboards.

**MCP.** "I'm growing more skeptical of MCP as a meaningful part of the future. It's fine as a protocol, but [...] OpenClaw just writing a big markdown file works better than a bunch of MCP servers." His reading: MCP exposes too little context — agents need history, intent, and the "why" behind APIs, not just the call surface. The harness layer (skills + docs + rules) carries that context; MCP doesn't.

**Multi-agent systems.** The classic whiteboard architecture (a fraud-detection agent, a personalization agent, a super-orchestrator on top) "looks really good on a whiteboard like most elegant-looking but completely nonsensical architectures." The failure mode: context gets stuffed into the subagents, and the orchestrator on top has no ability to *not* sound robotic. By contrast, OpenClaw's just-a-bunch-of-markdown-files approach gets the memory right "even though it's a little bit kludgey," because the orchestrating agent has the same expansive context the codebase metaphor naturally affords.

These critiques echo [[agentic-engineering-architecture|Tan's heuristic]] of fat-skills + thin-harness: the orchestration layer should be minimal, with knowledge in markdown context that the model consumes directly.

## Constellation of models: how Sierra grounds agents in practice

Sierra's production technique for keeping agents on-script is what Taylor calls a **constellation of models**:

1. The primary reasoning agent operates against goals and guardrails (not a prescribed sequence of steps).
2. A **supervisor model** observes the primary's reasoning trace.
3. If the supervisor judges the primary went off-script ("I think John should have actually looked up the policy here"), it sends the trace back with corrective notes: "you're not allowed to make that decision; here's why; redo it."

The arithmetic Taylor offers: a primary right 90% of the time chained with a supervisor right 90% of the time gets you 99% effectiveness. Layering reasoning on top of reasoning, rather than chasing a single perfect model, is the cheap win. The technique generalizes the supervisor pattern: it doesn't require prompt-engineering hacks (writing in all caps, etc.) to keep models conformant — guardrails live in a separate model whose only job is to catch deviation.

Taylor identifies a paradoxical product surface: well-known brands are *harder* to ground than obscure ones. For a deep-sea-drill-bit company, the LLM has no internet folklore to hallucinate from. For a famous brand, the LLM "knows" enough to get confidently wrong, and "I got this" is a worse failure mode than "I don't know." Counter-intuitively, the most prestigious clients need the strictest harnesses.

## Innate LLM knowledge as starting capital

Counterpoint to the hallucination concern: a lot of an agent's effective knowledge comes for free from pre-training. Sierra's Sonos agent benefits enormously from the LLM having absorbed every Wi-Fi troubleshooting thread on the internet, because Sonos failures are almost always Wi-Fi failures. You don't need to give the agent "the history of Wi-Fi" — it's already in there.

So the harness work is shaped: narrow guardrails for regulated conversations (insurance, banking), wider permissions for less-regulated ones, and aggressive grounding only for areas where the brand-specific facts diverge from internet folklore.

## English over PSTN

The most striking real-world detail in the interview: Sierra's healthcare clients (payers, providers, revenue-cycle-management firms) increasingly have AI agents calling each other on the phone. The substrate isn't a fancy agent-to-agent protocol — it's English over the public switched telephone network. "TCP/IP and English over PSTN."

Taylor concedes a softer version of his harness thesis here: backwards compatibility (with the phone system, with web forms, with English) is enormously valuable because you don't have to finish the last mile to extract value. But he holds that the long-run equilibrium is still rich harnesses, because "agents using a sophisticated application harness can just do a lot more, and do it with higher fidelity." PSTN-and-English is the bootstrap; the harness is where the durable value lives.

The race Dario Amodei flags is between two paths: companies retrofitting agent-friendly harnesses, vs. desktop computer use just getting good enough that agents can drive a regular GUI through the same Chrome login a human uses. Both paths work; the harness path has higher ceiling.

## Systems of engagement decay; systems of record persist

A consequence Taylor draws for the SaaS landscape: as agents perform the actual labor, the *system of engagement* loses its structural advantage as the gravitational center of a department's workflow.

For 30 years, ERP/CRM/marketing-automation systems collected "taxes" from their ecosystems because their database was the system of record. AI agents threaten that gravity in some categories:

- **Marketing system of record** (the customer database driving Black Friday email blasts) — value migrates to the agent generating leads, because the agent does the actual work.
- **CRM system of record** — value migrates to the agent that carves territories, since no human logs in to do it manually.
- **ERP general ledger** — *durable*, because the database itself is the value (auditors care about the ledger).

Taylor's framing: the closer a system is to "literally the database is the value, i.e. a ledger," the more durable it is. The closer it is to a system of engagement (a database that exists because it was easier to build software atop centralized data), the more it gets unbundled by agents that don't care about formatting and pluck data from ten different places. This is part of why public markets recently re-rated software 20–30% lower — the ARR annuity assumption depends on the system of engagement staying central, and agents are quietly breaking that assumption in some categories.

## Implications

- **Building software for agents is a different design discipline** from building for humans. UI elegance matters less; harness richness, supervisor coverage, and context-bundling matter more.
- **MCP as a protocol probably survives; MCP as the dominant agent-integration story probably doesn't.** Markdown context wins where it can.
- **Multi-agent diagrams should make readers suspicious.** A flat agent with rich context generally beats a hierarchy of specialized agents.
- **For SaaS incumbents, the long-run risk isn't "vibe-coded competitors" but "your harness loses to a competitor's harness"** — i.e., agent compatibility becomes a selection criterion, and your category-defining product becomes a commodity backend.

## Cross-connections

- [[ai-coding-harnesses]] — the same harness pattern, narrowed to coding agents; this article generalizes to the whole product surface.
- [[agentic-engineering-architecture]] — Tan's fat-skills / fat-code / thin-harness heuristic prefigures Taylor's harness thesis at the systems level.
- [[llm-knowledge-bases]] — Karpathy's markdown-as-memory workflow is the personal-knowledge counterpart to Taylor's "memory as scribbled notes" observation.
- [[claude-code]] — Boris Cherny's terminal-first design embodies the "Unix tools as lingua franca" point; agents ship best on substrates models were trained on.
- [[outcome-based-pricing]] — once a harness lets an agent execute end-to-end, outcome-based pricing becomes the natural revenue model.
- [[ai-and-org-design]] — Taylor's process-not-person thesis sits underneath this one: the harness exists to let an agent own a process end-to-end.

## Sources

- Bret Taylor & John Collison (2026). "Bret Taylor of Sierra on AI agents, outcome-based pricing, and the OpenAI board." Cheeky Pint. <https://www.youtube.com/watch?v=n4E4xNYCkYM> — [[2026-03-10-bret-taylor-sierra-cheeky-pint|local copy]]
