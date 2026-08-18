---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-08-11-ai-removing-middle-class-software-engineering.md
compiled_at: 2026-08-16
model: claude-opus-5
confidence: medium
---

# Understanding as the bottleneck

The thesis that AI has made **producing** software changes cheap and fast while **understanding** them remains slow, difficult human work — and that this single rate asymmetry, not any property of the models, is what determines whether an AI-heavy engineering org compounds value or compounds mess.

Florian Herrengt's August 2026 essay "AI is removing the middle class of software engineering" is the sharpest statement of it. His one-line version: **AI makes projects with weak engineering culture fail much faster.** The failure mode is not new; the *speed limit* on it is gone.

## The rate asymmetry

Herrengt's mechanism is deliberately unglamorous, and it is the load-bearing part of the argument:

- **Generation rate** — a person can now produce 20,000 lines of working code in an afternoon. A 25,000-line PR arrives Monday morning; a team can ship more change over a weekend than it used to over weeks.
- **Comprehension rate** — unchanged. Building a correct mental model of what a change does is still slow, still serial, still human. "We have no shortcut for building a correct mental model of what a change does. Maybe one day we will find one. As of today, I do not think we have one."
- **Repair rate** — also unchanged, and worse than comprehension because repair is gated by the physical world. His worked example: an LLM adds a batch of tables and columns in ten minutes. Removing them once data lives in them requires a migration plan, a failure plan, orphaned-FK checks, and zero disruption to paying users. "The speed at which bad decisions compound has changed completely while the speed at which you can fix them has not."

The compounding follows directly: *by the time you've untangled one bad decision, five more have been merged.* This is the crux — the org is not merely accumulating debt, it is accumulating it faster than the payoff channel can drain it, which is a solvency condition, not a quality complaint.

The credit-card framing is his: "You don't see the debt. You just see the car that looks great." The tragedy, he argues, is that **to the untrained eye it works** — pull the branch, test it, and you get something functional, which is exactly the signal that licenses another round.

## Why the existing process controls don't hold

The most useful section is his answer to "just fix your process," because it is the objection most engineering leaders will reach for first.

His claim is not that tests, CI, code review, and architecture review disappeared. It is that **the difficulty of producing code was itself one of the limiting factors**, and every one of those controls was calibrated against it:

- **Code review** was sized for human-authored volume. It does not survive ten PRs a day each carrying an AI-generated description. This is the [[code-review]] legibility check pushed past its budget, and the reviewer-attention scarcity that [[stacked-pull-requests]] attacks from the authoring side.
- **Tests** cover the behaviours you thought to test. They do not catch the behaviours nobody thought to test — and an agent introducing abstractions you did not ask for is generating precisely the untested-thought category. "How many times have you had a completely green CI with full coverage and still shipped a bug?"

His conclusion is a clean trilemma. If the people who understand changes and guard quality are now the bottleneck, you have exactly three options: **generate less, find a genuinely better way to validate, or accept lower quality.** Most orgs are choosing the third by default, without noticing they chose.

## Design-decision provenance disappears

A second failure Herrengt identifies is subtler than volume: the *record of why* evaporates.

His scene — asking why some code exists, receiving a link to a Claude conversation, "which part should I read?" / "probably all of it" — names a real artifact problem. A chat transcript in which the model recommends an architecture, apologises, reverses itself, and iterates fifteen more times technically contains the design decision, but it is unsummarizable, unindexed, and indistinguishable from the fifteen rejected alternatives. It has the form of documentation and none of the function.

He anticipates the standard rebuttal ("nobody ever fully understood large systems anyway") and answers it precisely: you were never expected to understand every service, **but at least someone did, and would explain it to you.** The change is not the loss of universal comprehension — that never existed. It is the loss of the *someone*. When the person who built a feature last week asks an LLM where its data comes from, the org has no comprehension floor at all.

This is the practical argument for the artifact discipline in [[spec-driven-development]] and for the plan/deviation-log habits in [[finding-your-unknowns]]: a checked-in spec is the durable form of the thing a chat log only pretends to be.

## The compiler objection, and where it fails

The strongest technical objection Herrengt takes on: we already trust compilers to emit machine code we never read, so why is unread AI output different?

His answer is the cleanest distinction in the piece. **A compiler is a deterministic, semantics-preserving translator. It does not decide what your system should do.** An LLM asked to build a feature is not translating intent into code; it is making dozens of design decisions on your behalf — choosing architectures, picking abstractions, deciding where things live. Those are the decisions the reviewer is nominally accountable for.

He states the falsification condition explicitly, which is rare for this genre: *if in five years I can give an agent a complete specification and reliably verify the resulting code against it, reviewing code may become obsolete and I would happily stop.* The claim is about today's verification tooling, not about model capability in principle — and it is therefore the thing to actually watch. Every advance in machine-checkable specification moves the argument.

## The productivity-transfer argument

Herrengt's second-most-portable idea is that headline output metrics can hide a *negative-sum transfer*:

> The supposed 10x engineer may simply be someone stealing productivity from everyone around them.

