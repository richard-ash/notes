---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2025-08-26-mjd-purpose-of-code-review.md
compiled_at: 2026-07-03
model: claude-opus-4-8[1m]
confidence: medium
---

# Code Review as Maintainability Check

Mark Dominus argues that most people misunderstand what code review is *for*. The primary purpose is **not** to find bugs, and certainly not to certify code as bug-free — "anyone who depends on code review to find bugs is living in a fool's paradise." His claim is that it is not *in general* possible to find bugs by examining code (later clarified as math jargon: like "even numbers are not in general divisible by 4" — many are, but you can't rely on it).

Instead, the primary purpose is to **find code that will be hard to maintain**. The reviewer tries to understand what the code does and how. If they can't, that code will be hard to maintain later — and it should be fixed *now*, while the author is still familiar with it.

## Why the reframing is practically better

Dominus's sharpest point is about the *task structure* the reviewer is handed, not the abstract goal:

- **"Find bugs"** is an unbounded, failure-only task. Success isn't guaranteed even on a good day; there's no principled stopping point ("how hard, for how long?"); and you can always be blamed later for the bug you missed.
- **"Understand this, and complain if you can't"** is bounded and almost always achievable. You don't have to understand everything — you just write a note about each part you didn't. Done = you've tried to understand it all and noted every gap. Achievable even on a bad day.

This is the operational core: reframing review from *auditing for defects* to *testing for legibility* turns an open-ended search into a checklist you can actually finish. Pozorvlak's corollary: **"if the reviewer doesn't understand it, that is itself a bug and should be fixed"** — and often the fix is simply pasting the author's answer to the reviewer's question into a code comment.

## The maintainability lens connects to the rest of dev practice

The "hard to maintain = fix it now" stance is a direct application of the [[internal-software-quality]] thesis (cruft has negative cost; it slows teams within weeks). Andreas (dj3ei) rephrases the goal as minimizing how much code a *future* developer must read to get anything done — messy code forces you to consider the whole codebase for any small task, which is the same failure mode [[wrong-abstraction]] describes. Making the change legible while the author is still in context is cheaper than reconstructing intent later, echoing the "explain *why*, not *how*" discipline of [[git-commit-messages]]. And the whole exercise presupposes the [[computers-can-be-understood]] posture: the reviewer's job is to *build a mental model*, and a gap in that model is a defect in the code, not the reviewer.

## Nuances and pushback from the thread

Dominus's framing is deliberately strong, and the replies sand off the edges:

- **He never claimed review doesn't find bugs.** "Of course it finds bugs" — just not all or even most of them. The disagreement (David Zaslavsky, Kyle Brown, Mark Rotteveel) is whether bug-finding belongs *in the job description*. Rotteveel's case for including it: review catches bugs precisely where both the code *and its tests* encode the wrong intent — a class tests structurally cannot catch.
- **Tests and review divide labor.** Several commenters treat "what are tests for, then?" as the retort — but the thread converges on review *checking test quality*: coverage gamed by copying logic into expectations (testing nothing), regression tests that lock in wrong behavior, date/time tests that only break at month rollover. Review is where a human notices the green checkmark is lying.
- **Teaching and diffusion are large secondary purposes.** Converging authors onto team conventions so they stop reproducing the problem (Jonathan Hartley), knowledge transfer surfacing weak design decisions (Karl), ensuring ≥2 people have seen every part of the codebase (Pozorvlak, dave — to which Dominus dryly replies "the triumph of hope over experience").
- **Style/readability comments are legitimate.** If the point is maintainability, "I have zero problems with the functionality but won't let bad practices through" (Mark Gardner) is on-mission, not bikeshedding.
- **Running the code isn't the reviewer's job** (Olivier Mengué) — CI does that; the reviewer's duty is to raise CI-blindness like missing coverage. Caveat: front-end changes can hide design issues only visible when actually run.
- **The author-explains pattern** (Calamity Jan): the best reviews are where the author narrates their approach — and verbalizing is frequently when the *author* discovers their own bugs. A pre-review walkthrough plus general review formalizes this.

sarah tonin's one-liner captures the whole argument: **"if the primary purpose is to find bugs, or lack of, then it isn't a review, it's an audit."** Or ferret's attempt at the TL;DR: "Looking for bad code, not wrong code."

## Relevance for AI-assisted development

The framing sharpens in the agent era. As machines generate more code (see [[judgment-in-ai-assisted-development]], [[unattended-coding-agents]]), the review question "will a human be able to understand and maintain this?" becomes the binding constraint that generation speed does not relax — and legibility-for-the-next-reader is exactly the property an eager-to-merge agent will not optimize for on its own.

## Sources
- Dominus, Mark (2025). "Post on the purpose of code review." <https://mathstodon.xyz/@mjd/115096720350507897> — [[2025-08-26-mjd-purpose-of-code-review|local copy]]
