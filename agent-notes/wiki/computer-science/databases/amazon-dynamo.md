---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2026-04-27-amazon-dynamo-sosp2007.md
  - agent-notes/raw/computer-science/databases/2026-03-27-implementing-amazon-dynamo-in-elixir.md
compiled_at: 2026-04-27
model: claude-opus-4-7
confidence: high
---

# Amazon Dynamo

**Dynamo** is the highly available, eventually consistent key-value store Amazon built around 2007 to back stateful core services like the shopping cart, session store, best-seller lists, and product catalog. The 2007 SOSP paper by DeCandia et al. is one of the most influential systems papers of its decade — it became the canonical reference for the "AP" corner of [[cap-theorem|the CAP triangle]] and seeded a generation of NoSQL databases (Cassandra, Riak, Voldemort, and indirectly DynamoDB).

Dynamo is *not* the same product as **Amazon DynamoDB**, the AWS managed service launched in 2012. DynamoDB borrows the name and inherits some ideas (consistent hashing, single-digit-millisecond latency targets) but is a separate, table-oriented service with stronger consistency options.

## The problem Dynamo solves

Amazon's platform stitches a single page render from over 150 backend services. To hit a customer-facing SLA at the 99.9th percentile, every dependency in that fan-out must be predictably fast and never fully unavailable. For services that only need primary-key access — cart, sessions, catalog — a relational database is over-featured and harder to scale-out. The authors argue from operational experience that **strongly consistent stores have poor availability** in the failure regimes Amazon actually experiences (network partitions, individual node death, whole-datacenter loss).

The shopping-cart constraint is the load-bearing motivation: an "Add to Cart" must **never** be rejected, even during partitions. This forces two unusual choices that pervade the design:

1. The system is **always writeable** — conflict resolution moves from write time to read time.
2. **Applications, not the data store, decide how to merge conflicts** when they happen. The cart service merges divergent carts by union; "last write wins" is an opt-in fallback for services (like sessions) that don't care.

## SLA at the 99.9th percentile

The paper makes a much-cited methodological argument: **measuring SLAs by mean or median is misleading** when the goal is uniformly good experience for *all* customers, not the majority. The expensive long-tail customers (long browsing histories, more personalization) need the same latency the median user gets. A cost-benefit analysis at Amazon showed pushing further into the tail (99.99%) wasn't economical, but 99.9% was. Several Dynamo design choices — load-balanced write coordination, client-driven request routing, the buffered-write optimization — are *only* about reducing tail latency at the 99.9th percentile.

## Five core techniques

Dynamo synthesizes well-known distributed-systems primitives. The paper's clearest contribution is the *combination* and the production validation, not the individual ideas.

### 1. Consistent hashing with virtual nodes for partitioning

The hash space is a ring; both keys (MD5 of key) and nodes are positioned on it; a key is owned by the first node clockwise. Naïve consistent hashing distributes load poorly and ignores hardware heterogeneity, so each physical node owns many **virtual nodes** (tokens) on the ring. Adding a node steals load proportionally from many neighbors, not just one.

The paper later (§6.2) describes how Dynamo's partitioning evolved through three strategies, ending at "Q/S tokens per node, equal-sized partitions" — fixing the partition boundaries (independent of token positions) made bootstrapping, archival, and Merkle-tree maintenance dramatically simpler.

### 2. Replication via preference lists

Each key is replicated to N nodes (usually N=3). The **preference list** is the ordered set of nodes responsible for a key. The list is constructed to:

- skip token positions so it contains N distinct *physical* nodes (otherwise virtual nodes could collapse replication onto one machine);
- span multiple data centers so a DC outage doesn't lose all replicas.

### 3. Vector clocks + read-time reconciliation for versioning

Every write produces a new immutable version tagged with a **vector clock** — a list of (node, counter) pairs. On read, if multiple causally unrelated versions exist, the system returns *all of them* with their contexts; the client reconciles and writes back the merged version. Reads are decorated with a **context** that the client must echo on the next write, so the system knows what version it descends from.

A practical worry — vector clocks growing without bound — is handled by **clock truncation**: oldest (node, counter) entries are dropped when the list exceeds a threshold (~10). This is theoretically lossy (you can lose the ability to detect that two versions are causally related) but the authors report it has not surfaced in production.

The actual divergence rate in production is striking: in 24 hours of shopping-cart traffic, **99.94% of reads saw exactly one version**, and divergence was driven mostly by concurrent automated writers (busy robots), not failures or human users.

### 4. Sloppy quorums + hinted handoff for transient failures

Dynamo uses a quorum-like protocol parameterized by R (read responses required) and W (write responses required), where R + W > N gives quorum semantics. But unlike a strict quorum, Dynamo writes to the first **N healthy** nodes from the preference list — not necessarily the *top* N. If node A is down, the write that should live on A goes to D with a hint saying "this belongs to A"; D delivers it back to A on recovery (**hinted handoff**). This is what keeps writes alive during transient failures.

The (N, R, W) tuple is the system's main tuning knob:
- **(3, 2, 2)** is the default for most services — balances availability, durability, latency.
- W=1 maximizes write availability (used when nothing must reject a write).
- R=1, W=N is "high performance read engine" mode for read-heavy data like catalog.

### 5. Anti-entropy with Merkle trees for permanent failures

For replicas that diverge over long periods (hinted handoff fails, replica is permanently lost), Dynamo runs background **anti-entropy** comparing **Merkle trees** per key range. Two replicas exchange root hashes; only branches that differ require traversal and key-level transfer. This minimizes both bandwidth and disk reads during reconciliation.

Above and beyond anti-entropy, every read does **read repair**: if R replicas reply with stale versions, the coordinator pushes the latest version back to them in the background.

### Membership and failure detection: gossip + seeds