Ten PRs in a day that cost three engineers two days each of reviewing, correcting bad assumptions, debugging regressions, and re-doing half of it is not 10× productivity — it is the same work relocated onto other people. And the people it lands on are, by construction, the ones whose attention is scarcest and who are hardest to replace.

The corollary is a measurement warning: PR count, lines changed, and features "completed" were always weak proxies, but AI has made them *individually gameable while team throughput falls*. He concedes the organizational-incentives version of the point without hedging — where ticket count is rewarded over quality, the careful engineer looks like the bad employee and the sloppy one gets promoted. That is a strictly organizational failure, and it means the fix is not available to the individual engineer holding the line.

## The labor-market claim

The essay's title claim is the least-evidenced part, and Herrengt presents it as a bet rather than a finding: **AI pushes engineering salaries further apart.**

The argued chain:

1. Implementation is cheap; you are paid for good decisions and for managing complexity.
2. The employability bar is now "whatever the current best model can do" — you must contribute beyond what anyone gets from a prompt.
3. Good engineers get more valuable, because AI lets them move faster *without* needing as many people around them purely for implementation.
4. Bad engineers get more expensive, because their blast radius per day grew and the review capacity to contain it did not.
5. Therefore the middle thins: money funnels to a shrinking set of people who can actually be trusted, and those who can't get much cheaper or get replaced.

His supporting argument is a good one and worth separating from the prediction: *if all companies needed was someone to turn a specification into working code, why were they ever paying London and San Francisco salaries when that was already cheaply available elsewhere?* The premium was never for typing. It has always been for the judgment — which is the same conclusion [[judgment-in-ai-assisted-development]] reaches from the tooling side and [[expertise-as-llm-leverage]] reaches from the prompting side (domain expertise is what makes the model useful, and it is not transferable via the prompt).

He extends the bet to knowledge work generally, on the same mechanism: previously someone would likely catch a bad decision before it went too far; now decisions arrive faster than the people around them can review or understand.

**Where to be skeptical.** The prediction is compatible with the essay's own evidence but not implied by it. The mechanism established is *comprehension capacity is the binding constraint*; the leap to *therefore wage dispersion widens* assumes firms can identify who has the judgment — the exact discrimination problem the essay elsewhere says is now harder, since output volume no longer signals competence and may anti-signal it. Herrengt is also describing a labor market from inside it, and the thesis flatters the reader who has read this far. Compare [[decide-execute-deliver-sandwich]], where Narayanan argues that AI compresses only the middle of the decide-execute-deliver sandwich and that the layoff narrative is substantially "AI washing" — that is the *volume* rebuttal, not a rebuttal of the comprehension-rate mechanism, and the two can both be true. [[messy-jobs]] and [[labor-share-under-automation]] are the economics-side treatments of whether the bundle actually separates.

## The junior-developer inversion

The most quotable reversal in the essay, and the one with the most direct managerial consequence: Herrengt reports that the two junior developers he rates highly are good *precisely because* they use AI to increase understanding — exploring what they don't know, clarifying their reasoning, double-checking assumptions — while senior developers he has worked with "basically gave up and stopped trying to understand the code" and became much worse engineers as a result.

His framing: **the problem is not AI, it is using AI as a substitute for understanding rather than a tool for building it.** Seniority does not predict which side of that line you land on. This is [[ai-judgment-atrophy]]'s friction-erosion argument observed in the field, and it is the empirical case for the guardrails in [[vibe-coding-apprenticeship]] (explain-before-commit, AI-free debugging, graduated autonomy) — which turn out to be a description of what his good juniors do unprompted.

On the pipeline question ("how do we make more senior devs if we don't hire juniors?") he concedes the industry is sabotaging its own future, declines to treat that as actionable ("the industry does not really owe people opportunities"), and gives a career-strategy answer instead: **maintenance is the essence of the software industry**, LLMs cannot modify projects spanning hundreds of thousands of lines, and the skill of partitioning architectures is still entirely human — so learn that. Note that this claim is the one most exposed to model progress; it is a statement about 2026 context windows and agent reliability, not a structural truth. It sits against the trajectory in [[unattended-coding-agents]].

## What the essay does not claim

Worth stating explicitly, since the argument is easy to flatten into anti-AI sentiment, which it isn't:

- **Not that AI-generated code is bad.** Herrengt ships mostly AI-written code himself. "If you are shipping AI code and you genuinely understand the system, you are doing it right. The article is not about you."
- **Not that technical debt is bad.** Intentional debt with a known trade-off and a payoff plan is fine. The distinguishing property is *knowing it's a shortcut* — the failure is unpriced debt, not debt.
- **Not that large PRs are inherently wrong.** The claim is a bet about the modal case: for very large AI-generated PRs, the person opening it does not understand all of it.

## Implications

