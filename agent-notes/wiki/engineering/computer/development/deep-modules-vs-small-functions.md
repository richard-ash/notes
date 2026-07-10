---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2025-02-15-aposd-vs-clean-code.md
compiled_at: 2026-07-09
model: claude-opus-4-8[1m]
confidence: medium
---

# Deep Modules vs Small Functions (Ousterhout vs Martin)

A recorded 2024–2025 debate between **John Ousterhout** (*A Philosophy of Software Design*, "APOSD") and **Robert "Uncle Bob" Martin** (*Clean Code*) over how far to decompose code. Both authors agree on the shared goal — code is read far more than it is written, so design should minimize the cognitive load on the reader — but they draw the line on function size in very different places. The published discussion covers three planned topics (method length, comments, TDD); this article captures the **method-length** section, the core of the disagreement.

## The shared premise

Both men open from the same place, which makes the disagreement sharper:

- **Ousterhout's frame:** the enemy is *complexity*, defined informationally — how much a developer must hold in their head to make a change, and how obvious/accessible that information is. The worst case is a crucial fact hidden in far-away code. Evaluate any design idea by whether it reduces that load.
- **Martin's frame:** a technique should make the reader's job easier — specifically the *future* reader (someone else, or yourself a week later), not the author. Programmers spend more time reading than writing.

They agree modular decomposition is one of the best tools for reducing what a reader must hold at once. They disagree on when it stops helping.

## Ousterhout's model: deep vs shallow, and entanglement

The load-bearing vocabulary from APOSD:

- **Deep module** — lots of functionality behind a simple interface. Reading (or calling) it, you pay a small cost (learn the interface) instead of a large one (read the implementation). This is the whole payoff of decomposition.
- **Shallow module** — the interface is nearly as complex as the implementation it hides. Splitting here buys little; at the limit the caller must understand the whole implementation anyway, so the method is "pointless."
- **Entanglement** (APOSD: "conjoined" methods) — two methods where understanding one *requires* reading the other. The tell: flipping back and forth between implementations. Entangled methods scatter information that needs to be held together, so they are harder to read than the un-split monolith. The fix is usually to **combine** them.

Ousterhout's central complaint: *Clean Code*'s advice ("functions should be smaller than that"; "hardly ever 20 lines"; "just two, three, or four lines"; one-line `if`/`while` bodies) is one-sided. It gives strong quantitative pressure to chop, with almost no guidance on when chopping has gone too far. Tiny methods tend to be both shallow *and* entangled.

## Martin's model: One Thing, applied with judgment

Martin concedes over-decomposition is possible (`void doSomething() {doTheThing()}`) but locates the guardrail in the **One Thing Rule**: if you can *meaningfully* extract a method — give it a descriptive name, and it does less than the parent — the parent was doing more than one thing. His defenses:

- *Ease of abuse isn't disqualifying.* `if`, `switch`, assignment are all abusable; the answer is judgment, not prohibition.
- *Prefer erring toward decomposition.* Extractions can always be inlined later if they prove excessive; there's value in "visualizing" the decomposition.
- *Method ordering compensates.* Present methods in call order so a reader meets the loop before the methods that depend on it.

Ousterhout's rebuttals: "one thing" is vague (two lines = two things?); "can it be named" is no filter (anything can be named); and the rule is simply wrong when two things are genuinely coupled. Martin's own `clearTotals()` example — bundling two unrelated field initializations because they're both "initialization" — Ousterhout reads as the rule failing to hold together, not applying cleanly.

## The worked example: `PrimeGenerator`

The debate's crux is *Clean Code*'s Listing 10-8, a prime generator Martin refactored (from a Knuth *Literate Programming* example) into a class of **eight tiny methods**. Martin's caveat: the chapter's real lesson was decomposing a giant method into *classes* (`PrimePrinter`, `RowColumnPagePrinter`, `PrimeGenerator`); the internal method breakdown was "an afterthought," never meant for production. But he stands by it as illustrating small-well-named-method style.

