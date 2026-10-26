---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-10-24-breunig-state-of-context-engineering.md
compiled_at: 2026-10-26
model: claude-fable-5-1
confidence: medium
---

# Context Engineering

**Context engineering** is the practice of deciding what goes into a language model's context window, and increasingly of writing the code that decides it. Drew Breunig, who cofounded the DSPy-focused startup Cmpnd and is editing O'Reilly's *The Context Engineering Handbook*, gave a "state of the field" talk at AGNTCon in October 2026 titled "Context Fails & Fixes." His frame is historical: each capability the labs ship creates the failure modes harness builders then have to work around. Long context windows (2024) produced four context failure modes and a six-tactic toolbox. Long-horizon agentic models (2026) produced two more failure modes, and the same six tactics turned out to be the fix. His prediction for 2027 is that persistent memory will produce the next one.

Breunig's defence of the discipline against the "it will be obsolete in weeks" worry is that giving consistent, noise-free instructions is hard even between humans, and models fail in their own ways because of how they are trained. The durable skill is understanding those failure modes and knowing which to handle in code and which to leave to the model.

## 2024: the long-context promise and its four failure modes

At the end of 2024 the pitch was "RAG is dead": make the window big enough, put everything in, and let the model sort it out. Gemini 1.5 took windows from roughly 128K to 1M tokens and teased 10M; Llama 4 Scout shipped 10M first, was hard to serve, and Breunig notes "we never got another Llama."

Breunig's June 2025 taxonomy of what goes wrong when you fill that window:

- **Context poisoning.** A hallucination or bad fact enters the context and the model cannot get past it. His example is from the Gemini 2.5 technical report: the agent playing the 1996 *Pokémon Red* repeatedly tried to give a guard tea, because the 2004 *FireRed* remake changed the lemonade bribe to tea and that version was in its weights. Once "get tea" was on its to-do list, it spent hours on it.
- **Context distraction.** The context grows so long that the model attends to it over its base knowledge. The Gemini 2.5 report's appendix says that past about 100K tokens the Pokémon agent began repeating actions from its history instead of synthesizing new plans, an observation Breunig suspects the marketing team never read. A 2026 paper by Carolina Camassa and Derek Shiller, "Do as I Say, Not as I Do," isolates the effect: instruct the model to answer in Russian, then fill the history with example turns answered in French. Every one of 13 models drifts toward the examples. Small models (Gemma 3 12B) fall below 50% instruction-following after a few contradictory turns; Opus 4.6 holds out far longer but also fails. Breunig's practical reading is that a long CSS-tweaking session seeds the context with bad examples that then steer the model.
- **Context confusion.** Superfluous facts about the user or situation change the answer in ways nobody fully understands. He calls it the most pernicious of the four, and it is why he turns memory off in ChatGPT and Claude: work and family projects get mixed.
- **Context clash.** Tools, skills, and other information in the harness conflict with each other.

"Long contexts let you fit more info, and more errors."

## The six tactics

Breunig's toolbox has not changed since mid-2025 even as the failure modes have, and he finds that notable:

1. **Context augmentation**: RAG, skills, anything that pulls in information relevant to the task.
2. **Tool loadout**: selecting which tools and skills to expose. His anecdote is an enterprise team whose agents suddenly degraded because the platform was loading 600 skills for every engineer at startup.
3. **Context quarantine**: subagents and peer agents that start with a blank history in the same environment.
4. **Context pruning**: dropping history that is no longer needed. Claude Code and Codex do this quietly; early compaction stages strip stale tool results.
5. **Context offloading**: storing state in the environment, in Markdown files or a database, to be read back later.
6. **Context summarization**: compaction. His preferred variant judges which turns matter first, with a small decision model, and summarizes only those.

His DSPy demo makes the point that these are small: an agent is a `while` loop around a ReAct module, and loadout, quarantine, pruning, and summarization each add one line, about 16 lines of change in total. Loadout and pruning run a tiny decision model (he uses a "Jev") per tool or per turn. The one caveat he gives on pruning is to mind [[prompt-caching]], since rewriting the history invalidates the cached prefix.

## The vocabulary ladder: probabilistic to deterministic

Breunig reads the renaming of the field as the one constant underneath it. *Prompt engineering* (2023) chose the words and examples for a single call. *Context engineering* (2025) had the system assemble the window dynamically. *Harness engineering* (2026) moved the assembly out of the context and into scaffold, orchestration, and tooling. The job is the same each time: get the right information in front of the model. What moves is how much of that job is done by deterministic code versus probabilistic model calls, and the direction is toward code. He quotes Stewart Brand: "If you want to know where the future is being made, look for where language is being invented and lawyers are congregating."

## 2026: the long-horizon promise and two new failure modes

The labs' current target is long-horizon agency. Breunig cites METR's task-length measure: GPT-5 around 3.4 hours, Gemini 3.1 at 6.4, Opus 4.6 at 12, all with a harness. The new pitch is "teach the model to drive the harness" and manage its own context. Two failure modes have followed.

**Fighting the weights.** Training models to drive harnesses well overfits them to the tools and environments they trained in. Small models botch a Playwright MCP call on the first try and recover, because the training environment had a similar-but-different tool. Breunig's diagnostic is to read a system prompt for repetition and capitals: Claude Code's prompt tells the model to make independent tool calls in parallel seven times in one place, four in another, then two, then three. Models trained in largely serial environments need to be pushed, and "when you crack open a prompt and see repetition and all-caps, there's a good chance you're fighting the weights." The labs fight their own weights too.