- **The reviewer's refusal is a real control, and it is the cheapest one.** Herrengt distributes blame across the whole cast, and the reviewer's share is *giving in* — agreeing to review something they cannot actually review. A team norm that a PR above some size gets returned unread converts an unbounded attention drain into a bounded one, and it requires no tooling. It is also the norm most likely to get you labelled toxic, which he addresses directly: flexibility on business trade-offs, but a backbone when something will cause real problems.
- **"Can you explain where the data comes from?" is a usable competence probe.** Unlike lines shipped, it is not gameable by generation volume, and it tests exactly the quantity the essay says is now scarce. The failure mode it detects — reaching for the model to explain code you wrote last week — is legible in seconds.
- **Comprehension capacity is now a planning input, not a cultural virtue.** If review-and-understand throughput is the binding constraint, then generation volume is something to *budget*, the way [[choose-boring-technology]] budgets innovation tokens. Teams that treat agent output as free are mis-costing the only scarce resource they have.
- **Independent verification is the only escape from the trilemma that doesn't cost quality or speed.** "Generate less" and "accept lower quality" are both concessions; "find a genuinely better way to validate" is the option that dissolves the constraint — which is why machine-checkable specs, the ensemble review workflows in [[ai-code-review]], and the environment-design discipline of [[harness-engineering]] are load-bearing rather than nice-to-have. Herrengt's own falsification condition is stated in exactly these terms.
- **Systems built past the comprehension horizon may be unmigratable, not just unmaintainable.** [[software-migrations]] treats large-scale migration as the only scalable mechanism for retiring cross-cutting debt — but every technique there assumes someone can characterize the current state. A codebase nobody understands cannot be derisked, which removes the standard remedy rather than merely making it expensive.

## Caveats

Single-source, opinionated, and anecdotal throughout: the numbers (25,000-line PRs, 10 PRs/day, 20,000 lines in an afternoon) are illustrative rather than measured, and the central scene is a composite. The essay's own appended objections do most of the adversarial work, which is unusual and to its credit, but it is still one practitioner's read. The rate-asymmetry mechanism is the part that generalizes; the salary-bifurcation prediction is a bet, and the "LLMs cannot modify large projects" premise is a snapshot claim with a short half-life.

## Sources

- Herrengt, Florian (2026-08-11). "AI is removing the middle class of software engineering." <https://blog.florianherrengt.com/ai-removing-middle-class-software-engineering.html> — [[2026-08-11-ai-removing-middle-class-software-engineering|local copy]]

## Connections

- [[judgment-in-ai-assisted-development]] — the same "judgment is the binding constraint" conclusion reached from the tooling side; this article supplies the rate-asymmetry mechanism that makes it binding
- [[ai-code-review]] — the review-side treatment, including *comprehension debt* and *rubber stamping* in the AI-writes/human-reviews quadrant against a fixed human LOC/hour ceiling; the concrete answer to Herrengt's "find a better way to validate"
- [[ai-judgment-atrophy]] — Heron's friction-erosion thesis at the individual level; Herrengt's senior-developers-who-gave-up are the field observation
- [[code-review]] — the legibility framing ("understand this, complain if you can't") that Herrengt's reviewer is being asked to abandon
- [[stacked-pull-requests]] — the authoring-side discipline that keeps changes inside the comprehension budget, and the direct counter to the 25,000-line PR
- [[internal-software-quality]] — the cost model underneath the credit-card metaphor: cruft slows teams in weeks, not months
- [[software-migrations]] — the standard remedy for cross-cutting debt, and the one that stops working once nobody can characterize the system
- [[expertise-as-llm-leverage]] — why domain expertise is the non-transferable input; the positive statement of what Herrengt says the middle is losing
- [[decide-execute-deliver-sandwich]] — Narayanan's counter on the employment consequences: AI compresses only the execute layer and the layoff stories are partly AI-washing
- [[vibe-coding-apprenticeship]] — the guardrails that produce Herrengt's good juniors deliberately rather than by disposition
- [[spec-driven-development]] — checked-in specs as the durable artifact a Claude-conversation link only imitates
- [[unattended-coding-agents]] — the generation volumes that make the comprehension constraint acute, and the trajectory that pressures his maintenance-is-still-human claim
- [[agentic-engineering]] — the discipline whose whole point is that code is cheap but verification isn't; Herrengt is the failure case when only the first half is adopted
- [[harness-engineering]] — designing the environment so the agent's output is legible and constrained; the systemic version of "generate less"
- [[choose-boring-technology]] — innovation tokens as the prior art for budgeting a scarce comprehension resource; the Kafka-with-no-justification example is an unbudgeted spend
- [[wrong-abstraction]] — what an agent introducing unrequested abstractions produces, and why duplication would have been cheaper
- [[tech-worker-sentiment]] — the large-N sentiment data on the same experience: burnout 44.7%→54.7% in a year with throughput up and effort flat
- [[messy-jobs]] — Garicano's supply-side account of when AI actually substitutes for a job bundle, the economics-side test of the bifurcation bet
- [[labor-share-under-automation]] — the factor-shares treatment of where the value goes if the bet is right
- [[product-management-in-the-ai-era]] — the same judgment-becomes-the-bottleneck sorting playing out in an adjacent function
