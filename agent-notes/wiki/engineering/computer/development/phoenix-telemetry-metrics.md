---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-06-16-measuring-what-matters-metrics.md
compiled_at: 2026-06-16
model: claude-opus-4-8[1m]
confidence: high
---

# Phoenix Telemetry Metrics

A practical foundation for application metrics in Elixir/Phoenix, drawn from Kate Rezentes's ElixirConf US 2025 talk *Measuring What Matters: Metrics from the Start*. The thesis: don't wait for an incident, a slowdown, or a stakeholder's tough question to start measuring. Lay the groundwork early with the tools Phoenix already gives you, and the eventual jump to production-grade observability is a continuation, not a rewrite.

## What a metric is

A metric is a **numerical measurement over time** — every emission carries a timestamp. The canonical example: counting API callbacks. Emit a count when each response is handled, send it to a visualizer, and the dashboard draws a line showing callback volume over time.

**Tags** split one line into many. Attach a `status` tag (`success` / `error`) and the single callback line becomes two, so you can see the success/error split and hover to find the exact moment behavior changed.

### Low cardinality is the discipline

Cardinality = the number of *unique* values in a set. Every distinct tag value becomes a new line on the graph, so tags must have **low cardinality** — `status` (two values) is fine; a user ID or request ID (unbounded) is not, because it explodes the series count and the cost. The companion rule: **measure things that matter** — actions with state, things you'd actually build a dashboard around. Don't measure everything. (Judgment about *what* is metric-worthy is treated as its own skill, adjacent to the [[internal-software-quality]] instinct for where effort pays off.)

## The four-step pipeline

Before a dashboard exists, four steps run in order:

1. **Define** the metric (in `telemetry.ex`).
2. **Emit** it from application code.
3. **Scrape** — a metrics backend (Prometheus) pulls metrics from the app at an interval and pushes them to an endpoint.
4. **Visualize** — the endpoint is the visualizer (Grafana).

A fresh Phoenix app already pulls in `telemetry_metrics` and `telemetry_poller` and wires them into the supervision tree. `telemetry.ex` starts a process whose child list is where the metrics backend gets added; its `metrics/0` function is where metrics are *defined*. A useful quirk: **the first segment of a metric's name is the LiveDashboard tab** it appears under.

Define a metric as a list (e.g. naming segments plus a `tags: [:status]` option), then emit it. Synchronous user actions emit from `handle_event`; recurring internal events emit from `handle_info`. Emitting with tags just means passing a metadata map alongside the measurement.

## Confirm locally with LiveDashboard before merging

You don't need a local Grafana to verify instrumentation works. **Phoenix LiveDashboard** (`/dev/dashboard` → Metrics tab) renders emitted metrics live. Trigger the action a few times, watch the count appear under its tab, and you've confirmed the metric is both *defined* and *emitting* correctly — before the PR even merges. This is the cheapest possible feedback loop and the reason the talk frames getting started as an "atomic task" (à la *Atomic Habits*): low barrier, high reward, builds momentum.

## A provider-agnostic wrapper module

Rezentes's preferred pattern: don't call `:telemetry.execute/3` directly from business logic. Wrap it in a small module exposing helpers like `count/…` that accept the name plus any subset of (count, tags) in any order, and that take the metric **name as a string** rather than a list. Benefits:

- Business code calls `Metrics.count("...")` instead of the raw telemetry API — cleaner call sites, no parameter-order bookkeeping.
- The telemetry provider is isolated behind one module, so swapping backends later (e.g. to OpenTelemetry) doesn't touch core logic.

This is the same separation-of-concerns instinct as [[wrapping-ai-provider-apis]] — a thin per-provider wrapper that keeps the rest of the app ignorant of the vendor — applied to the observability layer.

## Scaling to Prometheus + Grafana

The production step is additive, not a rewrite:

- Add `telemetry_metrics_prometheus_core` (the **core** package, not the bundle). The bundle drags in Cowboy; core lets you stay on **Bandit** — relevant if you're trying to get Cowboy out of your dependency tree (other deps using Cowboy will still pull it in).
- Add the Prometheus process to `telemetry.ex`'s child list, plus a controller exposing the scrape endpoint and a route to it.
- Stand up a local Grafana, point Prometheus at it, and set the **scrape interval** (5s is fine for local dev; production wants something coarser). Grafana defaults: `localhost:3000`, login `admin`/`admin`.
- Query the metric in a Grafana panel to build dashboards.

## Alerting is where most teams stop too early

The talk's strongest opinion is about **alert quality**, and Rezentes argues it generalizes across visualizers even if your stack differs. Most people create an alert rule, set a threshold (e.g. "≥1 metric with `status=error`"), point it at a contact point (Slack / PagerDuty / email), and stop. The result is a raw, unreadable alert: you have to *think* to parse it, and its link goes nowhere.

The fix is to **template the alert** (Grafana templates in Go): make it state plainly which alert is firing and link directly to the relevant dashboard panel — vertical markers showing when alerts fired. A good alert tells you exactly what's wrong and takes you straight to the monitoring. This echoes the broader principle in [[technical-accessibility]]: shipping the instrument isn't enough; you have to build the ramp that makes it usable under pressure.

## The atomic task — where to start

Rezentes prescribes a graduated on-ramp depending on where your team is:

- **Metrics already exist** → find a poorly-formatted alert, template it, wire it to a contact point. Low effort, immediately appreciated.
- **Noisy alerts** → study the dashboard behind a constantly-firing alert; either the dashboard/thresholds are misconfigured (fix them) or there's a real system issue (you've just learned to track issues through metrics). Then add your own metric to a feature you're working on, with its own dashboard and alert.
- **No metrics at all** → clone her observability-pillars repo, learn the define→emit→LiveDashboard loop locally, then spin up local Grafana and experiment. All of it is free.

The payoff compounds outward: code-performance metrics → DevOps system-health metrics (CPU, RAM, DB connections) → business metrics (revenue per feature for leadership, peak-time demographics for marketing). The throughline is **confidence in the application** — for the team and for stakeholders.

## Sources
- Rezentes, Kate (2025). "Measuring What Matters: Metrics from the Start." ElixirConf US 2025. <https://www.youtube.com/watch?v=7s4fy1SUaUU> — [[2026-06-16-measuring-what-matters-metrics|local copy]]
