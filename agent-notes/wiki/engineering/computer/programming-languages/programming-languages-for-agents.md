---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/programming-languages/2026-09-24-evolving-programming-languages-ai-era.md
compiled_at: 2026-09-24
model: claude-fable-5-1
confidence: medium
---

# Programming Languages for Coding Agents

What should a programming language optimize for once its primary *writer* is a coding agent rather than a human? José Valim, creator of Elixir, takes up the question in a September 2026 essay, "Evolving programming languages in the AI era." His answer splits in two. The reflective half argues that most of what languages have historically competed on — syntax, ergonomics, the shared sensibilities that bind a community — matters much less to agents, and that the forces that build ecosystems are being strengthened and undermined at the same time. The prescriptive half argues that the tools around a language should stop imitating what humans do (write tests, read logs, hop between files in an IDE) and instead give agents interfaces built around what *they* are good at: exhaustive querying, instrumenting, and correlating. His three concrete proposals are stronger guarantees over convenience, program databases over language servers, and runtime observability over debuggers.

Valim writes from a specific position. He designed a language whose runtime (the Erlang VM) already excels at the introspection he recommends, and his company Dashbit builds Tidewave, an agent-tooling product whose design informs the "program databases" section. The essay is explicitly a digest of evolving opinion ("my opinions on these topics will probably change") and, by Valim's own disclaimer, was polished with AI assistance. Read it as a well-placed practitioner's thesis, not a survey.

## Reflections: what stops mattering

**Community and ecosystem.** Valim observes that languages are held together by shared sensibilities — Python's one obvious way, Ruby's programmer happiness, Lisp's reshapeable language — and asks what glues a community together when its members no longer write most of the code. He identifies a tension in how agents affect ecosystems. On one side, agents shrink the gap between ecosystems: porting a tensor library or a web framework, implementing a known algorithm, or translating a paper are exactly the tasks agents do well, so small communities can catch up with large ones quickly. On the other side, if building the library you need is cheap, the incentive to collaborate on a shared one weakens. "Coding agents could dramatically reduce the cost of building an ecosystem while simultaneously weakening one of the forces that causes ecosystems to form in the first place."

An implication Valim leaves implicit: the "innovation token" calculus in [[choose-boring-technology]] rests on the cost of *operating* an unfamiliar technology, not just building it, and ecosystem breadth was a proxy for how many people had already paid that cost. If agents make breadth cheap to manufacture, the signal degrades: a language could have a full complement of ported libraries and nobody who has run them in production.

**Ergonomics.** A large share of language evolution consists of syntactic affordances — optional chaining instead of nested null checks, for example. Valim argues these are nice for the human who types them and nearly irrelevant to an agent, which is "not bothered by boilerplate." He anticipates the token-efficiency counterargument and rejects it: token efficiency is "at the tail end of the characteristics we should optimize programming languages for," and any language that markets itself as "for coding agents" and then focuses on syntax "is effectively building around today's limitations" — limitations that cheaper models and larger contexts are already eroding. From experience driving agents across HTML, CSS, JavaScript, Elixir, Rust and Lean, he reports that syntactic gaps that feel enormous to him are far smaller to the model: "it is all tokens-in, tokens-out."

This has the same shape as [[the-bitter-lesson]]: designing around a current capability ceiling loses to designing for the general case once the ceiling rises. It also implicitly bets against the cost-driven reasoning in [[token-pricing]] — Valim assumes token cost falls fast enough that syntax-level savings never become the binding constraint.

**Compilers.** To the recurring suggestion that agents might skip languages and emit assembly directly, Valim gives two answers. First, any multi-architecture program needs an architecture-independent representation and something to lower it, which is at least part of a compiler and a higher-level language, even if no human ever writes that language. Second, no single computational model has proven best at everything; systems languages, theorem provers, concurrent-and-resilient runtimes like Erlang/Elixir, query languages and hardware-description languages encode different semantics and guarantees, and a single low-level target cannot unify them. So languages survive, and the question becomes what to optimize them for once it is no longer human authorship.

## Agentic tooling: what should matter instead

Valim's framing for the second half: building good tools for humans has also produced good tools for agents, but only by having agents do what we already did — write the same tests, read the same metadata and logs. The opening is to have agents do what we *wouldn't* — work that is too tedious, too steep to learn, or needs more information than a person can process. None of this requires agents to write most of the code; he notes a team using agents for 20% of its code still benefits.

### Stronger guarantees over user constraints

Languages trade off expressiveness, guarantees and ergonomics. Valim's argument is that agents shift the trade-off away from ergonomics. His central example is type inference: humans value it because writing what the compiler could deduce is tedious, but agents do not mind tedium, and explicit types give the compiler, other agents and human readers more to work with. The sharper technical point is that the type systems whose types can be fully *inferred* are generally a subset of those whose types can be *checked*, so a language that optimizes for inference has capped both its expressiveness and its guarantees. "Why impose those limits on agents when we've already seen them capable of writing proofs in much more complex systems?"

