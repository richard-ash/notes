---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-10-inside-claude-code-boris-cherny.md
  - agent-notes/raw/engineering/computer/development/2026-04-20-claude-code-session-management.md
compiled_at: 2026-04-20
model: claude-opus-4-6
confidence: medium
---

# Claude Code

Claude Code is Anthropic's terminal-based coding agent, created by Boris Cherny starting September 2024. In a Y Combinator Lightcone interview, Cherny walks through the product's accidental genesis, the design principles behind it, and the broader bets about frontier-model product-building that those principles encode. The interview is the primary source for this article — most claims should be read as Cherny's perspective, not neutral fact.

## Origin: an accident, not a roadmap

Cherny joined Anthropic's "labs" team — the group that produced Claude Code, MCP, and the desktop app — with no mandate to build a CLI. The bet was just "the path to safe AGI runs through coding." To learn the Anthropic API, he wrote a throwaway terminal chat app in TypeScript. When tool use shipped, he wired up a bash tool (literally copied from the docs example), asked the model "what music am I listening to?", and watched it write AppleScript to query his Mac's music player. That was his "fuel the AGI" moment: *the model just wants to use tools*.

Two days after the first prototype he gave it to his team for dogfooding. The next morning a teammate was already using it to ship code. The CLI was supposed to be a starting point before moving to a "real" UI; it never left. Internally, the adoption curve went vertical with no mandate — Dario Amodei asked Cherny whether he was forcing engineers to use it, and the answer was no, they were telling each other.

Cherny frames the form-factor choice as opportunistic rather than principled: the terminal was the cheapest thing to build (no UI work), and every time he considered moving off it, the model improved so quickly that any UI he'd build would be obsolete in six months anyway.

## Core design principles Boris articulates

### 1. Build for the model six months from now

Cherny's single most-repeated piece of advice. If you find PMF for the product the current model can support, the next model ships in a few months and someone else leapfrogs you. Instead, use the current model, feel out the frontier of what it *can't* quite do, and build assuming it will. He offers this as "still my advice to founders building on LLMs."

### 2. Never bet against the model (the bitter lesson, framed)

A printed copy of Sutton's essay hangs on the wall in the Claude Code area. Cherny treats [[the-bitter-lesson]] as operational guidance: any code in Claude Code that isn't the model itself is "scaffolding." You can invest engineering effort to squeeze 10–20% more capability out of scaffolding in a given domain, or wait a couple months and get it for free from the next model. Assume all scaffolding is tech debt. Cherny claims essentially no code in Claude Code is more than a few months old — tools get unshipped and replaced constantly.

### 3. Latent demand

Cherny calls this "the single biggest idea in product" and says he didn't understand it in his first few startups. People do what they already do; you can't get them to do a new thing, only make an existing thing easier. Every feature in Claude Code is traced to latent demand he observed:

- **CLAUDE.md** — users were hand-writing markdown files and asking Claude to read them; `CLAUDE.md` just formalized the pattern.
- **Plan mode** — users were prompting "come up with an idea, plan it out, but don't write code yet." He wrote it Sunday night at 10pm in 30 minutes after reading GitHub issues and internal Slack; shipped Monday morning. Mechanically it's one sentence added to the prompt: "please don't code."
- **Claude Code in the desktop app / "co-work"** — non-technical users at Anthropic (designers, finance, data science) were jumping through hoops to install a terminal tool. Felix's team built the GUI wrapper in ~10 days, 100% written by Claude Code itself. It's the same agent under the hood.

### 4. Build for the model's desires, not just the user's

Cherny's advice to dev-tool founders: think about what the *model* wants to do and make that easier, the same way you'd do for a human user. Don't box the model in with a narrow API — observe what tools it reaches for and enable those.

## CLAUDE.md advice

Cherny's personal `CLAUDE.md` has two lines (auto-enable merge on PR; post PRs to the team stamps channel). Everything else is in the checked-in project `CLAUDE.md`, which the team edits multiple times per week — often by tagging Claude on a PR and saying "add this to the CLAUDE.md."

His advice when your `CLAUDE.md` grows to thousands of tokens: **delete it and start fresh**. People over-engineer these files. The right move is the minimal possible instruction to get the model on track, and to re-add rules only as the model actually drifts. Each new model version typically needs *less*, not more.

