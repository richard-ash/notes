---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2024-04-29-dhh-ci-on-developer-machines.md
compiled_at: 2026-06-29
model: claude-opus-4-8[1m]
confidence: medium
---

# Local CI on Developer Machines

In April 2024, DHH (David Heinemeier Hansson) announced that 37signals was dropping its remote CI runners and moving continuous integration **back to developer machines**. The argument: for a normal-sized web app, modern multi-core hardware runs the full verification suite faster than a remote runner can, and without the operational overhead of a CI platform.

## The numbers

For HEY (~55,000 lines of Ruby, ~5,000 test cases, plus 300 system tests that hit the full database stack without mocking):

- Remote BuildKite CI: **~5m30s** to run Rubocop style rules, Brakeman security scans, and the model/controller/system tests.
- A local Intel 14900K (20+ cores) or M3 Max (16 cores): the same work in **under 2m45s** — less than half the time.

DHH attributes the gap to two things: (1) the overhead a remote runner can't avoid — setup/teardown, isolation, pipeline management, artifact shuffling — and (2) local desktop CPUs simply being faster at burst-parallel work than wide server machines (peak boost clocks). On the developer's machine the app is already checked out and set up, so all of that CI scaffolding "just disappears."

## How it works: `bin/signoff` + branch protection

The mechanism is deliberately low-tech — a ~50-line bash script DHH dubbed `bin/signoff`:

1. The developer runs `bin/signoff` locally. It runs the same lint/security/test battery the remote CI used to.
2. On success, it reports a passing **signoff check** back to the PR on GitHub.
3. A **GitHub branch protection rule** prevents merging to `master` without that passing signoff check.

The result is the same "no unverified code reaches master" guarantee as cloud CI, but "burning none of the cloud calories." When someone suggested Dagger or just running the BuildKite agent locally, DHH's reply captured the ethos: *"Any time I can replace a fancy setup with a 50-line bash script is going to be a good day."* Even self-hosting the runners (which 37signals was already doing) still carries the isolation/setup overhead that local execution sidesteps.

This is the [[low-tech-devex]] philosophy applied to CI: a battle-hardened bash script plus a platform-native gate (GitHub branch protection) instead of a dedicated engine or service. It also echoes [[choose-boring-technology]] — spend no innovation tokens on a CI platform you don't need.

## The scaling caveat

DHH is explicit that this doesn't generalize to everyone. A Shopify- or GitHub-scale monorepo (millions of LOC, suites that take hours) cannot run its full battery on a laptop — those orgs genuinely need distributed, sharded, cached remote CI. His claim is about the long tail: *"99.99% of all web apps are much closer to HEY in breadth"* and are paying for CI infrastructure heavier than their codebase warrants. The underlying principle is to match stack complexity to the app's actual needs, and to actively **remove** layers as hardware improves rather than accreting them.

### Unaddressed tradeoffs

The source doesn't dwell on the costs of moving the verification loop onto the developer's machine, which are worth naming:

- **The machine is blocked.** A ~2m45s run ties up the developer's CPU (and fans) mid-flow, where a remote runner would absorb it asynchronously. In practice this pushes teams toward running signoff as a pre-push/pre-merge gate rather than on every commit.
- **Environment drift.** "Works on my machine" is exactly the failure mode hermetic remote CI was built to kill. Local CI re-exposes it unless the team standardizes runtime/toolchain versions (the problem Rails 8.1 later addressed; see below).
- **Trust.** A signoff check is asserted by the developer's machine, not an isolated third party. It's only as trustworthy as the script and the honesty of who ran it — fine for a small high-trust team, weaker as a hard security boundary.

## Temporal note: this shipped in Rails 8.1 (2025)

What began as 37signals' internal `bin/signoff` became a first-class Rails feature. **Rails 8.1** (beta Sept 2025, released Oct 2025; work led by Jeremy Daer of 37signals) ships local CI as a framework concern:

- **`config/ci.rb`** — a small DSL declaring CI steps (setup, Rubocop style, Brakeman/bundler-audit security, tests) in one place.
- **`bin/ci`** — a runner that executes that exact definition locally, so the local run and any remote run use *one* source of truth (killing the "green locally, red in CI" drift).
- **`gh signoff`** — an optional GitHub CLI extension that marks a PR merge-ready when `bin/ci` passes, or blocks the merge otherwise — the productized version of the 2024 branch-protection setup.

So the durable outcome wasn't "abolish remote CI" but "make local CI a real, standardized artifact" — and notably, the shared `config/ci.rb` definition directly mitigates the environment-drift objection above.

## Sources

- DHH (2024). "We're moving continuous integration back to developer machines." (announcement thread) <https://x.com/dhh/status/1785016820740788495> — [[2024-04-29-dhh-ci-on-developer-machines|local copy]]
- DHH (2024). "We're moving continuous integration back to developer machines." <https://world.hey.com/dhh/we-re-moving-continuous-integration-back-to-developer-machines-3ac6c611>
- FastRuby.io (2025). "Rails 8.1 Local CI as First-Class Support." <https://www.fastruby.io/blog/rails-8-1-local-ci.html>
- Rails (2025). "Rails 8.1: Job continuations, structured events, local CI." <https://rubyonrails.org/2025/10/22/rails-8-1>
