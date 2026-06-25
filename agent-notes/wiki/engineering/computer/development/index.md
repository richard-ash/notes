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
- [[phoenix-activity-feed-rendering]] — rendering an activity feed in LiveView with cursor-based pagination, streams, and a reusable function component
- [[low-tech-devex]] — philosophy of preferring battle-hardened, text-based CLI tools (vim, make, tmux, curl) over GUI alternatives for developer productivity
- [[unattended-coding-agents]] — fully autonomous agents that one-shot tasks from description to PR; Stripe's Minions produce 1,300+ merged PRs/week using hybrid blueprint orchestration (deterministic + agentic nodes), and Chris Wood's solo two-agent pipeline (Opus plans + reviews, Sonnet implements in worktrees on a VM, Linear/GitHub as memory, ~500-LOC PRs) as the "delegated slow loop" counterpart to interactive agentic engineering
- [[claude-code-skills]] — taxonomy of nine skill types, design patterns (gotchas sections, progressive disclosure, on-demand hooks), and distribution strategies from Anthropic's internal usage of Claude Code skills
- [[technical-accessibility]] — the gap between publishing a technical artifact and making it genuinely accessible; "build the thing, then build the ramp"
- [[judgment-in-ai-assisted-development]] — coding agents solve time and attention; judgment (maintainability, security, reliability decisions) is now the binding constraint, scalable via skill/datapack ecosystems
- [[vibe-coding-apprenticeship]] — using AI-generated code as a teaching surface under guardrails (explain-before-commit, AI-free debugging, graduated autonomy) to accelerate intern learning
- [[git-commit-messages]] — Beams's seven rules for commit-message style (subject ≤50 chars, imperative mood, body explains *why* not *how*) and why a well-cared-for log is a project's most underused tool
- [[agent-sandboxing-devcontainers]] — running coding agents inside Docker devcontainers with domain-based egress firewalls (Squid), protected-path masking, and explicit task tooling so `--dangerously-skip-permissions` becomes safe to use
- [[spec-driven-development]] — Notion's workflow of writing comprehensive plain-English specs (with code pointers + verification protocols) checked into the repo and handed to Codex to one-shot; specs become the source of truth, updates flow spec-first, plus Notion's Boxy background-agent VMs, AI-augmented standup pre-reads, and the CI-speed-as-agent-productivity argument
- [[html-agent-artifacts]] — Shihipar's case for HTML over Markdown as the human-agent artifact medium: as agents lengthen, the binding constraint shifts to human engagement; compute-allocator mindset; brainstorming/plans/throwaway micro-UIs/living design systems/status reports in HTML; just-in-time documentation
- [[lethal-trifecta]] — Willison's framing of the structural security problem in agent design (private data + malicious instructions + exfiltration channel); why prompt-injection filters capping at 97% is a failing grade; the Camel pattern; OpenClaw as central case study; Challenger-disaster prediction
- [[wrapping-ai-provider-apis]] — Reinhart's argument that unified AI SDKs are unnecessary; ~50-line per-provider Elixir wrappers using Req + SSE parser; cancellation via process messaging; carve-outs for multi-provider products and agent harnesses
- [[phoenix-telemetry-metrics]] — Rezentes's foundation for Elixir/Phoenix metrics: define→emit→scrape→visualize, low-cardinality tags, LiveDashboard for local verification, a provider-agnostic wrapper module, scaling to Prometheus+Grafana, and templated alerts as the step most teams skip
- [[wrong-abstraction]] — Metz's "prefer duplication over the wrong abstraction": the parameter-and-conditional decay pattern, the sunk-cost trap that keeps bad abstractions alive, and the inline-then-rebuild remedy ("the fastest way forward is back")
