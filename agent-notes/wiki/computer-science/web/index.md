# Computer Science > Web

Browser platform topics: rendering pipeline, animation, CSS/JS performance, and frontend APIs.

## Articles

- [[web-animation-performance]] — Comeau's CSS-vs-JS animation analysis: the real distinction is main thread vs compositor thread, not CSS-vs-JS; Motion escapes the main-thread trap via WAAPI while GSAP trades it away for expressive power
- [[local-first-architecture]] — Brotzky's reverse-engineering of Linear: server as sync target not source of truth, IndexedDB-backed MobX object pool, optimistic mutations, per-property observables (one delta = one cell re-render), render-first-authenticate-second, and the bundler/preload/service-worker first-load playbook
- [[websockets-vs-sse]] — Valim's reframing of the realtime-transport debate as ordering, not latency: two data-bearing streams (SSE + Fetch) can render a stale snapshot last and never converge, which is not "eventual consistency"; the fixes (single delivery stream, doorbell-and-refetch, client-side reordering) each cost latency or complexity, while one bidirectional connection orders reads and writes for free
