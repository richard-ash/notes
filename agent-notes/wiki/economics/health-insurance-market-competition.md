---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-03-01-competition-in-health-insurance-markets.md
compiled_at: 2026-05-27
model: claude-opus-4-7
confidence: high
---

# Competition in US Health Insurance Markets

## The two-failure structure

Gaynor and Starc (2026) argue that US health insurance markets are characterized by **two interacting market failures**: large firms wielding market power, in a setting of pervasive asymmetric information. Either failure on its own would be tractable. The interaction is what makes the policy problem hard — and what makes naive single-instrument interventions (more competition; more risk adjustment; more menu choice) often backfire.

This frames the entire paper: every regulatory tool has a different sign when both failures are present. Antitrust enforcement that would unambiguously help in standard markets can have ambiguous welfare effects here, because selection pressures change how an insurer responds to losing a competitor. Risk adjustment that solves selection can hurt competition by removing the incentive to attract low-cost consumers. Standardized menus that block discriminatory plan design also block accommodation of heterogeneous preferences.

## How concentrated are these markets?

US health insurance is concentrated everywhere policymakers look:

| Segment | Avg largest insurer share | Avg top-3 share |
|---|---|---|
| Commercial large group | 64% | 91% |
| Commercial small group | 65% | 94% |
| Commercial individual | 53% | 79% (89% in some metrics) |

Variation across states is real but skewed: largest-insurer share runs from 17% in New York to 94% in Alabama, where Blue Cross/Blue Shield is a *de facto* monopoly.

Medicare Advantage is similarly concentrated: UnitedHealthcare alone holds nearly one-third of the market, and the five largest plan sponsors cover ~73% of MA enrollees. The Part D premium gap (standalone PDP averages $39 in 2025 vs. ~$7 for MA-PD plans) is a structural force pushing seniors into MA. Medicaid managed care covers 85% of beneficiaries and is also dominated by a small number of insurers.

In 2016 DOJ blocked Aetna's attempted MA acquisition of Humana — the court agreed that traditional Medicare and Medicare Advantage are separate markets (beneficiaries rarely switch between them), so the merger would have eliminated a close competitor without an adequate substitute. This case is now a load-bearing precedent for the proposition that MA is its own product market for antitrust purposes.

### Why there is little entry

New entrants face a chicken-and-egg problem distinctive to health insurance: they can attract enrollees with low premiums, but cannot negotiate favorable provider rates without volume — so their costs are too high to sustain low premiums without losing money. The minimum viable scale is set not by consumer-side economies but by the bargaining table with hospitals and physician groups.

This is one of the most important structural facts in the paper. It means de novo entry cannot discipline incumbent pricing the way it might in other markets, and that proposals like Leemore Dafny's *nth-lowest-rate rule* (where providers would be required to accept payments from entrants at the *n*th lowest market rate, with *n* set by a regulator) are aimed at the right pressure point.

## Vertical consolidation and the rise of health care platforms

Horizontal consolidation among insurers has been accompanied by aggressive vertical integration. UnitedHealth Group, through Optum, has gone from $130B revenue in 2014 to over $400B in 2024 — much of the growth coming from acquiring physician practices, data firms, and pharmacy benefit managers. Optum employed tens of thousands of doctors by 2022; the $4.3B DaVita Medical Group acquisition in 2019 was a pivotal moment. CVS-Aetna ($69–77B in 2018), CVS-Signify ($8B), and CVS-Oak Street ($10.6B) combine an insurer with retail pharmacy, in-home care, and value-based primary care.

Gaynor and Starc highlight two distinct concerns:

**MLR regulatory evasion.** The ACA's Medical Loss Ratio rule requires large-group insurers to spend at least 85% of premiums on medical care. If an insurer acquires providers and then inflates payments to those providers, "medical expenses" rise without any real change in cost — letting the insurer extract market-power rents while staying MLR-compliant. The additional payments are just profits kept "in-house." Baker et al. (2019) frame this as a form of regulatory gamesmanship; Gaynor and Starc treat it as a primary motivation for insurer-provider integration, not a side effect.

This is a sharper version of the [[third-party-payment-problem|third-party payment problem]]: the MLR was supposed to constrain insurer margins by forcing money out the door to care. Vertical integration short-circuits the constraint by making the door circular.

