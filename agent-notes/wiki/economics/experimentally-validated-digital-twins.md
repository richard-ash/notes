---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-11-13-experimentally-validated-digital-twins.md
  - agent-notes/raw/economics/2026-11-13-cowen-experimentally-validated-digital-twins.md
compiled_at: 2026-11-13
model: claude-fable-5-2
confidence: medium
---

# Experimentally Validated Digital Twins

A method for measuring whether a program works without running an experiment on it: predict what each participant would have earned without the program, compare that to what they did earn, and use a set of past randomized trials to measure how wrong the prediction method tends to be. Chetty, Fogel, Katz, Noray, Porter and Reisinger (November 2026 working paper) introduce it for U.S. job training programs, using tax records on 327 million adults. They find its error is about the same size as the error of the randomized trials themselves.

The durable idea is the second half. Predicting a counterfactual from observational data is old and has a bad reputation. What is new is treating randomized trials as a **calibration set** for a cheap estimator, so that the estimator can be biased and still usable, because the size of its bias is known.

## The method

1. **Train on non-participants.** For each program, fit gradient-boosted trees (LightGBM) on people who never took part, drawn from the same counties and age range. The model learns how a person's past predicts their future W-2 earnings.
2. **Predict each participant's counterfactual.** Inputs are all measured before enrollment: five years of earnings and employment, industry, age, sex, marital status, children, county, and neighborhood characteristics. The prediction is the "twin".
3. **Subtract.** Average realized earnings minus average predicted earnings across a program's participants is the estimated effect. Individual predictions are rough; the group average is what is reliable.
4. **Calibrate against trials.** Run steps 1 to 3 on 37 randomized trials covering 24 programs (21,092 participants) and compare with the experimental answers. The model never sees the trials' control groups.

The estimator is formally double/debiased machine learning (an outcome model plus a propensity model), but the paper reports that the outcome model alone does nearly as well ($1,900 versus $1,717). Propensity reweighting alone is worse ($2,611).

## What the calibration found

| Measure (dollars per year, 2025 dollars) | Value |
|---|---|
| Correlation of twin and trial estimates across 37 trials | 0.93 |
| Mean difference, twin minus trial | -$569 |
| Twin bias alone (noise-adjusted RMSE) | $1,717 |
| Twin total RMSE at typical observational sample size | $2,073 |
| Trial RMSE (sampling error only) | $2,126 |
| Spread of true effects across programs (SD) | $5,699 |
| 1986-style estimator bias (LaLonde specification) | $4,485 |

The twin is **not unbiased**. A joint test of zero bias across the 37 trials rejects decisively. The authors' move is to stop asking whether selection on observables holds and ask whether the resulting bias is small relative to the decisions at stake. Their bar, the "digital twins criterion", is total RMSE no larger than that of the trials. The twin clears it because it trades a little bias for much less sampling noise: its comparison group is effectively the whole country, and observational participant counts are larger than trial arms.

A margin of error of 1.96 × RMSE ($4,063) is smaller than the spread of true effects ($5,699), so the method can tell a strong program from an average one.

One systematic miss: adults often enroll right after a job loss (the "Ashenfelter dip"). Pre-enrollment data cannot see that shock, so the twin overpredicts earnings in the enrollment year. The shock is transitory and the twin matches the trial control group again from the following years.

## Why it works now and failed in 1986

LaLonde (1986) showed that observational estimates of job training effects did not reproduce experimental ones, which helped found the "credibility revolution" and the rule that only experiments and quasi-experiments count. That work used a survey comparison sample of 15,992 people with one or two years of prior earnings.

The paper varies three ingredients separately. Each one alone leaves bias high:

- **Sample.** LaLonde's specification on a population-scale sample: $3,746. Most of that gain comes from restricting to similar people in the same places, not from size.
- **Covariates.** Richer history in a LaLonde-sized sample with a linear model: $3,365.
- **Model flexibility.** Machine learning on LaLonde-style data: $3,397, echoing Imbens and Xu (2025).
- **All three:** $1,717, about 60% below the starting $4,485.

Work history carries most of the signal. With work history alone the bias is $3,822. With only demographics or only residential history it is above $10,000.

## What the method showed once validated

