---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-06-18-working-with-mythos.md
compiled_at: 2026-06-18
model: claude-opus-4-8[1m]
confidence: medium
---

# Patron, Not Wizard: The Relationship Shift with Agentic AI

Ethan Mollick's account of using Claude 5 Fable (the first public "Mythos-class" model) argues that the headline change isn't raw capability — it's a shift in the *relationship* between human and AI. As models become autonomous enough to run for hours, spawn their own sub-agents, and make hundreds of unsupervised judgement calls, the human role collapses from *doing* to *commissioning*. Mollick frames this as the successor to his earlier "[working with a wizard](https://www.oneusefulthing.org/p/on-working-with-wizards)" metaphor: the spell has grown so powerful that he is no longer sure he is the wizard. He is the **patron** — he describes what he wants, pays for it, and judges the result, while the conjuring happens somewhere he cannot watch.

## The capability leap

Mollick reports Fable outperforming every prior public model "by a considerable margin," sustaining work for up to a dozen hours against multi-page specifications. Concrete artifacts from single prompts plus minor feedback:

- A sophisticated academic social-science paper from one prompt and one round of feedback.
- A 10-page rhyming epic poem about a haircut where every word starts with "s."
- Several playable games coded in Claude Code from vague prompts ("Balatro, but for coin flips") — notable because Claude generates no images, so all art and 3D objects are produced with math alone, no external assets.

## How the work actually gets done

The mechanism behind the leap is **orchestration**, not a single monolithic model thinking harder. On an isochrone-map project (a map of how far you can travel in a given time), Fable:

1. Launched multiple cheaper sub-agents (Mollick believes mostly Claude Sonnet) to research travel times in parallel — ultimately ~2,200 specific flights, rail schedules (TGV to Shinkansen), and per-country road speeds from academic papers.
2. Started coding *while* the research agents ran.
3. Spawned further agents and tests to verify its own code, taking notes on its progress throughout.

When asked to fix estimated (rather than exact) travel times for remote locations, it escalated to **adversarial groups of agents** that researched and checked each other's results — finding ship frequencies to Pitcairn Island and routes to Grise Fjord. A nine-and-a-half-hour run produced "Concord," a full statistical-software package for calibrating human and AI judgement against each other (a tool Mollick says researchers have needed for years but was never profitable to build; [released on GitHub](https://github.com/emollick/concord)).

This is the [[ai-coding-harnesses]] / multi-agent pattern at its logical conclusion: the model is less a chatbot than an orchestrator running its own [[enterprise-agentic-coding-adoption|fleet of sub-agents]] with verification loops.

## The black box as the price of power

Mollick's central unease: he did very little, and could see very little of what was done. His control was limited in three ways at once — how much *work* he contributed, how much he could shape the *approach*, and how much he could see of the *reasoning*. The model made hundreds of small judgement calls he never got a vote on, and the process was too long to be worth following even if exposed.

He frames two futures:
- **Temporary sidelining** — interfaces simply haven't caught up; we'll get better windows into the process and better mid-stream steering.
- **Permanent trade-off** — the more capable the model, the less there is for a human to meaningfully do, and opacity *is* the price of the power.

Mollick suspects the second is more likely. Crucially, this is *not* loss of control in the obvious sense — Fable follows instructions remarkably well, and the more ambitious the instruction the better the result. But **steering is no longer the same as doing**: you brief, it executes, what comes back is finished. The work shifts from *process* to *outcome*. His closing image: a patron commissions a single artist, but Fable is a whole studio where you sign off on the final work without ever setting foot on the floor.

## Limits and costs

- **Token burn**: Fable is twice as expensive as Opus per token and consumes them prodigiously; production cost is "a lot," though delegation to cheaper models softens it (a partial answer to [[ai-lab-economics]]'s cost questions — capability bought by spending sub-agent tokens, not just bigger context).
- **Over-cautious guardrails**: the security guardrails trip "at the faintest hint of a security problem," silently downgrading to the weaker Claude 4.8 Opus far too often. (The piece notes Mythos discussion has centered on software-security impact; Mollick deliberately avoided testing that dimension.)
- **Jagged frontier persists**: still writes in the same recognizable style — and the *software* it produces carries "Claudisms," as do its progress reports ("carrying the weight," "earning the answer").

## Synthesis and connections

- The "patron not wizard" framing is the human-side complement to [[agentic-engineering]] and [[agentic-engineering-architecture]]: those describe the discipline and architecture of orchestrating agents; this describes what it *feels like* and what it costs the human's sense of authorship and oversight.
- It sharpens the [[ai-judgment-atrophy]] worry: when the human only judges outcomes and never sees the hundreds of intermediate calls, the friction that builds judgment disappears entirely — yet Mollick notes expertise still mattered for catching the errors Concord and the map contained.
- Mollick's aside that we may need *more* coders, not fewer — to debug and extend the explosion of newly-cheap software — lines up with [[decide-execute-deliver-sandwich]] and [[why-ai-hasnt-replaced-software-engineers|the derived-demand argument]] that cheaper execution can grow, not shrink, demand for engineers.
- Treat the specifics (Fable, Mythos, "Claude 5," 2× Opus pricing, nine-hour runs) as Mollick's framing of an early-access preview, not settled product facts — hence `medium` confidence.

## Sources
- Mollick, Ethan (2026). "What it feels like to work with Mythos." <https://www.oneusefulthing.org/p/what-it-feels-like-to-work-with-mythos> — [[2026-06-18-working-with-mythos|local copy]]
