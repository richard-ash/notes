---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2019-05-14-keathley-building-resilient-systems-stacking.md
compiled_at: 2026-10-19
model: claude-fable-5-1
confidence: medium
---

# Resilient Application Boot

How an Elixir service should come up, in what order, and what each stage has to guarantee before the next one is allowed to exist. Chris Keathley, then a senior engineer at Bleacher Report (the auto-transcript renders it "Fletcher Park") and a co-host of the Elixir Outlaws podcast, gave *Building Resilient Systems with Stacking* at ElixirConf EU 2019 in Prague. He opens by disowning the title: the talk is really "how to boot your applications correctly," and it spends thirty minutes on a problem most people consider solved. The claim is that if the boot sequence is right, with the right guarantee at each layer, then graceful failure handling, feedback to neighbouring systems, and insight for operators fall out of the structure instead of being bolted on afterwards.

## Framing: resilience is not scaling

Keathley separates two things the Elixir community tends to run together. Scaling in the "two million WebSocket connections" sense is something the BEAM largely gives you. Resilience, "an ability to recover from or adjust easily to misfortune or change," has to be designed. His reference text is Richard Cook's 1998 paper *How Complex Systems Fail* (<https://how.complexsystems.fail/>), eighteen short theses written by an anaesthesiologist about medical systems that transfer directly to software. The one Keathley builds on is thesis five, *complex systems run in degraded mode*: the system works only because of redundancy and because people keep it working despite many latent flaws, with components "failing and being replaced continuously." At scale something is always broken; the engineer's job is to stop two simultaneous faults from combining into a catastrophe.

Three further premises set up the design:

- **Systems have dependencies, all the way down.** The thing you deploy is not your Elixir code but the box drawn around it together with its web server, database, cache, and queue, each of which is itself a complex system (Kafka "is just a bunch of files and a ZooKeeper").
- **Failure is decided by the client, not the service.** If a downstream call fails and the error surfaces to the caller, the caller experienced an outage regardless of how healthy your process tree looked. This holds in a monolith; services only multiply the opportunities.
- **Humans are a dependency too.** The people paged at three in the morning are what actually keeps the system up, so they need first-class inputs of their own. "There's only so many problems Kubernetes can solve for you. Humans are not one of them."

From these he derives the three goals every system should meet: handle failure gracefully, provide feedback to other systems, and give insight to operators.

## Stacked design

The method, which Keathley says Bleacher Report borrowed from airline-industry practice, is to arrange the boot as layers, each holding a guarantee before the next layer starts. Every layer answers the same two questions: what must already be true for this to start, and what does this layer promise to the one above it?

| Layer | What starts | Guarantee it provides | On failure |
|---|---|---|---|
| 0 | System config, the BEAM, the application, runtime config | Every required config value is loaded into ETS | Halt the boot |
| 1 | Dependencies you own (the Phoenix endpoint) | The node can answer a readiness probe, initially with 500 | Load balancer keeps it out |
| 2 | Connections to external systems (database pool) | Connection processes exist and are trying, with backoff | Readiness stays 500 |
| 3 | Feedback: readiness wired to dependency status, watchdog, alarms | Load balancer and operators learn about state changes | Alarm set, node drained |
| 4 | Calls to services you don't control | Circuit breaker plus cached fallback | Serve stale, or fail fast |

The rest of the talk walks the layers in order.

## Layer 0: no configuration, no boot

The runtime boot is system configuration (SSH, VM flags, the things that must exist before the BEAM does), then the BEAM, then the application, then runtime configuration. Keathley is emphatic that `config/*.exs` Mix configuration is the wrong place for anything that varies by environment at runtime, such as the Phoenix port or the database URL; Bleacher Report wrote that into its onboarding docs, and the talk predates the language-level fix (see temporal notes).

The mechanism is to make configuration the first child in the supervision tree. A `Config` GenServer takes a declaration of the keys the application needs, creates an ETS table, loads each value (from `System.get_env/1` in the example, but equally from etcd, Vault, or a parameter store), and stores it. Loading is a recursive function that retries with light backoff, and if it ultimately cannot produce a value it halts the boot. Keathley's reasoning: you do not want a process tree that is up with no assurance it is configured, and a halt at boot is far easier to diagnose than a half-configured service that fails on its first request. The pattern became his `vapor` library.

Halting is a deliberate fail-closed decision of the kind [[system-design]] says must be made per feature rather than by policy. A node that cannot read its configuration should never enter the load balancer, and on Kubernetes the resulting `CrashLoopBackOff` is itself the operator signal. Everything later in the tree reads configuration with a plain ETS lookup, because supervisor ordering guarantees the table exists.

## Layer 1: the endpoint before its dependencies