Ousterhout's teardown, and why it generalizes:

- `isNotMultipleOfAnyPreviousPrimeFactor` → `isMultipleOfNthPrimeFactor` → `smallestOddNthMultipleNotLessThanCandidate` are shallow and mutually entangled — you must load all three to understand any one.
- **The killer point:** `isMultipleOf...` *reads like a pure predicate but has a side effect* (it mutates `multiplesOfPrimeFactors`), and that side effect imposes a hidden precondition — `candidate` must be monotonically non-decreasing across calls. A reader who trusts the name will believe they understand code they don't. *"If there is one thing more likely to result in bugs than not understanding code, it's thinking you understand it when you don't."*
- The method is entangled with its **callers** too: it only works inside a loop that increments `candidate` by twos, four call-layers away in `checkOddNumbersForSubsequentPrimes`.
- **Ordering doesn't save it.** Martin's "read it in call order" defense fails because intervening methods make the reader forget the loop context, and the actual constraint lives in the deepest method, farthest from the loop. If two pieces are tightly related, no arrangement of separate definitions substitutes for putting them together.

Martin's honest concession: returning to the code cold, he too "struggled with the names and structure" until he re-derived the algorithm — and he now dislikes the buried side effect. Ousterhout's meta-point: *if you can't predict whether your own code will be readable, the methodology is the problem.* (Martin's tu quoque: he found Ousterhout's own rewrite equally painful — so neither methodology fully rescued the reader.)

## The disagreement, distilled

The two authors' agreed summary:

- **Agree:** modular design is good; over-decomposition is possible; *Clean Code 1st ed.* gives little guidance for recognizing it; the internal method breakdown of `PrimeGenerator` is problematic.
- **Disagree:** how small to go (Martin much smaller); whether the One Thing Rule has adequate guardrails (Ousterhout: no); how much entanglement costs (Ousterhout: it defeats the entire purpose of decomposing — a split-but-entangled pair is worse than the monolith); whether method ordering can compensate (Ousterhout: no).

Martin's closing framing: *"We both value decomposition, and we both avoid entanglement; but we disagree on the relative weighting of those two values."* Martin also notes *Clean Code*'s 2008 context — the norm then was 1,000-line web methods — and that the 2nd edition is more balanced.

## Connections and implications

- Ousterhout's shallow/deep tradeoff is the same warning as Metz's [[wrong-abstraction]]: structure imposed too eagerly (a wrong abstraction, or a too-small method) is worse than none, and the remedy in both is to **inline back to one place, then re-cut along the real seams**. "Prefer duplication over the wrong abstraction" and "combine entangled methods" are the same move.
- The "future reader's cognitive load" premise both share is the operating definition of [[internal-software-quality]] and the thing [[computers-can-be-understood]] presumes is worth defending.
- Ousterhout's "learn the interface, trust the name" only works when the name doesn't lie — the `isMultipleOf...` side-effect bug is exactly the class of hard-to-maintain code that [[code-review]] (Dominus) says review exists to catch: a reviewer who "can't understand this without reading three other methods" has found the defect, not failed the audit.
- **AI-era note:** the length axis matters less when a coding agent generates and holds the whole call graph, but Ousterhout's *hidden-precondition* critique gets sharper, not softer — an agent (like a human) that trusts a misleading name propagates the latent bug faster. The reader whose load matters is now sometimes a model, but "don't hide a precondition behind an innocent-looking interface" survives the shift. Cf. [[judgment-in-ai-assisted-development]].

## Sources
- Martin, R. & Ousterhout, J. (2024–2025). "A Philosophy of Software Design vs Clean Code." <https://github.com/johnousterhout/aposd-vs-clean-code> — [[2025-02-15-aposd-vs-clean-code|local copy]]
- Follow-up video: Book Overflow Podcast, <https://www.youtube.com/watch?v=3Vlk6hCWBw0>
