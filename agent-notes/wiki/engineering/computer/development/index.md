# Engineering > Computer > Development

Software development practices, workflows, and tooling.

## Articles

- [[choose-boring-technology]] — default to well-understood technology; spend limited "innovation tokens" only where novelty delivers outsized value
- [[computers-can-be-understood]] — cultivate the belief that any layer of a software system can be understood; build mental models, read source, debug across abstraction boundaries
- [[stacked-pull-requests]] — decomposing large changes into chains of small, individually-reviewable PRs to combat code-review fatigue
- [[internal-software-quality]] — internal code quality has negative cost; cruft accumulation slows teams within weeks, not months
- [[software-migrations]] — large-scale migrations are the only scalable mechanism for reducing cross-cutting technical debt; derisk, enable, finish
- [[react-re-rendering]] — React re-renders start with state changes and cascade downward; React.memo opts out; props don't trigger re-renders
- [[claude-code]] — Anthropic's terminal coding agent: origin story, design principles, session management (context rot, rewind vs. compact vs. clear vs. subagents), and Boris Cherny's advice for dev-tool founders
- [[bazel-ios-modularity]] — Bazel + iOS modular architecture: public/private module pattern, SPM integration via `rules_swift_package_manager`, and ~50% build-time wins from explicit dependency graphs
- [[phoenix-liveview-infinite-scroll]] — fully-virtualized infinite scroll in Phoenix LiveView using `stream/3`, `phx-viewport-top`/`bottom`, and the signed `:limit` option — zero custom JavaScript
- [[swift-sdk-for-android]] — cross-compiling Swift libraries for Android via the Swift SDK, Android NDK, and swift-java JNI bindings
- [[ecto-activity-tracking]] — automatic audit logging in Phoenix by overriding Ecto Repo operations with a Trackable protocol
- [[low-tech-devex]] — philosophy of preferring battle-hardened, text-based CLI tools (vim, make, tmux, curl) over GUI alternatives for developer productivity
- [[unattended-coding-agents]] — fully autonomous agents that one-shot tasks from description to PR; Stripe's Minions produce 1,300+ merged PRs/week using hybrid blueprint orchestration (deterministic + agentic nodes)
- [[claude-code-skills]] — taxonomy of nine skill types, design patterns (gotchas sections, progressive disclosure, on-demand hooks), and distribution strategies from Anthropic's internal usage of Claude Code skills
