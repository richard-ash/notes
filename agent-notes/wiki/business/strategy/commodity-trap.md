---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-07-09-up-the-stack-commodity-trap.md
compiled_at: 2026-07-21
model: claude-opus-4-8
confidence: medium
---

# The Commodity Trap and Moving Up the Stack

Arvind Narayanan and Akash Kapur's July 2026 essay (part of the *AI as Normal Technology* project) reframes the "is AI a bubble?" debate as the wrong question. The right question is **value capture**: the value AI *creates* will be enormous, but how much of it can the labs *capture*? Their answer has two moves. First, at the model layer, inference is an unusually pure instance of the [Bertrand paradox](https://en.wikipedia.org/wiki/Bertrand_paradox_\(economics\)) — homogeneous product, similar costs, no switching costs — so price is competed down to the marginal cost of a token, and no amount of volume recoups the $4–8T infrastructure buildout. Second, and this is what separates them from the bears, **the labs are not confined to being model vendors**. They can migrate "up the stack" into products, AI-native SaaS, bespoke deployment, and "digital workers," where enterprise-software-style moats become available. This escape is likely to work — which is precisely why lock-in and reduced competition, not a financial crash, are the concern worth taking seriously now.

The piece is the fuller, more optimistic-for-labs counterpart to [[ai-value-capture]] (Garicano & Saa-Requejo). Both accept the model layer gets squeezed; they diverge on the conclusion. Garicano assumes the labs are stuck as model vendors and concludes surplus flows past them (upstream to silicon, downstream to implementers). Narayanan & Kapur call that assumption "increasingly outdated" and argue the labs are *furiously migrating out of it*. It also sits alongside Evans's [[token-pricing]] and [[ai-platform-moats]] (same model-layer-commoditization diagnosis) and the swyx/Shaughnessy [[ai-lab-economics]] pieces — but goes further than any of them in cataloguing the specific escape routes.

## The historical argument: infrastructure rarely keeps the value it creates

The method is the *AI as Normal Technology* commitment to historical analogy — but disciplined by six capital-intensive infrastructure cases (railroads, electricity, telecom/fiber, cloud, semiconductor fabrication, commercial aviation). Three lessons:

