---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-04-13-theo-ai-coding-harnesses.md
  - agent-notes/raw/computer-science/ai/2026-04-13-mihail-eric-coding-agent.md
  - agent-notes/raw/computer-science/ai/2026-04-17-how-to-build-an-agent.md
compiled_at: 2026-04-17
model: claude-opus-4-6
confidence: medium
---

# AI Coding Harnesses

A **harness** is the program that wraps an LLM, gives it tools, manages chat history, executes tool calls, and feeds results back into the conversation. Claude Code, Cursor, Codex CLI, and Open Code are all harnesses. T3 Code, by contrast, is a UI layer that delegates to an underlying harness (Claude Code or Codex) already installed on the user's machine.

The term matters because the harness — not just the model — determines output quality. Theo cites Matt Mayer's independent benchmark showing Opus jumping from 77% accuracy in Claude Code to 93% in Cursor, with the only variable being the harness.

## The tool-call loop

Every AI coding tool runs the same fundamental loop:

1. **User sends a message.** The harness appends it to the chat history.
2. **The harness sends the full history (plus system prompt) to the model.** The system prompt includes tool definitions — names, descriptions, parameter schemas.
3. **The model responds with text, tool calls, or both.** A tool call is structured output (special syntax or a dedicated API field) naming a tool and its arguments.
4. **The model stops generating.** The connection is severed; the model is stateless between calls.
5. **The harness executes each tool call** — potentially checking permissions for destructive operations — and collects results.
6. **Tool results are appended to the chat history** and a new request is made to the same model with the updated history.
7. **Repeat** until the model responds with text only (no further tool calls).

The model's "brain" is paused and restarted at every tool-call boundary. It has no persistent state beyond what's in the chat history. This is why Theo describes it as "your memory gets reset every 30 seconds" — the model only knows what the accumulated history tells it.

## Minimum viable harness

Multiple independent implementations converge on the same architecture with roughly the same line count:

- **Mihail Eric** demonstrated a functional coding agent in ~200 lines of Python.
- **Thorsten Ball** (AMP) published a Go walkthrough in under 400 lines (most of it Go boilerplate).
- **Theo** stripped it down further to ~75 lines using only a **bash** tool.

All three arrive at the same three-tool minimum:

- **Read file** — returns file contents given a path
- **List files** — returns directory listings
- **Edit file** — replaces an old string with a new string in a file (or creates the file if the old string is empty)

### Eric's Python implementation

Eric's implementation reveals the concrete moving parts:

1. **Tool registry** — a dictionary mapping tool names to Python functions. Each function returns a structured dict (not a plain string) so the model gets typed context about what happened ("action": "edited" vs "action": "old_str not found").
2. **Auto-generated tool descriptions** — the system prompt is built dynamically using `inspect.signature()` and function docstrings. This means tool descriptions are always in sync with the actual implementation — no separate schema to maintain.
3. **Text-based tool-call protocol** — rather than using the Anthropic API's native tool-use feature, Eric has the model emit `tool: TOOL_NAME({JSON_ARGS})` lines that are parsed with simple string splitting. This works but is fragile; production harnesses use the API's structured tool-call format instead.
4. **Nested loop architecture** — an outer loop handles user input; an inner loop repeatedly calls the model and executes tool calls until the model responds with plain text (no tool invocations). This inner loop is what enables multi-step chains (read a file, then edit it, then confirm).

### Ball's Go implementation

Ball's AMP tutorial uses the Anthropic SDK's native tool-use API rather than text-based parsing. Each tool is defined as a struct with a name, description, JSON schema (auto-generated via reflection), and a function. The SDK handles serialization — the model responds with structured `tool_use` content blocks containing a tool ID, name, and typed input, which the harness dispatches to the matching function. This eliminates the fragile string-parsing step in Eric's approach.

Ball emphasizes that tool use is not really "magic" — it's the same mechanism as telling a friend "wink if you want me to raise my arm." He demonstrates this by getting the model to simulate tool use with plain natural language (prompting it to reply `get_weather(Munich)` and then feeding the "result" back) before introducing the structured API. Under the hood, the provider wraps tool definitions in the system prompt and the model simply responds in the expected format.

His central thesis: "There isn't [a secret]. It's an LLM, a loop, and enough tokens." The impressive-looking behaviors — multi-step file exploration, combining tools autonomously, editing code — emerge from giving the model tools and letting it decide when to use them. No routing logic, no explicit instructions about when to read vs. edit. The model figures it out.