Applied to Year Up beyond its 2013–14 trial (271 site-by-year estimates, 2007 to 2023):

- **Effects move a lot over time and place.** The average effect rose from $5,198 for 2007 enrollees to $12,000 for 2017, then fell to $9,077 for 2022. One city climbed from $3,781 to $13,247 while another stayed flat near $6,783.
- **An old trial can be the worse guide.** For a site whose true effect is one standard deviation ($7,000) from the trial average, reusing the pooled trial number has an RMSE of $7,050, against $2,073 for a twin built for that site and year. The twin wins whenever the site differs from the trial average by more than $1,872.
- **Placement predicts impact.** Site-years placing under 31% of trainees into full-time target-sector jobs added $3,040 a year; those placing 80% or more added $10,163. Each percentage point goes with $121. The authors bound how much of this could be estimator bias (at most 88%) and say plainly it is not shown to be causal.
- **Gains outlast the first job.** 90% of Year Up participants changed employers within five years and still earned $5,762 a year more than their twins. The authors read this as a better career ladder, not one good placement.

## Implications

- **Experiments change role.** The authors suggest trials may be most valuable as tools to calibrate observational estimators, which then produce the site-, year- and subgroup-specific estimates that decisions need. Tyler Cowen's one-line reaction was that "work of this sort is going to revolutionize economic method." He gave no argument; the abstract's content is the case.
- **It is an outside-view move.** The uncertainty attached to a new estimate comes from the empirical distribution of past errors for similar cases, which is the same logic as [[reference-class-forecasting]]. The method inherits that technique's weak point too: everything depends on the new case belonging to the reference class.
- **Evidence standards may be mis-ranked.** Clearinghouses give their top rating to a single trial at one time and place. If effects vary as much as Year Up's do, a validated observational estimate for the right site and year can be more accurate than that trial. Compare the single-setting quasi-experimental evidence in [[la-zones-of-choice]].
- **The scarce input shifts to data access.** The method needs population-scale administrative records, which few researchers can use. That fits the argument in [[ai-economics-research]] that cheaper analysis reprices what is scarce in the field. It is also a direct counterexample to one of Munger's complaints in [[academic-economics-critique]]: here the countable data turned out to be enough.
- **Continuous evaluation becomes possible.** The authors note the estimator could be run on any of roughly 5,000 U.S. training programs with linkable participant records, fewer than 1% of which have had a trial.

## Limits and caveats

- **The key assumption is untestable in a new setting.** Bias in an unevaluated program is assumed to come from the same distribution as bias in the 37 trials. The authors restrict the claim to career training for working-age adults with prior work histories and open or lightly screened enrollment.
- **Other domains need their own trials.** Health, education and criminal justice are named as future work, each requiring its own calibration set.
- **No work history, no twin.** Youth, immigrants and other first-time entrants are an open question, since work history is the main predictor.
- **Bias estimate is imprecise.** The $1,717 figure has a bootstrap standard error of $730, from 24 distinct programs. Excluding the welfare-to-work and subsidized-employment trials, the estimated bias is $0.
- **Prior negative results exist elsewhere.** Gordon et al. (2023) found the same class of estimator badly biased for Facebook ad measurement, where the selection mechanism (ad bidding) was unobserved. The paper's reading is that this is a data problem: the estimator works when the data captures what drives selection.
- **Disclosed interest.** Chetty leads Opportunity Capital, which invests in training programs using the methods developed in the paper. The paper states this.
- **Working paper.** Out-of-sample results cover only Year Up; the authors say more programs will follow in later versions.

## Sources
- Chetty, Fogel, Katz, Noray, Porter, Reisinger (2026). "Experimentally Validated Digital Twins: Evaluating Workforce Training Programs in the Age of Big Data." <https://opportunityinsights.org/wp-content/uploads/2026/09/DigitalTwins_FullPaper.pdf> — [[2026-11-13-experimentally-validated-digital-twins|local copy]]
- Cowen (2026). "Experimentally validated digital twins." <https://marginalrevolution.com/marginalrevolution/2026/11/experimentally-validated-digital-twins.html> — [[2026-11-13-cowen-experimentally-validated-digital-twins|local copy]]
