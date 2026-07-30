---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-05-25-lawson-better-code-more-slowly.md
  - agent-notes/raw/computer-science/ai/2026-07-29-deeplearning-qodo-ai-code-review-overview.md
compiled_at: 2026-07-30
model: claude-opus-5[1m]
confidence: medium
---

# AI Code Review

Using LLM agents to review code — finding bugs, validating designs, and improving codebase health — rather than (or in addition to) using them to generate code. The same models that produce "slop cannon" PRs when pointed at writing tasks are, when pointed at reading tasks, capable enough to surface real bugs at near-zero false-positive rates *if* the workflow is structured to suppress hallucinations. The contested question is no longer *can agents find bugs* but *how do you prioritize the firehose of findings without drowning*.

Two sources anchor this article from different altitudes: Nolan Lawson's individual-practitioner technique (a cross-model ensemble skill run by hand on your own PRs) and DeepLearning.AI's course with **Qodo**, which takes the platform view — what a hosted review agent must do at the org level, and how it fails. They agree on the load-bearing details (severity ranking, human-final-judgment) and diverge on where the bottleneck sits: Lawson says triage, Qodo says context.

## What review is actually for

The Qodo course grounds the AI question in a definition of the underlying practice: code review is the examination of a proposed change *before* it enters the main codebase, and its focus is code quality, structure, readability, and standards adherence — incremental source changes pre-merge. The course draws a boundary against quality assurance, which is about product behavior from the end user's perspective: whole features, workflows, integrations, release readiness. Conflating the two is how review scope inflates until nobody can finish one.

Four goals are offered as the yardstick, whether or not AI is involved:

1. **Correctness** — does the code do what it should? The course's worked example: a PR adds a priority field to a form plus a database schema change. It looks fine, but older parts of the app know nothing about the field, so it is a latent breaking change. A good review demands the migration/backfill, default handling, and null-safe logic that make the feature work for *existing* data, not just new rows.
2. **Maintainability** — can the next developer understand and safely change it? The example is a 500-line `app.tsx` doing UI rendering, form state, API calls, validation, table logic, and error handling at once, where a small change breaks unrelated code; the review outcome is decomposition into components, hooks, utilities, and API modules so each file has one job.
3. **Shared knowledge** — a senior reviewer commenting "we usually put server calls in hooks so components stay focused on UI" teaches a convention that propagates to the next similar task.
4. **Risk reduction** — code can be correct and still unsafe. The example is string-interpolated SQL: it works, but it invites injection *and* teaches a bad pattern to whoever copies it; the fix is a parameterized query.

