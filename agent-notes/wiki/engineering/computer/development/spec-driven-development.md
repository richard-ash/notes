---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-05-11-notion-spec-driven-development.md
compiled_at: 2026-05-18
model: claude-opus-4-7
confidence: medium
---

# Spec-Driven Development

**Spec-driven development** is the practice of writing a feature first as a comprehensive plain-English specification — checked into the codebase alongside the code, with code pointers and an explicit verification protocol — and then handing that spec to a coding agent to implement. When the feature needs to change, the human edits the *spec*, not the code; the agent re-derives the implementation. Ryan Nystrom, an engineering-manager-who-codes at Notion, describes the workflow as "the future of software engineering" after using it to rebuild Notion AI's agent harness.

The key reframe: experienced engineers were already writing technical design documents and debating implementations in review meetings. Spec-driven development takes the same artifact engineers were producing anyway, makes it the durable source of truth (instead of throwaway pre-implementation paperwork), and removes the meeting and review queue between the doc and the running code.

## The Notion workflow

Nystrom's account of building Notion AI's "ask mode" feature — a mode that bans mutating tools so the agent can only read and answer questions — is the cleanest description of the loop:

1. **Capture intent verbally.** Open Whisper, "just start yapping" about how the feature should work. No structure, no editing.
2. **Convert dictation to spec.** Feed the transcript to Codex with the existing spec library as format reference: *"Here's our other spec library, learn the format, take my information, write a spec."*
3. **Revise the spec.** A few rounds of human editing. The output is a markdown document with prose intent, code pointers into the existing codebase, and a verification section at the bottom.
4. **Hand the spec to the agent.** Open Codex again, point it at the spec file, say *"Build it."* Nystrom reports this one-shot produced "a couple thousand lines" in a few hours.
5. **Review and iterate via the spec.** Later changes update the spec first; the agent re-applies.

The spec is checked into version control next to the code. Spec history is the change log for *how the feature works*, separate from (and at a higher abstraction level than) the git log for the code that implements it.

## What makes a spec implementable

The transcript is explicit on the structural requirements that turn a spec from a design doc into something an agent can one-shot:

- **Code pointers.** The spec references specific files and call sites in the existing codebase, so the agent doesn't have to re-discover where to wire the feature in.
- **A verification section.** The bottom of the spec describes how the agent should verify correctness — typically by running tests and then driving the product through a CLI to confirm observable behavior.
- **A means for the agent to verify itself.** Notion built a CLI that lets Codex run Notion AI: send queries, enable/disable ask mode, read transcripts, observe responses. Without an executable verification loop the spec can't close on its own.

Nystrom frames the verification loop as the gating step: *"If the verification's a little hazy, that's the first thing you should be going and doing — do you have a tool to let the agent run itself?"* This is the same principle as [[agentic-engineering-architecture|fat code]] for correctness-critical operations: building the CLI is a one-time investment that converts an open-ended "did it work" judgment into a deterministic loop the agent can drive.

## The spec as source of truth (and as cross-functional asset)

The durable claim is that the spec — not the code — becomes canonical:

- **For engineers:** changes flow spec-first. The code is regenerable; the spec describes the invariant the code implements. Version history on the spec is the change log of how the feature behaves.
- **For the rest of the business:** the same plain-English document is a usable input for marketing copy, release notes, support documentation, and customer-facing explanations. Claire Vo, the podcast host, observes that code is "still a little intractable" as a cross-functional asset whereas a comprehensive spec is not.

This second point is subtler than it sounds. A traditional design doc decays the moment implementation starts diverging from the doc; a spec that *is* the input to implementation stays fresh as long as the workflow does. The artifact carries information from intent to running code *and* outward to non-engineering audiences in a way the codebase alone cannot.

## How this changes the engineer's role

Nystrom's framing: engineers evolve from implementers into "systems thinkers and architects," but the most specific work is **designing the verification loop**. Three implications:

- **Documents engineers were already writing become the deliverable.** Tech design docs used to wait for review meetings and then sit unread while the author re-derived the design in code. Spec-driven development collapses doc-and-code into a single artifact whose value compounds.
- **The slow path (meetings, review queue) drops out.** Nystrom: *"Now no more waiting for the meeting, no more waiting for review. Ship it. Have a verification loop. [Debate] the merits of it being live and working versus the theoretical merits of it sitting in a document."*
- **Verification design becomes the bottleneck.** If you can't articulate how correctness should be checked, you can't close the loop, and the agent's output is non-falsifiable. This is the practical pressure point that pulls engineering attention toward [[judgment-in-ai-assisted-development|judgment]] — specifically the judgment of what evidence constitutes a working feature.

This sits cleanly on top of Karpathy's [[agentic-engineering|agentic engineering]] discipline: the spec is the [[agentic-engineering-architecture|"fat skill"]] (rich natural-language intent), the agent + tests + CLI form the harness, and the human contribution is verifiability and taste rather than typing.

## Notion's broader AI engineering practice

The spec workflow is one of three layered practices in Nystrom's account. The other two are worth recording because they cohere as a single operating model:

### "Boxy" — Notion's background-agent VMs

Nystrom describes an internal system also called the "software factory" but nicknamed Boxy: a fleet of VMs with Codex and Claude Code pre-installed, invocable by `@mention`-ing the agent in a Notion comment on a task page. The walkthrough example: a friend texted Nystrom requesting a "copy link to tab" button on Notion's tab-block component. He opened a Notion task, wrote four sentences plus a screenshot of where the button should live and the edge cases, `@mention`ed codex in the comment, and 10 minutes later got back a PR with a preview URL and screenshots of the agent's own UI verification.

