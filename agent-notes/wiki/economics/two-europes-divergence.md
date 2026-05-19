---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-01-02-two-europes.md
compiled_at: 2026-05-13
model: claude-opus-4-7
confidence: medium
---

# The Two Europes: convergence at the frontier, sclerosis in the rear

Luis Garicano and Olivier Kooi's January 2026 *Silicon Continent* essay reframes the long-running argument about European stagnation as a category error: the EU is not one slow-growing economy but two economies moving in opposite directions, and the debate between Gabriel Zucman/Krugman/Saez (Europe is catching up) and Philippe Aghion (Europe has fallen behind on innovation) is really a disagreement about which half they are looking at. Their empirical contribution is a fixed-effects regression on EU-27 fiscal data showing that the post-2022 Russian shock is reallocating spending in the half of Europe that didn't need it — and not in the half that does.

## The fracture in IMF/per-capita numbers

The headline numbers, 2000 → 2030 (IMF projections), measured as a share of US per-capita GDP:

| Country | 2000 | 2030 (projected) |
|---|---|---|
| Poland | 34% | 67% |
| Romania | 27% | 60% |
| Lithuania | 29% | 69% |
| Bulgaria | 23% | 53% |
| Portugal | 64% | 57% |
| Spain | 72% | 61% |
| France | 86% | 71% |
| Italy | 93% | 68% |

Eastern Europe's gains are not catch-up illusion: they reflect three decades of capital deepening and institutional convergence following EU accession. France and Italy's drops are not measurement artifacts either; even in [[ppp-and-productivity-comparison|rolling-PPP terms that flatter Europe]] the underlying productivity gap to the US has widened.

Garicano's reconciliation of the academic debate: **Saez-Zucman are describing the eastern half; Aghion is describing the western and southern half.** Both empirical claims are correct on their own terrain. The EU-wide average that frustrates both camps is a meaningless aggregate over two divergent processes.

## Olson's framework, applied to Europe's rear

Garicano leans heavily on Mancur Olson's *The Rise and Decline of Nations* (1982). Settled democracies accumulate "distributional coalitions" — producer associations, trade unions, professions, public-sector constituencies, regional lobbies, business incumbents — each maximizing its rent from the current institutional setup. No coalition is large enough to wreck the economy alone, but their combined veto power makes any reform that imposes concentrated losses politically impossible. Olson's prediction is that mature democracies rarely reform voluntarily; they reform when an external shock changes the bargain.

The canonical example Garicano invokes is the **Meiji Restoration**: Commodore Perry's 1853 warships in Uraga Bay forced Japanese elites to industrialize within fifteen years, building railways, schools, and a tax system on pain of colonization. The mechanism is "industrialize or be conquered."

Continental Europe is, in Garicano's reading, Olson's textbook case: old democracies, two decades of low growth (so no surplus to buy off losers), and large ageing constituencies that have little reason to accept short-term pain for long-term benefits. This is why the Draghi agenda — innovation, energy investment, defence, larger firms — is so hard to deliver: every reform creates concentrated losers today.

