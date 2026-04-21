---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2017-01-05-how-ics-get-stuck.md
compiled_at: 2026-04-20
model: claude-opus-4-6
confidence: medium
---

# IC Anti-Patterns

A taxonomy of how individual contributors get stuck, from Camille Fournier. The piece distinguishes two failure modes — getting *sidetracked* (doing the wrong work) and getting *stuck* (unable to start or finish the right work) — and argues that recognizing these patterns in yourself and colleagues is a leadership superpower.

Will Larson later wrote a companion piece applying the same diagnostic framework to the management track — see [[manager-anti-patterns]].

## Sidetrack patterns (doing the wrong work)

Fournier identifies eight ways ICs get pulled away from their primary task:

1. **Analysis paralysis on architecture** — needing to think through every edge case before writing a line of code. The urge to have a complete mental model before starting becomes a substitute for starting.
2. **Infinite research** — evaluating solutions forever, often manifesting as "bakeoffs" where prototypes get built in multiple languages or frameworks. The research feels productive but never converges on a decision.
3. **Compulsive refactoring** — "this code could be cleaner" cascades into an unbounded cleanup. Each improvement reveals the next imperfection.
4. **Helping others instead of shipping** — substituting the dopamine of being useful to teammates for the harder work of delivering your own commitments.
5. **Jumping on fires when not on-call** — volunteering for urgent work that isn't yours. The adrenaline of firefighting displaces the grind of sustained project work.
6. **Side projects over the main project** — often a signal that the main project is in a stuck phase (see below) and the IC is unconsciously avoiding it.
7. **Excessive testing** (rare) — gold-plating test coverage well past diminishing returns.
8. **Excessive automation** (rare) — automating processes that don't yet warrant it.

## Stuck patterns (unable to do the right work)

Twelve situations where ICs consistently stall:

1. **The last 10–20%** — the most common stuck pattern. The exciting design and build work is done; what remains is polish, edge cases, documentation, and deployment. Many ICs lose momentum exactly here.
2. **Starting from scratch** — a blank editor is paralyzing. No existing patterns to extend, no momentum to ride.
3. **Project planning** — being asked to produce a roadmap or design doc feels like a different job entirely.
4. **Unfamiliar code/libraries/systems** — the activation energy of learning something new is high enough to trigger avoidance.
5. **Cross-team collaboration** — working with other teams requires social navigation that many ICs find draining.
6. **Talking to non-engineers** — especially stakeholder conversations outside engineering. The further from code, the more uncomfortable.
7. **Asking for help** — ICs often recognize they're stuck long before they ask for help. The delay between "I'm stuck" and "Can you help?" can be days or weeks.
8. **Unexpected setbacks** — a surprise failure can break momentum entirely, even when the setback is small relative to the overall project.
9. **Navigating bureaucracy** — processes, approvals, and organizational overhead.
10. **Going to production** — fear of shipping, sometimes disguised as wanting "one more round of testing."
11. **Dealing with vendors/external partners** — external dependencies introduce uncertainty and require different communication skills.
12. **Saying no** — instead of declining, stuck ICs go into avoidance mode or say yes to everything and then can't deliver.

## The sloppy counterpart

Fournier notes an important complement to the stuck/sidetracked pattern: some people get *sloppy* instead. They never get sidetracked — they stay on the main project — but they also never finish anything completely. The last project's rough edges get abandoned as they rush into the next one. This is the mirror failure mode: where stuck ICs over-invest in the wrong things, sloppy ICs under-invest in finishing.

## Why this matters for leads and managers

Fournier frames pattern recognition as a leadership tool: when you know how people get stuck, you can assign work that plays to strengths and provide support at known weak points. You know who to ask for which kinds of help, and who shares your particular blind spots. This connects directly to [[how-to-operate|Rabois's "barrels and ammunition" concept]] — identifying what each person is capable of driving end-to-end versus where they need a barrel to run through.

The piece's most important claim: **everyone has stuck patterns, and there's nothing pathological about it.** The value is in self-awareness and adaptation — overcoming the fear, avoiding the trigger, or applying extra diligence when you hit your known failure mode.

## Sources

- Camille Fournier (2017). "How do Individual Contributors Get Stuck?" <https://skamille.medium.com/how-do-individual-contributors-get-stuck-63102ba43516> — [[2017-01-05-how-ics-get-stuck|local copy]]
