---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-04-13-garry-tan-agentic-engineering.md
compiled_at: 2026-04-13
model: claude-opus-4-6
confidence: medium
---

# Agentic Engineering Architecture

A design heuristic for structuring AI agent systems, distilled by Y Combinator president Garry Tan: partition work into three layers based on the tolerance for ambiguity vs. the need for correctness, then keep the orchestration layer minimal.

## The Three-Layer Model

**Fat skills.** The "fuzzy" operations that humans naturally perform — interpreting intent, synthesizing information, making judgment calls — should live in rich, detailed markdown skill files that the LLM consumes as context. These are fat because they encode domain knowledge, heuristics, edge-case guidance, and stylistic preferences in natural language. The LLM's strength is exactly this kind of flexible, context-sensitive reasoning.

**Fat code.** Operations that must be deterministic and correct — file I/O, API calls, data transformations, validation, permission checks — belong in traditional code. These are fat because real-world agent systems require substantial tooling: parsers, sandboxes, retry logic, state management. Pushing correctness-critical work into code means it can be tested, typed, and audited conventionally.

**Thin harness.** The orchestration layer that connects skills to code should be as minimal as possible. It routes LLM output to the right tools and feeds tool results back. A thin harness is easier to debug, easier to swap models in and out of, and resists the temptation to encode business logic in the glue layer where it becomes invisible to both the LLM and the developer.

## Implications

Tan's heuristic is a practical application of [[the-bitter-lesson]] at the agent-systems level: rather than engineering elaborate orchestration logic, lean on the model's general capability (via rich skill context) and on conventional software (via deterministic code), keeping the bridge between them simple.

The pattern also echoes the Unix philosophy of small, composable pieces — but adapted for a world where one of those pieces is a foundation model that thrives on natural-language specification rather than formal APIs.

This framing has direct relevance to tools like Claude Code, Cursor, and similar coding agents, where the "skills" are system prompts and markdown instructions, the "code" is the tool implementations, and the "harness" is the agent loop itself.

## Sources

- Garry Tan (2026). "This is the simplest distillation of what I have learned about agentic engineering this year." <https://x.com/garrytan/status/2043566215927328955> — [[2026-04-13-garry-tan-agentic-engineering|local copy]]
