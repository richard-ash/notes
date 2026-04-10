# Engineering > Computer > Development

Software development practices, workflows, and tooling.

## Articles

- [[choose-boring-technology]] — default to well-understood technology; spend limited "innovation tokens" only where novelty delivers outsized value
- [[computers-can-be-understood]] — cultivate the belief that any layer of a software system can be understood; build mental models, read source, debug across abstraction boundaries
- [[stacked-pull-requests]] — decomposing large changes into chains of small, individually-reviewable PRs to combat code-review fatigue
- [[internal-software-quality]] — internal code quality has negative cost; cruft accumulation slows teams within weeks, not months
- [[software-migrations]] — large-scale migrations are the only scalable mechanism for reducing cross-cutting technical debt; derisk, enable, finish
- [[react-re-rendering]] — React re-renders start with state changes and cascade downward; React.memo opts out; props don't trigger re-renders
- [[claude-code]] — Anthropic's terminal coding agent: origin story, design principles (build for the next model, latent demand, never bet against the model), and Boris Cherny's advice for dev-tool founders
- [[bazel-ios-modularity]] — Bazel + iOS modular architecture: public/private module pattern, SPM integration via `rules_swift_package_manager`, and ~50% build-time wins from explicit dependency graphs
- [[phoenix-liveview-infinite-scroll]] — fully-virtualized infinite scroll in Phoenix LiveView using `stream/3`, `phx-viewport-top`/`bottom`, and the signed `:limit` option — zero custom JavaScript
