# Computer Science > Web

Browser platform topics: rendering pipeline, animation, CSS/JS performance, and frontend APIs.

## Articles

- [[web-animation-performance]] — Comeau's CSS-vs-JS animation analysis: the real distinction is main thread vs compositor thread, not CSS-vs-JS; Motion escapes the main-thread trap via WAAPI while GSAP trades it away for expressive power
- [[local-first-architecture]] — Brotzky's reverse-engineering of Linear: server as sync target not source of truth, IndexedDB-backed MobX object pool, optimistic mutations, per-property observables (one delta = one cell re-render), render-first-authenticate-second, and the bundler/preload/service-worker first-load playbook