Guarantees need not be static. Valim lists garbage collection for memory safety, model checking that validates implementations against model-generated execution traces, and the Erlang/Elixir process model, which trades some concurrency expressiveness for isolation and fault-tolerance properties that conforming programs inherit for free. He groups the approaches into four:

- **Correct by construction** — the language makes invalid states or programs hard or impossible to express.
- **Statically established** — types, proofs and static analysis establish properties before execution.
- **Runtime-enforced** — memory management, isolation, capability boundaries.
- **Empirically validated** — tests, property-based testing, fuzzing.

His prediction is that *how a language combines these* will increasingly drive differentiation and adoption — especially if, per the community section, agents erode the ecosystem-size advantages languages used to compete on. Frameworks, he adds, must do the same at their own level of abstraction.

This is a cleaner taxonomy for the ladder Quinn Wilton built in [[correctness-oracles]] (Wilton is thanked in the acknowledgements): vendored reference implementations and property tests are empirical validation, `assert_boundary` and Argus are static establishment, Accord's runtime monitors are runtime enforcement, and TLA+ checking of the contract sits between the static and model-based rungs. Both essays converge on the same reframing of the engineer's job, from writing code to building the constraints the code must satisfy. Lopopolo's [[harness-engineering]] (also acknowledged) reaches the same place from the other direction, mechanically enforcing architecture and taste on a codebase with zero hand-written lines.

### Program databases over LSPs

Valim expects the Language Server Protocol (LSP) to die with the IDE. LSP operations are keyed on document positions — file, line, column — that agents "do not track precisely," and they deliver information one hop at a time for a human to read, not for a program to explore. Tidewave's experience is that agents do better with name-based questions: "where is `BarBaz` defined?", "where is the documentation for `foo_bar`?"

His proposal: language servers already compute symbols, references, call graphs, type information and sometimes data flow. Expose that as a **program database** with a query language — SQLite, Datalog, or a custom DSL. A human would never write a query to find references to a function, but for an agent a query costs the same as a tool call, and it can compose queries no IDE would ship as a feature: every public function that transitively calls this one, every path along which a value can become nil. The same database doubles as a linter that blocks practices the team has ruled out.

Two implications follow. First, today's agents mostly navigate code with text search, which is a degenerate version of the by-name interface Valim describes; a program database is the upgrade path that grep cannot take, since grep cannot answer "transitively calls." Second, Valim draws out that **locality** becomes more valuable, not less: monkey-patching, implicit hooks, dynamic rebinding and other action-at-a-distance let code in one place change behaviour everywhere, in ways even a program database struggles to trace. He names no language, but those are hallmark Ruby and Rails techniques, and Valim was a Rails core team member before creating Elixir. This is a language-design corollary of Herrengt's [[understanding-as-the-bottleneck]]: if understanding is the scarce resource, the features that make understanding non-local are the expensive ones. It also gives Elhage's [[computers-can-be-understood]] a mechanical form — the database is what makes "any layer can be understood" cheap enough to be an agent's default move.

### Runtime observability over debuggers

Debuggers — breakpoints, stepping, inspecting variables — are built for a human's pace. Agents can instrument, collect traces and correlate them far faster, so Valim argues they deserve interfaces built for that. He extends the point along the lifecycle: if agents write most of the code, they will plausibly also monitor and diagnose production, and they should do so by querying the running system rather than reading logs and dashboards designed for humans. Runtime observability becomes one interface for diagnosing failures, reliability issues and bottlenecks across every environment.

The Erlang VM already exposes processes, sockets, applications, supervisors, ETS tables and message queues as built-in introspection; Valim says the remaining gap is exposing that to agents safely — as a set of tools, a query language, or a sandbox. This is the production-side counterpart to the compile-time program database, and the point where the essay's product thesis is most visible. It also fills a gap in the autonomy accounts in [[unattended-coding-agents]] and [[software-factory-pattern]], which extend agents *upstream* into planning and backlog maintenance but stop at deployment; Valim's is a case for extending them *downstream* into operations, on the same live data that [[phoenix-telemetry-metrics]] currently pipes to dashboards for humans.

## Open questions the essay leaves

- Valim asserts agents "do not track" file positions precisely, but harnesses could be built to. Whether name-based addressing is intrinsically better or only better matched to current agents is left open — the same "today's limitations" objection he raises against syntax-focused languages.
- The community section poses its questions without answering them: whether shared sensibilities are worth preserving, and what replaces them. The tooling half arguably answers by implication — a community could cohere around its *guarantees and query surfaces* rather than its syntax — but Valim does not say so.
- The explicit-types argument assumes agents write correct annotations. Richer type systems shift the failure mode from "wrong code" to "wrong specification," which is the problem [[correctness-oracles]] addresses by checking the specification itself.

## Sources

- Valim, José (2026). "Evolving programming languages in the AI era." <https://x.com/josevalim/status/2103133294317445290> — [[2026-09-24-evolving-programming-languages-ai-era|local copy]]
