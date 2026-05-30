---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-05-25-lawson-better-code-more-slowly.md
compiled_at: 2026-05-30
model: claude-opus-4-7
confidence: medium
---

# AI Code Review

Using LLM agents to review code — finding bugs, validating designs, and improving codebase health — rather than (or in addition to) using them to generate code. The same models that produce "slop cannon" PRs when pointed at writing tasks are, when pointed at reading tasks, capable enough to surface real bugs at near-zero false-positive rates *if* the workflow is structured to suppress hallucinations. The contested question is no longer *can agents find bugs* but *how do you prioritize the firehose of findings without drowning*.

## The slop-cannon inversion

The cultural default that Nolan Lawson is arguing against: AI coding means low-quality code produced as fast as possible — barely-passable output, massive PRs, merged unvetted. His counter-thesis is that LLMs are flexible enough to power the opposite workflow: writing higher-quality code more slowly than you would without them.

The lever is asymmetric: agents are very good at *finding* bugs, and that capability scales orthogonally to their (more contested) ability to *fix* them well. If you weight your AI usage toward review and validation rather than generation, you get a quality-focused practice that looks nothing like vibe coding. Lawson reports this is closer to how he was already trying to program before LLMs — careful, methodical, quality-obsessed — but supercharged.

This is a sibling stance to [[agentic-engineering]]: where Karpathy and Willison frame the discipline as "preserve the professional quality ceiling at higher velocity," Lawson frames it as "spend the velocity on quality and tolerate slower wall-clock output." Both are reactions to the slop-cannon default; they differ in whether the new affordance is used to ship more or to ship better.

## The ensemble bug-finding skill

Lawson's concrete technique, adapted from a [Milvus blog post](https://milvus.io/blog/ai-code-review-gets-better-when-models-debate-claude-vs-gemini-vs-codex-vs-qwen-vs-minimax.md) on multi-model code-review debate:

> Run a Claude sub-agent, Codex, and Cursor Bugbot to find bugs in this PR ranked by critical/high/medium/low. Once they're all done, review their findings, do your own research to rule out false positives, and write a final report.

Two design choices doing most of the work:

1. **Cross-model ensemble.** Different models hallucinate differently. A bug that only one model flags is more likely a false positive; one that multiple independent models converge on is more likely real. Running Claude, Codex, and Cursor Bugbot in parallel is the cheap version of the Milvus "models debate" insight — pluralism suppresses individual-model error modes without needing the models to actually argue with each other.
2. **Severity ranking baked into the prompt.** Asking for critical/high/medium/low up front means the output is already triaged. You don't get a flat list of 200 issues; you get a stratified list where the top tier is small and the bottom tier is decorative.

Lawson's reported result: "always finds tons of bugs… and the false positive rate is near zero." The bugs span the full severity spectrum, from security/correctness criticals down to "this comment is misleading" lows. The volume is the problem: you'll be "bored senseless" if you try to address them all.

Customization vector: the skill accepts a personal definition of "bug." Lawson's includes [KISS](https://en.wikipedia.org/wiki/KISS_principle), [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), accessible HTML/JSX, and proper SQL indexes — i.e., his own code-review style turned into a checklist the ensemble enforces. The skill is a vehicle for codifying a senior reviewer's taste so it gets applied at scale to every PR.

## The triage workflow

Once the findings exist, the human's job is allocation, not detection. Lawson's three rules:

- **Burn down criticals and highs in a loop.** Direct an agent to fix all critical/high findings with your guidance on the *right* solution, then re-run the ensemble. Repeat until the top tiers are clear. The human stays in the design seat; the agent is the implementer.
- **Skip findings where the juice isn't worth the squeeze.** A high or medium that requires 100 lines of code to patch a narrow edge case may not be worth the change. Severity is a guide, not a mandate.
- **Abandon the PR if the criticals are structural.** A flood of critical findings is signal that the whole approach is misguided, not that you have a lot of patching to do. The skill becomes a kill switch on bad designs before merge.

This is a markedly different relationship to AI output than the slop-cannon mode. The agent's output is treated as a *prosecutor's case file*, not a deliverable: you read it, weigh it, and decide what to do with each finding. The human supplies the judgment that the model lacks.

## The pre-existing-bug side quest

The most surprising side effect Lawson reports: running ensemble review on a new PR routinely surfaces bugs that *predate* the PR — flaws in code the PR merely touches. The review process becomes a discovery mechanism for latent issues, not just an audit of new changes.

The consequence is that the workflow doesn't reliably speed you up; if anything, it slows you down by adding tangential side quests of writing unit tests and fixing subtle pre-existing flaws. Lawson reports finding this satisfying — it improves codebase health while teaching him the codebase's failure modes. His pre-LLM mental model: the happy path of a complex architecture is less interesting than its failure modes, and getting your hands dirty fixing edge-case bugs was always how he got familiar with a system.

