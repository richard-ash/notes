---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2026-08-02-postgres-listen-notify-scalability.md
compiled_at: 2026-08-03
model: claude-opus-5
confidence: high
---

# Postgres LISTEN/NOTIFY

`LISTEN`/`NOTIFY` is Postgres's built-in pub/sub primitive: a session issues `LISTEN channel`, another session's transaction issues `NOTIFY channel, 'payload'`, and the notification is delivered to listeners when that transaction commits. It lets an application get low-latency wake-ups out of a database it already runs, instead of adding Kafka/Redis/SQS for the "tell me when something happened" half of a workload.

Its reputation is that it doesn't scale. The accurate version: **NOTIFY serializes the commit of every transaction that calls it**, so throughput is capped by sequential commit rate — but that cap applies per *notifying transaction*, not per logical event, which is the whole basis of the workaround below.

## The global exclusive lock

Postgres guarantees notifications are delivered **in transaction commit order**. Outgoing notifications live in a single global queue whose order must match commit order, and the queue insert has to happen transactionally as part of commit. But a transaction's commit order isn't known until it has finished committing — commits take variable time.

Postgres resolves that circularity with a global exclusive lock:

- Taken when a NOTIFY-containing transaction *begins* to commit.
- Held until the transaction is fully committed **and fsync'd to disk**.
- Therefore all notifying transactions commit strictly one at a time.

The expensive part isn't the lock acquisition, it's what's inside the critical section: a disk flush. And because the transactions are serialized, they lose **group commit** — Postgres's normal optimization of batching many concurrent commits into one `fsync()`. Notifying transactions get no amortization of the most expensive operation in the commit path.

The diagnostic signature is distinctive and worth memorizing: **throughput plateaus while CPU, memory, and IOPS all sit low**. Nothing is saturated because nothing is running concurrently. Contrast with an ordinary Postgres bottleneck, where some resource is visibly pinned. If you see a flat ceiling with an idle-looking database, suspect a serializing lock rather than under-provisioning.

DBOS measured this at **~2.9K writes/sec** on a large instance, using the natural implementation: an `AFTER INSERT` trigger on the table that calls NOTIFY on every row.

### The Postgres 19 patch does not fix this

A [commit landing in Postgres 19](https://github.com/postgres/postgres/commit/282b1cde9dedf456ecf02eb27caf086023a7bb71) is often cited as the fix. Per DBOS it addresses a narrower problem — many channels with listeners each subscribed to one specific channel — and leaves the global commit lock intact. Don't plan a migration around it.

## The fix: decouple notification from durability

The load-bearing observation generalizes far beyond streaming:

> For most LISTEN/NOTIFY applications the notification is **not the source of truth**. It's a hint to go read a table, which *is* the source of truth.

If that holds, then the two guarantees Postgres pays for with the global lock — total commit ordering and durability of notifications — are both unnecessary. A dropped or reordered notification costs you latency, not correctness, because the reader re-reads the table and gets the truth either way.

That licenses the workaround:

1. **Buffer notifications in application memory** rather than emitting NOTIFY inside the data-writing transaction.
2. **Flush the buffer periodically** as a single batched transaction. The global lock is now taken once per flush, not once per event.
3. Data writes become ordinary inserts — no lock, full group commit, high throughput.
4. **Add a low-frequency poll as a fallback** in every reader. A process crash with a non-empty buffer silently loses those notifications; the poll bounds the damage to one poll interval. Because it's a backstop rather than the primary path, the interval can be long enough that its load is negligible.

Note that step 4 quietly reinstates polling — the thing LISTEN/NOTIFY was adopted to avoid. The design isn't "notify instead of poll," it's **notify for the common-case latency, poll for the correctness floor**. That combination is strictly better than either alone: polling alone forces the interval-vs-load tradeoff that makes it unusable for interactive latency, while notification alone is not crash-safe once buffered.

Benchmarked result: **~60K writes/sec (20×) at 15–100ms latency**, with Postgres CPU fully utilized — i.e. the bottleneck moved from lock contention to actual work, which is where you want it.

## The pattern this generalizes to

The streams use case DBOS describes — one row per chunk (say, an LLM response token), readers tailing the end of the table — is one instance of a broader shape. The same buffer-and-batch treatment applies to any system where notifications are wake-up hints over a durable table: job queues signalling new work, cache invalidation fanout, change feeds driving websocket pushes.

The precondition to check before adopting it: **can a reader recover full correctness from the table alone?** If your consumers derive state from the notification payload itself rather than re-reading, buffering is unsafe — a lost buffer is lost data, and the fallback poll can't reconstruct it. Keep payloads as pointers ("row 12345 changed"), not as content.

Two further constraints worth knowing, independent of this optimization:

- The notification queue has a fixed size (8GB default, `max_notify_queue_pages` in newer versions). A listener that stops draining can eventually stall writers.
- Notifications only reach *currently connected* listeners. There's no replay for a disconnected consumer — another reason the table, not the notification, must be the source of truth.

## Assessment

This is a vendor blog post from DBOS, whose product is Postgres-backed durable execution, so it has an interest in "Postgres is enough." The mechanism explanation is checkable against the Postgres source and the benchmark code is [published](https://github.com/dbos-inc/dbos-postgres-benchmark), which is more than the genre usually offers. The 60K figure is single-server, on unspecified hardware, for a workload of small appends — treat it as evidence that the lock was the binding constraint rather than as a number to plan capacity against.

The durable takeaway is architectural rather than numeric: a serializing lock is a throughput ceiling you escape by **reducing the number of times you take it**, not by making the work inside it faster. Batching converts a per-event cost into a per-interval cost. The price is a weakened delivery guarantee, which is affordable exactly when the notification is a hint rather than data — and the fallback poll is what makes that weakening safe.

## Sources

- DBOS (2026). "Postgres LISTEN/NOTIFY Actually Scales." <https://www.dbos.dev/blog/postgres-listen-notify-scalability> — [[2026-08-02-postgres-listen-notify-scalability|local copy]]
- Referenced counterpoint: Recall.ai. "Postgres LISTEN/NOTIFY does not scale." <https://www.recall.ai/blog/postgres-listen-notify-does-not-scale>
