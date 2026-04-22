---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2024-02-21-karpathy-technical-accessibility.md
compiled_at: 2026-04-22
model: claude-opus-4-6
confidence: medium
---

# Technical Accessibility

The gap between publishing a technical artifact and making it genuinely accessible is far larger than most builders realize. Karpathy captures the principle as: **"Step 1 build the thing. Step 2 build the ramp."**

## The micrograd case study

Karpathy's [micrograd](https://github.com/karpathy/micrograd) repo — a ~200-line autograd engine that strips backpropagation to its essence — sat on GitHub for months with modest traction despite being well-commented with a thorough README. When he published a video building it from scratch, engagement increased roughly 100x. The code didn't change at all.

The video worked not just for beginners who needed the intro, but for experts who *could* have understood the code on their own but were deterred by the barrier to entry. Even a small cost of engagement — having to reconstruct the author's mental model from the finished artifact — is enough to lose most of your potential audience.

## Why the creator's perspective misleads

The creator builds something piece by piece, molding it over time. This creates what Karpathy and Tim Dettmers identify as an **unintuitively large perception gap**: the creator perceives the finished artifact as simple (because they built it incrementally), while fresh eyes see the accumulated complexity all at once. This gap persists even when controlling for technical expertise.

Dettmers frames the psychological mechanism: material presented all at once triggers an overwhelming "this is too much" reaction that incremental build-up avoids.

## Not marketing — onramping

Karpathy draws a sharp distinction between marketing and accessibility:

- **Marketing** increases the top of the funnel — more people hear about the thing.
- **Building the onramp** expands the width of the funnel — more of the people who encounter it can actually engage with it.

This reframing matters because "marketing" carries connotations of hype or promotion, while onramping is about removing genuine barriers to comprehension. The artifact's quality doesn't change; only its accessibility does.

## The distribution multiplier

A related heuristic from the thread: **spend as much time distributing as you spent creating**. This is consistent with research on academic paper distribution — a 2024 study found that papers highlighted by influential Twitter accounts (@_akhaliq, @arankomatsuzaki) received 2-3x higher citation counts than controls, suggesting that even in academia, discoverability and framing significantly amplify impact.

The implication is stark: a 10x-quality technical artifact with no ramp may have less real-world impact than a 1x artifact with an excellent one. Builders who dismiss this as "not their job" are leaving 10-100x of their work's potential on the table.

## Connections

This principle applies across technical domains: open-source libraries, internal documentation, API design, developer experience. It shares DNA with [[computers-can-be-understood]] — both argue against learned helplessness, but from opposite directions. "Computers can be understood" says the audience *can* do the work; "build the ramp" says the creator *should* lower the cost of that work.

## Sources

- Karpathy, A. (2024). "Thread on technical accessibility." <https://x.com/karpathy/status/1760388761349927356> — [[2024-02-21-karpathy-technical-accessibility|local copy]]