This is the Notion-internal equivalent of Stripe's Minions ([[unattended-coding-agents]]) at smaller scale: same architectural commitments (sandboxed VMs as the runtime, ergonomic entry point inside the tool engineers already use, agent output as a reviewable PR rather than a streaming chat) but invoked from Notion comments rather than Slack threads. Nystrom's claim, addressed to engineering leaders: if your org doesn't have a VM-plus-background-agent strategy, "it's time to get one." The "spin up agents on cattle VMs, never on engineer laptops" pattern is now table-stakes for org-scale AI adoption.

### AI-augmented standup pre-reads

Nystrom built a custom Notion AI agent — internal name "hot potato" — that runs at 9 a.m. daily, reads the last 24 hours of Slack messages, closed tasks, merged PRs, and Honeycomb CI metrics, then writes a pre-read into the day's meeting template covering: latest CI time, decisions, progress, bugs, feedback, open questions, risks. The agent ends by posting a brief, "fun" summary link into Slack.

Two structural points the transcript surfaces about why this matters beyond time-saving:

- **It democratizes contribution visibility.** Loud engineers dominate verbal standups; quiet engineers' wins get lost. An agent that scrapes the same sources for everyone equalizes the playing field.
- **It is a burnout protection mechanism for managers.** Manager time historically split between "in meetings" and "prepping for meetings." Just-in-time pre-reads collapse the prep tier, freeing managers to code up to the minute the meeting starts. Nystrom argues line managers, directors, VPs, and CTOs should be writing code now ("this is the era of the hard skill"), and just-in-time meeting prep is one of the structural changes that makes it feasible.

Vo's heuristic for designing these automations: *"Write down what you would do if you had time."* The agent description is just the manual workflow, prose-encoded, plus a Slack-funny voice constraint.

## Why CI speed is now an agent-productivity precondition

Nystrom's "Project Afterburner" is an effort to cut Notion's CI time by 4×. The pre-agent argument for fast CI was about engineer iteration loops (small batches, fast signal, willingness to ship). The post-agent argument is harder-edged: **an hour-long CI loop means an agent sits idle for an hour per iteration**, and agents that sit idle stop being able to one-shot.

This is the mathematical-ceiling argument: Stripe's 1,300 PR/week throughput from [[unattended-coding-agents]] is unreachable on slow CI regardless of model quality or harness sophistication. The total agent capacity of an org is bounded above by the CI loop length × the parallel agent count, and the only lever an engineering leader has on the first factor is to spend the political and engineering capital to make CI fast. Nystrom's claim that he's "not a CI expert" but took the project anyway is itself an argument for the [[#How this changes the engineer's role|engineers-as-systems-thinkers]] reframe: the bottleneck-fixing work is now visible enough to be a senior contributor's project regardless of pre-existing infra credentials.

## Prompting craft worth keeping

Two prompting moves Nystrom highlights, both anti-default:

- **"I literally don't know what I'm doing here. Explain it like I'm a 5-year-old."** Useful when working out of your depth (Nystrom uses this on CI infra). It defends against the agent pattern-matching to "experienced user wants concise pointers" when in fact the user wants caveman-level explanation. The transcript notes this lands differently with Codex (terse, didactic) than with Claude Code (warmer, more praise-coded), and Nystrom prefers the Codex tone for genuine learning.
- **"You're wrong. Defend your argument."** Used to break agent sycophancy when "are you sure this change looks okay?" produces a reflexive *yes, totally fine*. Demanding citations and pointed reasons separates models that can defend their work from models that fold under pressure. Useful precisely in the cases where Nystrom genuinely doesn't know the answer himself.

Both moves treat the agent as a colleague who can be told to argue back rather than a mirror of the user's confidence level — which is the same orientation that makes spec-driven development work at all.

## Cross-connections

- [[unattended-coding-agents]] — Stripe's Minions describe the same VM-fleet pattern at much larger scale; Boxy reads as a smaller-team Notion-native instantiation. Both share the "sandboxed VM as the runtime, ergonomic entry point inside the tool engineers already use, agent output as a reviewable PR" architecture.
- [[agentic-engineering-architecture]] — Tan's fat-skills/fat-code/thin-harness heuristic; the spec is the canonical fat skill, the verification CLI is the canonical fat code, and Codex is the thin harness. The spec-driven workflow is one concrete instantiation of the three-layer model.
- [[agentic-engineering]] — Karpathy's discipline framing of why velocity-without-quality-loss is the new bar; spec-driven development is one of the practical disciplines that holds the quality ceiling.
- [[judgment-in-ai-assisted-development]] — Larson's constraint hierarchy (time → attention → judgment → creativity); spec-driven development is the workflow that operationalizes judgment scaling, with the spec being the codified judgment.
- [[claude-code-skills]] — Notion's harness rewrite borrowed "skills and progressive disclosure" from coding agents; the spec library serves a similar role for Notion AI as the skills folder does for Claude Code.
- [[claude-code]] — Boris Cherny's Claude Code design philosophy; Nystrom's Codex-vs-Claude-Code personality contrast (Codex terse and didactic; Claude Code warmer) is the user-facing read of two different harness design choices.
- [[low-tech-devex]] — markdown-as-source-of-truth and CLI-as-verification-substrate are the same aesthetic; spec-driven dev is the agent-era extension of "text in version control beats GUIs and proprietary formats."

## Sources

- Ryan Nystrom and Claire Vo (2026). "Spec-driven development: the AI engineering workflow at Notion." *How I AI* podcast, YouTube. <https://www.youtube.com/watch?v=pUHA_jNwuYE> — [[2026-05-11-notion-spec-driven-development|local copy]]
