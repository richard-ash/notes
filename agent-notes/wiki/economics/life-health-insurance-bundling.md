---
source: agent
compiled_from:
  - agent-notes/raw/economics/1994-04-01-buy-health-not-health-care.md
  - agent-notes/raw/economics/2026-03-24-bundling-life-and-health-insurance.md
  - agent-notes/raw/economics/2020-01-01-combining-life-and-health-insurance.md
compiled_at: 2026-05-06
model: claude-opus-4-7
confidence: high
---

# Bundling Life and Health Insurance

## The core insight

Life insurance companies have a direct financial benefit from life-extending medical treatments: successful treatment pushes the death benefit payout further into the future and raises future premium income. This creates a natural alignment between life insurers and policyholders that health insurers lack — and implies the two industries should be integrated.

The intellectual lineage runs from [[#hansons-1994-lmomdc-architecture|Hanson (1994)]], who first proposed reorganizing the entire care relationship around a life insurance contract, through Koijen and Van Nieuwerburgh's 2020 *Quarterly Journal of Economics* paper, which formalized and quantified the case using FDA-approved immunotherapies, to Decker (2026), who popularized it as a broader argument for restructuring U.S. health insurance. The three converge on the same structural insight from very different angles: Hanson via mechanism design and the agency problem, Koijen/Van Nieuwerburgh via empirical asset pricing and treatment economics, Decker via institutional critique of employer-sponsored insurance.

## Hanson's 1994 LMO/MDC architecture

Robin Hanson's "Buy Health, Not Health Care" (Cato Journal, Spring/Summer 1994) is the earliest articulation of the bundling argument. Where Koijen/Van Nieuwerburgh and Decker propose layering life-insurance incentives onto existing health insurance, Hanson proposes restructuring the full care relationship.

### "Health" vs. "health care"

Hanson's framing anchor: the agency problem in medicine is that we contract for *health care* (attention from specialists) when what we actually want is *health* (a long, healthy life). Rewarding advisers for giving advice produces "costly mediocre advice that is also comforting, authoritative, and requires their further services." Standard institutional fixes — professional licensing, malpractice law, internal review, HMO long-term contracts — all push toward minimizing or merely complying with *standard practice* rather than evolving better practice. Hanson's prescription: "give your care-givers a clear incentive to keep you well" by making them buyers of life and disability insurance on the patient.

### The LMO

A **Life Maintenance Organization** is the dual of an HMO: instead of bundling health care with health insurance, it bundles health care with *life* insurance. The patient agrees to follow the LMO's medical advice and to buy life insurance only from them; the LMO pays for all care it advises. The higher the patient's mortality risk, the more the LMO's expected payout — so it has a direct stake in keeping the patient alive. Disability, disfigurement, and pain insurance generalize the mechanism to non-mortality outcomes.

### The MDC

The LMO design has two structural problems: (i) the death benefit needed to fully internalize the patient's life value (Hanson uses $10M as illustrative) is wasteful — there is no one the patient wants to leave that much money to; and (ii) heavy life insurance creates moral hazard, including the possibility that relatives or the LMO itself acquire incentives to harm the patient.

Hanson's solution is the **Medical Defense Club**: a third party that buys the life insurance from the LMO and is the beneficiary on death. The patient pays the MDC a copayment that, for large enough pools, approaches the actual cost of care. This gives the LMO a +100% interest in the patient's life and the MDC a −100% interest, while the patient retains her own +100% interest — the negative-interest position is held by an entity institutionally constrained from acting on it. Hanson proposes structural safeguards: open clubs with rotating amateur leadership; cryptographic anonymity (notable for 1994); geographically distant memberships barred from the patient's continent; or splitting the negative interest across multiple MDCs so no one party has a strong stake.

The mechanism composes across time: switching LMOs after one year leaves the old LMO with a 100% interest in the patient's whole future life (with action-rights expiring) while the new LMO acquires its own 100% interest, giving the MDC a −200% position.

### The formal model

Hanson's appendix shows that under common knowledge of the mortality function `q_k`, the unique subgame-perfect equilibrium of the LMO/MDC bidding game produces the same patient effort `x_i`, doctor effort `w_j`, and insurance levels `I_k = H_k` as the patient would choose if she were her own doctor — with zero profits to LMO and MDC. The bundled institution replicates first-best self-treatment at the cost of the actual care plus actuarial overhead. Even under incomplete information, MDCs only need to estimate `Σ q_k I_k` (which LMO track records can supply), and an iterative learning process can converge to the same outcome.

### Hanson's incremental rollout

Hanson's path from current institutions to the LMO/MDC equilibrium is gradualist:
1. Individuals start buying life and disability insurance from their HMOs rather than from separate insurers — this slowly reorients HMO internal incentives.
2. Legalize MDCs so individuals can cheaply over-insure to strengthen care-giver incentives.
3. With direct outcome incentives in place, localities experiment with relaxing medical regulations (licensing, drug approval, required benefits packages) — the indirect regulatory apparatus exists to compensate for misaligned incentives, and should weaken once incentives are realigned.

This rollout is materially obstructed by centralized "health care alliances" that allow only a few standardized contracts per region — the kind of architecture that emerged from later U.S. health reform. The Koijen/Van Nieuwerburgh and Decker proposals are partial workarounds to this constraint: bundle at the product layer, not the institutional layer.

### Hanson vs. Koijen/Van Nieuwerburgh: same insight, different scope

| Dimension | Hanson 1994 | Koijen/Van Nieuwerburgh 2020 |
|---|---|---|
| Unit of bundling | Care provider sells life insurance | Existing life insurer subsidizes specific treatments |
| Mechanism | LMO + MDC (third-party negative interest) | Death benefit drawdown, collateralized loans |
| Outcomes covered | Death, disability, disfigurement, pain | Mortality (via face value + premium component) |
| Moral hazard solution | MDC institutionally barred from action | Existing fraud/criminal law |
| Regulatory frame | Eventually deregulate | Work within ACA, state insurance regulation |
| Empirical content | Stylized formal model | Calibrated to FDA immunotherapy data |

Koijen/Van Nieuwerburgh's quantitative result — life insurers gain $0.44 per dollar of death benefit from a stage-4 melanoma immunotherapy — can be read as direct empirical support for Hanson's claim that the alignment is large enough to drive the mechanism, even without the full LMO restructuring.

## The employer-sponsored health insurance problem

The U.S. employer-sponsored health insurance system originated as a WWII-era workaround: making employer contributions tax-free. This creates two distortions:

1. **Job lock.** Losing your job means losing your health coverage, which discourages labor mobility and exposes patients to reclassification risk.
2. **Subsidized overconsumption.** The tax exclusion functions as a ~$300 billion annual subsidy to health spending, since the employer's contribution is simply offset by lower wages (the economic incidence falls on the worker regardless of who nominally pays).

Decker argues the system's only defensible property is that employer pools partially solve adverse selection without an individual mandate — a weak justification for a design no one would choose from scratch.

## Why health insurance is structurally different from other insurance

Fire, flood, and life insurance all follow the same pattern: a defined bad event triggers a cash payout, with no restrictions on spending. Health insurance instead promises to pay for *services* deemed medically necessary. Because what qualifies is not fully specified in advance, the insurer and the policyholder have a structural conflict of interest at the moment of claim — exactly when alignment matters most.

## Why life insurers would cover what health insurers won't

Koijen and Van Nieuwerburgh identify several structural reasons health insurers under-cover life-extending treatments:

1. **Preexisting conditions.** Under the ACA, health insurers cannot discriminate by health status, leading to high-deductible pooling equilibria. Life insurers *can* condition on health at underwriting, allowing them to price a "quantity of life" contract at marginal cost.

2. **Quality vs. quantity of life.** Health insurers cover treatments that improve both quality and quantity of life. Life insurers care only about quantity. This unbundling lets life insurers target coverage more precisely — they face a *favorable* asymmetry when a treatment fails (no further cost) versus when it succeeds (no further cost either, just delayed payout).

3. **Off-label and innovative treatments.** About 16% of chemotherapy spending is on drugs not supported by the National Comprehensive Cancer Network and not reimbursed by Medicare/Medicaid. Life insurers face different cost-benefit trade-offs and may be more willing to fund experimental treatments, since even a cautious life insurer benefits from keeping the patient alive.

4. **Neglected risks.** Households underestimate the probability of major illness. Combining life insurance with critical illness coverage can overcome this risk neglect through automatic enrollment — a form of behaviorally-informed product design.

## Quantifying the benefit: immunotherapy case study

Koijen and Van Nieuwerburgh apply their model to FDA-approved immunotherapies across 23 cancer sites using SEER mortality data, Medicare Part B cost data, and LIMRA life insurance coverage data.

### The melanoma example

Consider a person who purchases life insurance at age 30 and is diagnosed with stage 4 melanoma at age 40. The life insurer's benefit from immunotherapy is **$0.44 per dollar of death benefit** (face value). A policy with a death benefit of $339,000 would cover the entire $149,011 cost of a Yervoy + Opdivo 12-week course. Even a modest $46,000 policy generates enough benefit to cover the typical $20,000 ACA family copay.

The treatment effectiveness parameter θ = 0.51 for melanoma — meaning the treatment works for roughly half of patients. The benefit decomposes into:
- A **premium component** (future premiums the insurer collects as the patient lives longer) — ~$0.02–0.04 per dollar
- A **face value component** (deferred death benefit payout) — ~$0.38–0.43 per dollar, dominating the total

The benefit is robust: nearly invariant to interest rates, insurer markups, and lapsation rates.

### Aggregate numbers

- Nearly **400,000 new cancer cases per year** are eligible for at least one FDA-approved immunotherapy
- Life insurance participation: 68% of men, 63% of women aged 35–54 — the highest of any financial instrument
- Average death benefit, ages 35–44: ~$240,000 (men), ~$220,000 (women)
- **Aggregate annual benefit to life insurers: $9.8 billion** (present value at 3%: $326 billion)
- Total immunotherapy cost for insured patients: $12.65 billion; the insurer's benefit is 77% of total cost
- Aggregate patient copay: $4.83 billion — less than the insurer's benefit
- For comparison: combined life and health insurance sector net income was $39.42 billion in 2017

Even for households with income below $35,000, life insurance ownership rates are 45–48%, with average death benefits of $77–91K — enough to generate meaningful treatment funding.

## Implementation mechanisms

Koijen and Van Nieuwerburgh propose two zero-cost mechanisms:

1. **Death benefit drawdown.** Allow consumers to tap their death benefit to pay for immunotherapy and associated expenses, reducing the benefit accordingly. This is equivalent to a perfectly efficient life-settlement market but without the perverse incentives of traditional settlements (where investors profit from the patient's death). Drawback: exposes the patient to reclassification risk if the treatment fails.

2. **Collateralized loans.** Life insurers offer loans at actuarially fair rates, collateralized by the policy's market value (which *increases* after a cancer diagnosis, since the insurer is now more likely to pay out). This is superior to standard credit markets because life insurance provides better collateral than future labor income — a key limitation of existing proposals.

Decker's popularization emphasizes a simpler framing: restructure health insurance to insure *health outcomes* rather than services. If the insurer owes a payout when health fails, incentives are perfectly aligned post-contract.

## Barriers to integration

### Industry survey findings

Koijen and Van Nieuwerburgh surveyed 23 senior executives across the life and health insurance industries. The barriers, in order of importance:

1. **Operational frictions** (70% of respondents): Life and health insurance are historically siloed businesses with different skill sets, contract horizons, funding costs, capital requirements, and legacy IT systems. Even companies that own both (Aetna, Cigna, United Healthcare) run them as separate operations.

2. **Regulatory frictions** (61%): Life and health insurance face different regulatory frameworks across 50 states. The critical concern (52%): if an integrated product were classified as health insurance, the insurer would lose the ability to condition on health status at underwriting. Consumer financial protection concerns (43%) and reputational risk around coverage boundaries (30%) add further friction.

3. **Uncertainty about health insurer response**: Life insurers worry that health insurers could respond strategically by increasing out-of-pocket costs for treatments the life insurer subsidizes. Industry experts assessed this as a minor concern in practice.

4. **Recency**: 30% of respondents noted that life-extending immunotherapies are a recent development — the industry may simply need more time to respond.

### Existing partial solutions

Despite these frictions, innovation is beginning at the boundary:

- **Accelerated Death Benefits (ADBs)**: Life insurance riders allowing early access to death benefit, but limited by HIPAA's 12–24 month survival prognosis requirement — increasingly binding as treatments *extend* life beyond this threshold.
- **Critical Illness Insurance (CII)**: Stand-alone lump-sum payouts on diagnosis. Design flaw: does not restrict payouts to diseases where life-extending treatments exist, nor restrict spending to those treatments. Some U.S. insurers (John Hancock, Nassau Re) are beginning to combine life + CII.
- **Wellness programs**: John Hancock's Vitality product, LifeScore Labs, and LifeEpigenetics represent moves toward treating the life insurer as an "equity holder in the policyholder's life."

## Relationship to the third-party payment problem

The structural misalignment that makes this proposal necessary is itself a consequence of [[third-party-payment-problem|the third-party payment problem]]: because health insurers pay for services rather than outcomes, neither patients nor providers face meaningful price pressure. Bundling life and health insurance is one approach to realigning incentives within the third-party system, rather than replacing it with direct consumer payment.

## Broader implications

### Beyond cancer

The logic extends to any expensive, life-extending treatment:
- **Hepatitis C**: Sovaldi costs $84,000 but has a 90% cure rate
- **Organ transplants**: $415,000 average cost; 8,000 Americans die annually waiting — life insurers could fund artificial organ development
- **Heart failure**: MitraClip device ($30,000) shows 48% mortality reduction
- **HIV/AIDS**: Optimal treatment costs $18,300/year; life insurers benefit from funding access
- **Gene therapies**: Zolgensma costs $2.1 million for spinal muscular atrophy in children
- **Opioid addiction**: Opioid substitution treatment extends life expectancy by ~7 years

### Long-term care insurance

The same framework applies: treatments that reduce the probability of needing long-term care (e.g., a future Alzheimer's treatment) benefit LTC insurers, who would have incentives to fund them.

### Virtuous circle for medical innovation

If life insurers finance treatments, the drug market grows. Larger markets incentivize pharma R&D. More effective treatments lower life insurance costs, increasing participation, which further grows the market. Life insurers' long-term contracts also make them natural funders of long-term medical research — potentially alleviating the well-documented underinvestment in long-horizon cancer research. Better biomarker pretests would increase effective θ, improving cost-benefit calculus and enabling funding of even more expensive therapies.

## Sources

- Hanson, Robin (1994). "Buy Health, Not Health Care." *Cato Journal*, 14(1). <https://mason.gmu.edu/~rhanson/buyhealth.html> — [[1994-04-01-buy-health-not-health-care|local copy]]
- Koijen, Ralph S. J. and Stijn Van Nieuwerburgh (2020). "Combining Life and Health Insurance." *The Quarterly Journal of Economics*, 135(2), 913–958. <https://business.columbia.edu/sites/default/files-efs/citation_file_upload/qjz037.pdf> — [[2020-01-01-combining-life-and-health-insurance|local copy]]
- Decker, Nicholas (2026). "Bundling Life and Health Insurance." <https://nicholasdecker.substack.com/p/bundling-life-and-health-insurance> — [[2026-03-24-bundling-life-and-health-insurance|local copy]]