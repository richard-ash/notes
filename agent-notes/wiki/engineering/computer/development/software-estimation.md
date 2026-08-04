---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-08-03-goedecke-how-i-estimate-work.md
compiled_at: 2026-08-03
model: claude-opus-5
confidence: medium
---

# Software estimation

Sean Goedecke (GitHub) argues that the software industry runs on a polite fiction — that a skilled team can learn to predict how long its work will take — and that essentially everyone senior knows it is false. His interest is not in debunking estimation but in explaining what it is *actually for*, on the principle that **when a tech company is doing something silly, it is probably doing it for a good reason**: apparently senseless practices usually serve some illegible organizational function.

The resulting position has three moves, and the third is the one that makes the essay unusual:

1. Accurate estimation is impossible, because projects are dominated by unknown work.
2. Estimates are not produced by engineers; they are political instruments produced by and for management.
3. Therefore the estimate is an *input*, not an output — you are handed a duration and asked which designs fit inside it.

## Why estimation is impossible

Goedecke concedes the easy case: well-understood, tiny-scope work *can* be estimated. Changing the text of a link is ~45 minutes because the pipeline is known — five minutes to push, ten for CI, thirty to deploy.

Most work isn't that. In large systems, most programming is **research**: identifying prior art, mapping enough of the system to understand what a change touches. You do not know what is involved in a change until you go and look. And the arithmetic is brutal — projects are dominated not by the known work but by the unknown work, which "always takes 90% of the time," while only the known work is estimable. An estimate is therefore a confident measurement of the 10% that doesn't matter.

He rejects the standard rebuttal — *scope each item small enough to be estimable during planning* — on two grounds. First, it is a throwback to the mapped-out-in-advance software architect, which failed because programmers must make architectural decisions themselves, being the ones actually in contact with the code. Second, even if it worked it would only relocate the unestimable part into the planning meeting, which is the *worst* place to answer it, since you can't write or run code there.

The workarounds the industry has built are read as symptoms rather than solutions. T-shirt sizes exist because direct time estimates feel too obviously silly to engineers — and are converted back into hours and days the moment they travel up the management chain. Heuristics like "double it and add 20%" amount to giving up and estimating everything at a month.

## Estimates are political instruments

Goedecke's second claim is that estimates do not help teams deliver, and in a real sense **are not made by engineers at all**. A long estimate for a project a VP wants gets pressured down, or the work gets handed to a more compliant team. A short estimate on an undesirable project — or one meant to "hold space" for future unplanned work — gets talked up, or a manager simply adds a 30% buffer. Some of his most productive years were on teams that did no estimation at all: work that had to happen regardless, or work that dripped out value continuously and could just continue indefinitely.

He allows two exceptions:

- **Genuine impossibility.** If a manager repeatedly fails to pressure a team into the "right" number, that is a real signal travelling upward, and smart VPs use it to avoid taking on undeliverable projects.
- **Organizational backwaters.** Where no director cares, the formal process gets followed to the letter, because nobody is shaping it to their ends. He notes this is one mechanism by which one company contains radically different engineering cultures — and hints at the reckoning when a re-org drags such a team into the spotlight.

The positive statement: estimates are tools managers, VPs, directors and C-staff use to negotiate with each other about which projects get funded and which get cancelled. Their audience is lateral and upward, not the team.

## Estimates define the work, not the other way around

The inversion is the load-bearing idea. Teams do not start with a fixed piece of work and derive a duration; they start with a duration and derive what work fits.

His worked example: "talk with a PDF" in an LLM chatbot. Six months buys a robust upload system, a chunking-and-embedding pipeline for semantic search, page-to-image extraction to preserve formatting and diagrams. One day buys client-side PDF-to-text stuffed into the context window, or a plain-text "grep the PDF" tool. Both are the same feature request; the deadline selected the architecture.

The claim scales down to individual lines of code. Weeks of runway produce airy thinking about how to refactor so the feature fits elegantly; hours of runway produce laser focus on something that merely works. Because there are always many ways to solve a software problem, engineers hold far more discretion over *how* than the estimation ritual acknowledges.

This is the same structure Basecamp's Shape Up names an **appetite** rather than an estimate — fixed time, variable scope, "how much is this worth to us" instead of "how long will it take". Goedecke arrives at it from organizational politics rather than product methodology, which is the more interesting route: he is describing what already happens implicitly in companies that would deny doing it, not proposing a process to adopt.

## The method

Four steps, in order:

**Gather political context before looking at the code.** How much pressure is on this? Is it a casual ask or a must-do? What number is the management chain already carrying? "The CTO *really* wants this in one week" and "we were looking for work for your team" are different problems with different answers.

**Arrive at the code with the estimate already in hand.** Replace the unanswerable "how long would this take" — where "this" could be any of a hundred designs — with the tractable "which approaches could be done in one week?"

**Worry about unknowns, not knowns.** The more "dark forests" in the codebase a feature must touch, the higher the estimate — or, more usefully, the tighter you must constrain the candidate approaches to the *known* parts of the system. This is the actionable form of the 90% claim: the design lever is how much unfamiliar territory each approach forces you into.

**Return a risk assessment, not a number.** Never "this is a four-week project." Instead: "I don't think we'll get this done in one week, because X, Y and Z all need to go right, and at least one is bound to blow out." And ideally a *series* of plans rather than one — tackle X/Y/Z directly and risk a month; bypass Y and Z entirely, accepting different risks, to hit the date; or borrow expertise from a team that knows X and Y so you only have to solve Z. The tradeoff is then made by the person who owns it.

