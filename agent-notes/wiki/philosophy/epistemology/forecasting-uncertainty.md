---
source: agent
compiled_from:
  - agent-notes/raw/philosophy/epistemology/2018-12-17-taleb-silver-twitter-war.md
compiled_at: 2026-04-28
model: claude-opus-4-7
confidence: medium
---

# Forecasting Uncertainty: Aleatory vs. Epistemic

Probabilistic forecasts published as a single number between 0 and 1 fuse two fundamentally different kinds of uncertainty — and obscure the difference. Faber (2018), summarizing the long-running Nassim Taleb / Nate Silver argument over FiveThirtyEight, frames this as the central methodological problem with public forecasting.

## The two uncertainties

- **Aleatory uncertainty** is uncertainty intrinsic to a well-defined system. Given that a die has six sides, the probability of rolling a six is 1/6. The system is fully specified; only the outcome is random.
- **Epistemic uncertainty** is uncertainty about *the system itself*. How many sides does the die have? Is it loaded? Does this election have a Comey letter coming? Here you don't just need to predict the outcome — you need to guess the game.

Aleatory uncertainty is reducible by sampling. Epistemic uncertainty is reducible only by learning more about the structure of the world, and sometimes is not reducible at all in advance.

## Why the distinction matters for published probabilities

Faber argues that bespoke forecasting models like FiveThirtyEight's run a Monte Carlo simulation over a hand-built replica of the system and report the simulation average. What gets published — "Clinton has a 71% chance of winning" — is purely the **aleatory** output of a model whose **epistemic** uncertainty is silently set to zero. The headline number behaves like a probability (it lives between 0 and 1, it sums) without actually incorporating all the uncertainty a real probability would.

The practical consequences:

1. **No skin in the game.** A probabilistic forecaster never picks a winner, so they can never strictly be "wrong." When an unlikely outcome occurs, they retreat to "we said it could happen with probability *(1 − x)*." Faber, channeling Taleb, calls this a perfect scenario: the forecaster cannot lose.
2. **Implied decision boundary.** The public reads any forecast above 50% as a call. Forecasters accept credit for "calling 49 of 50 states" while disclaiming responsibility on the rare misses. The asymmetry only works because the decision boundary is left implicit.
3. **Narrative fallacy on noise.** Because the published forecast oscillates with news, every wiggle invites a causal story (Comey! emails!). Most of those wiggles are unmodeled epistemic uncertainty leaking in as variance — not signal about the world.
4. **Calibration on stable vs. non-linear systems.** Faber's empirical check — comparing FiveThirtyEight's stated probabilities to realized proportions — shows NFL forecasts are roughly calibrated within 2–5% (lots of repeated trials, stable mechanism), while Senate forecasts vary enormously. Sports approximate a closed aleatory system; elections do not.

## Taleb's normative claim

Taleb's argument, as Faber summarizes it: a forecast that does not incorporate all relevant uncertainty should not be published in the same units as one that does. Numbers in [0,1] are not automatically probabilities — they earn that status by behaving like probabilities, which means accounting for both kinds of uncertainty and being judged from the moment they are issued, not just the day before the event. Taleb's [2017 paper on the topic](https://arxiv.org/pdf/1703.06351.pdf) provides the technical statement.

The normative shift Taleb pushes for: **a forecaster is responsible for both aleatory and epistemic uncertainty.** In practice this implies (a) reporting forecasts whose variance reflects epistemic ignorance, (b) being judged across the entire pre-event window, not at the eleventh hour, and (c) declining to publish at all when a non-linear event is too far out to forecast meaningfully.

## The decision-boundary problem

In standard supervised classification, models commit to a **decision boundary** — typically 0.5 in binary settings, or argmax over softmax outputs in multiclass — as part of how the model is evaluated. The boundary is declared a priori, and accuracy is measurable against it.

Public probabilistic forecasts deliberately omit this commitment, leaving each reader to infer their own. Faber's argument is that this omission is what lets the forecaster appear correct regardless of outcome: with no stated boundary, no specific outcome can falsify the forecast.

## Connections

- **[[calibration]]** — calibration is the right framework for *checking* whether published probabilities behave like probabilities. Faber's NFL-vs-Senate empirical comparison is a calibration plot; the Senate miscalibration is a direct symptom of unmodeled epistemic uncertainty.
- **[[map-and-territory]]** — Box's "all models are wrong; some are useful" is the upstream maxim. The aleatory/epistemic split is one specific way models are wrong: they capture system-internal randomness but not system-structural ignorance. Carlson's "model obsolescence" failure mode is structurally an epistemic failure — the system itself changed and the model didn't notice.
- **[[reference-class-forecasting]]** — base-rate methods are partly a defense against epistemic over-confidence. By starting from the historical distribution of similar cases, a forecaster imports some of the epistemic variance that an inside-out model would zero out.
- **[[surprising-detail]]** — Salvatier's principle that reality contains more meaningful detail than expected is the root cause of irreducible epistemic uncertainty. The Comey letter is a "surprising detail" the model could not have enumerated.

## Takeaways for anyone publishing predictions

1. **State your decision boundary.** If your forecast is meant to inform action, name the threshold above which you'd act.
2. **Distinguish what your model captures from what it doesn't.** If your variance only reflects aleatory uncertainty, say so. Don't let the [0,1] format imply more than the model delivers.
3. **Be judgable from issuance, not just at the buzzer.** A forecast issued six months out should be either defended over the full window or not published.
4. **Treat non-linear, low-N domains differently from stable, high-N ones.** The same model architecture can be well-calibrated on NFL games and badly miscalibrated on elections. The honest move is to widen the variance — or decline.

## Sources

- Faber, Isaac (2018). "Why you should care about the Nate Silver vs. Nassim Taleb Twitter war." *Towards Data Science*, December 17, 2018. <https://medium.com/data-science/why-you-should-care-about-the-nate-silver-vs-nassim-taleb-twitter-war-a581dce1f5fc> — [[2018-12-17-taleb-silver-twitter-war|local copy]]
