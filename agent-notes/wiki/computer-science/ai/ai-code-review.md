---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-05-25-lawson-better-code-more-slowly.md
  - agent-notes/raw/computer-science/ai/2026-07-29-deeplearning-qodo-ai-code-review-overview.md
  - agent-notes/raw/computer-science/ai/2026-07-29-deeplearning-qodo-ai-code-review-best-practices.md
  - agent-notes/raw/computer-science/ai/2026-10-29-osmani-claude-code-team-code-review.md
compiled_at: 2026-10-29
model: claude-fable-5-1
confidence: medium
---

# AI Code Review

Using LLM agents to review code — finding bugs, validating designs, and improving codebase health — rather than (or in addition to) using them to generate code. The same models that produce "slop cannon" PRs when pointed at writing tasks are, when pointed at reading tasks, capable enough to surface real bugs at near-zero false-positive rates *if* the workflow is structured to suppress hallucinations. The contested question is no longer *can agents find bugs* but *how do you prioritize the firehose of findings without drowning*.

Three sources anchor this article from different altitudes: Nolan Lawson's individual-practitioner technique (a cross-model ensemble skill run by hand on your own PRs); DeepLearning.AI's course with **Qodo**, which takes the platform view — what a hosted review agent must do at the org level, and how it fails; and Addy Osmani's October 2026 account of how the **Claude Code team** runs review on a codebase where Claude writes about 90% of the code, which is the operator's view — a team that owns the reviewer, the merge policy, and the revert dashboard, and reports numbers. The three agree on the load-bearing details (severity ranking, human-final-judgment) and diverge on where the bottleneck sits: Lawson says triage, Qodo says context, and the Claude Code team says the bottleneck is *human time*, full stop — the right question is not whether a human read the code but which check, automated or human, is the one that would catch what could go wrong.

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

