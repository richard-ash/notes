---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-03-24-bundling-life-and-health-insurance.md
compiled_at: 2026-04-06
model: claude-opus-4-6
confidence: medium
---

# Bundling Life and Health Insurance

## The employer-sponsored health insurance problem

The U.S. employer-sponsored health insurance system originated as a WWII-era workaround: making employer contributions tax-free. This creates two distortions:

1. **Job lock.** Losing your job means losing your health coverage, which discourages labor mobility.
2. **Subsidized overconsumption.** The tax exclusion functions as a ~$300 billion annual subsidy to health spending, since the employer's contribution is simply offset by lower wages (the economic incidence falls on the worker regardless of who nominally pays).

The system's only defensible property is that employer pools partially solve adverse selection without an individual mandate — but this is a weak justification for a design no one would choose from scratch.

## The Koijen–Van Nieuwerbergh proposal

Decker draws on [Koijen and Van Nieuwerbergh (2020)](https://business.columbia.edu/sites/default/files-efs/citation_file_upload/qjz037.pdf) to propose a structural alternative: **make health insurance work like every other form of insurance** — a payout triggered by a bad event, not a managed-services contract.

### How insurance normally works

Fire, flood, and life insurance all follow the same pattern: a defined bad event triggers a cash payout, with no restrictions on how the money is spent. The insurer's only defense is proving the policyholder caused the event intentionally.

### Why health insurance is different

Health insurance instead promises to pay for *services* deemed medically necessary. Because what qualifies is not fully specified in advance, the insurer and the policyholder have a structural conflict of interest at the moment of claim — exactly when alignment matters most.

### The proposed realignment

Restructure health insurance to insure *health outcomes* (and, in the limit, life itself). If the insurer owes a payout when your health deteriorates or you die, their incentives flip:

- They are *motivated* to subsidize your medical treatment — including expensive treatments they might otherwise deny — because every year they delay a payout is a year they keep the premium.
- Post-contract incentive alignment becomes perfect: either the bad event happened and you have cash, or the insurer is working to prevent it for the same reasons you would.

### The immunotherapy example

Immunotherapies (e.g. monoclonal antibodies for cancer) can cost hundreds of thousands of dollars. Health insurers frequently refuse coverage or impose large copays. But a life insurer facing a death benefit payout has a straightforward actuarial reason to fund the treatment out of pocket — if it extends the policyholder's life, the insurer profits.

### Implementation mechanism

Koijen and Van Nieuwerbergh propose letting policyholders **draw down their death benefit** to pay for medical treatment. With appropriate restrictions on eligible spending, such a policy is actuarially costless — the insurer is simply moving a future payout forward in exchange for a probability of never paying the full amount.

## Barriers

The main obstacle is regulatory: health insurance operates under a dense, state-by-state regulatory framework with extensive provider-negotiation infrastructure. Life insurers entering the healthcare payment space would face significant institutional friction, even if the economics are sound.

## Sources

- Decker, Nicholas (2026). "Bundling Life and Health Insurance." <https://nicholasdecker.substack.com/p/bundling-life-and-health-insurance> — [[2026-03-24-bundling-life-and-health-insurance|local copy]]
- Koijen, Ralph S. J. and Stijn Van Nieuwerbergh (2020). "Combining Life and Health Insurance." <https://business.columbia.edu/sites/default/files-efs/citation_file_upload/qjz037.pdf>