---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2025-06-21-good-system-design.md
compiled_at: 2026-08-03
model: claude-opus-5
confidence: medium
---

# System design

Sean Goedecke (GitHub) defines system design by contrast with software design: **if software design is how you assemble lines of code, system design is how you assemble *services***. The primitives shift from variables, functions and classes to app servers, databases, caches, queues, event buses and proxies. His thesis is that good system design is not about clever tricks but about "knowing how to use boring, well-tested components in the right place" — and he is explicit that this is an experience-transfer essay, with the concrete judgment calls admittedly not fully conveyable in writing.

He is also picking a fight with the genre: the LinkedIn "bet you never heard of *queues*" post, the Twitter "never store booleans in a database" clever trick, and — more pointedly — *Designing Data-Intensive Applications*, which he loves but considers not particularly useful for the system design problems most engineers actually hit.

## Good design is self-effacing

Goedecke's diagnostic is aesthetic and inverted: good design looks *underwhelming*. In practice it looks like nothing going wrong for a long time, and it feels like "huh, this ended up being easier than I expected" or "I never have to think about this part of the system." Bad design is often more impressive than good. He is suspicious of systems carrying distributed consensus, several flavors of event-driven communication, and CQRS — either some fundamental bad decision is being compensated for, or the thing is simply over-designed.

