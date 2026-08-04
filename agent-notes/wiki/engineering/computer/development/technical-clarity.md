---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-08-03-goedecke-technical-clarity.md
compiled_at: 2026-08-03
model: claude-opus-5[1m]
confidence: medium
---

# Technical Clarity

*Sean Goedecke, 2026.* Goedecke's account of what he considers the highest-leverage part of the staff engineer's job: not shipping projects, but making sure the people who decide things have an accurate-enough working model of the software system.

His definition:

> Technical clarity is when non-technical decision makers have a good-enough practical understanding of what changes they can make to their software systems.

"Non-technical" here is a statement about *context*, not ability. A director or VP may have been an excellent engineer and may still have a fine technical mind; what they don't have is the time to maintain an accurate mental model of a system that changes weekly. They therefore run on a vague model plus advice from engineers they trust. Clarity is the quality of that pairing, and Goedecke's claim is that it can be the difference between a functional engineering org and a dysfunctional one.

## Why the default supply is near zero

The scarcity argument is the essay's strongest part, because it doesn't blame anyone. Decision-makers are confused about the technology because *the engineers are too*. For a large established codebase, it is normal for very senior engineers to be unable to definitively answer questions as basic as "can a user of type X do operation Y?" The honest answer is usually "I'll have to go and check."

Goedecke's worked example: a VP wants to extend an existing paid feature to some free-tier users. Almost all the technical detail is irrelevant to them, but five questions are not —

1. Can the feature be safely delivered to free users as it stands?
2. Can it be rolled out gradually?
3. If it goes wrong, can it be reverted without breaking accounts?
4. Can a subset of users get early access?
5. Can paid users be prioritized under capacity pressure?

Answering these is a research project. You can't settle them by trying the change on a test account, because the edge cases live in the combinations — users inside an organization, users on a trial plan, users mid-migration. Sometimes the only way to answer is to do the task. He attributes this to his "wicked features" thesis: systems accrete marginal-but-profitable features that interact in surprising ways until the whole is *almost* — not quite — impossible to understand. Design can tame that, never eliminate it.

The practical consequence, which the essay leaves implicit: the five questions above are all about **rollout affordances**, not about the feature. A system with feature flags, gradual rollout, clean reversibility, and per-cohort targeting is one where the answers are cheap and standing. A system without them requires a fresh investigation every time. Investment in those affordances is therefore investment in the *supply* of technical clarity — the same argument [[internal-software-quality]] makes about cruft, one level up. [[system-design]] is where Goedecke describes building them.

## The engineer as an abstraction

For a product leader, an engineer who can be relied on to navigate this is an enormous relief, and Goedecke observes that the role usually lands on staff engineers or on seniors about to become one. His causal claim runs the other direction from the usual promo story: senior engineers who are good at providing clarity sometimes get promoted to staff *without trying*, because the promotion makes them a more useful instrument for the leaders already leaning on them. Leaders keep a mental list of who helps them decide and are motivated to place those people on the most important work.

His framing of the relationship is the essay's sharpest image: **the engineer is an abstraction over technical complexity**. VPs use engineers the way engineers use garbage-collected languages — so they don't have to think about the layer below.

He is explicit that this is not the only way to be impactful. Plenty of strong engineers deliver through shipping, debugging, and design. But those engineers, he argues, will rarely be valued as highly, partly because leadership remembers who helped them and partly because clarity is higher-leverage than any single project.

## Inside the abstraction

What it feels like from the inside is *paranoia*. Goedecke tops out at 95% confidence on any technical opinion and is usually lower. The residual worry isn't about the risks he has enumerated — when he has been spectacularly wrong in his career, it has been about unknown unknowns, gaps in his model of the system he didn't know to look for. Leading a project, he spends a lot of time sitting and wondering what he hasn't thought of yet.

The discipline is keeping that to himself. Good leaders, like good engineers, understand that [all abstractions leak](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/) and don't punish the occasional miss from someone who is a useful abstraction the rest of the time. What they won't tolerate is **the absence of an opinion**. An engineer whose standard answer is "well, I can't be sure, it's really hard to say" is useless as an advisor — still able to write code and deliver projects, but adding nothing to the organization's clarity.

## Is simplifying just lying?

Goedecke takes the objection seriously enough to state it in its strongest form. If confident-sounding engineers get influence over honest ones, then once one engineer starts hiding their worries the rest must follow or be sidelined, and the fast-talkers end up running things while the careful engineers are relegated to implementation. On that reading, "no problem, we'll be able to roll back" is a con.

His answer is that the objection misreads what clarity is. Clarity was defined as a *good-enough* working model held by someone who cannot hold the real one — which means a **simplified** model, and simplification necessarily trades some accuracy for comprehensibility. An engineer optimizing for maximum technical accuracy in a conversation with a VP is optimizing for the wrong variable.

