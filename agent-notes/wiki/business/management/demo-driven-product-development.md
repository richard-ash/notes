---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2026-10-22-kocienda-jobs-demo-review-thread.md
compiled_at: 2026-10-22
model: claude-fable-5-1
confidence: medium
---

# Demo-Driven Product Development

The practice of running a product organization on working demos rather than documents, plans, or slides, with the demo review as the central decision-making ritual. The anchor source is Ken Kocienda's May 2022 X thread on how Steve Jobs actually operated as the iPhone's de facto product manager. Kocienda was the engineer behind the original iPhone keyboard and autocorrect and later wrote *Creative Selection* (2018), a book-length account of the same demo-feedback-iterate loop; the thread is its compressed form.

Everything attributed to Jobs below is Kocienda's recollection. The thread is a single insider's perspective, written with an explicit argumentative aim (a rebuke to conventional product management), so it carries `medium` confidence.

## The method as Kocienda describes it

- **Demos, not documents.** Jobs insisted on concrete, specific demos that showed what the product would be like. Not plans, slides, or "hand-wavy abstract talk."
- **Demos as the organizing standard.** Everyone knew the bar was a demo ready for Jobs' review. Kocienda credits this with eliminating vague thinking across the team.
- **Perfect within scope.** A demo had to be finished to the extent of what it included. Any detail shown was an exact proposal for what might ship. Showing a color or an animation and saying the shade or timing was not yet picked was "doom": the response was "Why are you wasting my time?" or, usually, worse.
- **Time-saving, not theater.** Kocienda frames the harshness as an efficiency mechanism. Nobody produced content that was not the product. The team went directly at the problem and the thing they were trying to make.
- **Taste plus exacting feedback.** The thread says Jobs "knew what he wanted, he had great taste, and he gave exacting feedback at the end of every demo," with clear instructions for the next one. (The tweet reads "It was just macho posturing either," almost certainly a dropped "n't"; the context makes the intended sense unambiguous.)
- **The closing challenge.** Compare this to any product manager you have worked with: do they save time, communicate clearly, focus effort on essentials, and catalyze great results?

Pedraum Pardehpoosh, another iPhone-era Apple engineer, adds in the replies that Jobs' standing instruction was "I want you to show me stuff that makes me crap my pants."

## Why the method works

Kocienda states the rules; the mechanism is mostly implicit. Three things seem to be doing the work.

**A demo cannot defer a decision.** A document can say "color TBD" and remain a valid document. A demo has to render *some* color, so every visible property is a decision already made. The rule that every shown detail is a ship proposal turns the demo from an illustration into a commitment device: the author has to decide, and the reviewer gets to judge the decision rather than a description of a future decision. This is the same reason the "demos beat decks" theme in [[elon-operating-philosophy]] holds. A demo is evidence; a deck is a promise. Musk's demos are mostly external (investors, partners, recruits) and Jobs' were internal, but the asymmetry is identical.

**Feedback lands on the artifact.** Reviewing a demo means reacting to the thing itself, in the medium the user will experience. Reviewing a spec means reacting to prose about the thing, and the translation back to the artifact is where ambiguity re-enters. Kocienda's "clear instructions about what he wanted to see next time" are only possible because reviewer and builder are looking at the same object.

**Narrow scope, high fidelity.** This is where the method departs from the [[minimum-viable-product]] tradition and from Larson's "prefer experimentation over analysis, find the cheapest path" advice in [[product-management-framework]]. Those argue for roughness in exchange for speed. Kocienda's version demands polish but keeps the surface small: one keyboard layout, one animation, one interaction. The two are compatible if you read them as operating on different axes. An MVP is rough across a broad scope to test whether anyone wants the thing. A Jobs demo is finished across a narrow scope to decide exactly what the thing should be. The iPhone team had already settled the first question and was spending all its effort on the second.

## What the method does not cover

The replies raise the right objections, and Kocienda does not answer them in the clipped thread.

- **Direction and resource allocation.** Jason Short and Arun Rao both ask how Jobs decided which products and use cases to pursue, whether there were strategy discussions or analytical documents behind the demos. The thread describes a *review* method, not a *strategy* method. It explains how Apple converged on the right keyboard, not how it decided to build a phone. Rabois's [[how-to-operate]] framing of the CEO as editor fits the review half; the selection half is left open.
- **The reviewer is load-bearing.** The method's quality is bounded by the taste of the person at the end of the table. "Every detail is a ship proposal" produces great products when the reviewer can tell a good proposal from a bad one, and produces expensive premature polish when they cannot. One commenter's objection that human perception is flawed is really an objection to concentrating judgment in one person, which is a fair reading of Apple under Jobs and a poor reading of the demo practice itself. The contrast with [[executive-role]] is sharp: Grove's executive ratifies decisions made by people closer to the facts, while Jobs made the decisions personally, at demo time. The demo method is an operator's tool and presupposes an operator.
- **Demos persuade whether or not they should.** The same property that makes a demo a good internal review object makes it dangerous as a buying object. [[ai-mania]] catalogs the "demo as mind-killer" pathology, where a polished demo overrides stated accuracy caveats and drives procurement. Kocienda's safeguard is the reviewer's expertise and willingness to say "why are you wasting my time." Strip that out and the demo culture inverts into a hype culture.

## Relevance in 2026

Kocienda's closing challenge was aimed at product managers who produce documents for a living. The AI-era PM debate in [[product-management-in-the-ai-era]] frames the split as builders versus information-movers, with AI absorbing the information-moving half. Demo-driven development sits squarely on the builder side: the PM who can put a working demo in front of a reviewer is doing the part of the job that does not get automated. At the same time, the cost of producing a high-fidelity demo has fallen sharply with the tooling described in [[agentic-engineering]], which weakens the old argument for specs (demos were too expensive to use as the primary communication medium). The residual scarce input is the one Kocienda names last: the taste to know what the demo should show, and the clarity to say what the next one should show instead.

## Sources

- Kocienda, Ken (2022-05-27). "People say Steve Jobs was a product genius..." (X thread, with replies). <https://x.com/kocienda/status/1530361503458938880> — [[2026-10-22-kocienda-jobs-demo-review-thread|local copy]]