Membership changes are administrator-initiated (explicit add/remove) and propagate via a gossip protocol — each node syncs with a random peer every second. To prevent **logical partitions** (two admins independently growing two disconnected rings), some nodes are designated **seeds**, externally discoverable and known to all nodes. Failure detection is purely local: A considers B failed if B doesn't respond to A's messages, regardless of whether B is responding to C.

## When the architecture leaks

Two production lessons stand out:

**Buffered writes trade durability for tail latency.** Each node maintains a small in-memory write buffer (~1000 objects) flushed by a background thread. This dropped the 99.9th-percentile write latency by 5x at peak. To recover the lost durability, the coordinator picks one of the N replicas to do a synchronous **durable write** — since the coordinator only waits for W responses, this doesn't slow the operation but reduces the window for buffered-write loss on a node crash.

**Client-driven coordination beats server-driven by ~30ms at p99.9.** Routing through a load balancer adds a network hop and adds variability. Smart clients that pull membership info every 10 seconds and route directly to preference-list nodes cut p99.9 read/write latencies from ~69ms to ~30ms — at the cost of giving clients up to 10s of stale membership state.

## Influence and what came after

The Dynamo paper is the lineage source for an entire family of databases:

- **Cassandra** (originally co-authored at Facebook by Avinash Lakshman, also a Dynamo co-author) — combined Dynamo's ring/partitioning/replication with Bigtable's column-family data model.
- **Riak** (Basho) — closest in spirit to Dynamo, with explicit vector clocks and customer-tunable (N, R, W).
- **Voldemort** (LinkedIn) — open-source Dynamo-style key-value store.
- **Amazon DynamoDB** (2012) — the AWS managed service. Borrows ring partitioning and 99.9th-percentile thinking but is a different product with stronger consistency, secondary indexes, and a structured item model.

The paper's broader influence is the framing that **eventual consistency is not just a fallback but a deliberate primary design point** for systems where availability dominates. The vocabulary it popularized — sloppy quorum, preference list, hinted handoff, the (N, R, W) tuning interface — is now standard.

## Building one yourself: lessons from an Elixir implementation

In a 2026 walkthrough, Jitesh implemented Dynamo from scratch in Elixir on top of ETS, libcluster, and `:persistent_term`. The exercise is a useful test of which parts of the paper are essential versus which are artifacts of Java/BDB. Four implementation lessons stood out — they aren't in the paper but they're load-bearing once you write it:

**The coordinator identity rule is non-optional.** The coordinator for a key must always be the first node in its preference list. If any node is allowed to handle a write locally, different nodes produce different vector clocks for the same key, and conflict detection silently breaks. Forwarding logic isn't a performance optimization — it's a correctness requirement. (The paper alludes to this in §6.4 but doesn't dwell on the failure mode.)

**Stale ring state after a coordinator-process crash is a silent bug.** Jitesh caches ring state in `:persistent_term` to skip the GenServer hop on the read path. If the Ring GenServer crashes and its `init/1` doesn't re-publish to `:persistent_term`, every other process reads pre-crash routing without erroring loudly — preference lists go wrong, keys route to dead nodes, debugging is miserable. Generalizes: any cache primed from a process's state needs to be re-primed on supervisor restart.

**Gossip and the ring form a one-way dependency that must stay one-way.** Gossip calls `Ring.remove_node/1` on death events, which changes the ring, which affects future preference lists. The dependency must be strictly Gossip → Ring; the reverse direction creates a feedback loop that's hard to test. Testing the modules decoupled first made the integration tractable.

**Eventual consistency requires a different debugging stance.** The mental shift is from "why didn't this write propagate immediately" to "will it propagate eventually, and is conflict detection correct when it does." Once that clicks, the rest of the design makes sense.

The Elixir implementation also illustrates how cleanly Dynamo maps onto the BEAM: each subsystem becomes a supervised GenServer (Ring, StorageEngine, Gossip, Replicator, Coordinator); ETS replaces BDB; `:rpc.call` replaces the SEDA messaging substrate. Property-based testing is a particularly natural fit for the vector-clock algebra (the four-way comparison `:after | :before | :equal | :concurrent` has clear algebraic laws to assert against). Default parameters from the paper carry over directly: N=3, R=W=2, 128 vnodes per physical node.

## Implementation notes worth remembering

- Dynamo is implemented in Java with **pluggable storage engines**: Berkeley DB Transactional Data Store (most common), BDB Java Edition, MySQL, in-memory + persistent. Choice depends on object size — BDB for tens-of-KB objects, MySQL for larger.
- Request handling uses an **SEDA-style state machine** per request — the same architectural pattern Welsh, Culler, and Brewer published in 2001.
- A single **MD5 hash** of the key produces the 128-bit identifier used for ring placement. (MD5 is fine here because the only property required is uniform distribution, not cryptographic resistance.)
- Background tasks (replica sync, hinted handoff delivery, Merkle anti-entropy) compete with foreground get/put for disk and locks. Dynamo runs an **admission controller** that monitors foreground latency and throttles background work accordingly — a pattern worth borrowing for any system where housekeeping starves the hot path.

## Sources

- DeCandia, G., Hastorun, D., Jampani, M., Kakulapati, G., Lakshman, A., Pilchin, A., Sivasubramanian, S., Vosshall, P., Vogels, W. (2007). "Dynamo: Amazon's Highly Available Key-value Store." *SOSP '07*. <https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf> — [[2026-04-27-amazon-dynamo-sosp2007|local copy]]
- Jitesh (2026). "Implementing Amazon Dynamo in Elixir." <https://jiteshcodes.com/blog/implementing-amazon-dynamo-in-elixir/> — [[2026-03-27-implementing-amazon-dynamo-in-elixir|local copy]]
