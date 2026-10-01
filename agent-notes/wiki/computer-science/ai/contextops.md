---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-10-01-alpeza-fde-boom-is-a-product-gap.md
compiled_at: 2026-10-01
model: claude-fable-5-1
confidence: medium
---

# ContextOps

**ContextOps** is the discipline of turning operational evidence and expert judgment into tested, approved instructions for agents, and keeping those instructions current as the business changes. The term comes from Eugen Alpeza's September 2026 essay "The FDE boom is a product gap." Alpeza co-founded Edra after leading forward deployed AI engineering at Palantir, and his argument is that the enterprise-agent market is "hiring its way around a missing product": forward deployed engineers (FDEs) are everywhere because operators have no direct way to teach agents how the company runs. The proposed fix is to treat agent instructions as operator-owned, versioned procedures with a software-style life cycle, so that the people who own a process can change what the agents do without an engineer translating each revision.

## The problem: history records what happened, not what should happen

Alpeza starts from the same diagnosis as [[company-wide-agent]] ("business context is the bottleneck, not intelligence"): agents don't know how the company operates, and the operators who do can't easily tell them. He names two fashionable responses and rejects both.

**Forward deployed engineers.** The operator teaches the FDE and the FDE teaches the agent. It works, but it is a premium service, and it puts an engineer in the middle of every operating change. [[ai-eats-the-world]] explains the FDE boom from the demand side (enterprises keep no spare capacity to reimagine their own workflows), and [[agentic-pods]] is Uber running the same motion internally. Alpeza's framing is narrower and more pointed: the FDE is a translation layer, and a translation layer is a product waiting to be built.

