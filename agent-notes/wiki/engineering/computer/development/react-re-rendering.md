---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-09-why-react-re-renders.md
compiled_at: 2026-04-09
model: claude-opus-4-6
confidence: high
---

# React Re-Rendering

React's rendering model is widely misunderstood, even by experienced developers. The mental model is simpler than most expect: **every re-render starts with a state change**, and re-renders cascade downward through the component tree — not upward, and not sideways.

## The core loop

React's job is to keep the UI in sync with application state. Each render produces a snapshot — a description of what the DOM *should* look like. When state changes, React re-runs the owning component and its descendants, produces a new snapshot, diffs the two, and applies the minimal set of DOM mutations.

This is the entire cycle: state change → re-render subtree → diff snapshots → commit DOM changes.

## Two common misconceptions

**Misconception 1: "The entire app re-renders on every state change."** Only the component that owns the changed state, plus its descendants, re-render. Ancestors and siblings in other subtrees are untouched.

**Misconception 2: "Components re-render because their props changed."** Props have nothing to do with triggering re-renders. A parent re-rendering causes *all* of its children to re-render, regardless of whether any props actually changed. React errs on the side of too many renders rather than risk showing stale UI, because components can be impure (reading `Date.now()`, mutated refs, etc.).

## Opting out with React.memo

`React.memo` wraps a component and tells React to skip re-rendering it when its props haven't changed (shallow comparison). This is *memoization* — React reuses the previous snapshot instead of computing a new one.

When to use it:
- Components with many descendants (skipping the subtree is a big win)
- Components doing expensive internal computation

When it's counterproductive:
- Components with many props and few descendants — the shallow-comparison overhead can exceed the cost of just re-rendering
- React is designed to render fast; memoizing everything adds overhead without proportional benefit

## Context and pure components

Context doesn't change the default cascade: if a component's state changes, all descendants re-render whether or not context is involved.

For memoized components, context acts as "invisible props." A `React.memo` component that consumes a context via `useContext` will re-render when that context value changes, even if its explicit props are unchanged. Components that don't consume the context are unaffected.

## The object identity trap

Because components are functions, anything defined inside them is re-created on every render. Inline objects and functions get new references each time, defeating `React.memo`:

```jsx
function App() {
  // New object reference on every render — breaks memoization downstream
  const dog = { name: 'Spot', breed: 'Jack Russell Terrier' };
  return <DogProfile dog={dog} />;
}
```

This is the primary use case for `useMemo` and `useCallback` — stabilizing references so that memoized children can actually skip re-renders.

## Performance profiling

The React DevTools Profiler records per-render snapshots and can report *why* each component rendered (state change, props change, context change). Enable "Record why each component rendered while profiling" in the Profiler settings.

Key caveats from Comeau:
- **Dev-mode timings are misleading.** React is dramatically faster in production. Profile against the deployed build using the browser's Performance tab for real numbers.
- **Lighthouse scores ≠ user experience.** Qualitative testing on real devices (especially lower-end hardware) is more informative than automated scores.
- **Don't over-optimize.** React is fast out of the box. Reach for memoization and profiling *in response to* sluggishness, not preemptively.

## Sources

- Josh W. Comeau. "Why React Re-Renders." <https://www.joshwcomeau.com/react/why-react-re-renders/> — [[2026-04-09-why-react-re-renders|local copy]]
