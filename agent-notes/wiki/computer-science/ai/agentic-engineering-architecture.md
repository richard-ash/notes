---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-04-13-garry-tan-agentic-engineering.md
  - agent-notes/raw/computer-science/ai/2026-04-14-lethain-agents-as-scaffolding.md
compiled_at: 2026-04-14
model: claude-opus-4-6
confidence: medium
---

# Agentic Engineering Architecture

A design heuristic for structuring AI agent systems, distilled by Y Combinator president Garry Tan: partition work into three layers based on the tolerance for ambiguity vs. the need for correctness, then keep the orchestration layer minimal.

## The Three-Layer Model

**Fat skills.** The "fuzzy" operations that humans naturally perform — interpreting intent, synthesizing information, making judgment calls — should live in rich, detailed markdown skill files that the LLM consumes as context. These are fat because they encode domain knowledge, heuristics, edge-case guidance, and stylistic preferences in natural language. The LLM's strength is exactly this kind of flexible, context-sensitive reasoning.

**Fat code.** Operations that must be deterministic and correct — file I/O, API calls, data transformations, validation, permission checks — belong in traditional code. These are fat because real-world agent systems require substantial tooling: parsers, sandboxes, retry logic, state management. Pushing correctness-critical work into code means it can be tested, typed, and audited conventionally.

**Thin harness.** The orchestration layer that connects skills to code should be as minimal as possible. It routes LLM output to the right tools and feeds tool results back. A thin harness is easier to debug, easier to swap models in and out of, and resists the temptation to encode business logic in the glue layer where it becomes invisible to both the LLM and the developer.

## The Scaffolding Pattern

Will Larson describes a complementary development process for arriving at this architecture: use agents as scaffolding to prototype, then progressively replace agent-driven control with code-driven workflow.

**The three-step pattern:**

1. **Prototype with agent-driven workflow** — let the agent handle the entire task end-to-end to discover what's hard about it and where ambiguity lives.
2. **Refactor toward code-driven control** — move deterministic operations (filtering, routing, formatting) into conventional code, eliminating the agent from steps where reliability matters more than flexibility.
3. **Narrow the agent's role** — keep the agent only where it adds genuine value: navigating ambiguous problems like determining code ownership, interpreting unstructured data, or making judgment calls.

**Why this matters:** Larson illustrates the pattern with a Dependabot security-alert pipeline. The fully agentic version could not reliably restrict itself to `critical` severity alerts despite extensive prompt engineering (including "CRITICAL: you must..." statements). The failure mode — occasionally surfacing `high` or `medium` alerts — was low-stakes individually but prevented rollout, because interrupting colleagues requires near-perfection. After refactoring so that code handled severity filtering and the agent only handled ownership lookup and message formatting, the system worked 100% of the time.

This is a concrete validation of the fat-code principle above: the severity filter is a deterministic operation that belongs in code, while identifying the right team to notify from CODEOWNERS files, recent commits, and organizational context is genuinely ambiguous and well-suited to an LLM.

Larson notes the transition is cheap — feed the agent's logs, prompt, and brief instructions to a coding agent, and you get a working code-driven replacement in minutes. The end result is faster, cheaper, and more maintainable.

## Implications

Tan's heuristic is a practical application of [[the-bitter-lesson]] at the agent-systems level: rather than engineering elaborate orchestration logic, lean on the model's general capability (via rich skill context) and on conventional software (via deterministic code), keeping the bridge between them simple.

The pattern also echoes the Unix philosophy of small, composable pieces — but adapted for a world where one of those pieces is a foundation model that thrives on natural-language specification rather than formal APIs.

This framing has direct relevance to tools like [[claude-code|Claude Code]], Cursor, and similar [[ai-coding-harnesses|coding agent harnesses]], where the "skills" are system prompts and markdown instructions, the "code" is the tool implementations, and the "harness" is the agent loop itself.

## Sources

- Garry Tan (2026). "This is the simplest distillation of what I have learned about agentic engineering this year." <https://x.com/garrytan/status/2043566215927328955> — [[2026-04-13-garry-tan-agentic-engineering|local copy]]
- Will Larson (2026). "Agents as scaffolding for recurring tasks." <https://lethain.com/agents-as-scaffolding/> — [[2026-04-14-lethain-agents-as-scaffolding|local copy]]
