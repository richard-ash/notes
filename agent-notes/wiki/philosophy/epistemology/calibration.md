---
source: agent
compiled_from:
  - agent-notes/raw/philosophy/epistemology/2026-04-20-calibration.md
compiled_at: 2026-04-20
model: claude-opus-4-6
confidence: high
---

# Calibration

Calibration is the epistemic skill of having confidence levels that match your actual accuracy. A perfectly calibrated person's "70% sure" claims are correct exactly 70% of the time, their "90% sure" claims are correct 90% of the time, and so on.

## The concept

Perfect calibration is an abstract ideal — no one achieves it exactly — but it serves as a useful benchmark. The goal is not to know as many things as possible, but to *know how much you know*. This is a distinct skill from raw knowledge: you can be highly knowledgeable but poorly calibrated (overconfident), or modestly knowledgeable but well-calibrated (you know what you don't know).

Calibration sits alongside [[map-and-territory]] as a core rationality concept: the map-territory distinction tells you your models are imperfect; calibration tells you *how imperfect* to expect them to be.

## Measuring calibration

Galef provides a simple method: answer binary questions (true/false, A or B) and assign a confidence level to each answer. Then group your answers by confidence level and check what fraction you actually got right.

- If you said "75% sure" on 20 questions and got 15 right (75%), you're well-calibrated at that level.
- If you said "75% sure" but got 18 right (90%), you're *underconfident*.
- If you said "75% sure" but got 12 right (60%), you're *overconfident*.

The result can be plotted as a calibration curve: confidence on the x-axis, actual accuracy on the y-axis. Perfect calibration is the 45-degree line.

## Key properties

- **Learnable with modest practice.** A couple of hours of practice is enough for most people to become well-calibrated within a single domain (e.g., trivia questions).
- **Domain-specific transfer.** Calibration in one domain partially but not completely transfers to others. Being well-calibrated on trivia doesn't guarantee calibration on, say, career predictions.
- **Distinct from accuracy.** Calibration measures the *match* between confidence and correctness, not correctness alone. A person who says "55% sure" on everything and gets 55% right is perfectly calibrated, even though they're barely better than chance.

## Connections

Calibration is a central skill in the [[mental-models|mental models]] toolkit and underpins good [[decision-matrix|decision-making]] — if you can't accurately assess how likely your beliefs are to be correct, you can't properly weigh options. It also connects to the [[circle-of-competence]] concept: knowing the boundary of what you know well is itself a calibration judgment.

## Sources

- Galef, Julia (2021). "Calibration." <https://juliagalef.com/calibration/> — [[2026-04-20-calibration|local copy]]
