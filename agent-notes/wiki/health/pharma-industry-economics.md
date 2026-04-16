---
source: agent
compiled_from:
  - agent-notes/raw/health/2025-11-11-dave-ricks-eli-lilly-glp1s-pharma.md
compiled_at: 2026-04-15
model: claude-opus-4-6
confidence: high
---

# Pharma Industry Economics

The pharmaceutical industry has unusual economic properties: extreme R&D intensity (~25% of revenue), binary risk at late stages, regulatory ratchets that never unwind, a pricing system where "none of the numbers mean anything" (per the Collisons), and a generic cliff that transfers 97% of value to consumers overnight. Understanding these dynamics is essential for evaluating both health policy and pharma as a business.

## R&D economics

### Scale of investment
- Eli Lilly spends ~$14 billion/year on R&D — "at the nation state level" (total NIH budget: $40B)
- Industry-wide, pharma spends ~25% of revenue on R&D, more than any other sector
- The average drug costs **$3.5-4 billion** to develop
- **60%+ of that cost is the final step** (Phase III trials)
- Most drugs that complete Phase III still don't generate positive returns

### The capital allocation problem
Dave Ricks describes Lilly as making "three or four important decisions a year, and they're all science." The Phase III go/no-go decision is the critical one: burning $1 billion+/year per program on a binary outcome. Lilly's approach:

- Rigorous quantitative framework ("bumpers on the bowling alley") plus judgment within that
- Rule: never decide in one meeting — return, reflect, push again
- Target **$0 markets** — conditions with no existing treatment, where there's no incumbent to displace but also no proven reimbursement path (echoes Jensen Huang at NVIDIA)

### Where biotech fits
More than half of medicines approved in the last decade originated in biotech, but almost none traveled the full path through biotech alone. The biotech investor base won't fund the large binary Phase III bets. Lilly runs a **hybrid model**: internal discovery (distributed in ~400-person satellite labs to preserve diseconomies-of-scale benefits for invention) plus biotech acquisitions where they're "buying proof that there's something here, not the specific solution" — often redoing the invention loop to create a "big pharma asset."

## Clinical trials

### Why they're so expensive
The median clinical trial enrollee costs **$40,000** (vs median US wage of $60,000). This isn't primarily waste — it reflects:

1. **Running the healthcare system** for participants: standardizing and leveling up care across sites and countries (~20-30% of cost)
2. **Institutional premiums**: overhead markups similar to NIH indirect cost rates (the "60% Harvard markup")
3. **Competition for elite trial sites**: MD Anderson, Brigham & Women's are the most congested and expensive

### The enrollment bottleneck
Half of Lilly's ~7-year clinical development time is waiting for enrollment. "If Taylor Swift can sell out a concert in a few seconds, why can't I fill an Alzheimer's study?" Key barriers:

- US healthcare data in EHRs is "very poorly organized"
- Physicians and institutions may not be interested in spending time on trials
- US has decentralized ethics review (IRB at every institution) vs Australia's single national system
- Only 4% of US cancer patients are in trials vs 25%+ in Spain and Australia

Lilly's innovation: **direct-to-patient trials**. Their Alzheimer's prevention study screened 80,000+ people with one US investigator, using televisits and blood-based diagnostics — the fastest-accrued Alzheimer's study in history.

### The regulatory ratchet
"Regulations are added but never taken away." The Vioxx (Merck) and Avandia (GSK) controversies — both later shown to have no real cardiovascular signal under better analysis — caused a decade-long chill and added a mandatory cardiovascular outcome trial requirement that added 4-5 years to diabetes drug development. By "happy accident," this now serves as a barrier to entry since incretins show massive cardiovascular benefit.

## Drug pricing

### The US pricing system is fundamentally broken
Ricks describes a system where **no price means what it says**:

- Manufacturers set a list price that almost nobody pays
- PBMs (pharmacy benefit managers) take a percentage of the spread between list and net price, incentivizing higher list prices
- Small employers and uninsured individuals pay the worst prices
- "The little guy gets the worst deal and the big guy gets the best deal"

The **insulin pricing bubble** illustrates perfectly: Lilly's net revenue was ~$30-40/month per patient, but list prices reached $275. When Lilly launched their own biosimilar (Insulin Lispro) at 1/3 the list price, insurance companies called Ricks saying "Don't — this is a threat to our model." No formulary covered it in the first year despite being dramatically cheaper.

### The free-rider problem
80-100% of biotech business plan returns come from the US market. Ex-US markets are purely incremental margin after US launch pays for R&D. This:
- Turns Americans against pharma (politically untenable)
- Skews R&D toward US health problems (5% of world population) instead of global health problems

### Ricks's "One Fair Price" proposal
1. Manufacturers set one price, indexed to GDP per capita across developed economies
2. Eliminate all discounts and rebates in the US
3. Products move through the channel at one transparent price

### The generics cliff
When a patent expires, the innovator loses **97% of pricing** overnight. This is "a fantastic deal for society, but a terrible situation for an inventor." Generic drugs require no efficacy proof — only pharmacokinetic similarity within a ±5% tolerance of active ingredient. Problems:
- Different excipients and absorption rates create real differences for sensitive patients
- Manufacturing has moved entirely offshore (India, China, Israel, Eastern Europe)
- Quality fraud is documented (Cipla's $500M fine)
- Injectable generics frequently run short due to cheap manufacturing
- "We probably should pay a little more for generics" for supply resilience

### Gene therapy pricing: shrinkwrap vs SaaS
One-time genetic cures (e.g., PCSK9 gene edit to permanently lower LDL) create a pricing paradox. The industry evolved around recurring unit pricing ("shrinkwrap software"), but a one-time cure displacing an $8-9K/year chronic therapy needs a new model. Ricks suggests a licensing/warranty concept: free procedure, ongoing payments while it works. The consumption side (governments, insurers) currently has no infrastructure for this.

## Patent system under pressure

### First-to-file enables clone drugs
The 2011 US switch from first-to-invent to first-to-file forces early patent publication. Chinese biotechs feed published patents into computers that generate molecules with 1-2 atom differences — creating a "shadow generic industry" that undermines patent protection while it's still nominally in force.

### Proposed reforms
1. **Data exclusivity**: 12 years of protection for companies that complete Phase III trials with primary data — a $3 billion ticket that copycats won't match
2. **Extended confidentiality**: increase patent secrecy from 12 months to 6 years before publication, so the product is well into clinical development before copycat nations can begin

## The biotech capital environment (late 2025)
- Large-cap pharma multiples (ex-Lilly): most compressed in 20 years
- Half of XBI (biotech index) trading below cash
- Half of venture rounds were down rounds
- The Inflation Reduction Act's government price intervention at 7 years further compresses expected returns

## Key numbers
| Metric | Value |
|---|---|
| US healthcare spend on medicine | 10 cents per dollar (8 cents branded, 2 cents generic) |
| Generic volume share | 90% |
| Life expectancy gain since 1965 | ~8 years (5-6 attributable to medicine) |
| Unpromoted drug adoption time | ~16 years |
| Promoted drug adoption time | ~8 years |
| Lilly's target | 4 years |

## See also

- [[glp1-drugs]] — mechanism, applications, and market dynamics of GLP-1 receptor agonists
- [[eli-lilly]] — company case study including LillyDirect and competitive position

## Sources
- Stripe / Patrick & John Collison (2025). "Dave Ricks, CEO of Eli Lilly, on GLP-1s and the business of pharma." <https://www.youtube.com/watch?v=-FmVCDx_kFw> — [[2025-11-11-dave-ricks-eli-lilly-glp1s-pharma|local copy]]
