---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2022-08-28-kocienda-dri-apple.md
compiled_at: 2026-10-22
model: claude-fable-5-1
confidence: medium
---

# Directly Responsible Individual (DRI)

Ken Kocienda — an iPhone-era Apple software engineer and author of *Creative Selection* (2018) — describes how the original iPhone was built **without product managers**. In their place Apple used *directly responsible individuals*: for each important piece of work, one named person was charged with seeing that it got done. Kocienda was the DRI for the iPhone keyboard while an individual contributor on the software engineering team.

## The model as Kocienda describes it

**Many functions, not three.** Kocienda rejects the common product/design/engineering trichotomy as too simple for a product like the iPhone inside a company like Apple. The real functional landscape also included operations, marketing, legal, finance, and developer relations, each with sub-disciplines and specialists. Two further structures sat alongside these:

- **Program management**, focused narrowly on schedule, progress, and risk.
- A **small, highly skilled executive team**, each member keeping tabs on one functional area.

**The DRI cuts across functions.** A DRI could come from any function and worked across all of them. Being tapped did not mean doing all the work yourself — the cross-functional nature of the work usually made that impossible. The DRI's job was ownership of the outcome, not execution of every part.

**The DRI traverses the hierarchy.** Years after the keyboard, still an IC, Kocienda was DRI for a project with legal ramifications and simply set meetings with a VP in legal. At another company, he notes, that request would have been escalated up the management chain. At Apple the DRI was *expected* to reach out directly. (That project did not ship — his aside, not a caveat on the model.)

**Decisions were collective but centered.** Questions of what the product is, what it should do, who it serves, and how to get it built were arrived at collectively, centered on the DRI's work, with a strong design emphasis, and finally submitted to the executive team for approval.

Kocienda's verdict: "This scheme seemed to work out pretty well."

## What the DRI model actually unbundles

The product-manager role as typically practiced bundles four things: singular accountability, cross-functional coordination, product judgment, and schedule/risk tracking. Apple's arrangement, on Kocienda's account, distributes them rather than concentrating them in a job title:

| PM responsibility | Where Apple put it |
|---|---|
| Accountability for an outcome | The DRI (a role, not a title; held by an IC from any function) |
| Schedule, progress, risk | Program management |
| Product judgment | Collective discussion around the DRI's work, with design weighted heavily |
| Final decision | Executive team ratification |
| Functional depth | Each executive on their own area |

Two features do the real work. First, the DRI is *orthogonal to both function and seniority* — an IC engineer can own a cross-functional outcome. Second, the DRI carries **authority to cross the org chart directly** rather than through chains of escalation. The label "DRI" has since spread widely (GitLab's handbook, countless startups), but it is often applied as a RACI-style accountability tag without that second feature. On Kocienda's telling the traversal right, not the name, is the mechanism.

The scheme also maps cleanly onto Grove's executive-as-ratifier model in [[executive-role]]: decisions are made by the people closest to the facts (the DRI and the collective around them) and the executive team's role is to approve, not to originate. Kocienda's "eventually submitted to the executive team for approval" is that model stated from the IC's side.

## Thread reactions worth keeping

- Asked whether Steve Jobs was "the de facto product manager," Kocienda replied: "Why do you feel the need to fit your chosen terminology onto a different way of working?" The refusal is the point — the model is not PM-by-another-name.
- Asked about RACI (which the questioner called contrived and ambiguous, since one still cannot tell who is in charge from the chart), Kocienda: "I have no idea what RACI is." A DRI answers the question RACI charts obscure.
- Giff Constable raised the strongest caveat: the iPhone team had an unusual amount of *time* to stay small and work until the product was right enough. Whether the DRI model survives the schedule pressure of ordinary companies is untested by this account.
- Marty Cagan pointed to his SVPG essay "Products and People" and noted that how Apple covers the product role differs across its three very different product types (devices, system software, internet services) — "not a small topic." Kocienda's thread describes one of these, the device, at one moment in time.

## Connections

- **The demo review as the ratification venue.** Kocienda's companion thread, compiled in [[demo-driven-product-development]], describes the same organization from the decision side: working demos shown to Jobs, every detail an exact ship proposal. That article calls Jobs the iPhone's de facto product manager; this thread is Kocienda's explicit refusal of that framing. The two are reconcilable — the DRI owns the work between reviews, and the demo review is where the executive team approves it — but the terminological point stands: Apple did not have a product-manager *role*, it had a decision *ritual*.
- **Named owners over departments.** Musk's first rule in [[elon-operating-philosophy]] is that every requirement must carry an individual human name, never a department. The DRI is the same instinct applied to outcomes rather than requirements.
- **Process ownership in the AI era.** [[ai-and-org-design]] diagnoses the failure of AI rollouts as "no one owns the end-to-end process"; Taylor's proposed hyper-generalist process owner is a DRI with tooling. Larson's observation in [[ai-era-engineering-leadership]] that migrations can now be 95% owned by one individual makes DRI-shaped work more common, not less.
- **Barrels.** Rabois's barrels in [[how-to-operate]] — people who take an idea from inception through shipping and bring others along — are the population DRIs are drawn from. The DRI mechanism is how an organization deploys a barrel without promoting them into management.
- **PM-less structures.** [[product-management-in-the-ai-era]] argues AI eats the information-moving half of the PM job, leaving judgment and ownership. That residue is close to what the DRI already was; the Apple precedent suggests those functions can sit with an IC, with judgment shared collectively. [[product-management-framework]] offers an engineering leader a way to carry the product-judgment piece when no PM exists.

## Caveats

Single-source memoir perspective on 2005–2007 Apple; Kocienda's own thread admits a DRI-led project that did not ship. Apple has long had product marketing managers who occupy part of the PM space in other companies, which Kocienda's "no product managers" claim elides. Constable's timeframe point and Cagan's product-type point both suggest the model's portability is unproven.

## Sources
- Kocienda, Ken (2022). "Post by @kocienda on X" (thread on DRIs at Apple). <https://x.com/kocienda/status/1563917075189358593> — [[2022-08-28-kocienda-dri-apple|local copy]]