Goals 1 and 2 are exactly the axis [[code-review|Dominus's maintainability thesis]] argues over — he would say Qodo has the priority backwards, since "find bugs" is an unbounded task while "understand this and complain if you can't" is a bounded one. But note that his own preferred failure mode is the second example here (the 500-line god component), and the first (the un-backfilled schema change) is precisely a bug that neither the code nor its tests would flag, because both encode the same wrong intent.

Goal 3 is the one that changes shape most under AI. Traditional knowledge sharing was conversational and synchronous — it required a senior reviewer to be present and inclined to explain. A review agent with a chat interface will answer "what are the risks of this shell command injection in a real user scenario?" on demand and in depth. The course's presenter draws the interesting second-order move: having gotten that explanation, you feed it back into your *coding* agent's skills and Markdown files, so the lesson is enforced at generation time rather than re-litigated at review time. That closes a loop the human-only version never had — a review finding becomes a permanent constraint on future output. It is the same mechanism as [[claude-code-skills|codified skills]], sourced from review rather than from taste.

## The heat map: comprehension debt and rubber stamping

Qodo's framing device is a 2×2 over who writes the code and who reviews it:

- **Human writes, human reviews** — the state of software engineering for decades. Frictional, but the volumes match.
- **Human writes, AI reviews** — a straightforward win; the arduous part of review gets faster.
- **AI writes, human reviews** — the bottleneck quadrant. Thousands of lines per PR, hundreds of PRs a week, against a human capacity the course puts at roughly **400 lines per hour** before attention quality degrades.
- **AI writes, AI reviews (human adjudicates)** — the quadrant the course argues is actually manageable, because generation speed is met with comparable review speed.

Two named pathologies come out of the third quadrant. **Comprehension debt** is a developer progressively losing the ability to understand what is going on in their own codebase because too much of it was machine-written. **Rubber stamping** is the downstream behavior: under pressure to keep the pipeline moving, PRs get approved close to blindly.

The 400-lines-per-hour figure is the load-bearing number, and it deserves scrutiny — it is a widely-circulated industry rule of thumb (traceable to SmartBear's Cisco study) rather than a fresh measurement, and it was derived from human-authored code. There is no particular reason the ceiling holds constant for machine-authored diffs; it plausibly falls, since the reviewer has no prior context from having written it. Either way the argument survives: the human ceiling is roughly fixed while generation throughput is not, so the gap widens on its own.

Worth naming what the fourth quadrant does *not* solve, which the course concedes only in passing: developers can still blindly trust AI output, and AI review of AI code shares failure modes with the generator. The claim is bounded — AI review maintains a *floor* on quality and relieves schedule pressure. It does not restore comprehension. That is the same worry as [[ai-judgment-atrophy]], and it is why Lawson's comprehension-forcing companion practices (below) are not optional garnish.

## Division of labor: what each side is good at

The course's comparison, which lands in the same place Lawson does by a different route:

| | Strengths | Limitations |
|---|---|---|
| **Human** | Nuanced subject-matter expertise within the constraints of the team and company; knows what is best for *this* code and how to change it safely; holds final judgment | ~400 LOC/hour of high-quality attention before decline |
| **AI** | Synthesizes findings and presents them ranked by importance and severity; a run takes ~2–7 minutes even on thousands of lines | Only as good as its context integration — Jira, coding-agent sessions, architecture docs, coding rules |

The prescribed composition: AI as first pass and summarizer, human as final judgment with business context. The payoff is *attention allocation* — you stop treating every PR and every line as equally worthy of scrutiny and spend your attention where the summary says it matters. That is the same insight as severity ranking in Lawson's prompt, arrived at from the org side rather than the prompt-design side, and the same insight [[stacked-pull-requests|stacked PRs]] attacks from the authoring side: reviewer attention is the scarce resource, so either shrink the diff or triage it.

The stated AI limitation is worth dwelling on, because it is where this source most differs from Lawson. Lawson's ensemble sees only the PR diff and the repo; his bottleneck is triage. Qodo's claim is that the bottleneck is **context** — a reviewer that cannot see the Jira ticket does not know what the change was *supposed* to do, and a reviewer that cannot see the architecture docs cannot tell a convention violation from a deliberate exception. This is [[knowledge-graph-llm-context|context engineering]] applied to review, and it is the course's central thesis (the description promises "context is what makes a review reliable").

## The slop-cannon inversion

The cultural default that Nolan Lawson is arguing against: AI coding means low-quality code produced as fast as possible — barely-passable output, massive PRs, merged unvetted. His counter-thesis is that LLMs are flexible enough to power the opposite workflow: writing higher-quality code more slowly than you would without them.

The lever is asymmetric: agents are very good at *finding* bugs, and that capability scales orthogonally to their (more contested) ability to *fix* them well. If you weight your AI usage toward review and validation rather than generation, you get a quality-focused practice that looks nothing like vibe coding. Lawson reports this is closer to how he was already trying to program before LLMs — careful, methodical, quality-obsessed — but supercharged.

This is a sibling stance to [[agentic-engineering]]: where Karpathy and Willison frame the discipline as "preserve the professional quality ceiling at higher velocity," Lawson frames it as "spend the velocity on quality and tolerate slower wall-clock output." Both are reactions to the slop-cannon default; they differ in whether the new affordance is used to ship more or to ship better.

## The ensemble bug-finding skill

Lawson's concrete technique, adapted from a [Milvus blog post](https://milvus.io/blog/ai-code-review-gets-better-when-models-debate-claude-vs-gemini-vs-codex-vs-qwen-vs-minimax.md) on multi-model code-review debate:

> Run a Claude sub-agent, Codex, and Cursor Bugbot to find bugs in this PR ranked by critical/high/medium/low. Once they're all done, review their findings, do your own research to rule out false positives, and write a final report.

Two design choices doing most of the work:

1. **Cross-model ensemble.** Different models hallucinate differently. A bug that only one model flags is more likely a false positive; one that multiple independent models converge on is more likely real. Running Claude, Codex, and Cursor Bugbot in parallel is the cheap version of the Milvus "models debate" insight — pluralism suppresses individual-model error modes without needing the models to actually argue with each other.
2. **Severity ranking baked into the prompt.** Asking for critical/high/medium/low up front means the output is already triaged. You don't get a flat list of 200 issues; you get a stratified list where the top tier is small and the bottom tier is decorative.

Lawson's reported result: "always finds tons of bugs… and the false positive rate is near zero." The bugs span the full severity spectrum, from security/correctness criticals down to "this comment is misleading" lows. The volume is the problem: you'll be "bored senseless" if you try to address them all.

Customization vector: the skill accepts a personal definition of "bug." Lawson's includes [KISS](https://en.wikipedia.org/wiki/KISS_principle), [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), accessible HTML/JSX, and proper SQL indexes — i.e., his own code-review style turned into a checklist the ensemble enforces. The skill is a vehicle for codifying a senior reviewer's taste so it gets applied at scale to every PR.

## The triage workflow

Once the findings exist, the human's job is allocation, not detection. Lawson's three rules:

- **Burn down criticals and highs in a loop.** Direct an agent to fix all critical/high findings with your guidance on the *right* solution, then re-run the ensemble. Repeat until the top tiers are clear. The human stays in the design seat; the agent is the implementer.
- **Skip findings where the juice isn't worth the squeeze.** A high or medium that requires 100 lines of code to patch a narrow edge case may not be worth the change. Severity is a guide, not a mandate.
- **Abandon the PR if the criticals are structural.** A flood of critical findings is signal that the whole approach is misguided, not that you have a lot of patching to do. The skill becomes a kill switch on bad designs before merge.

This is a markedly different relationship to AI output than the slop-cannon mode. The agent's output is treated as a *prosecutor's case file*, not a deliverable: you read it, weigh it, and decide what to do with each finding. The human supplies the judgment that the model lacks.

## The pre-existing-bug side quest

The most surprising side effect Lawson reports: running ensemble review on a new PR routinely surfaces bugs that *predate* the PR — flaws in code the PR merely touches. The review process becomes a discovery mechanism for latent issues, not just an audit of new changes.

The consequence is that the workflow doesn't reliably speed you up; if anything, it slows you down by adding tangential side quests of writing unit tests and fixing subtle pre-existing flaws. Lawson reports finding this satisfying — it improves codebase health while teaching him the codebase's failure modes. His pre-LLM mental model: the happy path of a complex architecture is less interesting than its failure modes, and getting your hands dirty fixing edge-case bugs was always how he got familiar with a system.

This connects to [[ai-judgment-atrophy]] from the opposite direction. Heron warns that AI removes the friction that builds judgment; Lawson's workflow deliberately reinvests AI's velocity gains into *additional* friction — the kind that builds understanding of the codebase's weak points. The slow-and-careful style isn't anti-AI; it's anti-shortcut.

## Companion practices: forcing comprehension

The bug-finding skill is one half of Lawson's recommendation. The other half is using agents to make sure you actually understand the code you're shipping:

- **Ask the agent how the PR works and how it might fail.** Treat the agent as a Socratic partner that walks you through the code's behavior and edge cases.
- **Have it write Markdown docs with [Mermaid charts](https://mermaid.ai/open-source).** Forcing the agent to diagram the change exposes structure that a flat code review would miss.
- **Use [Matt Pocock's `/grill-me`](https://www.aihero.dev/my-grill-me-skill-has-gone-viral) skill** to be interrogated about the PR until you can answer questions front-to-back. The agent stress-tests your mental model rather than building it for you.

The unifying principle: the agent is positioned to *deepen* the human's understanding, not to substitute for it. This is the practical instantiation of Karpathy's "you can outsource your thinking but not your understanding" line in [[agentic-engineering]].

## Why ensemble review works: the harness perspective

The ensemble approach exploits an architectural property of [[ai-coding-harnesses|coding harnesses]]: each harness (Claude Code, Codex, Cursor Bugbot) wraps its model with different system prompts, tool definitions, and search backends. Even when two harnesses run the same underlying model, the harness scaffolding biases what gets surfaced. Running three different harnesses against the same PR is, in effect, three different reviewers — not just three samples from one distribution.

This also implies the technique is robust to model improvement: as individual models get better at single-pass review, the ensemble's marginal value shrinks but doesn't disappear, because the harness-induced divergence remains. The bet is structural, not contingent on any particular model generation.

## Cost and constraints

Lawson notes the technique can burn "a ton of tokens just to find out that your entire plan was wrongheaded from the start." That's a feature in his framing — early detection of a bad design is cheaper than building on it — but it's a real cost. Three-model ensemble review on every PR is not free; the workflow makes sense for codebases where the cost of a bad merge dominates the cost of compute.

Two boundary conditions worth naming, even though Lawson doesn't:

- **Verifiable domains amplify the value.** Per [[agentic-engineering]]'s verifiability framing, bug-finding is exactly the kind of task where RL-trained models excel: there's a checker (does the bug reproduce?) and the reward is clean. Code review sits inside the RL distribution.
- **Aesthetic and design-level critique is weaker.** The same framing predicts the ensemble will miss "this abstraction is wrong" or "this name is bad" findings — the taste axis Karpathy flags as the human-defended bottleneck. Use the ensemble for correctness, not for design.

## Four ways a review agent fails

Qodo's most portable contribution is a failure taxonomy — the vocabulary for saying *how* a review tool is bad, which matters because all four failures present identically to the user as "I don't trust this thing":

- **Low precision** — the findings are nitpicks rather than important callouts. The reviewer learns to skim, and the tool's real findings get skimmed too.
- **Low recall** — the tool misses issues a human would have caught. Worse than useless if it induces the false confidence that the PR was checked.
- **Weak evidence** — findings that don't point at specific lines or at the relevant docs. Without a citation, the developer has to redo the analysis to evaluate the claim, which costs more than not having the finding.
- **Context gap** — the tool's picture of your standards is stale, so it enforces a convention you abandoned or misses one you adopted.

The taxonomy pays off because the four have *different* remedies, which is exactly what a single "trust" metric obscures. Precision is a ranking and filtering problem (Lawson's severity tiers, or the ensemble's cross-model agreement as a confidence signal). Recall is a coverage problem — more passes, more lenses, more finders. Evidence is an output-format requirement, and the cheapest of the four to fix: mandate file/line citations and the tool becomes auditable. Context gap is the only one that is an *integration* problem rather than a model or prompt problem, and it is the one that gets worse with time rather than better with model upgrades. A review agent left alone drifts, not because the model degrades but because the codebase's standards move underneath it.

Note the tension with Lawson's ensemble: cross-model agreement raises precision by discarding findings only one model flags, which is a recall trade. Qodo's taxonomy lets you see it as a trade rather than a free lunch. Which side to err on is a property of the codebase — the ensemble's near-zero false-positive rate is bought with silent misses, acceptable when reviewer attention is the scarce resource and unacceptable in a security-critical path.

## The reference architecture

The course's under-the-hood sketch of a hosted review agent, which the rest of the course builds piece by piece:

1. A developer opens a PR, **triggering** one or more agents against the change.
2. Agents **retrieve context** from a knowledge base — the org's docs, standards, tickets, prior sessions.
3. They **analyze the change against that context** to generate candidate findings.
4. The system **synthesizes, ranks, and filters** those candidates.
5. The developer is presented with issues, an explanation of the change, and suggested fixes.

Two things about this shape are worth flagging. First, step 4 is a separate stage from step 3 — candidate generation and triage are architecturally distinct, so the ranking logic can be tuned without touching the finders. That is the platform version of Lawson putting severity ranking in his prompt, and the more robust one: the ensemble's ranking lives inside the same model call that produces the findings, so you cannot adjust the org's tolerance for medium-severity noise without re-prompting every finder.

Second, step 2 is where the knowledge base enters, and it is what makes this an architecture rather than a prompt. Steps 1, 3, 4, and 5 are all commodity — any harness does them. The retrieval layer is the differentiator, and it is the reason review tools are sold rather than written: the diff is public to any tool, but the org's accumulated standards, decisions, and ticket history are not. This is the same wager as [[enterprise-rag-architecture|enterprise RAG]] and, on the vendor-defensibility side, exactly the data-gravity moat that [[commodity-trap]] identifies as one of the few places above the model layer where value can be held.

## Implications

- **AI code review is the most defensible AI coding use case.** Even practitioners skeptical of AI-generated code can adopt ensemble review with low risk: the model doesn't ship anything; it just flags. The downside is wasted reviewer time on false positives, which the ensemble suppresses to near-zero.
- **PR review may be where the slop-cannon paradox resolves.** The same tool that lets the slop cannon ship faster also lets the careful reviewer catch the slop. The asymmetry favors defense: the reviewer can pre-filter what the cannon produces.
- **Severity ranking is the load-bearing prompt design.** Without triage, agent output is a firehose. Ranking turns it into a workflow. Future skills that produce structured AI output for human consumption will reach for the same pattern.
- **The "slow down" framing is a hireable taste signal.** A developer who reports using AI to slow down and improve quality is implicitly claiming the senior-reviewer taste needed to know what "better" means. The framing is a credential as much as a technique.
- **The side-quest property is a codebase-health subsidy.** Teams adopting ensemble review on new PRs will accumulate a steady stream of pre-existing-bug fixes as a byproduct. Over time, this is a meaningful investment in codebase health that no one explicitly budgeted for.
- **Context integration, not model quality, is the vendor's moat.** Qodo's stated limitation — a review agent is only as good as its wiring into Jira, agent sessions, architecture docs, and coding rules — is also the reason a hosted product can beat a prompt. Any team can write Lawson's ensemble skill in an afternoon; nobody can retrieve an org's institutional memory in an afternoon.
- **Review findings should flow back into generation.** The loop the course sketches in passing (take the agent's explanation of a security bug, encode it in the coding agent's skills file) is the highest-leverage move in the whole workflow, because it converts a one-time catch into a standing constraint. Review that only gates is strictly worse than review that also teaches the generator.
- **"AI writes, human reviews" is a transitional state, not an equilibrium.** The quadrant framing implies the human-only review stage is structurally doomed at AI generation volumes — not because humans are bad at review, but because the ceiling is fixed while the input is not. The interesting question is what the human's residual role becomes, and both sources answer the same way: adjudication, not detection.

## Connections

- [[agentic-engineering]] — Lawson's slow-coding stance is a quality-spending variant of the agentic-engineering discipline; both are reactions to the slop-cannon default, but allocate the velocity gain differently
- [[ai-coding-harnesses]] — the ensemble technique exploits harness-induced divergence between Claude Code, Codex, and Cursor Bugbot even when underlying models overlap
- [[ai-judgment-atrophy]] — Heron's warning about AI eroding the friction that builds judgment; Lawson's workflow is a counter-pattern that reinvests AI velocity into additional friction, and comprehension debt is the same erosion seen from the review side
- [[generative-ai-as-pattern-generation]] — Evans's error-tolerance framing predicts code review (high tolerance for false alarms when triaged by humans) is a structurally good fit for current AI
- [[code-review]] — Dominus's maintainability-first thesis, the human-only baseline this article's AI workflows are layered on top of
- [[stacked-pull-requests]] — the authoring-side attack on the same scarce resource (reviewer attention) that severity ranking attacks on the reading side
- [[judgment-in-ai-assisted-development]] — the general form of the human-as-adjudicator conclusion both sources reach
- [[unattended-coding-agents]] — the generation volumes that make the "AI writes, human reviews" quadrant untenable
- [[enterprise-rag-architecture]] — the retrieval layer that step 2 of the reference architecture depends on
- [[commodity-trap]] — data gravity as one of the few defensible positions above the model layer; the review agent's knowledge base is a worked instance

## Sources

- Lawson, N. (2026-05-25). "Using AI to write better code more slowly." <https://nolanlawson.com/2026/05/25/using-ai-to-write-better-code-more-slowly/> — [[2026-05-25-lawson-better-code-more-slowly|local copy]]
- DeepLearning.AI & Qodo (2026-07-29). "AI Code Review — Overview of AI Code Review" (course lesson transcript). <https://learn.deeplearning.ai/courses/ai-code-review/lesson/de16nq/overview-of-ai-code-review> — [[2026-07-29-deeplearning-qodo-ai-code-review-overview|local copy]]
