---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-03-17-devcontainer-for-elixir.md
compiled_at: 2026-05-06
model: claude-opus-4-7
confidence: medium
---

# Agent Sandboxing with Devcontainers

Once a coding agent is good enough that you stop wanting to click "yes" on every permission prompt, the bottleneck shifts from agent capability to agent containment. The pragmatic answer in 2026 is to run the agent inside a devcontainer — a local Docker container with restricted network egress, hidden secrets, and explicit task tooling — and grant it `--dangerously-skip-permissions` (Claude Code's "YOLO" / "Danger" mode) inside that boundary. Peter Ullrich's [Elixir-specific devcontainer](https://github.com/PJUllrich/devcontainer) is one fully worked example of the pattern, built on top of [Anthropic's reference devcontainer](https://github.com/anthropics/claude-code/tree/main/.devcontainer).

This is the operational complement to [[judgment-in-ai-assisted-development]]: agents now solve time and attention, but the human's binding constraint shifts toward judgment about *what the agent is allowed to touch*. The sandbox is where that judgment gets crystallized into config.

## The threat model

Ullrich names the two failure modes that motivate sandboxing:

1. **Exfiltration.** "An OpenClaw moment" where the agent uploads SSH keys to GitHub, posts secrets to Pastebin, or follows a malicious link and downloads malware. (OpenClaw refers to a viral incident where an agent leaked credentials.)
2. **Local destruction.** The agent removing the root directory, mangling unrelated repos on the host, or otherwise damaging the host system.

Permission prompts are the safety net. The cost of disabling them on a bare host is unbounded; the cost of disabling them inside a properly-scoped container is the (much smaller) blast radius of that container.

## What a devcontainer is, minimally

A devcontainer is just a Docker container that you spin up locally and run your agent in. The original devcontainer spec ([containers.dev](https://containers.dev/)) was designed for cloud-hosted dev environments; agentic coding gave it a second use case as a *local isolation boundary*. Anthropic ships a reference implementation in the Claude Code repo, which Ullrich used as his starting point.

Spinning the container is trivial. The work is in restricting it correctly.

## Three layers of restriction

Ullrich's setup hardens the Anthropic baseline along three axes.

### 1. Domain-based egress firewall (Squid)

Anthropic's reference devcontainer allow-lists outgoing traffic by **IP**, resolved at container build time. This breaks for any domain behind a load balancer or DNS round-robin (e.g. `claude.ai` itself) — Docker resolves to one IP at build, the agent's HTTP request hits a different IP at runtime, request blocked.

Ullrich replaces this with **domain-based** allow-listing via [Squid](https://www.squid-cache.org/). The allow-list lives in a single `.txt` file; Squid handles both SSL and non-SSL traffic and enforces the list at request time, not build time. Ullrich notes he tried [TinyProxy](https://tinyproxy.github.io/) and [3Proxy](https://github.com/3proxy/3proxy) first; neither handled the SSL + domain-filtering combination well. Squid was "overpowered" but was the only thing that worked without elaborate configuration.

The implication: if you're rolling your own agent sandbox in 2026, **don't allow-list IPs — allow-list domains via a forward proxy.** Build-time DNS is a known footgun.

### 2. Protected-path masking

Even when you put `MUST never read .env` in the agent's instructions, the agent will still read it sometimes — instruction-following is probabilistic, not enforced. Ullrich's approach has three layers:

- **Mount empty files/folders over the protected paths** inside the container. The agent sees the file exists (so it doesn't get confused about repo structure) but reads zero bytes.
- **Add the protected paths as deny rules** in Claude Code's project-wide `settings.json`. This doesn't prevent reads, just makes them less likely.
- **Inject required env vars at container start.** The agent can still `echo $MY_SECRET` and pull the value, so even with all this protection, *never use production secrets in `.env`*. The sandbox is a defense-in-depth layer, not a replacement for keeping prod creds out of your dev environment.

The key insight: it's easier to mask files than to convince an agent to ignore them. The container is where you enforce the policy, because the agent is where you can't.

### 3. Makefile shortcuts

A small but operational point: a [Makefile](https://github.com/PJUllrich/devcontainer/blob/main/.devcontainer/Makefile) with shortcuts for `start`, `stop`, `rebuild`, `logs`, `phoenix server`, `tidewave` makes the boundary easy to live behind. Friction kills security; if the safe path isn't the easy path, the safe path doesn't get used.

This rhymes with [[low-tech-devex]]: text-based, scriptable, composable tooling around the boundary, not a GUI.

## Elixir-specific changes

Ullrich's deltas from Anthropic's Node-flavored reference devcontainer:

- **Base image:** swap `node` for the official Hex.pm Elixir/Erlang image.
- **Non-root user:** run the container as a non-root user by default (Anthropic's reference does run as root in some configurations; Ullrich treats this as a baseline hardening).
- **Tidewave preinstalled:** [Tidewave](https://tidewave.ai/) is an Elixir-native MCP runtime that exposes the running Phoenix app's state to the agent (queries, logs, function calls). Ullrich treats it as table stakes for an Elixir-agent workflow.

These are mechanical changes — most of the value is in the firewall and protected-paths design, which generalizes to any language.

## Where this fits in the agent-tooling stack

- [[claude-code]] is the agent being sandboxed; the sandbox is what makes its `--dangerously-skip-permissions` mode usable in practice.
- [[unattended-coding-agents]] takes this further: Stripe's Minions run agents fully autonomously to produce 1,300+ merged PRs/week, which is only possible if the sandbox boundary is well-defined enough that no human is in the permission loop.
- [[claude-code-skills]] live *inside* the sandbox; sandboxing constrains what the skill can do, the skill constrains what the agent does.

The progression — permission prompts → devcontainer → unattended fleet — tracks the same gradient: as the agent gets more capable, the human moves from approving each action, to approving the boundary, to approving the policy that generates boundaries.

## Implications and gaps

**For Elixir/Phoenix specifically:** Ullrich's repo is a drop-in starting point. The non-trivial bits (Squid config, protected-path mounts, Tidewave wiring) are already done. Forking and tweaking the domain allow-list is probably the right path for anyone who wants this today.

**Generalizable lesson:** the hard part of sandboxing isn't the container — it's the egress policy. Domain-based proxies beat IP allow-lists. File masking beats prompt-level "don't read this." Defense-in-depth beats any single layer.

**What this doesn't solve:** the agent can still exfiltrate secrets that are in the `env` it's given (production credentials should never be there in the first place); it can still mangle the project source it's *supposed* to edit (use git, commit often); and the host filesystem outside the container is only protected by Docker's isolation, not by anything stronger. Ullrich's setup is a pragmatic local sandbox, not a hostile-multi-tenant boundary.

## Sources
- Ullrich, Peter (2026-03-17). "A Devcontainer for Elixir." <https://peterullrich.com/a-devcontainer-for-elixir> — [[2026-03-17-devcontainer-for-elixir|local copy]]
