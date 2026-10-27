---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-06-22-mukta-learning-while-you-sleep.md
compiled_at: 2026-10-27
model: claude-fable-5-1
confidence: medium
---

# Agent Memory: In-Band Writes and Out-of-Band Dreaming

**Agent memory** is the durable store an LLM agent reads from and writes to across sessions, so that a frozen-weight model gets better at a recurring task without retraining. Lamis Mukta, a member of technical staff on Anthropic's applied AI team who works with startups, gave a talk at AI Native DevCon in June 2026 titled "Learning while you sleep: beyond memory to dreaming." It is the first vendor account in this wiki of how a memory system is actually run at fleet scale, and of a named consolidation process, **dreaming**, that runs over the memory store between sessions.

Her argument has four moves. Context is the lever that multiplies model intelligence, because what an organization needs an agent to know is mostly orthogonal to what a new model ships knowing. A year of iteration (CLAUDE.md, memory tools, skills, the file system as memory) converged on markdown files that agents search and write autonomously. Running that at production scale needs four engineering properties: versioning, concurrency control, permissions, and portability. And in-band memory, written by the agent during its own session, hits a ceiling that only a separate, out-of-band process can lift. The Q&A reveals that the design she describes is the memory and dreaming API inside Claude Managed Agents, so the talk is also a product description. Treat its performance claims accordingly.

## Why context compounds and intelligence alone does not