Phoenix's endpoint is the next child. Its `init/2` callback runs after `Config` is up, so it can ask the config process for the port and merge it into the endpoint's own configuration. Keathley then adds an `UpController` whose action returns 500 by default. The point of bringing the endpoint up before any external connection is that the app "does not exist in a vacuum": the load balancer and Kubernetes probes are going to ask whether it is healthy, and a meaningful 500 is a better answer than a refused connection.

What the talk calls the "up" endpoint is specifically a *readiness* probe, not a *liveness* probe, a distinction the talk does not draw but that the layers below depend on. Readiness controls whether traffic is routed to the pod; liveness controls whether Kubernetes restarts it. If the same endpoint, which will shortly start reporting database status, were wired as the liveness probe, a database outage would make Kubernetes kill and restart every pod in a loop, adding a restart storm to the outage. The dependency-aware check belongs on readiness only.

## Layer 2: start disconnected

The database is a worker under the application supervisor that is itself a pool supervisor starting N connection processes. Keathley's rule, which he says newcomers to Elixir struggle with most, is that every one of them starts *disconnected*, with no assurance that the database exists. "Supervisors are about guarantees": a supervisor's promise is that its children are running, and a child whose `init` blocks on or crashes without a remote resource turns that promise into one the supervisor cannot keep. His scenario is auto-scaling under load: the new nodes are coming up precisely because the database is overwhelmed, so their connection attempts may fail for a while, and a tree that cannot start without a database cannot help recover one.

The implementation is a small state machine in a GenServer. `init` returns immediately and sends itself a `:connect` message; the handler attempts the connection and on success moves to `:connected`, on failure schedules another attempt after a backoff with jitter. The process is alive, supervised, and restartable the whole time. Connection is a state it moves into, not a precondition of its existence.

Two notes beyond the talk. Fred Hebert made the same argument in 2015 in *It's About the Guarantees* (<https://ferd.ca/it-s-about-the-guarantees.html>): `init` should do only what it can guarantee, and connecting to a remote resource is not that. And Ecto already follows the rule. `DBConnection` pools start disconnected and reconnect with configurable backoff (`backoff_type`, `backoff_min`, `backoff_max`), so a `Repo` child needs nothing extra; the lesson applies to the clients people write by hand for Redis, Kafka, gRPC, and HTTP keep-alive pools, where a `connect!` in `init` is the common mistake. The structural companion is [[correctness-oracles]]: Wilton's rule that a `:one_for_one` supervisor is only safe when no child depends on an unmonitored sibling is the same discipline applied to the shape of the tree rather than the behaviour of one child.

## Layer 3: tell the load balancer, then tell the humans

Once connections can exist, the readiness check becomes real: `UpController` calls a database status check (as simple as `SELECT 1`) and returns 200 if it succeeds and 500 otherwise. That is feedback to the first external system, the load balancer, which now takes nodes that cannot reach the database out of rotation or never admits them.

Feedback to operators uses what Keathley calls his favourite under-discussed Erlang feature, SASL alarms. A separate *watchdog* process polls database status on a timer and runs a two-state machine, degraded or connected, with a counter of consecutive passing checks. It starts degraded with the counter at zero. A failure while connected sets an alarm immediately via `:alarm_handler.set_alarm/1`. A success while degraded increments the counter, and the alarm is cleared with `:alarm_handler.clear_alarm/1` only after three consecutive passes. Keathley names this hysteresis: alarms should not flap on a single good packet. The asymmetry (trip on one failure, clear after three successes) is the design, not an omission. He uses a GenServer for slide space but recommends `gen_statem` for the real thing.

The payoff is that `:alarm_handler` is a `gen_event` manager whose default handler only writes to the error log. Swapping in your own handler, a module with `handle_event/2` clauses for `{:set_alarm, {:database_disconnected, _}}` and `{:clear_alarm, :database_disconnected}`, lets you page Opsgenie, post to Slack, emit to Datadog, send a recovery notice, or run remediation code anywhere in the system. Because it is plain Elixir, any subsystem can raise alarms into the same channel. A bonus the talk does not mention: Erlang's `os_mon` application already raises `:disk_almost_full` and `:system_memory_high_watermark` through the same handler, so a custom handler picks those up for free.

Alarms and metrics are complementary rather than competing. An alarm is a *state* with set and clear events, which is why hysteresis lives naturally there; a metric is a sample, and alert rules over metrics ([[phoenix-telemetry-metrics]], [[grafana-alerting]]) reconstruct state by thresholding. The alarm approach keeps the state transition inside the application, next to the code that knows what "degraded" means, and uses the external tooling only for delivery.

