---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-07-05-field-guide-to-fable-finding-your-unknowns.md
compiled_at: 2026-07-05
model: claude-fable-5
confidence: medium
---

# Finding Your Unknowns

Thariq Shihipar (@trq212, Anthropic) argues that as agentic models get more capable, the quality bottleneck shifts from the model to the human's ability to surface and resolve their own **unknowns** — the gap between the *map* (prompts, skills, context handed to the agent) and the *territory* (the codebase and real-world constraints where the work actually happens). Claude Fable 5, he says, is the first model where his output quality is bottlenecked by this, not by model capability. Every unknown the agent hits forces it to guess what you want; the more work delegated, the more guesses accumulate.

This is the same human-side-is-the-bottleneck conclusion that [[agentic-engineering]] reaches via "taste" and [[patron-not-wizard]] reaches via the shift from doing to commissioning — Shihipar's contribution is an operational toolkit: named techniques for each phase of a project, most of them cheap HTML artifacts, each one "a cheap way to find out what you didn't know before it gets expensive to fix."

## The four-quadrant breakdown

Shihipar adapts the Rumsfeld matrix to prompting:

- **Known knowns** — what's in your prompt.
- **Known unknowns** — what you know you haven't figured out yet.
- **Unknown knowns** — things so obvious to you that you'd never write them down, but would recognize (or miss) on sight. Visual design is his canonical example.
- **Unknown unknowns** — what you haven't considered at all, including not knowing how good the result *could* be.

He observes that elite agentic coders (he names Boris Cherny and Jarred Sumner) have relatively few unknowns — they are deeply in sync with both the codebase and the model's behaviors — but they also *plan for* the unknowns they still have. Reducing and planning for unknowns is, in his framing, the core skill of agentic coding.

## Why specificity alone doesn't fix it

Instruction-giving fails in both directions: too specific and the agent follows the letter of the plan when a pivot was appropriate; too vague and it fills gaps with industry best practices that may not fit. Unaccounted-for unknowns mean you can't predict which failure mode you're in. The fix isn't more instructions — it's using the agent itself to discover the unknowns (it searches code and the web faster than you, knows more about the average topic, and iterates from failure faster), while you supply context about your starting point: where you are in your thinking, your experience with the problem and codebase.

## The techniques, by phase

**Pre-implementation:**

- **Blind spot pass** — for unknown unknowns in unfamiliar territory. Literally ask for a "blindspot pass" using the words "unknown unknowns," with context on who you are and what you already know ("I know nothing about the auth modules in this codebase — do a blindspot pass to help me prompt you better").
- **Brainstorms and prototypes** — for unknown knowns (know-it-when-I-see-it criteria). Throwaway HTML mockups with fake data, or 4 wildly different design directions to react to, before anything is wired up. Shihipar starts almost every session with a brainstorm phase to calibrate scope.
- **Interviews** — have the agent interview *you*, one question at a time, prioritizing questions whose answers would change the architecture.
- **References** — when you can't articulate what you want, point at source code that already does it, even in another language ("this Rust crate implements the exact backoff behavior I want; reimplement the semantics in our TypeScript client"). Source code beats diagrams, docs, and screenshots as a reference.
- **Implementation plans** — front-loaded with the decisions most likely to change (data models, type interfaces, anything user-facing), mechanical refactoring buried at the bottom.

**During implementation:**

- **Implementation notes** — a temporary `implementation-notes.md` where the agent logs plan deviations as it hits edge cases ("pick the conservative option, log it under 'Deviations', keep going"). Acknowledges that no amount of planning eliminates unknowns discovered mid-flight — a lighter-weight cousin of the repo-as-system-of-record documentation loops in [[harness-engineering]].

**Post-implementation:**

- **Pitches and explainers** — package the prototype, spec, and implementation notes into a single buy-in doc, on the theory that reviewers start with the same unknowns you did and experts approve faster when they see their anticipated failure points addressed.
- **Quizzes** — after a long session, ask for a report on the changes plus a quiz, and only merge after passing it perfectly. A defense against the comprehension gap that [[ai-judgment-atrophy]] worries about: diffs alone undersell what happened because behavior depends on existing code paths.

## Worked example: the Fable launch video

The Fable launch video was edited entirely by Claude Code, in a domain (video editing) where Shihipar was a novice. The arc illustrates the techniques compounding: start from known knowns (Claude can script ffmpeg), use explainers to convert unknown unknowns into known ones (how does Whisper-style transcription work? can it cut "ums" accurately?), prototype to test feasibility (a Remotion UI timed to the transcript), and — the key move — when the variations-to-pick-from approach failed on color grading because he didn't know what "good" looked like, switch to asking Claude to *teach* him color grading first. Recognizing that you don't know what good looks like is itself an unknown-unknown discovery.

## Implications

- The framework inverts the usual planning advice: planning is not a phase you complete but an iterative unknowns-discovery loop running before, during, and after implementation. When a long-horizon task comes back wrong, the diagnosis is usually insufficient unknowns-definition, not model failure.
- It puts operational detail on the "steering ≠ doing" claim in [[patron-not-wizard]]: what the commissioner actually does all day is run blind-spot passes, interviews, and quizzes.
- The techniques are mostly model-agnostic prompting patterns, but the premise — that the human is now the bottleneck — is a claim about frontier-model capability that Shihipar, as an Anthropic employee writing about his employer's model, has an interest in; treat the "first model where..." framing as marketing-adjacent even if the toolkit stands on its own.

## Sources

- Thariq Shihipar (2026). "A Field Guide to Fable: Finding Your Unknowns." <https://x.com/trq212/status/2073100352921215386> — [[2026-07-05-field-guide-to-fable-finding-your-unknowns|local copy]]