The Claude Code team measured the same phenomenon from the other side and drew the opposite conclusion (see [[#Review has to converge|convergence]] below): when they ran git blame on what their reviewer kept flagging across rounds, about 59% of it was code that predated the reviewer's first pass. For a solo practitioner on his own repo the side quest is a subsidy; for a team whose unit of work is the merge it is non-termination. The reconciliation is to keep the side quest but move it off the PR's critical path, which is what their nightly review over existing code does at the level of the codebase and what the *Pre-existing* tag on a finding does at the level of a single comment.

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

The Claude Code team's experience adds a fifth failure that the taxonomy cannot express because it is a property of the *loop* rather than of any single review: **non-convergence**, where an agent author and an agent reviewer keep each other busy indefinitely. It does not appear until the author is also an agent, which is why neither Lawson nor Qodo sees it; see [[#Review has to converge]].

## Three best practices

A second Qodo lesson turns the failure taxonomy into workflow prescriptions. Each one attacks a different failure, which is the reason to read them as a set rather than as three tips.

### 1. Review with a harness that did not write the code

The argument is about *optimization target*, not model quality: Claude Code, Codex, and their peers are built and tuned for generation, so asking one to review its own PR gets you a reviewer whose priors are the priors that produced the code. Qodo's presenter demonstrates on a payments PR adding an `under_review` status — Codex, having written the change, catches the central correctness bug (the capture endpoint will still capture a payment that is under review) but stops there. The dedicated review harness catches the same bug plus coding-rule violations (missing docstrings) and breaking changes for downstream services. The line worth keeping is "one useful AI comment shouldn't be the whole review experience."

Two things about the evidence are worth being honest about. The demo is a single PR, and *more findings* is not self-evidently better — a longer list is exactly what the low-precision failure mode looks like from the outside, and the taxonomy in the previous section is the course's own tool for saying so. What the demo does establish is the weaker but still useful claim: the generating agent's findings were a strict subset, so the review agent had recall the generator lacked.

The underlying mechanism is the same one that makes Lawson's ensemble work — independence between the thing being checked and the checker. Lawson gets independence across *models*; Qodo gets it across *purpose-built harnesses*. These are complements, not alternatives, and the harness-divergence argument above says the second is the more durable of the two, since harness scaffolding diverges by design while model behavior converges as capabilities improve. The corollary nobody in either source states plainly: self-review by the generating agent is the one configuration that provides neither kind of independence, and it is also the default in every coding harness that ships a `/review` command.

### 2. Run a pre-PR review before spending human attention

The stated premise is that other developers' attention is expensive, so a PR should not be the first time anything gets checked. The worked example: nine issues on the raw PR (two bugs, two requirements gaps, five cross-repository conflicts, spanning security, correctness, reliability, maintainability). Ask Codex to review its own branch locally first — it surfaces five issues, four P1 and one P2 — apply those fixes, and the same change re-reviewed at PR time carries three issues instead of nine. Those three are the ones local analysis could not reach.

This is the [[stacked-pull-requests|reviewer-attention]] argument again, but applied across *stages* rather than within a report: severity ranking triages a single review's output, while staged review triages which findings ever reach a human at all. Cheap, low-context, local passes absorb the low-severity and locally-visible issues; the expensive stages only see what survives. It also rehabilitates self-review — practice 1 says the generator is a bad final reviewer, and practice 2 says it is a fine *first* one, because a filter that only needs to catch the easy cases does not need independence.

Two cautions the demo glosses. The 9→3 arithmetic is not a controlled comparison — the local pass changed the code, so the second review is reviewing a different diff, and fixes can introduce findings as well as remove them. And the assertion that the surviving three are "higher signal" is a claim about what local analysis *cannot* see (cross-repo conflicts, downstream breakage) rather than something the demo measures. The structural argument holds anyway: findings visible without org-wide context are strictly cheaper to catch before the PR than after.

The Claude Code team runs this practice as the default shape of the pipeline rather than as a tip: the agent runs tests, build, and linter and shows the output, a subagent reviews the diff in fresh context, and a handful of internal skills (bug hunt, simplify, end-to-end behavior check) run — all before a PR exists. Their framing, review as spellcheck while you write rather than a gate at the end of the road, is practice 2 generalized.

### 3. Give the reviewer the task, not just the diff

The third practice is the course's thesis in operational form. Qodo contrasts two Jira tickets for the same change: DX-4, a one-sentence summary with a few notes on expectations, and DX-3, "Prevent capture for payments under manual review," with a purpose, a user story, and a long list of acceptance criteria. Reviewed against the thin ticket, the agent returns four findings, all internal to the code — a missing docstring, a missing enum, a missing web status view, a hard-coded status enum where the rest of the model uses a data type. Reviewed against the thorough one, it returns two **requirements gaps** marked action-required: the PR introduces `under_review`, but an endpoint unconditionally sets status to `captured` and emits a capture event, violating the acceptance criterion that such payments be blocked with a 409. Each gap cites the ticket as evidence.

The important observation is that context did not merely improve the findings — it unlocked a **category of finding that is unreachable without it**. With only the diff, an agent can check code against itself: internal consistency, convention adherence, self-evident bugs. Checking code against *intent* requires the intent to exist somewhere machine-readable. This maps directly onto the four goals: a specless review can serve maintainability, shared knowledge, and much of risk reduction, but correctness-against-requirements is structurally out of reach. It is also why the schema-migration example in that section is the course's sharpest one — the un-backfilled migration is a bug that neither the code nor its tests can reveal, because both encode the same wrong intent, and only an external statement of what was supposed to happen breaks the tie.

Two consequences follow that the source leaves implicit:

- **Ticket quality stops being a courtesy and becomes a machine-checked input.** Acceptance criteria have always been the thing a careful human reviewer silently checked against; making that check automatic and evidence-linked converts vague tickets from a social annoyance into a measurable capability gap. Teams that could never justify the discipline on human-review grounds now have a mechanical reason.
- **Independence has to hold for the spec too.** The presenter notes in passing that agents now write the tickets as well as the code. If the same agent authors both, the requirements-gap check degenerates — you are comparing one generation against another from the same source and the same misunderstanding, which is practice 1's problem relocated one layer up. The check is only load-bearing when the ticket has an independent author, or at minimum a human who reviewed and signed off on the acceptance criteria before code existed. That gate is where the human's residual judgment concentrates.

Taken together the three practices are a pipeline with the failure taxonomy as its design rationale: local self-review for cheap precision, an independent harness for recall, and task context to close the context gap and open the requirements dimension. And practice 3 is the one that cannot be replicated by prompt engineering, which is why it, not the review prompt, is the product.

## The reference architecture

The course's under-the-hood sketch of a hosted review agent, which the rest of the course builds piece by piece:

1. A developer opens a PR, **triggering** one or more agents against the change.
2. Agents **retrieve context** from a knowledge base — the org's docs, standards, tickets, prior sessions.
3. They **analyze the change against that context** to generate candidate findings.
4. The system **synthesizes, ranks, and filters** those candidates.
5. The developer is presented with issues, an explanation of the change, and suggested fixes.

Two things about this shape are worth flagging. First, step 4 is a separate stage from step 3 — candidate generation and triage are architecturally distinct, so the ranking logic can be tuned without touching the finders. That is the platform version of Lawson putting severity ranking in his prompt, and the more robust one: the ensemble's ranking lives inside the same model call that produces the findings, so you cannot adjust the org's tolerance for medium-severity noise without re-prompting every finder.

Second, step 2 is where the knowledge base enters, and it is what makes this an architecture rather than a prompt. Steps 1, 3, 4, and 5 are all commodity — any harness does them. The retrieval layer is the differentiator, and it is the reason review tools are sold rather than written: the diff is public to any tool, but the org's accumulated standards, decisions, and ticket history are not. This is the same wager as [[enterprise-rag-architecture|enterprise RAG]] and, on the vendor-defensibility side, exactly the data-gravity moat that [[commodity-trap]] identifies as one of the few places above the model layer where value can be held.

## Review as a production system: the Claude Code team

Addy Osmani's October 2026 post describes the review pipeline on the Claude Code repositories (the CLI, the desktop and web apps, the mobile apps), where Claude writes about 90% of the code and the volume makes line-by-line human review "incredibly difficult if not impossible." Anthropic's monorepo went from roughly 2,500 changes landing per day in May 2026 to more than 30,000 in September. The post is the third altitude for this article: not a technique and not a product, but the operating policy of a team that owns the reviewer, the merge rules, and the revert dashboard — and that is also the vendor of the review product, which is worth keeping in mind when reading its numbers.

### The objective function

The team's stated reframe is that "did a human read the code?" is an imprecise proxy for "what could go wrong with this change, and which check — automated or human — is the right one to catch it?" Asking the second question moves review from a gate at the end of the road to something that runs continuously, "more like spellcheck while you write": most changes have been reviewed and fixed by Claude at least once before a human is asked to look.

What makes this more than a slogan is that it is written as a constrained optimization. The goal: most PRs merge with at most one human in the loop, who can be the author. The objective: minimize human time, measured as human approvals per PR (median and 95th percentile), human comments, and how long a PR waits on a person. The constraint: revert and incident rates must not rise — "if they rise, we haven't saved human time, we've only moved it." Human time is explicitly defined to include both sides of review's cost, the time spent reviewing and the time spent fixing what bad code breaks, which is the accounting identity that keeps the optimization honest.

Reported outcome: from June to September 2026, merged PRs to the Claude Code codebase more than doubled while the share reverted fell by more than 40%. This is a before/after with no control, from the team that sells the reviewer, during a period when the underlying models also improved; it establishes that the policy did not visibly break the guardrail, not that the policy caused the gain. The same honesty the article applies to Qodo's 9→3 demo applies here.

### Seven layers

The pipeline, in order:

1. **Verification before anyone looks.** Give Claude something it can run — tests, a build, a screenshot against the design — and ask it to show the output rather than say it is done; then a subagent reviews the diff with fresh context. Boris Cherny's estimate, quoted in the post, is that giving Claude a way to verify its work makes the result two to three times better. Internal skills run before the PR: one hunts bugs, one simplifies the diff, one checks behavior end to end; UI changes are checked against design guidelines. This is [[correctness-oracles|oracle]]-first review: the cheapest independent checker is a thing that runs, not a thing that reads.
2. **AI review on every PR.** The reviewer reads the diff against the whole repo and the PR's stated intent and asks whether the change solves its problem, fits the system, or breaks something else; on a bug fix it looks for the root cause. Several agents hunt for bugs in parallel, a separate group **votes on each finding**, and a finding is posted only if enough verifiers agree it is real. Findings that are only style, diagnostics, or cleanup are dropped — filters the team A/B tested on its own PRs before keeping. Survivors appear as inline comments sorted by severity and tagged *Important*, *Nit*, or *Pre-existing*. **Every finding has to be answered**: fix it, or resolve the thread with a reason. When the research preview launched, the share of internal PRs getting substantive comments went from 16% to 54%; most PRs over 1,000 lines get findings and most small ones come back clean. Repos are set to Quick, Standard, or Deep, with Deep reserved for where one missed bug costs more than the extra review time.
3. **Security review that can block.** A separate automated pass. A PR cannot merge while any finding from either review is open; a later commit that fixes the issue clears the finding on its own.
4. **Required CI.** Lint, types, tests on every platform, a build; dozens of checks on a typical CLI PR. The PR template asks how the change was tested and how to undo it — Claude can fill it in, but the person who asked for the change signs off.
5. **Human approval scaled by risk.** Low risk (docs, copy, internal-only features, additive changes behind a flag): no human required once automated review and security are green. Medium (ordinary product changes, and sensitive areas such as caching, the auto-updater, system prompts): one person. High (the highest-risk code plus a small set of paths): two. A classifier reads the change and picks the tier; a second classifier asks whether this particular change needs another person even when its tier says no. Owner-listed sensitive paths and any CI workflow file always need a person.
6. **Merge queue, flags, gradual release.** Every check re-runs against main with the change applied so two PRs that pass separately cannot combine into a broken main; new behavior ships behind a flag to Anthropic employees first; public releases go to `latest` before `stable`.
7. **Fast detection, fast rollback.** Flags turn off without a deploy; a weekly on-call rotation; incident reviews ask *which layer should have caught this*. The team is candid that noticing a bad merge still depends on the author, on-call, and dashboards, and that it does not yet have circuit breakers that tighten approval when revert or incident numbers move — which its engineers want before more code moves to zero-human merges.

Layer 7 is the one that makes the rest affordable. The post's framing — a colleague's line that "slowing down does lower your error rate, but mostly because you're doing less of everything" — is a bet that recovery speed substitutes for prevention depth, and the bet only pays where changes are small, reversible, and behind flags. That is also why the design is less portable than its checklist suggests: a team shipping a database migration or a billing change cannot buy back a missed bug with a flag flip, which is exactly why those paths sit in the high tier.

### Approval rules worth copying verbatim

Four rules in layer 5 do most of the governance work, and each closes a specific hole:

- **The change sets the tier, not the author.** Risk is a property of the diff. But the lighter paths are then gated on a second axis — only authors on the repo's trusted list get them, mostly the team that owns it; everyone else needs a second person — so the real policy is a two-key: change risk × author trust. The post presents the first as the principle and the second as the exception, which is the right emphasis, but the second is doing as much work.
- **An agent's approval never counts as a person's.** Automated review can clear a low-risk change; it cannot fill a slot that calls for a human. This is the line the public Code Review product also holds (it posts findings, not approvals); the team's own repos go further only in letting owners decide which low-risk changes merge on automated checks alone.
- **Whoever prompted the change is on the hook for it.** On an agent-written PR, the person directing the agent counts as one of the required reviewers, as if they had typed the code. This is the operational answer to [[accountability-for-ai-generated-code|Ewerlöf's accountability problem]]: responsibility attaches to the prompter, and the review slot is where it attaches.
- **An approval covers one specific commit.** New commits the system cannot vouch for — an agent's push, a merge resolved by hand — dismiss the approval. Without this rule, layer 2's "an agent picks up the fix overnight" would silently launder unreviewed code through a stale approval.

### Fix it at the source: `CLAUDE.md` and `REVIEW.md`

When the reviewer keeps flagging the same thing, the team fixes it in the skill, a lint rule, or the instructional files rather than in the finding. `CLAUDE.md` says what the project is (stack, conventions, goals, non-goals), is loaded by every review, and is kept short with pointers outward; the reviewer flags both code that breaks a convention in it and changes that make a line in it stale. `REVIEW.md`, written by code owners, says what matters in their part of the code, and the team checks separately whether the reviewer actually follows it. The post's description of a good one is specific enough to be a spec:

- say what failure looks like in that repo (for docs, "it lies"; for config, "it misroutes")
- cap the nits
- list paths to skip
- ask for a file and line as evidence rather than a guess from a name
- ask for a summary that starts with a count and says plainly when there is nothing to fix

Read against Qodo's taxonomy, `REVIEW.md` is the cheap remedy for two of the four failures. *Weak evidence* is fixed by the file-and-line rule. *Context gap* is fixed not by retrieval from Jira and architecture docs but by owners writing down the failure definition — a few hundred words of maintained prose instead of a knowledge base. Qodo's claim that context integration is the product may still hold at the org scale it sells into; the Claude Code team's practice shows how far a repo can get on owner-authored context alone, and it is the same move as [[claude-code-skills|skills]] and [[agent-memory|memory files]]: context that is written, versioned, and loaded rather than retrieved.

### The reviewer has a test suite

The team's method for improving the reviewer is the part of the post with no analogue in the other two sources. **Every incident is an eval.** Past PRs that caused incidents, with their fix-forwards and reverts, were collected; engineers who know the code confirmed each bug and where it lived; the reviewer runs against that set daily. A change to the reviewer — its prompts, tools, or model — is kept if the score goes up and dropped if not. This is hillclimbing with the incident history as the objective, and it means the reviewer is now an artifact with regression tests, maintained the way code is. It is the review-specific instance of the loop [[self-improving-harnesses]] describes in general and [[harness-engineering]] describes for generation: the harness, not the model, is what the team iterates on.

**Noise is measured by what people do with comments.** Every reviewer comment is sorted by the author's response — fixed it, said it was wrong, said the behavior was intentional, decided it did not matter — and the reviewer is also run on PRs known to be clean, counting how often it reports something that would have led someone to make a harmful change. The written priority is catching real bugs first and cutting review rounds second. This resolves the precision/recall trade flagged above in Lawson's ensemble: verifier voting is a *precision* filter applied online, and recall is measured *offline* against the incident set, so the team can tighten the vote threshold without losing sight of what it stops catching. Neither of the other sources has an instrument for the recall side.

The post also names why noise costs more under agent authorship: a person waves off a nit in seconds, while an agent fixes it, which is another commit and another review round. Noise is no longer a reading cost; it is a loop cost.

### Review has to converge

The failure the other sources could not see, because neither runs agent authors against agent reviewers at volume: **an agent author and an agent reviewer can keep each other busy indefinitely.** One CLI PR went through more than fifty rounds of review and fixes overnight before its author stopped it. Git blame on what the reviewer kept flagging showed about 59% was code that had been there since the first pass — the reviewer was not finding new bugs, it was finding a few more old ones each round. The team admits it made this worse by running several rounds by default because each pass caught something. The fixes:

- **A round cap.** After three rounds the reviewer asks the author to step back and reconsider the approach — Lawson's "abandon the PR if the criticals are structural," made automatic.
- **Diff-only re-review** after the first few passes.
- **Flag the class of bug** so the author fixes every instance, not one line.
- **No repeats** of findings already posted.
- **Nightly review over existing code**, so the pre-existing findings have somewhere to go that is not the PR.

Reported results on internal PRs: pass after one review-and-fix round rose from 65% to 78%; PRs needing five or more rounds fell from 8.9% to 1.5%; mean reviews to pass fell from 2.08 to 1.32. The team now tracks rounds-to-pass alongside recall.

The 59% figure is the quantitative version of Lawson's side quest, and the two sources value the same phenomenon oppositely: for Lawson, finding old bugs while reviewing new code is the point; for a team whose unit of work is the merge, it is the thing that stops PRs from terminating. The resolution is not to pick a side but to separate the loops — the *Pre-existing* tag at the level of a comment, the nightly job at the level of the codebase — so that side quests happen without holding the PR hostage. Round caps are the other half: a review loop with two agents in it needs a termination condition that neither agent will supply, and "three rounds, then reconsider" is one.

### What stays human, and the second job of review

The post's list of what people on the team remain responsible for: deciding whether to build it at all (direction, taste, scope — one team that declared its review bottleneck solved still kept human review for changes from outside the team, so someone asks "should we even do this?"); reviewing risky code such as billing, the auto-updater, and CI workflows; reviewing architecture that sets a pattern others will copy; **reading the evidence** — test output, the command that ran and what it returned, a screenshot, the reviewer's findings — with the rule that if you cannot say what the checks would miss, you ask for a real review rather than a quick approval; and owning the outcome. This is the same residual the other sources reach (adjudication, not detection), with one sharper formulation: the human's job is to know what the automated layers *cannot* see, which is a question about the checks rather than about the code.

On review's second job — spreading codebase understanding — the team says plainly it has no formal process. Nobody keeps a complete mental model of Claude Code and the post argues nobody needs to; when someone wants to understand a slice, they ask Claude for an explainer of exactly that slice, which takes minutes and reflects the code as it is today, or have it build a small [[html-agent-artifacts|HTML artifact]] that teaches the slice the way they learn. The claim is that this beats reading trivial diffs — a one-line copy change teaches nothing, an explainer for the module you are about to change teaches a lot — and that working in open Slack channels does the ambient part. This is a pull model of comprehension replacing the push model that diff-reading provided, and it is the team's implicit answer to the *comprehension debt* Qodo names. It is a weaker answer than Lawson's: an explainer is read, a `/grill-me` session is passed, and only the second verifies that understanding landed. Whether pull-based comprehension holds up when the person who would have read the diff never asks is the open question, and the post does not claim to have closed it.

The surrounding norms are what make zero-human merges survivable rather than reckless: changes are small; everything is reversible; blast radius sets the bar; regressions surface fast through telemetry and internal use; "you land it, you own it" means the person with the most context fixes it, and incident reviews look at the system rather than the person. And because code is cheap to write, closing a PR is cheap too — the team's norm is to raise a different direction in the thread early, not as a blocking comment on a finished PR.

### The adoption checklist

The post closes with a sequence most teams can run with today's tools, which doubles as a summary of the layers:

- **Before the PR.** Give the agent checks it can run, listed in a short `CLAUDE.md`, plus hooks for formatters and linters; run `/code-review` and `/security-review` locally or a fresh-context subagent review; add a `REVIEW.md` and move repeated review comments into it.
- **On every PR.** Require CI; add Testing, Risk, and How-to-revert sections to the PR template; add an AI reviewer on one repo and tune `REVIEW.md` for a few weeks before widening; add security review and require every thread resolved before merge; match review depth to risk; cap rounds and re-review only the new diff after the first few.
- **Approval.** Write down risk tiers set from the change rather than the author, start strict and loosen with evidence; keep lighter paths for trusted authors; use CODEOWNERS and branch protection so auth, billing, CI and release workflows, and installers always need a person; never let a bot's approval replace a required human's, and dismiss approvals on new commits.
- **Merge and after.** Merge queue, feature flags, internal use first, staged releases, one-step rollback; turn incidents and reverts into an eval set and rescore the reviewer whenever its prompts, tools, or model change; measure human time with revert and incident rates as the guardrail.

## Implications

- **AI code review is the most defensible AI coding use case.** Even practitioners skeptical of AI-generated code can adopt ensemble review with low risk: the model doesn't ship anything; it just flags. The downside is wasted reviewer time on false positives, which the ensemble suppresses to near-zero.
- **PR review may be where the slop-cannon paradox resolves.** The same tool that lets the slop cannon ship faster also lets the careful reviewer catch the slop. The asymmetry favors defense: the reviewer can pre-filter what the cannon produces.
- **Severity ranking is the load-bearing prompt design.** Without triage, agent output is a firehose. Ranking turns it into a workflow. Future skills that produce structured AI output for human consumption will reach for the same pattern.
- **The "slow down" framing is a hireable taste signal.** A developer who reports using AI to slow down and improve quality is implicitly claiming the senior-reviewer taste needed to know what "better" means. The framing is a credential as much as a technique.
- **The side-quest property is a codebase-health subsidy.** Teams adopting ensemble review on new PRs will accumulate a steady stream of pre-existing-bug fixes as a byproduct. Over time, this is a meaningful investment in codebase health that no one explicitly budgeted for.
- **Context integration, not model quality, is the vendor's moat.** Qodo's stated limitation — a review agent is only as good as its wiring into Jira, agent sessions, architecture docs, and coding rules — is also the reason a hosted product can beat a prompt. Any team can write Lawson's ensemble skill in an afternoon; nobody can retrieve an org's institutional memory in an afternoon.
- **Review findings should flow back into generation.** The loop the course sketches in passing (take the agent's explanation of a security bug, encode it in the coding agent's skills file) is the highest-leverage move in the whole workflow, because it converts a one-time catch into a standing constraint. Review that only gates is strictly worse than review that also teaches the generator.
- **Self-review by the generating agent is the one configuration with no independence at all** — and it is the default that ships in every coding harness. Both sources' techniques (cross-model ensemble, dedicated review harness) are ways of buying independence; the cheapest correct use of the built-in `/review` is as a *pre-PR* filter, where catching the easy cases is all that is asked of it.
- **Review staging is severity ranking applied across time.** Ranking allocates attention within one report; staging decides which findings ever reach a human. Both are consequences of the same fixed human ceiling, and a team can adopt staging without adopting any particular tool.
- **Specs are the input that makes correctness reviewable.** Without a machine-readable statement of intent, an agent can only check code against itself, which caps review at maintainability and self-evident bugs. Requirements gaps are a finding category, not a better version of an existing one — and the most defensible reason to write acceptance criteria has become mechanical rather than social.
- **The spec's independence matters as much as the reviewer's.** Agent-written tickets reviewed by agents against agent-written code is a closed loop with one origin for the misunderstanding. Human sign-off on acceptance criteria *before* implementation is where the residual human judgment has the most leverage, and it costs far less attention than reviewing the diff.
- **"AI writes, human reviews" is a transitional state, not an equilibrium.** The quadrant framing implies the human-only review stage is structurally doomed at AI generation volumes — not because humans are bad at review, but because the ceiling is fixed while the input is not. The interesting question is what the human's residual role becomes, and both sources answer the same way: adjudication, not detection.
- **Write the objective function down.** The Claude Code team's framing turns "should humans read agent code?" from a culture question into a measurable one: minimize human time per change subject to reverts and incidents not rising. Any team can adopt the metric without adopting any of the tooling, and the metric is what tells you whether a lighter review path saved time or merely moved it to the fix.
- **The reviewer needs its own regression suite.** An incident eval turns reviewer tuning from taste into hillclimbing, and it is the only instrument in any of the three sources that measures recall. Without it, every precision filter — severity tiers, cross-model agreement, verifier voting — is a blind trade.
- **Non-convergence is a failure mode of loops, not of reviewers.** Qodo's taxonomy has no entry for it because it does not appear until the author is also an agent. Round caps, diff-only re-review, class-level findings, and no-repeat rules are the four cheapest termination conditions, and a nightly job over existing code is where the pre-existing findings go instead.
- **Recovery depth and prevention depth are substitutes, within limits.** Flags, a merge queue, and one-step rollback are what let the Claude Code team spend less on prevention. Where rollback is not cheap — migrations, billing, installers, CI workflows — the same design says to spend on prevention again, which is what the high tier and the always-a-person paths are.
- **Accountability attaches to the prompter.** "Whoever prompted the change is on the hook" and "an agent's approval never counts as a person's" are the two rules that keep zero-human merges from becoming zero-accountability merges.

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
- [[finding-your-unknowns]] — implementation plans and change-ordered specs as the artifact that gives an agent something to be checked against; the authoring-side supply for practice 3's demand
- [[knowledge-graph-llm-context]] — context engineering in general form, of which pulling the Jira ticket into the review is the narrow case
- [[harness-engineering]] — the OpenAI account of the same "human time is the scarce resource" reframe from the generation side; the Claude Code team's pipeline is the same discipline applied to the reviewer
- [[self-improving-harnesses]] — the incident eval as the review-specific instance of hillclimbing a harness against a held-out score
- [[correctness-oracles]] — verification before review (tests, builds, screenshots the agent must show) as the cheapest independent checker, ahead of any reading
- [[accountability-for-ai-generated-code]] — Ewerlöf's accountability problem and the Claude Code team's operational answer: the prompter fills a required reviewer slot
- [[html-agent-artifacts]] — the explainer-and-artifact answer to review's knowledge-sharing job
- [[claude-code]] — the product whose own repositories are the case study
- [[agent-memory]] — `CLAUDE.md` and `REVIEW.md` as written, versioned, loaded context, the same ladder as memory files
- [[understanding-as-the-bottleneck]] — the rate asymmetry (cheap to produce, slow to understand) that comprehension-on-demand is meant to address, and the open question of whether a pull model closes it

## Sources

- Lawson, N. (2026-05-25). "Using AI to write better code more slowly." <https://nolanlawson.com/2026/05/25/using-ai-to-write-better-code-more-slowly/> — [[2026-05-25-lawson-better-code-more-slowly|local copy]]
- DeepLearning.AI & Qodo (2026-07-29). "AI Code Review — Overview of AI Code Review" (course lesson transcript). <https://learn.deeplearning.ai/courses/ai-code-review/lesson/de16nq/overview-of-ai-code-review> — [[2026-07-29-deeplearning-qodo-ai-code-review-overview|local copy]]
- DeepLearning.AI & Qodo (2026-07-29). "AI Code Review — AI Code Review Best Practices, Part 1" (course lesson transcript). <https://learn.deeplearning.ai/courses/ai-code-review/lesson/79yprh/ai-code-review-best-practices-%E2%80%93-part-1> — [[2026-07-29-deeplearning-qodo-ai-code-review-best-practices|local copy]]
- Osmani, A. (2026-10-15). "How the Claude Code team does code review." Claude Code blog. <https://claude.dev/blog/solving-code-review-at-anthropic/> — [[2026-10-29-osmani-claude-code-team-code-review|local copy]]