**Health care platforms.** Kanter and Gaynor (2025) extend the framework to "platforms" that integrate insurers, providers, data, and analytics. Their argument, which Gaynor and Starc endorse, is that platforms substantially raise entry costs, create strong incentives for self-preferencing, and expand regulatory-evasion opportunities — analogous to concerns about tech platforms (Stigler Committee 2019). The vertical literature in health insurance is thin (Ma 1997 is the main theoretical anchor), but evidence is accumulating: Gray, Alpert, Sood (2023) on the UnitedHealth-Catamaran PBM merger find non-integrated insurers pay much higher premiums after vertical integration, with no offsetting consumer benefits at the merged firm; Yde (2025) documents "profit tunneling" in Medicare Part D, where insurers shift profits from regulated insurance to less-regulated owned pharmacies; Cuesta, Noton, and Vatter (2024) on Chile show integrated insurers preferentially include their own hospitals and fragment markets, with double-marginalization gains offset by distorted plan design.

## Why competition behaves strangely under adverse selection

Standard intuition: more competitors → lower prices → better consumer welfare. In selection markets, this can flip in several ways.

### Downward pressure on markups (not upward)

Under adverse selection, an insurer that raises prices doesn't lose a random subset of customers — it loses the most price-sensitive ones, who are also the *healthiest* (and therefore cheapest to insure). The marginal customer lost has below-average cost, so a $1 price increase reduces average costs by *less* than $1 on the remaining pool. This puts *downward* pressure on markups, opposite to the standard intuition.

### The "unnatural monopoly"

Layton, Kong, and Shepard (2024) formalize the dynamic: aggressive price competition under adverse selection can push prices below the level needed to cover the risk pool's total cost, making the market sustain only one firm even with many potential entrants. The most price-sensitive consumers are the healthiest, so undercutting rivals is doubly attractive — and the equilibrium firm count collapses. The label "unnatural monopoly" captures that this monopoly emerges from competitive forces under selection, not from scale economies in production.

### Risk adjustment can hurt consumers

Mahoney and Weyl (2017): when firms have market power, risk adjustment (government-administered transfers that adjust insurer premiums up for sicker pools and down for healthier ones) removes the incentive to attract low-cost consumers. In standard adverse-selection settings this is a feature; under market power it weakens price competition. The authors apply their model to health insurance and find that typical risk adjustment policies hurt employees and employers while benefiting insurers. The point is general: an instrument calibrated for one market failure can exacerbate the other.

### Insurance "death spirals" and missing markets

Rothschild and Stiglitz (1976) is the canonical reference for adverse selection under competition leading to missing markets. Even when markets exist, plans are likely mispriced (Einav et al. 2010). The reason Medicare exists at all is that without it, health insurance would be priced in ways that made it unaffordable for many of the elderly.

## How insurers respond to information asymmetries

Beyond price, insurers have two instruments: **risk-rating** (price-discriminating on age, smoking, health history where permitted) and **menu design** (offering a portfolio of plans that screen consumers).

Gaynor and Starc emphasize that menu design becomes a primary tool for insurers with market power. Chade et al. (2022) show that a monopolist will exclude more consumers and offer more detailed menus than a social planner would. Gottlieb and Moreira (2023): market power leads to systematic exclusion — a monopolist leaves a portion of the market without coverage, while competitive markets usually provide at least minimal coverage. Shepard (2022) finds Massachusetts Exchange plans excluding costly "star" hospitals attract healthier patients — a profitable form of cream-skimming that persists even with risk adjustment.

This connects to the [[third-party-payment-problem|third-party payment problem]] from a different angle: not only does third-party payment dull price competition, but the insurer's freedom to design the contract becomes an exclusion instrument when competition is weak.

## Empirical evidence on consolidation

The empirical literature consistently finds that insurer consolidation raises premiums:

- **Dafny (2010):** large multisite employers with positive profit shocks face higher premium growth in markets with fewer insurers — direct evidence that insurers price-discriminate by willingness-to-pay. Challenges the assumption that health insurance markets are competitive.
- **Dafny, Duggan, Ramanarayanan (2012):** the 1999 Aetna-Prudential merger raised large-group premiums ~7% by 2007 in most-affected markets. Rivals also raised prices. Insurers simultaneously extracted *monopsony* gains — physician earnings growth slowed in concentrated markets. Both monopoly and monopsony power coexist.
- **Dafny, Gruber, Ody (2015):** UnitedHealthcare's 2014 exit from individual Marketplaces raised benchmark silver-plan premiums 5–11% in markets where UHC would have been a major competitor.
- **Starc (2014) on Medigap:** contractually identical policies see large premium variation. Sicker consumers buy more expensive plans from trusted brands. Two firms held ~70% of the market. Low elasticity (brand loyalty + search costs) lets prices stay high. *Imperfect competition*, not selection alone, drives premium dispersion.
- **Ho and Lee (2017) on CalPERS:** removing a major insurer like Kaiser typically *raises* premiums, because employer bargaining power falls. Whether hospital prices rise or fall depends on context. Large buyers like CalPERS act as a countervailing force.
- **Saltzman, Swanson, Polsky (2021) on California ACA:** consumer inertia (sticking with current plan) bestows substantial market power on insurers. Switching costs ≈ half the annual premium; four firms dominate. Removing inertia could lower premiums substantially — but only in markets where strategic pricing and risk adjustment are both present.