One rule Cherny highlights from his own file: "for every plan decide whether it's over-engineered, under-engineered, or perfectly engineered and why."

## Plan mode and its expected obsolescence

Cherny is a heavy plan-mode user — ~80% of his sessions start there — but predicts plan mode has a "limited lifespan," possibly a month. The pattern has shifted over successive models:

- Six months ago: plans were insufficient, you had to babysit execution after the plan too.
- With Opus 4.5/4.6: once the plan is good, execution stays on track "almost every time," so babysitting is only needed before the plan.
- Next step: you won't need an explicit plan-mode slash command; Claude Code already experimentally enters plan mode on its own when a human would have wanted it to.

He runs many parallel plan-mode sessions across terminal tabs and the desktop app simultaneously, then greenlights execution on each as the plans converge.

## Subagents as the dominant execution pattern

Cherny suspects most agents running today (his own and externally) are prompted by Claude rather than humans — a subagent is just a recursive Claude Code spawned by what the team calls "mama Claude." For hard tasks, he calibrates the number of parallel subagents to difficulty (3, 5, or 10 researching in parallel).

The **plugins feature** was shipped largely autonomously this way: an engineer gave Claude a spec, told it to use an Asana board, and Claude spawned subagents that picked up tickets independently without the full spec context. The swarm ran for a few days with minimal human intervention, and plugins shipped in the form that came out of it.

