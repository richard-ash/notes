---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-09-20-software-factory-experiment.md
compiled_at: 2026-09-24
model: claude-fable-5-1
confidence: medium
---

# Software Factory Pattern

The **software factory pattern** is running an agent harness in a loop against a *goal* rather than a *task*: the human states what a project is trying to achieve and how success is measured, and the harness is responsible for figuring out which work is missing, doing the unblocked work, and re-checking direction as it goes. Will Larson's (CTO of Imprint) definition is compact — "looping on a broad goal, and then relying on the harness to drive progress towards that goal" — and his September 2026 post is a first-pass field report on adopting it at Imprint.

Larson attributes the AI-context usage of the term, tentatively, to Justin McCarthy's February 2026 essay *Software Factories And The Agentic Moment*, published by StrongDM. That is the same company whose no-one-reads-the-code verification regime Simon Willison calls the **dark factory** (see [[agentic-engineering]]). The two ideas are siblings but address different problems: the dark factory is about *trusting* unread code (a verification problem), while the software factory is about *steering* autonomous work toward a goal (a direction problem). A team can run one without the other.

## Where it sits in the autonomy ladder

Each rung of coding-agent autonomy moves the human one level up the abstraction stack:

| Rung | Human supplies | Agent supplies | Wiki article |
|---|---|---|---|
| Interactive | Each instruction | Code | [[claude-code]], [[agentic-engineering]] |
| Task-level unattended | A ticket | A PR | [[unattended-coding-agents]] (Stripe's Minions, Chris Wood's loop) |
| Goal-level factory | A goal + a metric | The task list, the PRs, and the re-plan | this article |

Larson's diagnosis of why the middle rung was insufficient is the crux of the post: he was already pointing agents at specific Linear projects, "but they didn't have the ability to evaluate if they were going in the right direction, or if it was missing necessary tasks." Task-level agents execute a backlog; a factory *maintains* one. That is what distinguishes the factory from simply queueing many tickets into an orchestrated harness like Imprint's Agent Fleet or Stripe's Minions.

## Imprint's first implementation

The whole thing is one agent skill, `/linear-project-loop`, which Larson describes as "fairly basic." It takes a Linear project and runs four steps:

1. **Audit the goal definition.** Check that the project has (a) an RFC in Notion describing the goals, how they are measured, and the general approach, and (b) a Datadog dashboard or Snowflake queries that measure progress against those goals. If either is missing, or the Linear project itself does not exist, the skill iterates *with the human* to create them. It does not proceed on an ill-defined goal.
2. **Reconcile state.** Review the metrics and the project's issues. Add issues for newly identified work; update issues whose state has moved.
3. **Do the unblocked work.** Write a PR, update a PR, ping for review, ask a clarifying question — whatever the project's current state calls for.
4. **Decide whether to re-plan.** When a task completes, take the next task if the project description is fresh. If the description "hasn't been updated in a while," go back to step 1.

Two design details are worth noticing. First, the re-plan trigger is **staleness of the project description**, not metric movement or task-count thresholds. That is a cheap heuristic that effectively gives every plan a time-to-live, after which the loop re-audits goals before continuing. Second, step 1 is a **precondition, not a nicety**: the factory refuses to run without a written goal and a measurable target, which turns the pattern into a forcing function for project legibility. Larson reports this bit as the most personally useful — it exposed "the places where I was accidentally hording parts of the state for myself regarding the goals of the project."

Larson is running the loop in a local harness as of publication, but says it works well enough that he expects to move it into Agent Fleet, the same orchestrated harness Imprint uses for one-off tasks. That would make the factory a persistent process rather than something a human kicks off.

## Post-release mode

A second use Larson highlights is running the factory at low frequency against projects that have *already shipped*. His example is Imprint's passkeys implementation: months pass without anyone checking on it, so an adoption spike or a rising error rate could go unnoticed. Because the factory's first two steps are "find the metrics" and "compare them to the goal," a post-release cadence turns the loop into an owner-of-record for finished work — one that notices drift and opens issues before a human would.

This is a partial answer to a problem Larson raised in [[ai-era-engineering-leadership]]: durable teams matter more in the AI era precisely because someone has to hold context on a system after it ships. The factory does not replace that team, but it automates the check-in habit that busy teams drop first.

## The compounding stack

Larson's closing observation is that each piece "compound[s] only to the extent that you have the other pieces." His own adoption timeline at Imprint reads as a dependency chain, where each migration unblocked the next:

| When (2026) | Move | What it unblocked |
|---|---|---|
| January | Every engineer on Claude Code daily | Baseline agent fluency |
| March | Everyone else on Claude Code or Claude Cowork | Non-engineering work agent-addressable |
| April | ~10 local workspaces, each with an independent checkout of *every* repo; operate at workspace level, not repo level | Cross-repository PRs across frontend, backend, infra, and data monorepos |
| June | Company-wide move from Jira to Linear, hard stop | A single source of state for work, with better visibility and less permission complexity |
| July | Agent Fleet, an orchestrated harness modeled on Stripe's Minions | Trivial tickets handled without local development |
| September | `/linear-project-loop` | Goal-level loops |

The factory specifically requires three of these to already exist: **measurement** (Datadog MCP and Snowflake access, so the loop can read progress), **a single source of work state** (Linear, so the loop can read and write the backlog), and **execution independent of a laptop** (the orchestrated harness, so the loop can run continuously). Larson notes the Linear migration in [[ai-era-engineering-leadership]] as motivated by MCP and Slack integration; this post shows what it was for. Keeping up with this many migrations is, in his words, "a fascinating industry moment" — the same author's [[software-migrations]] playbook now applies to tooling that turns over in months rather than years.

## Implications

- **Each autonomy rung raises the bar on organizational legibility.** A task-level agent needs a well-written ticket. A goal-level agent needs a written goal *and* a metric that a machine can read. Companies without RFCs and dashboards cannot run a factory, and step 1 of Larson's skill is a polite way of refusing to. This echoes [[spec-driven-development]]'s "the spec is the source of truth," lifted from the feature to the project, and [[external-memory]]'s point that writing things down is the one scaling move that works for both humans and frozen-weight models.
- **The human's job moves from authoring tasks to authoring goals and reviewing.** The loop still "iterates with you," "asks a clarifying question," and "pings for review," so the human remains in the loop at exactly the decision points. That is the shape [[judgment-in-ai-assisted-development]] predicts: implementation and now backlog maintenance become cheap, and judgment about what the goal *should be* becomes the binding constraint.
- **Expect the loop to follow Larson's own scaffolding pattern.** In [[agentic-engineering-architecture]] he describes prototyping with a fully agentic workflow, then moving deterministic steps into code. The current loop is all-skill. Step 2 (reconciling issue state against metrics) and the staleness check in step 4 are the obvious candidates to become code once the pattern stabilizes.
- **An open risk the post does not address (my note, not Larson's):** a loop that is allowed to add issues to its own project has no explicit scope bound. The only brake described is the re-audit on description staleness, which re-reads the goal but does not cap the backlog. Teams adopting the pattern will likely want a human approval gate on step 2's additions, or a budget, before letting it run unattended in Agent Fleet.
- **Pattern churn is itself the story.** Larson opens by saying effective patterns now emerge faster than he can adopt them. The factory is at least the fifth workflow migration Imprint made in nine months, and each depended on the previous one. That suggests the adoption *sequence* matters more than any single tool — a company cannot skip to a factory without the state and measurement layers underneath it.

## Sources

- Larson, Will (2026). "Trying the Software factory pattern." <https://lethain.com/software-factory-experiment/> — [[2026-09-20-software-factory-experiment|local copy]]