The cumulative picture is that insurer consolidation reliably raises premiums, that risk selection and competition interact in non-obvious ways, and that the welfare arithmetic in any given market depends on the specific bundle of market power, selection pressure, and regulatory constraints in force.

## "Rules of the road" — the policy menu

Gaynor and Starc are explicit that competition alone will not produce socially desirable outcomes. Their policy discussion enumerates the tools without claiming a unified prescription:

**Antitrust enforcement.** Necessary but not sufficient. Modeling imperfectly-competitive insurer responses is critical because selection changes post-merger price dynamics — welfare can go either way.

**Standardized menus.** A fixed menu of plan alternatives (used in Medigap, ACA marketplaces, Netherlands, Switzerland) makes comparison easier and limits obfuscation, at the cost of accommodating heterogeneous preferences.

**Risk adjustment, but carefully.** Naive risk adjustment dampens the incentive to seek cost savings from both efficiency *and* healthier consumers. Better designs (higher rebate pass-through, lower benchmarks in Medicare Advantage; broader risk corridors) can do better — Curto et al. (2021) find that ~two-thirds of MA cost savings accrue to insurers, not consumers, but market-design changes could shift the split.

**Informational interventions.** Abaluck et al. (2021) show consumer willingness-to-pay for plan quality is strikingly low. Choice frictions (inertia, limited attention, missing quality information) limit competition's bite (Handel and Kolstad 2015). Transparency about insurer administrative performance and plan quality could help.

**Long-term contracts.** US contracts are annual and don't insure against **reclassification risk** — the risk of premium increases following a health decline. Germany and Chile have efficient long-term contracts (Atal, Fang, Ziebarth 2025); enabling US versions is "a promising and important area for policy."

**Lower entry barriers.** Beyond Dafny's nth-rate proposal, Einav and Finkelstein (2023) propose automatic, basic, free universal coverage with optional supplemental purchase — using markets where they work (supplemental) and bypassing them where they don't (basic coverage).

**Unified oversight.** Given the interactions among issues, a single entity for monitoring, oversight, and policy implementation should be considered. State-by-state because insurance is state-regulated; federal for FEHBP and TRICARE.

## Connections

- [[third-party-payment-problem]] is the structural feature that makes all of this hard: because insurers pay for services rather than outcomes and consumers don't face marginal prices, neither side disciplines pricing. The market-power and selection dynamics Gaynor and Starc document are amplifications of that underlying problem, not independent failures.
- [[life-health-insurance-bundling]] proposes one path around the alignment problem — restructure insurance around outcomes (mortality, disability) so the insurer has a direct stake in the patient's health. Gaynor and Starc don't take up this proposal directly, but their long-term-contract discussion (reclassification risk) points at the same gap from a different angle: short-horizon contracts make insurers indifferent to long-run health, and any restructuring that lengthens the insurer's horizon (life bundles, long-term contracts) realigns incentives in the same direction.
- The MLR-evasion mechanism through vertical integration is a striking case of regulatory gamesmanship — a binding constraint becomes non-binding when the regulated entity acquires the counterparty whose payments determine compliance. This generalizes beyond health insurance to any context where a ratio-based regulation can be gamed by integrating the denominator.

## Open research questions flagged by the authors

The paper explicitly notes large gaps:

1. **Moral hazard under competition.** It is unclear whether competition leads to optimal or *excessive* insurance coverage when insurers compete by offering generous plans to attract consumers — particularly under employer-sponsored insurance where consumers weight coverage over premiums. Both theory and empirics are needed.
2. **Vertical integration effects.** The horizontal literature is mature; the vertical literature is in its early empirical phase. The opacity of ownership structures in modern health care conglomerates is itself a barrier to analysis.
3. **Platform dynamics.** Kanter and Gaynor (2025) raise the question; rigorous theoretical and empirical exploration of health care platforms is identified as "an important avenue for theoretical research."

## Sources

- Gaynor, Martin and Amanda Starc (2026). "Competition in Health Insurance Markets." NBER Working Paper No. 34928. <https://www.nber.org/papers/w34928> — [[2026-03-01-competition-in-health-insurance-markets|local copy]]