**Context graphs.** Connect the company's records and decisions so agents can draw on accumulated experience. Alpeza's objection is that if access to history were enough, FDEs would not be in demand. His worked example is a Palantir engagement with a large telecom that handed over the data behind tens of billions of dollars of supply chain spend and asked for controls flagging equipment orders that deviated from how the business should operate. In one equipment family, units of a certain voltage were replaced most of the time but not always. The pattern was easy to find. What it meant was not. When the team took it to the process owners, some departures turned out to be mistakes (people not following a procedure they often didn't know existed) and others were legitimate regional requirements the written procedure had never captured.

His conclusion: "The telecom's order history was a context graph already! It indiscriminately recorded both mistakes and legitimate exceptions." FDEs could find the pattern; only the operators could decide which practices should stop and which should become official.

The underlying point is an is/ought gap. A company's history is descriptive. An agent needs something normative. No amount of retrieval over what people did tells you what they should have done, and the only party who can close that gap is whoever is accountable for the process. This is a different objection from Posel's in [[llm-knowledge-bases]], and the two stack. Posel argues the record is incomplete, because intent lives in Slack and calls rather than in the final document. Alpeza argues that even a complete record is ambiguous, because it doesn't label its own errors. [[enterprise-rag-architecture]] answers Posel by ingesting more of the record; that does nothing for Alpeza's objection.

Alpeza applies the same argument to **fine-tuning on company history**. It trains in whatever bad habits the history contains, and it needs fresh examples and a retrain for every new supplier, region, or policy. His line: "You can ask a supply chain operator to maintain a written procedure. You cannot ask them to fine tune a behavior out of a model." The procedure is a legible, editable artifact; a weight update is not.

## The mechanism

Alpeza's claim is that AI has changed both sides of the economics of documentation. Keeping a current, complete account of a company's procedures used to be brutal work whose payoff was a document people still had to read, remember, and apply one case at a time. Now agents can read across thousands of cases, surface candidate rules, flag contradictions, and put proposals in front of process owners, so assembly is cheap. And agents can execute an approved procedure at scale, so the return on having one is high. Maintaining the instructions becomes "part of maintaining production infrastructure."

The unit of work is the recurring operation: equipment requests, incidents, claims, customer support, anywhere a team does the same kind of work repeatedly. A **case** arrives, the agent finds the applicable **procedure**, and it uses **tools** to do the work. Around that sits a division of labour:

- **The process owner** is accountable for what the instructions say.
- **AI** assembles and updates them, drafting proposed rules with supporting cases attached and non-fitting cases flagged.
- **Engineering** maintains the systems that execute them.

Replaying the telecom engagement under this model: agents read the order history and find the voltage pattern, draft a rule, and attach the evidence. The supply chain owner confirms the rule, marks one group of exceptions as non-compliance and the regional group as legitimate, adds a line explaining why, and approves. The resulting procedure states the general rule, the regional exceptions, and the circumstances that still need human judgment, and it is tested against representative cases before deployment. Note that this is a counterfactual. Alpeza describes how the engagement "could have worked," not a deployment that happened.

### The learning loop

The compounding part is **escalation, resolution, updated procedure**. A request arrives from a region the procedure doesn't cover. The agent escalates. An operator resolves the case and records the reasoning. As similar cases accumulate, agents propose a procedure update with supporting evidence and contradictions. The responsible operator decides which judgments should become standing instructions and approves the change for testing and deployment. Every agent using that procedure inherits the fix. In Alpeza's phrase, "the enterprise now owns the learning loop instead of renting it."

This is a recurring shape across the wiki. [[ai-code-review]] calls encoding a review finding into the coding agent's skills file the highest-leverage move in its workflow, because it converts a one-time catch into a standing constraint. Sierra's experiment with letting its agent "dream" and propose improvements to its own skills ([[company-wide-agent]]) and the research systems in [[self-improving-harnesses]] run the same loop with the agent as its own editor. ContextOps is that loop with two things added: an accountable human approver, and evidence attached to each proposed change. It also fills in a step that [[low-margin-ai-winners]] waves at ("route to a human only when judgment is needed, and learn from the approval feedback over time") and that the article there flags as the place deployments actually succeed or fail.

### Executable coverage

Alpeza's proposed metric is **executable coverage**: the share of cases in a process that an agent can handle correctly using current, approved procedures, without someone supplying missing operating judgment. The test is concrete. Take a representative sample of a hundred equipment requests and count how many meet the standard. If you can't answer for a process you already want agents to run, you don't know how much of your operating model is explicit enough for an agent to use.

This is a candidate answer to the measurement gap Sierra admits in [[company-wide-agent]], where sessions and tool calls are activity and there is no good outcome measure yet. Executable coverage is per-process and sample-based, and it measures the thing the learning loop is supposed to move. It is also, in effect, test coverage for an operating model, with the usual weakness: "handled correctly" needs an oracle, so the number is only as good as the sample and the operator-labelled answers behind it.

### A development life cycle for context

The governance model is borrowed from software. Agent instructions need an owner and a version. Proposed changes come with evidence, are reviewed, tested, deployed, and can be rolled back. You should be able to see which version governed a given agent decision.

Alpeza's caveat is that GitHub is the right model for the discipline and the wrong interface for the user. A proposed rule may be synthesized from decisions by many people across hundreds of cases, and a text diff shows only what changed. To approve it, an operator needs to see the tickets, logs, and judgments behind it: which cases support the rule, which contradict it, and which were one-offs. The reviewable unit is the diff plus its evidence. Edra's product pitch is exactly this: "the GitHub equivalent for operators," one interface to create, review, test, deploy, and improve the instructions behind every agent. He adds a portability requirement, that the instructions must "remain with the company as it changes models, adds agents, and expands into new processes."

Engineers already work this way. [[harness-engineering]] treats the repo as the system of record for agent instructions, and [[claude-code-skills]] are versioned procedures in everything but name. ContextOps is the claim that the same practice should exist for people who don't live in git.

## Reading it against the rest of the wiki

**ContextOps is closer to a governance layer on a context graph than an alternative to one.** The loop's second step is an operator who "resolves the case and records the reasoning." That is a decision record with the why attached, which is what a context graph is supposed to accumulate. What Alpeza adds is promotion: a human decides which recorded judgments become standing rules. So the essay's target is best read as the passive version of the idea, where history is merely connected and retrieved, not the idea of capturing decisions at all.

**It is consistent with the residual-decision-rights argument, and quietly depends on it.** [[messy-jobs]] argues that some human must hold authority over the situations a process doesn't specify, because the institutional machinery of accountability exists only for people. ContextOps doesn't dispute this. It keeps the process owner accountable and amortizes each exercise of that authority: a judgment made once becomes an instruction applied to every later case. The human is not removed from the loop so much as moved from deciding cases to deciding rules. [[ai-and-relational-scarcity]] makes the adjacent point from the labour side.

**It explains steady-state maintenance better than first deployment.** [[agentic-pods]] holds that you can't automate complex workflows by reading documentation; you have to sit next to the people doing the work. [[institutionalized-vs-improvised-software]] adds that the domain expert has the expertise but not the builder's eye to see what is automatable. Alpeza's loop assumes a process has already been chosen, tooled, and given an initial procedure. Someone still has to do that scoping, and it looks a lot like what FDEs do in their first weeks. The stronger form of his thesis is that FDEs should not be needed for the *second and later* revisions, which is a real cost but a smaller claim than the headline.

**"Own the learning loop instead of renting it" is the customer-side counter to lab lock-in.** [[commodity-trap]] lists bespoke FDE deployment as one of the rungs labs climb to escape commodity inference, and names embedding and data gravity among the moats that open up there. A model-independent procedure store, owned by the customer, is precisely what blunts that moat. It also moves the dependency rather than eliminating it: the procedures, their evidence links, and their test cases now live in the ContextOps vendor's system, which is its own kind of data gravity.

## Caveats

This is a single-source vendor essay that ends in a product pitch, and it contains no deployment data. There are no coverage numbers, no before-and-after on FDE hours, and the central example is a hypothetical replay of an old engagement. Treat it as a well-argued framing, not evidence.

Three assumptions carry weight and go unexamined:

- **Operator attention.** The loop moves the bottleneck from engineers to process owners. Agents can generate proposed rule changes far faster than an accountable human can review evidence for them, which is the same fixed human ceiling [[ai-code-review]] identifies for review findings. The essay doesn't say what happens when the proposal queue outruns the approver, or when approval degrades into rubber-stamping.
- **Operator incentive.** Writing your judgment down as standing instructions is how you make yourself less necessary. The essay treats operators as willing teachers. The sentiment data in [[tech-worker-sentiment]] suggests that willingness can't be assumed.
- **Expressibility.** The method requires that operating judgment can be stated as text procedures plus enumerated exceptions. The voltage rule can. Much of what [[messy-jobs]] calls the strong components of a job (handling genuinely novel situations, relational knowledge) may not reduce to "the circumstances that require human judgment" as neatly as a clause in a procedure implies. Executable coverage would reveal this as a plateau, which is an argument for measuring it, and a reason not to assume it trends to 100%.

Executable coverage is also gameable in the usual way. Coverage rises if procedures are written broadly, so the "correctly" in the definition is doing all the work, and it needs an evaluation set the procedure authors don't control.

## Sources

- Alpeza, E. (2026). "The FDE boom is a product gap." <https://x.com/EugenAlpeza/status/2104936003282546913> — [[2026-10-01-alpeza-fde-boom-is-a-product-gap|local copy]]