### Common patterns across implementations

The edit tool uses a convention where an empty `old_str` means "create this file with `new_str` as content." Otherwise it does a find-and-replace of the first occurrence. Production harnesses add fallback behavior when the target string isn't found (fuzzy matching, re-prompting), but exact-match replacement is the baseline.

With only a bash tool, Theo shows the agent still works because the model knows how to compose `cat`, `ls`, `sed`, and other shell commands to accomplish read/list/edit operations.

## Why the harness matters more than it seems

### Tool descriptions steer model behavior

Theo demonstrates that changing a tool's *description* — without changing any code — alters which tools the model selects. Marking the read-file tool as "(deprecated, use bash instead)" caused Gemini to avoid it entirely and use bash for everything, while Sonnet ignored the hint and kept using the read tool. Different models respond differently to the same descriptions, which is why Cursor invests heavily in per-model prompt tuning.

### You can lie to the model

The model has no way to verify what a tool actually does. Theo shows that returning a hardcoded "print hello world" from the read-file tool causes the model to confidently describe the file as a single-line hello-world script. The model trusts its tool results completely. This is also how Cursor's search tool works — it tells the model it's "grep" but actually routes through Cursor's own vector-indexed search backend.

### Harness quality is prompt engineering at scale

Theo reports that Cursor employs people whose entire job is to test new models against their tool descriptions and system prompts, iterating on wording until the model reliably uses the right tools. This is why models often perform better inside Cursor than in their native harnesses — not because Cursor has access to a different model, but because they've invested more in tuning the scaffolding around it.

## Context management

The harness also determines how the model learns about the codebase:

- **CLAUDE.md / agent.md files** are injected into the system prompt at bootstrap, giving the model project context before any user message. If the context is sufficient, the model may answer without any tool calls at all.
- **Without pre-loaded context,** the model must use search and read tools iteratively to build its own understanding. Modern models (Opus 4.5/4.6, Sonnet 4.6, GPT-5.x) are good enough at this that pre-loading the entire codebase is unnecessary.
- **Stuffing too much into context hurts.** Theo cites data showing Sonnet's accuracy plummets to ~50% of baseline when context exceeds 50–100K tokens. Targeted tool-based exploration outperforms brute-force context loading. This is why tools like Repomix (which compressed entire codebases into a single XML file) are "largely dead."
- **Session continuity helps** — staying in one conversation thread means prior tool results remain in history, so the model doesn't need to re-explore the same files.

## Harness vs. UI layer

Theo draws a distinction relevant to the current product landscape:

| Product | Role |
|---------|------|
| Claude Code | Harness (provides tools, manages loop) |
| Cursor | Harness |
| Codex CLI | Harness |
| Open Code | Harness |
| T3 Code | UI layer (wraps Claude Code or Codex) |
| Codex app | UI layer (wraps Codex CLI) |

A UI layer can't function without a harness installed underneath it. T3 Code requires Claude Code or Codex CLI to be installed and authenticated on the user's machine.

## Cross-connections

- The three-tool minimum (read, list, edit) maps directly onto Garry Tan's [[agentic-engineering-architecture]] model: these tools are the "fat code" layer, the system prompt is the "fat skills" layer, and the agent loop is the "thin harness."
- [[claude-code]] was born from exactly this pattern — Boris Cherny's prototype was a terminal chat app with a single bash tool wired up, and the model "just wanted to use tools." The harness grew from there.
- The finding that large context degrades model accuracy reinforces [[the-bitter-lesson]] framing: rather than trying to stuff knowledge into context, let the model use compute (tool calls) to find what it needs.

## Sources

- Theo / t3.gg (2026). "How does Claude Code *actually* work?" <https://www.youtube.com/watch?v=I82j7AzMU80> — [[2026-04-13-theo-ai-coding-harnesses|local copy]]
- Mihail Eric. "The Emperor Has No Clothes: How to Code Claude Code in 200 Lines of Code." <https://www.mihaileric.com/The-Emperor-Has-No-Clothes/> — [[2026-04-13-mihail-eric-coding-agent|local copy]]
- Thorsten Ball / AMP (2025). "How to Build an Agent." <https://ampcode.com/notes/how-to-build-an-agent> — [[2026-04-17-how-to-build-an-agent|local copy]]
