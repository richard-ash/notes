---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-06-22-the-wrong-abstraction.md
compiled_at: 2026-06-22
model: claude-opus-4-8[1m]
confidence: medium
---

# The Wrong Abstraction

Sandi Metz's thesis, from her RailsConf 2014 talk and the 2016 essay that distilled it: **"duplication is far cheaper than the wrong abstraction,"** and therefore **"prefer duplication over the wrong abstraction."** The claim is deliberately provocative against [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) orthodoxy — it does not say duplication is good, only that a *premature or mismatched* abstraction costs more than the duplication it replaced.

## The decay pattern

Metz observes a recurring lifecycle by which a once-clean abstraction rots:

1. Programmer A sees duplication, extracts it, and names it (a method or class).
2. The code looks perfect; A moves on.
3. Time passes. A new requirement arrives for which the abstraction is *almost* right.
4. Programmer B feels honor-bound to keep the existing abstraction, so adds a **parameter** and a **conditional** to handle the new case.
5. More requirements, more parameters, more conditionals — until the code is an incomprehensible "condition-laden procedure which interleaves a number of vaguely associated ideas."

The key signal: **passing parameters and adding conditional paths through shared code means the abstraction is wrong.** It may have been correct when created; that day has passed.

## Why people don't fix it: the sunk cost fallacy

Existing code "exerts a powerful influence — its very presence argues that it is both correct and necessary." The more complex and hard-won the code, the more we feel obligated to preserve it, precisely because the effort invested makes it *feel* important. Metz names this the [sunk cost fallacy](https://en.wikipedia.org/wiki/Sunk_costs): the investment is already spent and should not factor into the forward decision. The trap is that each attempt to "preserve the investment" by bending the abstraction further makes the next change harder, so the code gets worse the harder people try.

## The remedy: the fastest way forward is back

When stuck with a wrong abstraction, *retreat is the advance*:

1. **Re-inline** the abstracted code back into every caller (re-introducing the duplication).
2. In each caller, use the parameters it was passing to select the subset of inlined code it actually runs.
3. **Delete** everything that caller doesn't need.

This strips out both the abstraction and its conditionals, leaving each caller with only the code it uses. A common discovery: each caller's "shared" path was actually fairly unique. Once the old abstraction is fully gone, you can re-observe the genuine duplication and re-extract a *better* abstraction from current requirements rather than the original ones.

## Synthesis and connections

- **Relation to DRY and the Rule of Three.** Metz is not anti-DRY; she's arguing about *timing and fit*. The essay is the canonical complement to the "Rule of Three" (wait for three uses before abstracting): both counsel patience, because early abstraction commits you to a shape before you know the variation it must absorb. Knowledge about the right abstraction accrues only after the variation appears.
- **Abstractions are bets on the future.** An abstraction encodes an assumption about which parts of the code will stay common. Conditionals creeping in are evidence the bet was wrong — the "common" part wasn't actually common. Duplication keeps the bet small and reversible.
- **Reversibility over preservation.** The deeper move is to treat code as disposable evidence, not sunk investment: "This code made sense for a while, but perhaps we've learned all we can from it." This reframing — code as a learning artifact you're allowed to discard — is what makes the inline-and-rebuild remedy psychologically possible. It rhymes with the disposability discipline behind [[choose-boring-technology]] (minimize what you can't easily replace) and with the cruft-accumulation argument in [[internal-software-quality]] (wrong abstractions are a major source of the internal-quality decay that slows teams within weeks).
- **Heightened relevance with coding agents.** When LLM coding agents generate and modify code at speed, the wrong abstraction compounds faster — an agent will dutifully thread "another parameter, another conditional" through shared code rather than question the abstraction. The human judgment of *when to inline and rebuild* is exactly the kind of maintainability call that [[judgment-in-ai-assisted-development]] identifies as the new binding constraint.

## Temporal notes

The essay is from 2016; its argument is design-philosophy and has aged well — it's now one of the most-cited counterweights to over-eager DRY. The closing "News" section advertises the 2nd edition of *99 Bottles of OOP* (then newly available in Ruby, JavaScript, and PHP), which remains the book-length treatment of the same ideas.

## Sources
- Metz, Sandi (2016-01-20). "The Wrong Abstraction." <https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction> — [[2026-06-22-the-wrong-abstraction|local copy]]