**Context inertia.** Models hyper-focus on a hypothesis, subtask, or goal and keep pursuing it after they should stop. Breunig named it on October 14, 2026, and four groups documented it in the same week:

- Anthropic's **Memento** harness, from its self-replication research. Long runs fixate on an incorrect idea instead of backtracking (one Qwen agent spent hours debugging package versions when the bug was an endpoint incompatible with the grader). The fix: every 90 minutes the agent writes a short note and its context is cleared, with the environment and all work preserved.
- Microsoft Research's **Fork-and-Flush** (Jack Cai and Christos Ziakas). Autoresearch runs show a jump, then a long plateau while compute burns. The agents were not idle; they were making ever-smaller changes to the idea they had, rather than searching for alternatives.
- Stanford's **Stateless Language Agents** (Qizheng Zhang).
- UC Berkeley's **Scaling Discovery Requires Forgetting** (Shangyin Tan). Periodically clear the context, keep the artifacts. On the AHC014 task four agents with forgetting reached 1,144,695 against 1,007,073 for four parallel agents and 961,136 for one, with each forget point followed by another climb.

Breunig's observation is that persistence is exactly what the labs train for, because it makes a good coding agent, and it is the same trait that produces inertia. The fixes are old ones: quarantine, offloading, and deleting the accumulated history. His standing advice to anyone whose coding agent "got nerfed" is to ask how big the context is; his own reset point is about 200K tokens.

## 2027: the memory problem

Each solution moves the problem. Longer windows admitted bad information; agentic models run too long and override preferences because they were trained for their own harnesses. Breunig's prediction for the next one is memory. Few people have run a personal agent (Hermes, OpenClaw, Dot, Bot, Muse) for more than six months. His own six-month Hermes agent shows skills that accumulate odd fixes, solve similar tasks two different ways, and build instructions and memories that conflict with one another. "Overly precise memories become conflicted and messy, and nobody has yet figured out how to handle this." The missing discipline, he says, is strategic forgetting.

## The closing principle

Output is the product of weights and context. Three levers improve it: a bigger model (expensive), more reasoning (slow), or a better context (cheap and fast). Every advance in model capability changes what gets delegated to the model and what the system must enforce, so the job of the harness builder is to choose where to be deterministic and where to be probabilistic. His corollary is to read the technical reports: knowing what a model was trained on is the mental model you debug with.

## Reading it against the rest of the wiki

Breunig's taxonomy and Jozefiak's [[agent-failure-modes]] describe the same phenomena from different seats. Jozefiak's "context rot" and "tool-space interference" are Breunig's distraction and clash, and his fix, prune plus search-then-load, is loadout plus augmentation. Jozefiak's "memory poisoning" is the 2027 problem Breunig is predicting, already observed by someone running a personal agent daily. The [[llm-knowledge-bases]] distinction between a corpus wiki and identity-scoped memory is relevant here: the thing that rots is the memory, not the sources.

The vocabulary ladder places [[harness-engineering]] (Lopopolo's zero-hand-written-code experiment at OpenAI) and [[custom-harnesses]] at the deterministic end: mechanical constraints and legibility are context engineering that has been compiled into code. Weng's [[self-improving-harnesses]] survey found that the benefit of harness updates is non-monotonic, which is a formal version of Breunig's Hermes observation that accumulated skills can make an agent worse. [[contextops]] is one proposed answer for the enterprise case, treating instructions as versioned, owner-approved procedures with a life cycle, though it addresses company procedures rather than a personal agent's self-written skills.

Context offloading is Thompson's [[external-memory]] thesis applied as a harness primitive, and Memento's note-then-reset is its purest form: durable state in files, volatile state discarded on a timer. The Berkeley result also bears on [[multi-agent-scaling]]: on that task, forgetting beat parallelism per dollar, which suggests the population leg of agent scaling competes with a cheaper axis, resetting the same agent.

## Implications

- Treat context size as an operational metric, not a budget to fill. Breunig resets around 200K; Gemini's own report saw degradation past 100K. The audience's habit of filling a million tokens is the behaviour his talk argues against.
- Repetition and capitals in a system prompt are a smell, not a technique. They mark a place where the harness is fighting training, and where a mechanical constraint (a linter, a permission gate, a tool that only accepts the right shape) would be cheaper than persuasion.
- Put the clock in the harness. The inertia fixes all involve the harness, not the model, deciding when to reset. A model trained for persistence will not reliably stop itself.
- Keep state in artifacts so forgetting is cheap. Files, databases, and the repository make context resets nearly free, which is the precondition for Memento-style schedules.
- Any persistent memory layer, including the auto-memory of a coding agent, is exposed to the 2027 problem. Dated, sourced, deliberately pruned memories are the current best practice; a real solution for strategic forgetting does not yet exist.

## Caveats

Single opinionated source with an incentive: Breunig is selling a book and a DSPy-centred company, and the "same six tactics" framing conveniently matches his handbook's structure. The Camassa and Shiller setup is, by his own admission, contrived. The METR numbers are as cited in the talk, not checked against the reports. Two of the four context-inertia sources are a lab's own harness write-up and a slide-level reading of papers that are days old. His memory-off stance is a personal preference presented as a warning rather than a measured result.

## Sources
- Breunig, D. (2026). "The State of Context Engineering." <https://www.dbreunig.com/2026/10/24/the-state-of-context-engineering.html> — [[2026-10-24-breunig-state-of-context-engineering|local copy]]
