---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/web/2026-05-26-css-vs-javascript-animation.md
compiled_at: 2026-05-26
model: claude-opus-4-7
confidence: high
---

# Web animation performance: main thread vs. compositor

The conventional wisdom that "CSS animations are faster than JavaScript animations" is correct in outcome but wrong in mechanism. The real distinction isn't computational cost — it's **which thread the animation runs on**.

## The mechanism: two threads, one bottleneck

Browser rendering happens on two relevant threads:

- **Main thread** — runs JavaScript, parses fetch responses, reconciles React state, handles event listeners, and performs layout/style recalculation. In a modern SPA, this thread is busy most of the time.
- **Compositor thread** (often described as a separate animation thread) — runs the browser's low-level animation engine. Independent of JavaScript execution.

CSS keyframes and CSS transitions are declared once and then handed off to the compositor. A `requestAnimationFrame` loop that mutates `element.style.transform` on every frame runs on the main thread, so it stutters whenever the main thread is blocked — by a React re-render, a fetch response landing, anything.

Comeau emphasizes that the cost of *crossing the JS→DOM bridge* and *recomputing transform values per frame* is negligible on modern engines, even on low-end devices. The stutter is not about CPU work; it's about scheduling contention on a single thread.

This is also why "spinners that freeze right before the UI updates" happen — the same main thread driving the spinner animation has to stop and reconcile incoming data.

## Why Motion (formerly Framer Motion) escapes the trap

A naive read is that all JS animation libraries inherit the main-thread limitation. Comeau's surprising data point: **Motion and GSAP are both JS libraries, but only Motion stutters when the main thread is blocked. Motion does not.**

The mechanism is the **Web Animations API (WAAPI)** — a JavaScript interface that delegates to the same compositor-thread animation engine that CSS keyframes use. Motion is essentially a JS-ergonomic facade over WAAPI: you write JavaScript, but the animation runs where CSS animations run.

GSAP doesn't use WAAPI because WAAPI cannot express everything GSAP supports (complex tweening, timelines, plugins like MorphSVG, etc.). Comeau frames this as a trade-off, not a mistake: GSAP buys expressive power by paying the main-thread cost.

## Practical hierarchy

Comeau's working order, in his own work:

1. **CSS transitions / keyframes** by default. Compositor-threaded, declarative, zero runtime cost in JS.
2. **Motion (WAAPI-backed)** when CSS alone can't express the animation (orchestration, gesture-driven motion, layout animations).
3. **GSAP or raw `requestAnimationFrame`** when you genuinely need their expressive power and accept the main-thread cost.

He notes that CSS has absorbed so many former JS-only capabilities — View Transitions, `linear()` easing, scroll-driven animations via Animation Timeline — that the "CSS can't do this" cases keep shrinking.

## What the article leaves implicit

- **Which properties qualify for compositor offload.** Even within CSS, only `transform`, `opacity`, and `filter` are reliably composited. Animating `width`, `top`, or `background-color` triggers layout or paint and re-enters the main thread regardless of whether you used CSS or JS. Comeau's example uses `translateX` for exactly this reason but doesn't spell out the rule.
- **`will-change` and `transform: translateZ(0)`** as hints to promote elements to their own compositor layer. The article assumes the browser makes the right call, which it usually does on `transform`/`opacity` animations.
- **WAAPI is not new.** It's been broadly supported since ~2020. The "use WAAPI" advice has been available longer than Motion's marketing implies; Motion's contribution is the React-ergonomic surface, not the underlying performance trick.

## Related concepts

- [[generative-ai-as-pattern-generation]] — Evans's argument that LLMs are great at syntax but the engineer's judgment about *which pattern fits* is the load-bearing work; Comeau makes the same point at the end ("LLMs are great at generating syntax, but we still need to use our own judgment") and uses it to motivate his Whimsical Animations course.

## Sources

- Comeau, Josh W. "CSS vs. JavaScript." <https://www.joshwcomeau.com/animation/css-vs-javascript/> — [[2026-05-26-css-vs-javascript-animation|local copy]]