Mukta's opening claim is that releasing a smarter model does not by itself make an organization's agents better, because the knowledge that makes an agent useful in a specific environment (the shape of the codebase, the user's preferences, what went wrong last time) is not in the weights of any model. Context engineering is therefore a durable investment: it "multiplies the intelligence even as models get smarter." The three symptoms she names are familiar: agents that do not know their way around a codebase, agents that do not know the user's preferences, and agents that are no better the second time they do a task. The third is the one the rest of the talk is about. Without it there is no continual learning, which is the capability Karpathy and Thompson both put at the top of the missing list ([[agi-timelines]], [[external-memory]]).

## A one-year ladder: four stops

Anthropic's motto, she says, is "do the simple thing that works," and the timeline she gives spans only the previous year.

| Stop | What it is | What it taught | Where it broke |
|---|---|---|---|
| **CLAUDE.md** | A markdown file of instructions injected at the start of every session | "Unreasonably effective." Human-readable, writable by both the person and the agent | Grows long; everything is paid for at session start whether or not it is relevant |
| **Memory tools** | The agent decides in-band when to read, write, and update memories | Autonomy over memory works. The lesson over time was to become *less* opinionated about the tool's shape | Still confined to one session's view |
| **Skills** | Procedural workflows behind a short frontmatter; the body loads only when the frontmatter matches | Progressive disclosure: deep detail without a loaded context. Her image is a bookshelf you scan by title, pulling the French dictionary only when someone speaks French | Humans still decide which things deserve a skill |
| **File system as memory** | Markdown in directories; agents use bash and grep over it | Agents are good at ordinary file tools, so stop designing bespoke memory tools. Indexing gives progressive disclosure for free | Scaling to many agents, long runs, and complex codebases |

The distilled principles: markdown for reading, let the store grow large but give the agent an index and search, and give it autonomy on writes. A system built on these, she says, produces "the feeling of continual learning."

Two things are worth noting against the rest of this wiki. First, the ladder is the same one Breunig calls the vocabulary ladder in [[context-engineering]]: each step moves a decision from a hand-written prompt into something the harness does mechanically. Second, the CLAUDE.md failure mode is exactly the one Cherny answers with "delete it and start fresh" in [[claude-code]]. Mukta's answer is structural rather than disciplinary: move the long tail out of the start-of-session file and into searchable memory.

## What breaks in production

The theoretically neat design fails, she says, "time and time again" once many agents collaborate, run for a long time, and work in complex codebases. Her list:

- Several agents writing the same memory file at once.
- One agent hitting a problem and writing its fix into organization-wide context that every other agent reads, so one wrong entry propagates to the whole fleet.
- Humans and agents editing the same store with no record of who changed what.
- Memories going stale, being written incorrectly, or being planted by a prompt injection aimed at the memory layer.

The last item is Jozefiak's "memory poisoning" from [[agent-failure-modes]] and the hazard Breunig flags as the 2027 problem in [[context-engineering]], named by the vendor as something already seen in production.

## Four production principles

1. **Versioning.** Store every version so a bad update can be rolled back. Record the provenance of each update: which session and transcript motivated it, and which agent or human made it.
2. **Concurrency.** Optimistic concurrency control on a content hash. The agent hashes the memory, drafts its edit, hashes again before committing, and if the hashes differ it re-reads, re-drafts, and retries. (The auto-caption has the agent "ripple" the memory; the sense is re-read.) This is compare-and-swap, applied to markdown files.
3. **Permissions.** Memory is a hierarchy: carefully curated organization-wide knowledge at the top, an individual agent's working scratchpad at the bottom, team or project layers in between. Agents get write access to their own scratchpad and, by default, read-only access to the shared top. The blast-radius argument above is the reason.
4. **Portability.** The curated store is an asset that outlives any one product surface, so expose it through a clean API that other systems can reach.

Her reported results, with no figures attached: higher accuracy on the second run of a task, lower token spend and latency because agents one-shot tasks they have notes on, and freed developer attention because the agents maintain their own context.

When an audience member asked whether this is "reinventing databases from first principles," she agreed in part. The job is to find the boundary between what the agent does autonomously and what the harness does programmatically. Teams started by letting agents "commit whatever they wanted" to markdown; having seen which primitives work, they are codifying those deterministically, "and there's no need to reinvent the wheel." That is the same probabilistic-to-deterministic migration Breunig describes and the fat-code rule in [[agentic-engineering-architecture]], reached from the vendor side.

## The ceiling of in-band memory

In-band memory is memory the agent reads and writes inside the session that is doing the work. Mukta gives three reasons it cannot carry a fleet's learning on its own:

- **Split budget.** The agent is asked to finish the task and, at the same time, to invest in notes that help a future version of itself. How much of its capacity to spend on each is "a very difficult optimization problem," and curation adds latency to the task the user is waiting on.
- **No visibility.** A session sees only itself. It cannot notice that it is making the same mistake it made last week, and one agent in a fleet cannot see the failures other agents are hitting in other environments. "When you get frustrated that your agent keeps making the same mistake over sessions, it just doesn't understand how frustrating that is."
- **Staleness.** Nothing in the in-band loop re-checks that what was written is still true.

Her analogy is a school. Students submit work; teachers mark it; a head teacher reviews across the whole school. Two things make that arrangement work and are missing from in-band memory: dedicated capacity for helping others learn, and visibility across every learner so patterns can be seen and the curriculum changed.

## Dreaming

Dreaming is a second-order process over memory. It runs in batch, asynchronously, with its own token budget. Inputs are the existing memory store and a set of session transcripts over some period, where "transcript" explicitly includes tool calls and other metadata, not only the messages between agent and user, because tool failures are where many of the patterns show. An agent reviews the transcripts against the store, finds places where the memories could be better, and outputs proposed changes to the store, so that "next day when you run these agents again, they actually feel smarter."

The production design:

- An **orchestrator** fans out a fleet of subagents, each analysing a share of the transcripts. (The caption says "subjects"; the sense is subagents.)
- The orchestrator aggregates their findings and decides which patterns are prevalent enough to warrant a memory change.
- It proposes **individual changes**, each with example transcripts where the pattern occurred and statistics on how prevalent it is.
- A **human accepts or rejects** each proposal.
- Both the in-band memory writers and the dreaming agents are **steerable**: the operator tells them what kinds of things matter for this organization and what does not.

Her three head-teacher examples map onto three kinds of memory change:

| Observation across transcripts | Memory change |
|---|---|
| Every geography student answers one question with garbage, and the topic is absent from the curriculum | Add missing knowledge to the store |
| Every maths student outputs radians where degrees were wanted | Fix a configuration: for agents, a tool whose calls keep failing in the same way |
| Everyone is using too many dashes | Add an organization-wide style instruction |

The two processes then run side by side:

| | In-band memory | Dreaming |
|---|---|---|
| When | During the task session | Batch, between sessions |
| Budget | Competes with the task | Dedicated token spend |
| View | One session | Many sessions, many agents |
| Latency to effect | The very next session | The next dreaming run |
| Review | Agent decides | Human accepts or rejects proposals |

On cost, her answer to "why spend extra tokens on this" is that a better store makes every subsequent run cheaper, because agents one-shot tasks they have notes on.

Two Q&A exchanges add detail. Asked for an enterprise memory implementation, she pointed to the memory and dreaming API in Claude Managed Agents, where versioning and hashing are built in, after noting she was not supposed to make product calls to action. Asked how dreaming respects per-user permissions when it runs out of band, she said the two compose: a dreaming job is configured with exactly the transcripts it may read, so the operator selects transcripts whose permission set matches the memory store being updated rather than everything in a time window. The same questioner referred to a "Claude Code leak" in which memory and dreaming code had appeared; the talk does not address it, and this wiki has no independent source on it.

## Reading it against the rest of the wiki

**Breunig's 2027 problem has a candidate answer.** [[context-engineering]] predicts that persistent memory is the next failure mode: over-precise memories that conflict, skills that accumulate odd fixes, and no discipline of strategic forgetting. Dreaming, described four months earlier, is a scheduled pass whose stated mandate is to "consolidate your memory and cut things that are no longer relevant." But every worked example Mukta gives is additive (add a topic, fix a tool, add a rule). The deletion half is asserted, not demonstrated, and Breunig's reason for turning memory off, context confusion from mixed projects, is a permissions and scoping question that dreaming inherits rather than solves.

**Thompson's weekly review, mechanized.** [[external-memory]] reads GTD as a spec for agent memory: the trusted bucket is the file store and the weekly review is consolidation. Dreaming is that review with a budget and a reviewer. Thompson's own harness also landed on the same split Mukta describes in the Q&A, deterministic bookkeeping (his tickler, her hashes and versions) around probabilistic content.

**Weng's non-monotonic harness updates explain the review gate.** [[self-improving-harnesses]] finds that automatic harness edits do not reliably improve things, which is why its systems keep evaluators and permissions outside the loop. Dreaming is the ACE-style generator/reflector/curator pattern pointed at a memory store instead of a playbook, and its human accept/reject step plus versioned rollback are the same precaution. Weng's AHE diagnosis, that the bottleneck is observability into which component failed, matches Mukta's insistence that dreaming reads tool calls and metadata, not just dialogue.

**The shared store is a message bus.** Thompson's security rule in [[external-memory]], that any surface one agent writes and another reads is a communication channel, applies directly to a fleet's shared memory. Mukta's permissions tier is a correctness measure in the talk, but it is also the containment measure. [[contextops]] proposed versioned, owner-approved procedures for company context; dreaming is the proposer that model lacked.

**For a personal knowledge base.** [[llm-knowledge-bases]] describes compiling a wiki from raw sources, which is what the agent partition of this vault does. That workflow is entirely in-band: each ingest session writes what it learned and nothing re-reads the whole store looking for contradictions, duplicates, or stale claims. Dreaming names the missing pass.

## Implications

- **Specify the store, not just the format.** Markdown files are the easy part. A production memory store needs per-write provenance (session, author), compare-and-swap on a content hash, permission tiers, and an API. These are database properties, and Mukta's own answer is to stop pretending otherwise.
- **Separate the two budgets.** Do not ask the agent doing the work to also curate deeply; its notes will be local and rushed. Schedule consolidation as its own job with its own tokens.
- **Dreaming outputs a pull request, not a merge.** Each proposed change carries evidence transcripts and prevalence numbers and waits for a human. Any consolidation pass without that gate is an auto-merging self-modifier, which [[self-improving-harnesses]] shows to be unreliable.
- **Transcript scope equals permission scope.** Feed a dreaming job only transcripts the target store is allowed to learn from.
- **Measure before believing.** The reported gains are qualitative and come from the vendor selling the API. The test is cheap: second-run accuracy and token spend on a fixed task before and after a consolidation pass.
- **The cheapest dreaming is a cron job.** For a single-user memory directory, a periodic pass that reads recent transcripts against the store, merges duplicates, dates claims, and deletes contradicted entries captures most of the idea with none of the orchestration.

## Caveats

Single source, and a vendor's: the speaker's team ships the product the talk describes, and no numbers accompany the accuracy or cost claims. The school examples are hypothetical. The transcript is auto-captioned, so a few terms are reconstructed here ("ripples" read as re-reads, "subjects" as subagents, "Lamish" as Lamis). The "Claude Code leak" remark is an audience member's and is unverified.

## Sources
- Mukta, L. (2026). "Learning while you sleep: Beyond memory to dreaming." AI Native DevCon, June 2026. <https://www.youtube.com/watch?v=tTcxVv8HHNw> — [[2026-06-22-mukta-learning-while-you-sleep|local copy]]