This connects to [[ai-judgment-atrophy]] from the opposite direction. Heron warns that AI removes the friction that builds judgment; Lawson's workflow deliberately reinvests AI's velocity gains into *additional* friction — the kind that builds understanding of the codebase's weak points. The slow-and-careful style isn't anti-AI; it's anti-shortcut.

## Companion practices: forcing comprehension

The bug-finding skill is one half of Lawson's recommendation. The other half is using agents to make sure you actually understand the code you're shipping:

- **Ask the agent how the PR works and how it might fail.** Treat the agent as a Socratic partner that walks you through the code's behavior and edge cases.
- **Have it write Markdown docs with [Mermaid charts](https://mermaid.ai/open-source).** Forcing the agent to diagram the change exposes structure that a flat code review would miss.
- **Use [Matt Pocock's `/grill-me`](https://www.aihero.dev/my-grill-me-skill-has-gone-viral) skill** to be interrogated about the PR until you can answer questions front-to-back. The agent stress-tests your mental model rather than building it for you.

The unifying principle: the agent is positioned to *deepen* the human's understanding, not to substitute for it. This is the practical instantiation of Karpathy's "you can outsource your thinking but not your understanding" line in [[agentic-engineering]].

## Why ensemble review works: the harness perspective

The ensemble approach exploits an architectural property of [[ai-coding-harnesses|coding harnesses]]: each harness (Claude Code, Codex, Cursor Bugbot) wraps its model with different system prompts, tool definitions, and search backends. Even when two harnesses run the same underlying model, the harness scaffolding biases what gets surfaced. Running three different harnesses against the same PR is, in effect, three different reviewers — not just three samples from one distribution.

This also implies the technique is robust to model improvement: as individual models get better at single-pass review, the ensemble's marginal value shrinks but doesn't disappear, because the harness-induced divergence remains. The bet is structural, not contingent on any particular model generation.

## Cost and constraints

Lawson notes the technique can burn "a ton of tokens just to find out that your entire plan was wrongheaded from the start." That's a feature in his framing — early detection of a bad design is cheaper than building on it — but it's a real cost. Three-model ensemble review on every PR is not free; the workflow makes sense for codebases where the cost of a bad merge dominates the cost of compute.

Two boundary conditions worth naming, even though Lawson doesn't:

- **Verifiable domains amplify the value.** Per [[agentic-engineering]]'s verifiability framing, bug-finding is exactly the kind of task where RL-trained models excel: there's a checker (does the bug reproduce?) and the reward is clean. Code review sits inside the RL distribution.
- **Aesthetic and design-level critique is weaker.** The same framing predicts the ensemble will miss "this abstraction is wrong" or "this name is bad" findings — the taste axis Karpathy flags as the human-defended bottleneck. Use the ensemble for correctness, not for design.

## Implications

- **AI code review is the most defensible AI coding use case.** Even practitioners skeptical of AI-generated code can adopt ensemble review with low risk: the model doesn't ship anything; it just flags. The downside is wasted reviewer time on false positives, which the ensemble suppresses to near-zero.
- **PR review may be where the slop-cannon paradox resolves.** The same tool that lets the slop cannon ship faster also lets the careful reviewer catch the slop. The asymmetry favors defense: the reviewer can pre-filter what the cannon produces.
- **Severity ranking is the load-bearing prompt design.** Without triage, agent output is a firehose. Ranking turns it into a workflow. Future skills that produce structured AI output for human consumption will reach for the same pattern.
- **The "slow down" framing is a hireable taste signal.** A developer who reports using AI to slow down and improve quality is implicitly claiming the senior-reviewer taste needed to know what "better" means. The framing is a credential as much as a technique.
- **The side-quest property is a codebase-health subsidy.** Teams adopting ensemble review on new PRs will accumulate a steady stream of pre-existing-bug fixes as a byproduct. Over time, this is a meaningful investment in codebase health that no one explicitly budgeted for.

## Connections

- [[agentic-engineering]] — Lawson's slow-coding stance is a quality-spending variant of the agentic-engineering discipline; both are reactions to the slop-cannon default, but allocate the velocity gain differently
- [[ai-coding-harnesses]] — the ensemble technique exploits harness-induced divergence between Claude Code, Codex, and Cursor Bugbot even when underlying models overlap
- [[ai-judgment-atrophy]] — Heron's warning about AI eroding the friction that builds judgment; Lawson's workflow is a counter-pattern that reinvests AI velocity into additional friction
- [[generative-ai-as-pattern-generation]] — Evans's error-tolerance framing predicts code review (high tolerance for false alarms when triaged by humans) is a structurally good fit for current AI

## Sources

- Lawson, N. (2026-05-25). "Using AI to write better code more slowly." <https://nolanlawson.com/2026/05/25/using-ai-to-write-better-code-more-slowly/> — [[2026-05-25-lawson-better-code-more-slowly|local copy]]