The concession is precise and worth keeping: some systems genuinely earn their complexity. But **a complex system that works always evolves from a simple system that works** — starting from scratch with a complex one is the failure mode. (This is Gall's Law, restated without attribution.)

This is the same posture as [[choose-boring-technology]] one level up the stack. McKinley's argument is about the *carrying cost* of novel components; Goedecke's is about the *arrangement* of components you already have. They rhyme because both are really about unknown unknowns: boring components have small ones, and boring topologies do too. Goedecke adds the organizational observation that at a large company the off-the-shelf event bus and caching service already exist, so good system design there "is going to look like nothing" — in ten years he has seen conference-worthy design (hand-rolled data structures enabling otherwise impossible features) once or twice.

## State is the axis everything else hangs off

The essay's real spine is that **stateful components can get into a bad state, and stateless ones cannot**. A stateless service — his example is GitHub's internal PDF-to-HTML rendering API — runs forever if you put it in a restartable container: anything goes wrong, kill it, it comes back correct. A stateful service has no such repair path. A bad row that crashes your application has to be fixed by hand; a full disk has to be pruned or expanded by hand.

The practical rule: **one service owns the state, everything else is stateless around it.** Don't have five services writing to the same table; have four of them send API requests or emit events to the one that owns the writes. He is deliberately less absolutist about reads — sometimes a direct read of `user_sessions` beats a 2× slower HTTP hop to an internal sessions service.

Almost every later section is a corollary of this one. Caching is discouraged *because a cache is state*. Background job queues get a database-backed variant *because Redis persistence is state you can't trust over a month*. Idempotency keys exist *because a retried write is state you can't observe*. Read the essay as one idea with eight applications rather than eight tips.

## Databases

**Schemas.** Aim for human-readable tables: reading the schema should give a rough idea of what the application stores and why. Flexibility is necessary because schema changes get painful at millions of rows, but too much flexibility — everything in a JSON `value` column, or generic keys/values tables — pushes complexity into application code and buys awkward performance constraints. Where to draw the line is a judgment call.

**Indexes.** Match indexes to your common queries, put the highest-cardinality field first (indexes behave like nested dictionaries, so a low-cardinality prefix forces a scan), and don't index everything — each index taxes writes.

**Bottlenecks.** Database access is usually the constraint in high-traffic applications, even when compute is inefficient, because complex applications issue hundreds of sequential queries per request. Four remedies:

- **When querying the database, query the database.** JOIN rather than stitching results in memory. Watch for ORM queries in inner loops turning one `select id, name` into one `select id` plus a hundred `select name ... where id = ?`.
- **The occasional tactical query-split.** Rarely, a query is ugly enough that splitting it is easier on the database. He concedes indexes and hints could probably always fix it, but keeps the tool.
- **Route reads to replicas.** The write node is busy enough. The exception is genuine zero-tolerance for replication lag — usually avoidable by filling in updated fields in memory rather than re-reading immediately after a write. (This "don't read your writes" line was the single most contested point in the Hacker News thread, drawing both "who would ever do that" and "that's way too fiddly.")
- **Beware query spikes**, especially writes and transactions, because overload makes a database slow, which makes it more overloaded. Throttle anything that can generate them, like a bulk-import API.

Replication lag is the practical face of the consistency tradeoffs formalized in [[amazon-dynamo]]; Goedecke's answer is to route around it in application code rather than reason about it in the abstract.

## Slow work, fast work, and the background job

Split out **the minimum amount of work needed to do something useful for the user**, return that within a few hundred milliseconds, and push the rest to a background job — render the PDF's first page immediately, queue the remaining pages.

He treats "background job" as a core primitive worth spelling out: a set of queues (typically Redis) plus a runner service that pops `{job_name, params}` items and executes them, optionally on a schedule. It should be the *first* choice for slow operations precisely because it is such a well-trodden path.

The interesting move is the roll-your-own case. To enqueue something a month out, don't use Redis — persistence isn't guaranteed that long and you can't query far-future jobs conveniently. Instead create a table with a column per param plus `scheduled_at`, and run a daily job over `scheduled_at <= today`. He pairs this with the same trick for caching (below) under a shared principle: **use the idea without using the technology named after it.**

## Caching

The stated inversion: junior engineers learn about caching and want to cache everything; senior engineers want to cache as little as possible. The reason is the state argument — a cache can hold weird data, drift out of sync with truth, or serve stale data that produces mysterious bugs. Hence the rule: **never cache something without first making a serious effort to speed it up.** Caching an expensive SQL query that no index covers is silly; add the index.

Goedecke says he does use caching a lot, and offers the large-object variant of the use-the-idea-not-the-technology move: for results too big for Redis or Memcached (a weekly usage report for a large customer), have a scheduled job write a timestamped blob to S3 or Azure Blob Storage and serve the file directly.

## Events vs. API calls

An event hub (usually Kafka) is the same queue shape as background jobs, but the payload is "this thing happened" rather than "run this job." The canonical example is a `new account created` event fanning out to welcome-email, abuse-scanning, and per-account-infrastructure consumers.

The advice is restraint. Much of the time a direct API request between two services is better: the logs are in one place, it's easier to reason about, and you can see the response. Events earn their keep in two specific conditions — **the producer genuinely doesn't care what consumers do**, or **the volume is high and latency-insensitive** (abuse-scanning every new post).

## Pushing vs. pulling

Pulling is simpler and is how most of the web works, but wastes work when many clients repeatedly request the same data. Pushing — clients register, the server delivers on change — is how GMail avoids the refresh. For *services* rather than browsers, pushing is often obviously right: a hundred HTTP calls when data changes beats serving the same data a thousand times a second.

At a million clients neither wins outright, and either way the work leaves the single server. Pushing means an event queue plus a horde of processors sending pushes; pulling means a fleet of fast read-replica cache servers in front of the application (fast because they never touch the database — potentially just a file on disk or data in memory). In a footnote he notes those cache servers themselves poll or get pushed to, and he doesn't think it matters much: pushing is fresher, pulling is simpler.

The client-side end of this same axis is the subject of [[local-first-architecture]], where the data is pushed all the way down to a local replica and the sync protocol becomes the design problem.

## Hot paths: where to spend design attention

Rather than designing every flow, focus on the **hot paths** — the most critical part and the highest-volume part. In metered billing, the charge decision and the hook consuming all user actions.

His justification is the sharpest budgeting argument in the piece and generalizes past the examples. Hot paths have *fewer possible solutions* — there are a thousand workable ways to build a billing settings page but only a handful of sensible ways to consume a firehose of user actions — and they *fail more spectacularly*, since code triggered on every user action can take the product down in a way a settings page cannot. Design effort should follow constraint density and blast radius, not surface area.

## Logging and metrics

Two habits, both learned from "my most paranoid colleagues":

**Log aggressively on unhappy paths.** Log which condition produced a 422; log every billing decision including the negative ones ("not billing for this event because of X"). He acknowledges the objection — it adds boilerplate and spoils elegant code — and dismisses it, because when an important customer complains you still need to determine *what they did wrong* on their behalf.

**Watch percentiles, not averages.** Alongside host CPU/memory, queue sizes and per-request/per-job timings, track p95 and p99, because a handful of very slow requests are disproportionately your largest and most important users. Averages hide the fact that some users find the service unusable.

This is the design-time counterpart to the instrumentation mechanics in [[phoenix-telemetry-metrics]] and the alert-routing layer in [[grafana-alerting]] — Goedecke is specifying *what* to emit and which statistic to trust, not how to plumb it.

## Designing for failure

- **Killswitches** on every piece of automation (cross-referenced to his separate post): a feature-flag early-return is minutes faster than a deploy, and hours faster during an incident.
- **Retries are not a magic bullet** — blind retries add load to an already-failing service. Wrap high-volume calls in a **circuit breaker** that stops sending after too many consecutive 5xx responses.
- **Idempotency keys** for retried writes, because a 5xx on "bill this user" leaves you genuinely unable to know whether the user was billed. The receiving service records the key and silently ignores repeats.
- **Fail open or fail closed** is a per-feature decision, not a policy. Rate limiting should almost always fail open, so a rate-limiter problem isn't a user-facing incident. Auth should always fail closed: better to deny a user their own data than to hand one user another's. He is candid that many cases sit between these and the tradeoff is genuinely hard.

The fail-open/fail-closed pair is the most portable idea in the essay, because it is a question you can ask of every dependency in a system and get a defensible answer for — and because the two worked examples bracket the range rather than resolving it.

## What he deliberately omits

Monolith-vs-services splitting, containers vs. VMs, tracing, and API design — for three separately-stated reasons: it doesn't matter much (monoliths are fine), it's too obvious (use tracing), or it's too complicated to do justice to (API design). The omissions are load-bearing for reading the rest: he is not claiming a complete theory, and the "monoliths are fine" aside quietly removes the topic most system-design content is actually about.

## Connections

The essay's boring-components thesis is the system-level statement of the same instinct that [[choose-boring-technology]] makes at the component level and [[wrong-abstraction]] makes at the code level — in all three, the recommended move is to resist the impressive structure and accept the duller one that fewer people have to decode later.

The software-design/system-design boundary Goedecke draws at the top is exactly the boundary the [[deep-modules-vs-small-functions]] debate operates *below*: Ousterhout and Martin are arguing about how to assemble lines of code, which by Goedecke's definition is a different discipline with different primitives.

Goedecke later cites this post's stance — that system design is dominated by concrete specifics rather than generic principles — as the basis for a claim in [[expertise-as-llm-leverage]]: he would rather have familiarity with a specific codebase than a deep general understanding of software systems. That is a notable self-limiting move for an essay titled "everything I know about good system design," and the honest reading is that he considers the transferable part genuinely small.

## Caveats

This is a single opinionated practitioner essay, explicitly grounded in one context — SQL databases (MySQL and Postgres), and large-tech-company infrastructure where event buses, job runners and caching services already exist off the shelf. Several recommendations weaken outside that context: "background jobs are a well-trodden path" and "good system design is going to look like nothing" both presuppose the platform is already there, which is precisely what an early-stage team does not have. Goedecke offers no measurement, only pattern recognition over ten years, and says so.

## Sources

- Goedecke, Sean (2025). "Everything I know about good system design." <https://www.seangoedecke.com/good-system-design/> — [[2025-06-21-good-system-design|local copy]]