1. **Infrastructure providers rarely capture the value they create.** Builders get competed, regulated, or commoditized into thin margins, often bankrupted. The late-1990s telecom/fiber buildout: capacity up 186,000× in seven years, prices crashed, ~$2T of market cap erased — the value went to the applications built *on top*. Commercial aviation has destroyed investor capital for eight decades at 2–4% net margins, below the cost of capital, even as everyone else benefited from cheap flight. Carlota Perez's "installation period" names the paradox: the builders rarely survive to capture what they built.
2. **Enterprise software is the exception**, sustaining 75%+ gross margins for decades via three properties infrastructure lacks: zero marginal cost of reproduction, deep switching costs, and non-ephemeral value (fixed costs amortize over decades, not one demand cycle). The labs' lock-in strategies are best read as attempts to *import these software properties into AI*.
3. **Two partial escapes show the price of admission.** Cloud acquired software-like lock-in (managed services, egress fees, committed spend); TSMC achieved near-monopoly in leading-edge fab. A capital-intensive business sustains margins only by *becoming functionally software* or *achieving concentration*. (This is exactly Evans's semiconductor/Rock's-Law read in [[token-pricing]] — but note even TSMC captures little of the tech economy's value.)

## Why inference is Bertrand-paradox-pure

The authors ground the forecast in theory rather than year-to-year financials (both bull and bear "mistake the transitional period for the equilibrium"). Model inference matches the paradox's preconditions more cleanly than the historical precedents did:

- **Undifferentiated product** — OpenAI, Anthropic, Google cluster near the top of hundreds of public benchmarks; the near-equivalence is *legible to customers*, and open weights are "good enough" for a growing share of use cases. (Contrast: Apple escapes this by refusing to compete on observable specs and selling "it just works" instead.)
- **Similar capital costs** — knowledge diffuses fast; scaling, inference-scaling, and RL proceeded in near-lockstep, so a token of given quality costs all labs about the same. Inference cost converges even harder than training cost.
- **No geographic differentiation** — unlike railroads' patchwork of local monopolies, any lab can serve the whole market. Today's capacity constraint is treated as temporary.
- **Free, non-collusive repricing** — sub-frontier competition makes tacit price support (which utilities and railroads sometimes managed) impossible.
- **Minimal switching costs** — provider-agnostic routers (OpenRouter, LiteLLM) erase even API-migration friction. This is the same low-switching-cost fact Garicano leans on in [[ai-value-capture]].

The "make it up in volume" rebuttal fails on arithmetic: at a 5% net margin (better than airlines), recouping $4–8T over five years needs $16–32T/yr in revenue — the top end is a quarter of world GDP.

**Three red herrings** the equilibrium view lets you discount: (1) *falling token prices* aren't fatal — [Jevons' paradox](https://en.wikipedia.org/wiki/Jevons_paradox) means unlocked demand can more than compensate (the same point the finance-side [[ai-capex-required-returns]] framework makes about revenue-per-token being the wrong metric); (2) *token scarcity* is temporary and won't durably raise margins; (3) *willingness to pay* is not fixed — if AI is as transformative as the industrial revolution, long-run WTP is enormous. Value creation ≠ value capture; the capturable fraction is endogenous to whether labs escape the trap.

## The stack, and how the labs are already climbing it

Ruling out the "hard takeoff / recursive self-improvement produces a monopoly" route as implausible (and, more to the point, not something regulators or investors can plan around), moving up the stack is the remaining path. The stack describes **what the customer pays for, not the billing unit** — token pricing can appear at any layer; it's the *type of value* that determines whether the commodity trap bites. Layers, ascending:

- **Products** (ChatGPT, Claude Code) — not interchangeable the way raw models are. ChatGPT already drives the majority of OpenAI's revenue; Claude Code's growth may soon flip Anthropic off API-dominance.
- **AI-native SaaS / "intelligence as a service"** (ChatGPT Company Knowledge, Anthropic's agents-in-the-System-of-Record) — but this is where the labs are *most exposed to SaaS incumbents*, Microsoft above all.
- **Bespoke deployment & workflow redesign** (forward-deployed engineers, consulting partnerships like PwC–Anthropic) — monetizing the transformation itself rather than the transformed steady state.
- **"Digital workers"** (Claude Tag, June 2026) — the most speculative and most lucrative: a digital worker embedded across teams becomes a store of tacit org knowledge that "effectively cannot be fired," a lock-in exceeding enterprise software at its worst, with a TAM equal to the entire labor spend — and therefore the vision enterprises will resist hardest.

The uneven-playing-field caveat matters: standalone labs (OpenAI, Anthropic) must climb against incumbents with distribution and enterprise relationships already in place — Google integrating into its consumer line, Microsoft betting it cracks intelligence-as-a-service first — often while renting infrastructure from the very companies they compete with. This is the structural handicap [[low-margin-ai-winners]] and [[minimum-viable-saleable-software]] circle from the buyer side.

## Five moats that open up higher in the stack

The load-bearing contribution. Moving up the stack isn't just more value — it makes value *capturable and durable* by escaping the undifferentiation at the heart of Bertrand. Derived by asking which enterprise-software moats transfer to AI, plus what's newly available:

1. **Embedding moats** — even if the model stays swappable, the *state wrapped around it* need not: persistent memory, uploaded corpora and retrieval indexes, custom skills/eval suites, encoded workflows, fine-tuning. This "data gravity" is why replacing enterprise software is "open-heart surgery." The catch: the richest data sits in Salesforce/Workday/SAP, out of the labs' reach — so labs may fight for the *orchestration layer*, but open standards (MCP) could keep that thin and swappable, handing value to integrators and enterprises instead. (The orchestration-layer land-grab is the same terrain as [[company-wide-agent]].)
2. **Ecosystem moats** — weak so far: the GPT store failed, Claude plugins are too thin to lock anyone in. The unrealized prize is the **IP flywheel** — training on customers' data, agent environments, execution traces, private evals. Enterprises are skittish, but "it takes only one suitably incentivized customer per sector to defect" to start it. (This is exactly the flywheel Garicano argues corporate-use agreements currently *bar*, in [[ai-value-capture]].)
3. **Commercial moats** — multi-year contracts, committed-spend tiers, prepaid credits. Durability is questionable: procurement demands portability, and contractual lock-in is legible to antitrust. **Vertical integration** is the stronger version — Copilot inside M365, Gemini inside Workspace make AI's marginal cost *appear* zero and fold it into renewals, but this is available only to integrated incumbents, not standalone labs.
4. **Behavioral moats** — work through humans, not tech or contracts. Skill erosion (unaided ability atrophies while vendor-specific driving skill builds) creates dependence with acute societal stakes. Plus genuinely novel forms: relational attachment to a model's personality (the #Keep4o backlash that forced GPT-4o's reinstatement), and judgment-heavy knowledge work as a **credence good** (like law or consulting — quality unverifiable even after the fact, so buyers rely on reputation/trust, muting price competition even when technical switching cost ≈ 0).
5. **Pricing strategies** — outcome pricing (% of cost saved, per resolved ticket), OpenAI CFO Sarah Friar's "scale with the value of intelligence." Additive *after* lock-in, but hard short-term: it's a measurement problem the labs lack the embedded customer teams to solve, and naive metrics invite gaming on both sides (stuff many issues into one ticket; close tickets without fixing). Tractable only if labs reach the System of Record. This is the AI-native model [[outcome-based-pricing]] argues for — Narayanan & Kapur are more skeptical about its near-term feasibility.

## Why this matters — the concentration concern

The counterintuitive punchline: the *worse* outcome for society is the one where the labs **succeed**. Failure to escape the trap is merely financial (a confidence crisis in the largest capital buildout in history). Success — durable switching costs and lock-in — raises costs for every AI-dependent enterprise and entrenches a few players in a structural advantage that's hard to contest later. Hence the timing argument: interoperability standards, portability requirements, and switching-cost transparency have to be set *early*, before moats harden. The authors fault the FTC and CMA for focusing their scrutiny on the *bottom* layers of the stack (chips, partnerships) and argue they must look up.

## Where it sits in the cluster

- **vs. [[ai-value-capture]] (Garicano & Saa-Requejo):** same model-layer diagnosis, opposite conclusion, because of one assumption. Garicano treats the labs as model vendors → surplus flows past them to silicon (up) and implementation (down). Narayanan & Kapur reject that premise → the labs move up the stack and capture the implementation surplus themselves. The disagreement is empirical and near-term-testable: does the orchestration/System-of-Record layer stay thin and open (Garicano wins, value flows to integrators/enterprises) or does a lab own it (Narayanan & Kapur's lock-in materializes)?
- **vs. [[token-pricing]] / [[ai-eats-the-world]] (Evans):** Evans reaches the same "commodity infrastructure, value captured up the stack" default but stops at radical uncertainty ("every non-commodity outcome requires something to change we can't yet see"). Narayanan & Kapur are more committal — they name the specific up-the-stack moves and treat the escape as *likely*, not merely possible.
- **vs. [[ai-lab-economics]] (swyx/Shaughnessy):** the model-lab/agent-lab split is the org-chart mechanism by which "value moves up the stack" already happens; Shaughnessy's subsidy-unwind bear case is what the *model layer alone* looks like without an up-the-stack escape.
- **vs. [[competitive-moats]] / [[ai-platform-moats]]:** the five-moat taxonomy is the AI-specific instantiation of Neumann's structural moats and Evans's "foundation models aren't platforms" argument — with two moats (behavioral/credence-good, IP flywheel) that the general frameworks don't foreground.

## Caveats

- **Opinionated single source**, confidence medium. It's a forecast of an equilibrium, and the authors are explicit that the industry is mid-transition. The load-bearing claims (frontier stays competitive; hard takeoff is implausible; labs successfully climb the stack) are each contestable and are argued more fully in their forthcoming paper.
- The moats are catalogued as *available*, not *proven durable* — the authors flag every one's fragility (open standards, procurement portability, antitrust legibility, unsolved outcome measurement). The essay's own honest read is that whether lock-in actually hardens is still open.
- **The framing is US/enterprise-centric.** Ad-driven consumer revenue is bracketed as possible-but-orthogonal; the whole moat analysis assumes enterprise is where the revenue is.

## Sources

- Narayanan, Arvind & Kapur, Akash (2026). "Up the Stack: How AI's Escape From the Commodity Trap Risks Enterprise Lock-in." *AI as Normal Technology*. <https://www.normaltech.ai/p/up-the-stack-how-ais-escape-from> — [[2026-07-09-up-the-stack-commodity-trap|local copy]]