The load-bearing move is a claim about relevance, not about truth: **most of his worries are not information the decision-maker can act on**. Someone asking "is it safe to roll this out" wants a yes or a no. A stream of hedges forces them to do the filtering themselves, and they are worse at it — which is why they asked. The budget framing he ends on: a VP has only so many mental bits for technical detail, so fill them with what's possible, what's impossible, and what's risky, rather than making them extract those from irrelevant context.

The guardrails are real and worth not losing. He is not advising a default yes. Sometimes the answer is "we won't be able to roll back safely, so we'd better be sure" or "no, not to this class of users yet." The rule is to **commit to a recommendation in one direction or the other**, with caveats reserved for when the risk is extreme or the odds genuinely high.

## What it takes

His three prerequisites:

1. **Taste** — knowing which risks and context to mention and which to omit. He concedes he has little to say about how to acquire this beyond feeling it out per relationship, which makes it the least transferable part of the essay.
2. **Deep technical understanding**, maintained by continuing to ship code and deliver projects. If he loses direct contact with the codebase, his ability to communicate about it decays as the system changes and his memory of specifics fades. This is a real constraint on the "staff engineer as pure advisor" trajectory — the advisory value has a half-life measured against commit velocity.
3. **The confidence to present a simplified picture**, including claims he is only 80–90% sure of. Engineers who won't do this, in his view, are abdicating a responsibility rather than exercising rigor.

## Connections

The closest neighbor is Goedecke's own [[software-estimation]], and the two essays are the same argument applied to different questions. There, the advice is to return a menu of risk-differentiated plans rather than a number; here, it's to return a recommendation rather than a confidence interval. Both rest on the premise that the decision-maker's scarce resource is attention, not information, and that an engineer who dumps their full uncertainty onto them has moved work upward to the person least equipped to do it. [[system-design]] supplies the substrate: killswitches, circuit breakers, and fail-open-vs-fail-closed decisions are precisely what makes questions 2–5 answerable without a research project.

Against [[executive-role]], the fit is unusually clean. Pennarun's Grove-derived model says the executive is the least-informed person in the room and their job is to *ratify* decisions made by those closest to the facts. Technical clarity is the input that makes ratification possible at all — and the non-committal engineer is exactly the failure mode that model can't absorb, because a leader with no recommendation to ratify is forced back into deciding on their own.

There is a genuine tension with [[truth-telling-leadership]]. Horowitz's rule is that leaders must state hard facts and then assign them meaning, because hidden facts destroy the trust that makes an organization executable. Goedecke's rule is to withhold. The reconciliation is that they're withholding different objects: Horowitz is talking about *facts material to the audience* (the layoff, the missed quarter), which Goedecke also says to surface when the risk is extreme. Goedecke is talking about the *error bar around a judgment* — the residue of unknown unknowns, which is not a fact and which the recipient cannot price. Horowitz's own trust-communication identity actually predicts Goedecke's practice: as trust rises, the required volume of communication falls, and hedging is volume.

The sharpest limit case is [[ai-mania]]. Ludic's field report describes organizations where the honest technical assessment gets you removed and replaced by someone who will say yes — "government by assassination." Goedecke's technique presumes a leader who genuinely tolerates a "no" and doesn't punish the occasional leak. Where that presumption fails, the norm he describes has no stable honest equilibrium, and the skeptics' version of the objection he dismisses is simply correct as a description of that org. The two pieces read together suggest the diagnostic question isn't "should I hedge?" but "what happened the last time someone here said no?"

Two further links. [[public-speaking]] carries the same genre-relative insight from a different direction — the standard for a good talk is set by the audience's conventions, not by an absolute — and Bloom's go-simpler advice is the presentation-layer version of Goedecke's mental-bits budget. And [[judgment-in-ai-assisted-development]] extends the scarcity argument: if agents lower the cost of "going and checking," the estimable fraction grows and the five VP questions get cheaper to answer, but taste about *which* risks to surface is exactly the judgment that doesn't get automated. On that reading, the advisory half of the staff role gets more valuable as the investigative half gets cheaper.

## Caveats

A single opinionated practitioner essay with no measurement, grounded in large-tech-company environments with attentive VPs and directors. The strongest empirical-sounding claim — that engineers providing clarity are promoted and better rewarded than those who merely ship well — is a career observation, not evidence, and it is unfalsifiable in the direction that matters: we don't see the engineers who committed confidently, were wrong, and lost standing. Goedecke's "95% confidence" is a self-report about a feeling, not a calibration record. And the advice is genuinely double-edged in a way the essay underweights: the same behavior that makes a well-calibrated engineer useful makes a poorly-calibrated one dangerous, and nothing in the framework helps a reader tell which one they are.

## Sources

- Goedecke, Sean (2026). "How I provide technical clarity to non-technical leaders." <https://www.seangoedecke.com/clarity/> — [[2026-08-03-goedecke-technical-clarity|local copy]]
