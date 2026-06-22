---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/web/2026-06-22-hows-linear-so-fast.md
compiled_at: 2026-06-22
model: claude-opus-4-8[1m]
confidence: medium
---

# Local-first architecture (Linear case study)

A *local-first* web app inverts the conventional client-server relationship: the database the UI reads from lives in the browser (IndexedDB), mutations apply to local memory first, and the server becomes a **sync target rather than a source of truth for the UI**. Dennis Brotzky's reverse-engineering of [Linear](https://linear.app/) is the canonical worked example. He is explicit that he has never seen Linear's code — the article is informed inference from the shipped app, blog posts, and conference talks — so treat the specific config reconstructions as illustrative, not authoritative.

The throughline of the whole piece is one sentence: **the network is the bottleneck, so the win is to hide or eliminate network requests entirely.** Every technique below is a corollary of that.

## The core inversion

A traditional CRUD update is `fetch(PATCH) → await → setState → hide spinner` — ~300ms of latency the user watches. Linear's equivalent is:

```typescript
issue.title = "Faster app launch";  // mutate in-memory MobX observable → UI re-renders synchronously
issue.save();                        // queue a transaction the sync engine batches/flushes in background
```

There is no spinner because there is nothing to await. Co-founder Tuomas has said the sync engine was *literally the first code written* — unusual for a startup, but it's the foundation everything else sits on. Brotzky's pragmatic caveat: most teams don't need a custom sync engine. Libraries like Tanstack Query or SWR get most of the perceived-speed benefit through **optimistic updates** (update state immediately, validate in background, roll back only if the server rejects). The durable principle is that UI responsiveness should not depend on network latency.

## The sync engine: three pillars

The speed is a property of how three pieces *fit together*, not of any one:

1. **The data is already there.** On boot the app hydrates IndexedDB into an in-memory MobX object pool; every UI query hits the pool first, so there's no "loading" state. The two heaviest tables (Issue, Comment) **lazy-hydrate on demand** — "data-level code splitting," the same idea as JS chunking. Startup cost tracks workspace *structure*, not *size*: a 10,000-issue workspace boots about as fast as a 100-issue one.
2. **Mutations don't wait for the network.** A change updates the observable, writes to a durable transaction queue in IndexedDB, and enqueues for the server — all before the network is touched. The server is a *confirmation* step, not a *permission* step. Most invalid mutations are caught before the transaction is even created, so server rejections (which revert the observable with a brief flicker) are rare.
3. **One delta, one cell.** Every property on every model is its own observable, and every component is wrapped in `observer()`. A change to one field re-renders exactly the components reading that field — not the list, not the sidebar. A 50-issue update is 50 cell re-renders, not one list re-render. Update cost scales with *what changed*, not *what's on screen* — which is what keeps a busy multi-user workspace smooth.

Remove any pillar and slowness returns: a local DB without optimistic writes still spins on save; optimistic writes without granular observables still jank on every update; granular observables without a local DB still wait on first load.

## Making the first load feel instant

Local-first solves *steady-state* speed but not *cold start* — the bundle still has to arrive. Linear's first-load playbook (relevant to any CSR app, local-first or not):