Sometimes the set of viable approaches is empty and the requirements have to change. But Goedecke ties this to a trust budget: a team that always says "impossible" stops being believed, and management routes around it. Pragmatic estimates the rest of the time are what make the impossibility verdict credible when it matters — the same reserve-of-credibility logic Horowitz applies to hard news in [[truth-telling-leadership]].

## Objections he addresses

- **"I can't estimate until the unknowns are answered."** He calls this cowardly: refusing to estimate forces someone less technical to estimate for you. (His related essays are *Engineers who won't commit* and *How I provide technical clarity to non-technical leaders*.) This is the same failure surface as the analysis-paralysis and infinite-research patterns catalogued in [[ic-anti-patterns]] — the refusal is legible as rigor from the inside and as absence from the outside.
- **"Helping management find compromises is a betrayal."** He'd rather work with managers than treat pushback as a professional duty.
- **"I don't experience this pressure; your org is dysfunctional."** Possibly — but he suspects such engineers work out of the spotlight, where there is little pressure of any kind, and doesn't think that qualifies them to advise people who do feel it.

In follow-up discussion he adds a concession from the Hacker News thread: non-engineers arguing that well-paid professionals should estimate regardless are correct, "as long as we're on the same page that it's fictional." And he sharpens the scope of his claim — you probably *can* estimate "build a user flow in Svelte"; what defeats estimation is "build a user flow in Svelte **on top of an existing large codebase**." The difficulty is a property of the codebase, not the feature.

## Team capability is the missing variable

A Lobste.rs commenter's point, which Goedecke endorses as under-appreciated: companies treat estimates as **fungible between engineers and teams**, when some teams deliver ten times faster than others — and some cannot deliver a given piece of work *at all*, regardless of time budget. This breaks the estimate-as-planning-currency model more fundamentally than the unknown-work argument does, because it means an estimate isn't even a property of the work. It is a property of a (work, team) pair, and the entire apparatus of moving estimates between teams during planning is measuring the wrong object.

It also supplies the mechanism behind the unknowns claim. Goedecke argues elsewhere ([[expertise-as-llm-leverage]]) that he would rather have familiarity with a specific codebase than deep general understanding of software systems. Familiarity is precisely what converts unknown work into known work — so estimation accuracy is a function of codebase-specific expertise, and the "10× team" and the "team with fewer dark forests" are largely the same team.

## Connections

The unknown-work thesis is the estimation-side statement of the instinct running through [[choose-boring-technology]] (innovation tokens as an explicit budget for unknown unknowns) and Goedecke's own [[system-design]] (boring components in the right places, because good design "looks underwhelming"). All three are ways of shrinking the 90%.

[[internal-software-quality]] supplies the causal loop: Fowler's argument is that cruft slows teams within weeks, not months. Cruft *is* how dark forests get planted — every unfixed piece of internal quality debt is a future estimate inflated by an engineer who has to go and look. That makes quality investment legible as estimation-variance reduction, which is a framing management can actually price.

[[software-migrations]] is the canonical case where the essay's advice is hardest to follow: cross-cutting migrations touch the maximum number of unfamiliar systems, so the estimable fraction is smallest and the range of viable designs widest — exactly the conditions under which returning a menu of risk-differentiated plans beats returning a number.

There is a real tension with [[spec-driven-development]]. Notion's workflow writes comprehensive plain-English specs — with code pointers and verification protocols — before handing work to an agent, which is close to the "answer the unknown questions during planning" position Goedecke calls a throwback. The resolution is probably that agents changed the cost structure his objection depends on: his complaint about the planning meeting is that *you can't write or run code there*, and a spec authored interactively with an agent that reads the codebase is not that meeting. Where the essay says exploration is expensive so constrain the design space, spec-driven development says exploration got cheap so explore first. Both can be right at different exploration costs, and Goedecke's framework predicts what should follow: as agent-assisted reconnaissance lowers the cost of "going and looking," the unknown fraction shrinks and the estimable fraction grows. That is a testable consequence of his own model, not something he claims.

Against [[executive-role]], the two accounts of who decides what are more compatible than they first look. Pennarun's Grove-derived claim is that the executive is the least-informed person in the room and should ratify decisions made by those closest to the facts. Goedecke's is that the *duration* comes from above and the *design* from below. Read together they partition the decision cleanly: management owns the constraint, engineering owns the solution inside it — and the failure mode both warn about is the same one, an executive reaching past the constraint to specify the approach.

## Caveats

Single opinionated practitioner essay, no measurement, explicitly grounded in large-tech-company environments with active VP and director attention — a context Goedecke himself concedes may not generalize, since he allows that low-pressure parts of an organization really do run the formal process as written. The strongest claims are the least verifiable: "unknown work always takes 90% of the time" is a figure of speech, not a finding, and "estimates aren't made by engineers at all" is a description of political dynamics he has observed rather than a structural result. Read the essay as a set of moves for operating inside a system that behaves this way, not as evidence that all systems do.

## Sources

- Goedecke, Sean (2026). "How I estimate work as a staff software engineer." <https://www.seangoedecke.com/how-i-estimate-work/> — [[2026-08-03-goedecke-how-i-estimate-work|local copy]]
