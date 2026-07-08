---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-07-07-uber-agentic-pods.md
compiled_at: 2026-07-07
model: claude-opus-4-8[1m]
confidence: medium
---

# Agentic Pods

**Agentic Pods** is Uber's program for extending agentic AI *beyond engineering* into business functions — finance, legal, operations, marketing, customer support, HR, procurement. Described by Uber VP Praveen Neppalli in a July 2026 X thread, it is a repeatable two-week embed-and-ship methodology, and its central claim is a reframing: **the workflow, not the task, is the unit of automation.**

## The setup: engineering adoption as the precondition

Neppalli anchors the program in Uber's internal AI-coding numbers, which serve as the launchpad:

- **99%** of engineers use AI tools.
- **>70%** of pull requests are attributed to local or cloud agents.
- **2,500+** agent skills built across the software development lifecycle.

These are the mature-adoption figures that make the harder question askable: engineering has internalized agents, so how do you bring the same leverage to functions that "run on complex workflows that are often manual, highly nuanced, and spread across dozens of systems"? Uber's answer starts from the premise that **you can't automate these by reading process diagrams or documentation — you have to see how the work actually gets done.** This is the same "enterprises have no spare cycles to reimagine their own workflows" gap that [[ai-eats-the-world]] uses to explain why frontier labs are hiring forward-deployed engineers; Agentic Pods is Uber running that FDE motion *internally*, pairing its own engineers with its own domain experts.

## The method: a two-week pod

Each pod is one AI-proficient engineer (Uber handpicked ~30 with deep systems knowledge) paired with one domain expert from a business function, on a fixed 10-day clock:

| Days | Activity |
|------|----------|
| 1–2 | **Shadow** the expert. Observe every step, document workflows, ask questions, build intuition. |
| 3 | **Prioritize** opportunities by scale, repetition, business impact, and data availability. |
| 4–5 | **Build** a working agent alongside the person doing the job. |
| 6–9 | **Validate** with several others doing the same work — does it generalize? does it actually make the job better? |
| 10 | **Ship.** |

In two months Uber ran **16 pods across 16 business functions**, reporting compressions like:

- Capital allocation across 150 cities: **15 hours → 30 minutes**
- Financial pacing reports: **2 days → 10 minutes**
- Marketing web QA: **2 weeks → 50 minutes**
- Support workflow creation: **9,000 manual workflows → self-service automation**

(These are self-reported single-source figures from the company doing the promoting; treat the magnitudes as directional.)

## The load-bearing claim: workflow as the unit of automation

The thesis is not that agents do tasks faster. It is that **the biggest wins come from redesigning the entire workflow around AI**, which then lets you *eliminate handoffs, remove unnecessary approvals, replace legacy tooling, reduce vendor spend, and accelerate decisions.* Automating a single task inside an unchanged process leaves most of the value on the table; the most impactful agent skills are the ones that **cut across teams, orgs, functions, tools, and systems.**

This is a distinct and stronger position than the coding-productivity story. It rhymes with the "writing code was never the bottleneck" observation in [[decide-execute-deliver-sandwich]] (compressing execution alone yields little if the surrounding process is untouched) and with the harness-first view in [[harness-engineering]] and [[agent-harness]] that the leverage lives in the *environment and workflow design*, not the model. Where Airbnb's rollout in [[enterprise-agentic-coding-adoption]] optimizes agents *within* the existing SDLC, Agentic Pods is explicitly about **re-architecting the process** the agent runs inside.

## The method's own thesis: proximity beats documentation

Neppalli's stated biggest lesson: *"The best AI opportunities are rarely visible from the outside. You discover them by sitting next to the people doing the work... building with them, not for them."* The surprise wasn't the speed — it was how fast engineers dropped into unfamiliar domains surfaced opportunities "hiding in plain sight." This is the same critique of documentation-as-substitute that [[llm-knowledge-bases]] raises about company brains (intent lives in the doing, not the final artifact) applied to workflow discovery: the map is not the territory, so you embed to find the real work — an organizational-scale version of [[finding-your-unknowns]].

Uber is now standing up a dedicated permanent team to scale the model — "deeply understand the work, redesign it from the ground up, and use AI to fundamentally change how the business operates."

## Open questions raised in the thread

- **Maintenance / drift.** Workflows in these functions rarely stay static; the two-week ship gives no account of who owns enhancement and support for the resulting internal products afterward — the classic build-vs-maintain gap.
- **No PMs in the pods.** The pod is engineer + domain expert only; whether that omission is a feature (fewer handoffs) or a debt (no product ownership) is unresolved.
- **Review quality behind the 70% figure.** How much of the agent-authored-PR share is genuinely reviewed versus rubber-stamped — the perennial question about auto-approve discipline that [[enterprise-agentic-coding-adoption]] treats as a hard rule ("hold agent code to prod quality; don't drop your standards").

## Sources
- Neppalli, P. (2026). "Agentic AI adoption is on fire at Uber." X thread. <https://x.com/praveentweets/status/2074605343439810922?s=46> — [[2026-07-07-uber-agentic-pods|local copy]]
