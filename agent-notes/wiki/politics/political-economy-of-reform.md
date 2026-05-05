---
source: agent
compiled_from:
  - agent-notes/raw/politics/2026-04-01-how-reform-happens.md
compiled_at: 2026-05-04
model: claude-opus-4-7
confidence: medium
---

# The Political Economy of Reform

How do regulatory reforms actually pass? Two long-standing traditions in economics give opposing answers, and a 2026 paper by Djankov, Glaeser, and Shleifer settles much of the debate empirically using a new dataset of 3,590 reform attempts across 189 countries.

## The Coase–Olson divide

- **Coase (1960):** Reforms that raise aggregate wealth get implemented because winners can compensate losers. Reform is determined by social returns and the efficiency of bargaining — and per Lipset (1959), should be more frequent in richer countries with better institutions.
- **Olson (1982):** Welfare-improving reforms are frustrated by interest groups with veto power. Such groups proliferate as countries develop ("the accumulation of distributional coalitions leads to economic inefficiency and political rigidity"), so reform becomes *harder* with prosperity.

The choice matters because economists, as Djankov et al note in their conclusion, typically reach for cost-benefit analysis and ignore feasibility. Olson is a warning that returns may be irrelevant if no one can compensate the blockers.

## The Djankov–Glaeser–Shleifer model

A reformer (executive branch, legislature, or high court) proposes a reform with:
- pre-compensation social return `R` (higher in countries with heavier initial regulations),
- `L` losers per reform (the share of those harmed; structurally larger for labor reform than for tax reform),
- `θ` = inefficiency of compensation (1 dollar of compensation costs `1+θ` dollars; varies across countries — under Lipset's modernization hypothesis, θ is lower in richer countries),
- `N` veto points (each rejects with probability `φ(1−q)L` where `q` is the share of losers compensated).

Two parameters that vary across countries are `R` (returns to reform — "demand") and `θ` (compensation efficiency — "supply"). `N` varies *within* country across reform types — it's lower for technological reforms (existing legislation reapplied) than administrative ones (ministerial decrees) than legal ones (acts of parliament).

The model produces three testable predictions:
1. **Higher R** → more attempts, lower success rate per attempt, higher impact conditional on success.
2. **Lower θ** → more attempts, higher success rate per attempt, lower impact conditional on success (because more marginal reforms get tried).
3. **Veto points (N) and loser concentration (L)** make reform harder, especially when θ is high. With low θ, veto points can paradoxically *increase* success because they raise compensation.

The "Reform Possibilities Frontier" — analogous to a budget set — captures the tradeoff between probability of success and payoff conditional on success as the reformer chooses how broadly to compensate losers.

## What the data say

The dataset covers six World Bank Doing Business domains from 2005–2022: starting a business, paying taxes, protecting minority investors, labor regulation, enforcing contracts, resolving insolvency. Reforms are classified as legal, administrative, or technological, and tagged with which branch proposed them and which (if any) blocked them.

### Three headline findings

**1. Lipset beats Olson.** Holding initial regulatory levels constant, *richer* countries reform more, not less. Total reform success rate is **84% in rich countries vs 51% in poor**. Olson's prediction that prosperity breeds sclerosis is empirically wrong.

**2. Capacity dominates need.** Across countries, reform attempt rates are strongly correlated with reform *success* rates but uncorrelated (or weakly negatively) with reform *impact*. As attempts per year rise by 1, the success rate rises by about 26%. The pattern is "supply-shaped": countries good at implementing reform are the ones that try more, not countries that need it most.

**3. Veto points shape what kinds of reforms succeed.** Within a country, technological reforms — which reapply existing legislation and need no new laws — succeed at a 6:1 ratio. Administrative and legal reforms succeed at 2:1. The substantial worldwide improvements in starting-a-business and paying-taxes regulations are largely the prevalence of technological reforms in those domains. Labor regulation, where reforms are almost exclusively legal and create concentrated losers, has changed little.

### The "θ in poor countries" finding

The single most striking number: in poor countries, **25% of technological reforms are stopped by the executive itself**. In rich countries, the comparable rate is **3%**. Even within a single branch of government, poor countries cannot close deals. Sixteen percent of executive-initiated reforms are killed within the executive in the poorer half of countries (vs 3% in rich ones). This is the empirical signature of high θ — high cost of compensating losers, even where everyone is theoretically on the same team.

### The convergence pattern

Poor countries' regulations have moved toward rich-country norms in business-friendly directions. The model decomposes this into R vs θ:
- Reforms in low-initial-index countries have *larger* impact per reform → higher `R` (genuine returns to reform are bigger where regulations are worse).
- But these countries have *lower* success rates → higher `θ` (compensating losers is harder).

Convergence happens because R is high enough to overcome the θ disadvantage. R and θ tend to move together: countries with bad initial regulations have both more to gain *and* more difficulty extracting those gains.

## Implications

The authors' central methodological claim — directed at fellow economists — is that the cost-benefit framework that dominates policy analysis ignores feasibility. The key questions for would-be reformers are not just "what would this do if implemented?" but:

1. **Who has veto power?** Legal reforms face Parliament; administrative reforms face ministry-level vetoes; technological reforms face only the implementing agency. Pick the lowest-N vehicle that gets the job done.
2. **Where can compensation flow?** Reforms in functional polities (low θ) can absorb high-veto-point structures because losers get bought off. Reforms in dysfunctional polities need to *avoid* veto points entirely.
3. **Domain expertise gives partial veto immunity.** Branches are less likely to stop reforms originating in their own domain. Judiciary-led contract-enforcement reforms succeed 84% of the time. Executive-led starting-a-business reforms succeed 90% of the time.

This explains why some areas — business entry, tax payment digitization — have seen dramatic worldwide convergence while others (labor regulation, insolvency) have not. The reforms that succeed are not the ones with the highest social returns; they're the ones with the lowest veto-point exposure.

## Connection to other concepts

- The capacity-over-need finding parallels [[capitalism-and-democracy|Geloso & Tabarrok's claim]] that capitalism and democracy are mutually reinforcing open-access orders: the same institutional thickness that makes a society capitalist (low θ, functional bargaining) also makes its political system capable of reform.
- The "labor regulation barely changes" finding aligns with Olson's emphasis on concentrated interests — but Djankov et al show this isn't universal sclerosis; it's specific to domains where L (number of losers) is large and concentrated.
- The veto-points-matter result extends Tsebelis (1995) — originally a model of legislative bargaining — into the regulatory domain, with branches of government as veto players.

## Sources

- Djankov, S., Glaeser, E. L., & Shleifer, A. (April 2026). "How Reform Happens." NBER Working Paper No. 35119. <https://www.nber.org/papers/w35119> — [[2026-04-01-how-reform-happens|local copy]]