- **Ship less code.** Four bundler rewrites (Parcel → Rollup → Vite → Rolldown), each chasing less JS/CSS. Claimed gains: ~50% less code shipped, 30% smaller compressed, time-to-first-paint of the active-issues view down 59% on Safari, memory down 70–80%. The biggest lever is **dropping legacy-browser support** (target `esnext`, no polyfills, no ES5 transpile, no nomodule fallback), then aggressive dead-code elimination and code splitting. Even so, Linear ships ~21 MB of minified JS — but split into *hundreds* of route-level chunks fetched on demand.
- **One chunk per npm package.** Vendor caching becomes fine-grained: bumping one dependency invalidates one chunk instead of a monolithic `vendor.js`.
- **`modulepreload` to flatten the waterfall.** Hundreds of chunks would otherwise create a serial fetch-parse-fetch waterfall. Listing every critical chunk as `<link rel=modulepreload>` in `<head>` fires the requests in parallel before the entry script's first `import`. The `crossorigin` attribute must match the entry script's, or the browser double-fetches.
- **Service worker for "what's needed next."** A precache manifest (~1,200 hashed assets) pulls route chunks/icons/fonts lazily after first paint. Subsequent navigations skip the network entirely; combined with data already in IndexedDB, the app **works offline** — read, create, edit, change status, all queued locally and flushed on reconnect. (Modulepreload = what's needed *now*; service worker = what's needed *next*.)
- **Font loading done right.** A single variable woff2 covers the 100–900 weight axis (no per-weight requests), `font-display: swap` paints the fallback immediately, and `crossorigin="anonymous"` on the preload avoids a double-fetch when CSS later references the font.
- **Inlined app shell.** Enough CSS inlined in `<head>` to paint the loading state with zero stylesheet fetch, plus inline JS that reads `localStorage.splashScreenConfig` and applies remembered shell tokens (sidebar bg/width, dark mode, Electron class) to `document.documentElement` *before any bundle parses*. The splash screen is correctly themed and sized before the app code even arrives.

### Render first, authenticate second

Auth is treated like a mutation: **assume the happy path, verify in background.** Instead of a `/me` round-trip or a parallel JS-readable cookie, the boot script just checks `localStorage.ApplicationStore`:

```javascript
if (localStorage.getItem("ApplicationStore") === null)
  document.documentElement.classList.add("logged-out");
```

If the store exists, the workspace is already in IndexedDB, so render it. The real session token sits in a cookie; the bundle never inspects it. The *next* network call (WebSocket handshake, sync delta, any HTTP request) is what 401s if the session is stale, triggering a redirect to login. The question on boot isn't "do you have a valid session" but "do we have anything to show you" — the same trust-local-reconcile-async pattern as the sync engine.

## Designed for speed (the input model)

A fast engine loses to a slow input model. Linear's keyboard-first design is the other half: single-letter shortcuts for the focused issue, two-letter combos for navigation, modifiers for global actions, and a `⌘K` command palette that searches the **local MobX pool** (not a server) over nearly every action. Every action is also mouse-reachable so beginners aren't alienated. Engineering speed makes a single interaction fast; design speed makes the *path* to each interaction short.

## Animations

The animation discipline overlaps directly with [[web-animation-performance]] — the main-thread-vs-compositor distinction is the load-bearing idea in both. Linear's rules:

- Animate only **composited** properties (`transform`, `opacity`) that run on the GPU off the main thread; sometimes `background-color`/`border-color` (paint, no layout). **Never** animate layout-triggering properties (`width`, `height`, `top`, `margin`, `padding`) — a `margin-left` hover recomputes the layout of every row beneath it, every frame, for the full transition.
- **Know when not to animate.** No transitions on list items; animations that survive *reference their origin* (a popover scales out of the pill it represents) rather than fading in as decoration.
- **Short, asymmetric durations.** Linear's tokens (`--speed-quickTransition: .1s`, `--speed-regularTransition: .25s`) sit well below Material's 200ms / iOS's ~350ms norms. Things appear *instantly* on summon and fade out over ~150ms on dismiss.

## Connections and implications

- The recurring move is **treating the server as eventually-consistent confirmation** — for data (sync engine), for auth (render-first), and for first load (optimistic precache). It's the same architectural bet applied at three layers.
- "Data-level code splitting" (lazy-hydrating heavy tables) borrows the bundler's chunking mental model for the data layer — a useful cross-pollination for anyone scaling a local-first store past the point where the full workspace fits comfortably in memory.
- The stack is deliberately boring (React, MobX, TypeScript, Postgres, a CDN — no RSC, no edge DB, no meta-framework). Brotzky's thesis is that the speed comes from *years of disciplined decisions on a coherent foundation*, not from exotic technology. The hard part is sustaining the craft, not the implementation.

## Sources
- Brotzky, Dennis (2026). "How's Linear so fast? A technical breakdown." <https://performance.dev/how-is-linear-so-fast-a-technical-breakdown> — [[2026-06-22-hows-linear-so-fast|local copy]]