One caution Keathley does not raise. A readiness check that fails whenever the database is unreachable turns a database outage into the removal of every node from the load balancer at once, converting degradation into total outage, including for any traffic the cache in layer 4 could have served. AWS's Builders' Library essay *Implementing health checks* (<https://aws.amazon.com/builders-library/implementing-health-checks/>) describes exactly this failure mode in dependency health checks and recommends failing open when a dependency check fails fleet-wide. Which dependencies are allowed to drain a node is the fail-open/fail-closed decision from [[system-design]] again, taken per dependency.

## Layer 4: services you don't control

The last layer is the downstream service your handler calls on behalf of a client. When it degrades, its errors propagate to your clients, who by the earlier premise decide that you are down. Even without overload, you are failing to serve.

**Circuit breaker.** Bleacher Report uses Jesper Louis Andersen's `fuse`, which Keathley calls very well tested and highly optimised. Before each call the code asks `:fuse.ask(name, :async_dirty)`, which reads the fuse state from ETS without a round trip through the fuse process, so the check itself cannot become a bottleneck on the request path. If the fuse is `:ok`, make the call; on a failure call `:fuse.melt(name)`. Enough melts inside the configured window blow the fuse, after which `ask` returns `:blown` and the handler returns a "service down" response immediately rather than queueing more doomed requests. This is the mechanism [[system-design]] prescribes in place of blind retries.

**Write-through cache as fallback.** Depending on how stale the data may be, successful downstream responses are written into an ETS table keyed by request. When the fuse blows, reads come from the table instead, which Keathley notes is far faster than the live service. The cost is consistency: the downstream data may have changed, and the trade has to be made with eyes open. Where the staleness bound is acceptable this is the layer that turns a dependency outage into Cook's degraded mode rather than an outage of your own.

**The sledgehammer problem.** Circuit breakers cut all traffic. When the downstream service begins to recover, the fuse resets, the full load returns at once, and the half-recovered service falls over again, so the breaker trips again, at three in the morning. Keathley's answer, still exploratory in 2019, was to borrow TCP congestion control, additive increase and multiplicative decrease (AIMD), and adapt the volume sent to a downstream system to what it can currently absorb, using the then-new Mint HTTP client as the substrate. This is the only part of the talk that is a research direction rather than practice; the temporal notes record where it went.

## Why thirty minutes on booting

Keathley's closing argument is that the three goals were never separate problems. If each layer only starts once the layer below holds its guarantee, then a lost database connection is already visible to the load balancer (readiness flips), already visible to operators (the watchdog raises an alarm), and already handled for clients (the fuse and the cache), without anyone writing failure-handling code after the fact. The runtime is "the fulcrum upon which we'll place the lever": the BEAM provides supervisors, ETS, `gen_event`, and alarms, and the design is mostly a matter of using them in the right order. The same conviction, that the BEAM's runtime-enforced guarantees are a differentiator rather than a detail, is what Valim and McCord argue from the agent side in [[programming-languages-for-agents]] and [[beam-in-the-agent-era]]; this talk is the 2019 operational version. It also puts a price on each dependency added to the stack, which makes the argument of [[choose-boring-technology]] concrete: every box in the diagram needs a disconnected-start client, a readiness contribution, a watchdog, and a breaker.

## Temporal notes

- **Releases.** Keathley recommends Distillery as the only real option. Elixir 1.9 shipped `mix release` in June 2019, two months after the conference; Distillery is now in maintenance mode and `mix release` is the default.
- **Runtime configuration.** The Mix-config argument the talk calls contentious was settled by `config/runtime.exs` in Elixir 1.11 (October 2020), which is evaluated inside the release at boot; Phoenix later deprecated the endpoint `init/2` callback in its favour. Keathley's `vapor` library still exists for the cases `runtime.exs` does not cover (typed providers, multiple sources, watching for changes), but the plain port-and-database-URL case no longer needs a config process. The idea that unloadable config should halt the boot survives: a `raise` in `runtime.exs` does exactly that.
- **Adaptive concurrency.** The AIMD direction became Keathley's `regulator` library (2020), which implements AIMD and gradient-based concurrency limiters in the style of Netflix's `concurrency-limits`, and the Mint-based work fed into Finch (2020), the pooled HTTP client Keathley helped build.
- **Kubernetes probes.** Startup probes (GA in Kubernetes 1.20, December 2020) now cover the slow-boot case the talk handles by returning 500 from readiness until layer 2 is up; readiness remains the right place for the dependency check.
- **Fuse and alarms.** `fuse` is still maintained with the same interface; `:alarm_handler` and `os_mon` are unchanged since 2019.

## Sources

- Keathley, Chris (2019). "Building Resilient Systems with Stacking." ElixirConf EU 2019, published by Code Sync. <https://www.youtube.com/watch?v=lg7M0h9eoug> — [[2019-05-14-keathley-building-resilient-systems-stacking|local copy]]
