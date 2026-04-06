---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2019-05-29-is-quality-worth-cost.md
compiled_at: 2026-04-06
model: claude-opus-4-6
confidence: medium
---

# Internal Software Quality

Internal software quality — the cleanliness of architecture, code organization, naming, and modularity — is invisible to end users but profoundly affects the economics of software development. Fowler argues that the conventional cost-quality trade-off is inverted for internal quality: investing in it doesn't cost more, it costs *less* over any non-trivial time horizon.

## The external vs. internal distinction

External quality (UI polish, reliability, feature completeness) follows the familiar consumer-goods trade-off: higher quality costs more to produce, and customers decide whether to pay the premium. Internal quality — code structure, naming, test coverage, separation of concerns — is different because customers never see or directly value it. This makes it tempting for managers to deprioritize, but the economics point the other way.

## Cruft and the productivity curve

Fowler introduces "cruft" as the gap between the current codebase and its ideal form. Cruft accumulates when teams skip refactoring, tolerate unclear naming, or let architecture drift. The consequence is a characteristic productivity curve: low-quality codebases start fast but decelerate sharply as developers spend ever more time understanding existing code and tracing side effects. High-quality codebases maintain steadier throughput. Critically, Fowler claims the crossover point arrives within *weeks*, not months or years — making the "move fast now, clean up later" strategy self-defeating even in the short term.

## Even good teams produce cruft

Cruft isn't purely a symptom of carelessness. Requirements evolve, technologies shift, and the best architectural decisions only become clear after building the system. The distinguishing practice of elite teams is not avoiding cruft but *removing it continuously* through refactoring, automated testing, and continuous integration. The DORA (DevOps Research and Assessment) studies corroborate this: top-performing teams ship faster *and* more reliably, not by choosing between speed and quality but by investing in practices that reduce cruft systematically.

## Empirical support

Research by Tornhill and Borg (2024), analyzing 39 proprietary codebases, found that resolving issues in low-quality code takes more than twice as long as in high-quality code, and low-quality code exhibits 15× higher defect density. This quantifies the intuition that cruft compounds: poor quality doesn't just slow you down, it multiplies the bugs you must fix.

## Implications

The argument is economic, not moralistic. Fowler reframes quality investment as having *negative cost* — it pays for itself through faster future development. This inverts the usual framing where quality is a luxury. For engineering leaders, the practical takeaway is that "we don't have time to do it right" is almost always wrong: you don't have time *not* to.

This connects to [[choose-boring-technology]] — both arguments share the insight that disciplined, unglamorous choices (proven tech stacks, clean code) compound into sustainable velocity, while exciting shortcuts create debt that slows teams down.

## Sources

- Fowler, Martin (2019). "Is High Quality Software Worth the Cost?" <https://martinfowler.com/articles/is-quality-worth-cost.html> — [[2019-05-29-is-quality-worth-cost|local copy]]