This connects to what Cherny calls "uncorrelated context windows" — the idea that multiple agents with fresh, unpolluted contexts are a form of test-time compute, and that agent *topology* (how they're laid out and communicate) is a new design surface.

## Productivity claims

Cherny reports that Anthropic's productivity per engineer has grown ~150% since Claude Code shipped (measured primarily by PR count, cross-checked against commits and commit lifetime). He contrasts this with his prior role owning code quality at Meta, where a 2% productivity gain was "a year of work by hundreds of people." For himself personally, he claims to ship ~20 PRs/day, has uninstalled his IDE, and writes no code by hand since Opus 4.5.

These are self-reported, single-source figures from someone with strong incentive to promote the tool — treat as indicative of direction rather than rigorously measured. The PR-count metric in particular is vulnerable to Goodhart effects in an agent-heavy workflow.

## Claude Code as a TypeScript analogue

Cherny (who wrote a TypeScript book a decade ago) draws a parallel between Claude Code and early TypeScript. TypeScript's type system made unusual design choices — literal types as first-class citizens, conditional types — not because of academic theory but because Anders Hejlsberg's team observed how JavaScript programmers actually wrote code (reflection, mutation, unstructured object shapes) and built a type system around those practices rather than asking people to change. Fifteen years later, TypeScript is everywhere and academically purer languages like Haskell are not.

Cherny's analogous claim for Claude Code: it isn't a principled academic product, it's "the tool we wanted" built by observing users (starting with himself). The Unix-utility affordances (pipe in, pipe out) are a rigorous surface, but most of the product is organic and iterated through taste.

## Prototyping the terminal UI with Claude Code itself

Terminal UI is a hard design space — 80 columns, 256 colors, one font size, no mouse, organically evolved escape-code specs from the 1960s. No one writes about modern terminal UX patterns, so the team has had to rediscover them. The terminal spinner alone has gone through ~50–100 iterations, 80% of which didn't ship.

What makes that tractable is that Claude Code itself can generate 20 prototypes back-to-back in a couple of hours. In a previous era, three prototypes in Framer/Origami would have taken two weeks. This is an underrated compounding advantage: the tool accelerates its own design loop.

## Session management and context hygiene

A separate Anthropic blog post by Thariq Shihipar addresses the practical side of working within Claude Code's one-million-token context window. Where Cherny's interview focuses on product philosophy, Shihipar's piece is an operator's manual for context management — the set of decisions a user makes after every turn.

### Context rot

Context rot is the observation that model performance degrades as the context window fills. Attention gets spread across more tokens, and older, irrelevant content distracts from the current task. This is not a bug to be fixed but a fundamental property of attention-based architectures: more context means more noise competing for the model's limited attention budget.

### The five options after every turn

Shihipar frames each completed turn as a branching point with five options:

1. **Continue** — send another message in the same session. Best when everything in context is still load-bearing.
2. **Rewind** (`/rewind` or double-Esc) — jump back to a previous message and re-prompt from there, dropping everything after that point. Often better than correcting forward: if an approach failed, rewind to just after the file reads and re-prompt with what you learned, rather than adding "that didn't work" to an already-polluted context. The `/rewind` command can also generate a "summarize from here" handoff — a message from the future iteration of Claude to its past self.
3. **`/clear`** — start a completely fresh session. The user writes down what matters and starts clean. More work, but the resulting context is exactly what the user decided was relevant.
4. **`/compact`** — the model summarizes the conversation so far and replaces the history with that summary. Lossy but low-effort. Can be steered with instructions (e.g., `/compact focus on the auth refactor, drop the test debugging`).
5. **Subagent** — delegate a chunk of work to a child agent with its own fresh context window. Only the synthesized result comes back to the parent.

### When to use which

The general rule of thumb: **new task = new session**. Related follow-on work (e.g., writing docs for a feature you just implemented) can stay in the same session to avoid re-reading files, but unrelated tasks should start fresh.

Rewind beats correction when you want to keep useful file reads but discard a failed approach. Compact beats `/clear` when you want the model to decide what mattered (low effort, moderate precision). `/clear` beats compact when you want to control exactly what carries forward (high effort, high precision).

Subagents are the right tool when the next chunk of work will produce a lot of intermediate output you only need the conclusion from — codebase search, verification runs, doc writing. The mental test Anthropic uses internally: *"Will I need this tool output again, or just the conclusion?"* This echoes Cherny's point about [[unattended-coding-agents|subagents as the dominant execution pattern]] — most agents running are spawned by Claude rather than humans.

### Why autocompact fails

Bad autocompacts happen when the model can't predict where the user's work is heading next. A long debugging session gets compacted into a debugging-focused summary, then the user asks about an unrelated warning that appeared earlier — and that warning was dropped from the summary. Compounding the problem: the model is at its *least* intelligent point when compacting, because context rot peaks right before the compaction trigger fires.

The mitigation with 1M context: you have more time before autocompact fires, so proactively run `/compact` with a description of your planned next steps while the model still has enough headroom to produce a good summary.

## Implications and cross-connections

- Cherny's "build for the next model" principle and his treatment of scaffolding as disposable echo the core claim in [[the-bitter-lesson]]: general methods that scale with computation consistently beat hand-engineered knowledge. Claude Code treats its own engineering the same way Sutton said AI research should — as scaffolding that the next model capability will subsume.
- The "delete your CLAUDE.md and start fresh" advice is a corollary: `CLAUDE.md` entries are a form of hand-engineered knowledge that a sufficiently capable model won't need.
- The latent-demand principle resembles classical YC product advice ("talk to users, build what they're already trying to do") but updated for a context where users are attempting to do new things *with agents* — and you find those by reading GitHub issues and Slack, not by surveys.
- The shift from "software engineer" toward "builder/PM who also codes" — where every function on the Claude Code team (PMs, designers, EMs, finance) ships code — is presented as a preview of a broader labor-market shift. This is speculative and self-serving but worth flagging as Cherny's explicit prediction.
- The session-management guide crystallizes the practical implications of context rot: the five options after every turn are really five different strategies for managing the attention-noise tradeoff. Rewind and `/clear` are human-directed curation; compact is model-directed curation; subagents are delegation to a fresh context. The pattern matches Cherny's "uncorrelated context windows" concept — subagents aren't just parallelism, they're a way to keep each context window clean.

## Sources

- Y Combinator / Lightcone (2026). "Inside Claude Code With Its Creator Boris Cherny." <https://www.youtube.com/watch?v=PQU9o_5rHC4> — [[2026-04-10-inside-claude-code-boris-cherny|local copy]]
- Shihipar, T. (2026). "Using Claude Code: session management and 1M context." <https://claude.com/blog/using-claude-code-session-management-and-1m-context> — [[2026-04-20-claude-code-session-management|local copy]]