**This invocation of Olson is in direct tension with [[political-economy-of-reform|Djankov-Glaeser-Shleifer's 2026 empirical refutation]] of the sclerosis hypothesis.** Their dataset of 3,590 reform attempts across 189 countries shows that *richer* countries reform more, not less, and that what predicts reform success is institutional capacity to compensate losers (low θ), not absence of distributional coalitions. The two papers can be partially reconciled: Djankov et al. find that *labor regulation specifically* — the domain with the largest, most concentrated losers — barely changes anywhere, which is precisely the kind of reform Garicano has in mind for France/Italy/Spain. But the broader Olson story that "old democracies accumulate veto coalitions and can't reform" is not what the cross-country data show. Garicano's stronger claim — that Europe's rear is stuck because of Olsonian sclerosis — has to be specifically about labor-and-pension reform in three rich countries, not a general property of mature democracies.

## Besley-Persson on state capacity, and where Europe doesn't fit

Tim Besley and Torsten Persson's work on state capacity argues that external threats can function as a common-interest public good: when state survival is at stake, elites tolerate less rent-seeking and fund the things that hold the state together (taxation, courts, infrastructure, schools, military). The mechanism is not enlightenment, it's the alternative.

Garicano's contribution here is to note that **Besley-Persson's mechanism distinguishes two cases — strong-institution states (South Korea under Park, Israel, Taiwan) where threat builds capacity, vs. weak-institution states (Pakistan, Egypt) where threat converts into repression — but neither case fits modern Europe.** European states already have high common-interest capacity. What they don't have is that capacity *pointed at growth-promoting public goods*. It is pointed at consumption transfers — pensions, public-sector employment, sectoral protections.

So a security shock to such a state can do two things:

1. **Defence spending goes up easily** — this is what capable states reflexively do under threat. Adding a new claim on the budget is straightforward.
2. **Public investment and education going up requires displacing existing consumption claims** — pensioners, incumbents, protected sectors. This is much harder, because it requires not just raising revenue but reallocating it.

Garicano's central empirical question is whether the post-2022 shock has done (2), or only (1).

## The empirical core: proximity-to-Moscow gradient

Garicano and Kooi run a panel fixed-effects regression on EU-27 data, 2000–2024. The specification:

- Outcome: defence / public investment / education / pensions, each as a share of GDP
- Treatment: standardised proximity to Moscow (negative of great-circle distance from capital to Moscow), interacted with a post-2022 indicator
- Controls: country fixed effects (permanent differences), year fixed effects (common EU shocks), and **newcomer-by-year fixed effects** so the 13 post-2004 entrants get their own catch-up path in every year — the coefficient does not just pick up the East/West income gradient

Per standard deviation of proximity (≈ 750 km closer to Moscow), post-2022:

| Outcome | Effect (pp of GDP) | SE |
|---|---|---|
| Defence spending | +0.30 | 0.09 |
| Public investment (gross capital formation) | +0.39 | 0.12 |
| Education spending | +0.18 | (less precise) |
| Bundle (def + inv + edu) | +0.90 | significant |

The bundle moving together — not just defence — is the headline finding. Frontier governments aren't only buying weapons; they're reallocating fiscal effort in a way that is broader than pure security spending. Whether that becomes durable state-capacity building is "too early to say."

**Crucially, pension spending shows no post-2022 effect.** But pensions are descriptively higher in countries far from Moscow than near it: each additional 1,000 km from Moscow correlates with +1.07 pp of GDP higher 2022 pension spending and +0.49 pp more projected growth by 2040 (Pearson correlations 0.28 and 0.32). The mechanism is demographic and historical — eastern accession states have younger populations and pension regimes rebuilt later, on tighter terms — not a Russian-threat response. But the **joint distribution** is the point: the rear of Europe carries the heavier consumption claim *and* feels the weaker security shock at the same time.

## The political mechanism is missing

The Draghi report's implicit hope was that Europe's two crises — competitiveness and security — would reinforce each other: the Russian threat would supply the political urgency the competitiveness agenda has always lacked. Garicano's argument is that the data show the opposite correlation: **the shock is mobilizing the countries where the Draghi problem is not most severe** (Poland, the Baltics, Finland, Sweden — already closer to the administrative frontier or growing fast via convergence) **and is not creating comparable political room where the agenda is most needed** (Italy, Spain, France, where low productivity growth, ageing fiscal commitments, and protected incumbents are the heart of the problem and the war is "still a foreign-policy event" for the median voter).

This leaves Garicano with what he calls the missing piece in the European debate: nobody has supplied a political mechanism that can make the rear of Europe invest, modernise, and grow. A growth coalition strong enough to take on pensioners *and* incumbents *at the same time* is something few European democracies have managed durably. Macron's first term came closest before the Gilets Jaunes shut it down. On present evidence, Garicano expects the mechanism, if it comes, will be a **fiscal crisis** or a **larger external shock**. Without one, Europe will split into "a mobilising frontier, and a comfortable rear drifting into managed decline."

## Caveats Garicano acknowledges

- The post-2022 window is short — three years. Education and public investment respond with long lags; the education coefficient may grow or fade with more data.
- Fixed effects cannot rule out other shocks correlated with distance from Russia after 2022.
- Including 2022 itself is conservative — some 2022 budgets were set pre-invasion, so the estimate is a lower bound on the true shock effect.

The proximity-to-Moscow design is not a randomized treatment; it is a cross-sectional gradient interpreted as response to threat. The defensive reading is sound (eastern states near Russia really did mobilize more), but the *causal* attribution to Russian threat specifically (vs. younger demographics, smaller incumbent classes, fresher institutions) cannot be cleanly separated.

## How this connects

- The east/west growth divergence is the same fact described in [[ppp-and-productivity-comparison|Bergeaud's PPP thread]] from the other side: a "cheaper" France or Italy is the *mirror image* of slower productivity growth in tradables, not evidence things are fine. Garicano's per-capita figures (constant-PPP basis, from the IMF) make the productive-capacity divergence visible because they sidestep the rolling-PPP compression. The two articles are using different methodological apparatus to reach the same diagnosis about Western/Southern Europe.
- The implicit theory of reform — that Olsonian distributional coalitions are the binding constraint — sits in tension with [[political-economy-of-reform|Djankov-Glaeser-Shleifer's empirical finding]] that rich countries reform more, not less, and that capacity to compensate losers (low θ) is what drives reform prevalence. The reconciliation has to specify that pension-and-labor reform in three rich Western European countries is the narrow case where Olson's mechanism actually bites — not a property of mature democracies in general.
- The framing of pensioners as the entrenched consumption-claim that blocks growth investment is structurally similar to Hanson's argument in [[cultural-drift-maladaptation|cultural-drift-maladaptation]] about old, growth-favoring selection pressures being eroded — though Hanson's mechanism is cultural evolution by natural selection, not political coalition formation.

## Sources

- Garicano, Luis, and Kooi, Olivier (2026-01-02). "The two Europes." *Silicon Continent*. <https://www.siliconcontinent.com/p/the-two-europes> — [[2026-01-02-two-europes|local copy]]
