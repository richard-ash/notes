---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-05-22-three-theses-on-ai-value-capture.md
compiled_at: 2026-05-22
model: claude-opus-4-7
confidence: medium
---

# AI Value Capture

Where in the AI value chain does the surplus actually flow? Garicano and Saa-Requejo argue that Silicon Valley's central wager — that whoever holds the most capable model captures the value — is wrong on industrial-organization grounds. The model layer is sandwiched between customers who can switch providers with a config change and suppliers (TSMC, Nvidia, the memory oligopoly) who are monopolists in their respective layers. The surplus flows past the labs both upstream to hardware and downstream to whoever does the unglamorous organizational work of implementing AI inside firms and governments.

This is the third installment in Garicano's "Smart Second Mover" series arguing for a European AI strategy that doesn't try to win the model race.

## The three theses

### 1. Competition in the output market will remain intense

Foundation models lack the network effects that locked in the previous generation of platforms. An API call sends tokens and receives tokens; switching providers is a configuration change. Fine-tuning data and finetuned weights stay with the corporate user, so there's no data flywheel returning to the lab.

The competitive fringe of open-weight models places a ceiling on frontier pricing. MiniMax M2.5 is priced at $1.15 per million output tokens against $25 for Claude Opus 4.6 — comparable capability roughly 20x cheaper. If frontier labs implicitly cooperated to raise prices, customers would defect to less capable models that are good enough.

The labs can still book enormous revenue (Anthropic guided to $10.9B in Q2 2026 with a first $559M operating profit) but margins are structurally compressed and the WSJ flagged that the accounting methodology is unclear. The deeper problem: even when inference becomes profitable, the logic of the race forces every dollar back into the next training run, whose cost has risen ~2.4× per year since 2016. Garicano and Saa-Requejo invoke the EMI CT-scanner case as the canonical innovator's trap — Nobel-prize-winning invention in the early 1970s, bankrupt by 1980 because all revenue went into staying ahead.

The favorable case for the labs is a learning-curve flywheel (the mechanism by which Google beat Microsoft on search without network effects). The authors qualify this: corporate use agreements typically bar labs from training on customer data, and Google's search-scale gap over Microsoft by 2008 was much larger than today's gap between frontier and open-weight labs. They concede the mechanism may work in narrow domains like coding (where recursive self-improvement is the extreme case), but argue it will fail wherever users retain control of proprietary data.

This thesis aligns closely with Evans's argument in [[ai-eats-the-world]] that foundation model APIs lack the lock-in of Windows or iOS — different framing, same conclusion.

### 2. The upstream bottleneck is concentrated and powerful

TSMC's N3 wafer capacity is the binding constraint on AI growth. AI accelerators absorbed 9% of N3 output in 2025, projected at 60% in 2026 and 90% in 2027. Hyperscaler 2026 capex consensus was revised up to $665B for the big four; on-demand GPU prices are rising even for older Hopper chips. Multi-year contracts with TSMC and the memory suppliers make the upstream layer un-replicable on any reasonable timeframe.

The puzzle: why do Nvidia and TSMC ration wafers and orders rather than clear the market through price? Because they're maximizing usage to grow the market and collect revenue tomorrow. The shadow price of frontier compute is dramatically higher than the contracted price, and the implicit rents are flowing to TSMC, to the memory oligopoly (SK Hynix, Samsung, Micron), and to Nvidia as architect of the entire supply chain — not to the labs that pay them.

### 3. Intelligence is not the bottleneck

This is the load-bearing thesis and the one Garicano draws from *Messy Jobs* (his book with Jin Li and Yanhui Wu, June 2026). In most organizational applications, the marginal increase in model capability buys a small marginal increase in deployed value. AI lowers the cost of processing information, but information processing is rarely the binding constraint. The scarce inputs are workflow redesign, organizational authority, proprietary data, and the political ability to overcome resistance.

The tax-authority example: a frontier model can review past files, cross-reference declarations, and flag anomalies, but every adverse decision must be legally justified and subject to appeal. The empirical-analysis bottleneck is already solved by models six months old; the binding constraint lives in the legal and procedural layer.

The HITECH Act provides the canonical case: the United States spent $27 billion starting in 2009 to digitize hospital records. A decade later, physicians spend roughly half their day on records and about a quarter with patients. The technology was available; the organizational knowledge of how to use it was not. The Stanford AI Index 2026 puts AI agent deployment in the single digits as a share of activity across nearly all business functions despite two years of saturation coverage.

This connects to [[task-automation-vs-paradigm-replacement]] (automation within existing paradigms is slow and bounded) and adds the IO point that the implementation layer's organizational capacity is the actual rent-generating asset. Regulation matters here not as a constraint on labs but as the variable that determines whether incumbents can block adoption.

## The middle-power prescription

The policy prescription follows directly from the three theses. If the surplus flows to implementation, Europe and other middle powers don't need to win the model race — they need a capable enough model, plus the organizational and regulatory work to actually use it. But the implementation strategy *requires* that the model layer stays competitive; if it doesn't, the labs can ration access or weaponize it.

Garicano and Saa-Requejo propose that a coalition of middle powers fund a shared, open-weights model held one or two tiers behind the frontier. The point is not to win — even Meta and xAI find frontier-keeping hard — but to keep the race competitive enough that European firms can use whatever's available.

The framing is options-theoretic under radical uncertainty. The shared cluster is insurance against two tail scenarios: (1) frontier access gets rationed or weaponized, and (2) a single provider locks in the market. In any other scenario, the cluster becomes ordinary infrastructure — not wasted, just unremarkable.

The feasibility argument is sized to the goal. The U.S. private sector invested $286B in AI in 2025 and is projected to triple in 2026; China invested $12.4B (one twentieth). A one-or-two-tiers-behind open-weights effort is affordable to a European coalition in a way that a frontier-keeping effort is not.

Footnote 2 explicitly distinguishes this from the "CERN for AI" proposals in the von der Leyen guidelines, the Letta and Draghi reports, and the Centre for Future Generations blueprint. The CFG version aims for trustworthy general-purpose AI and treats open weights as a first stage that closes as the model becomes more capable. Garicano and Saa-Requejo argue the opposite: aim deliberately behind the frontier and keep weights open by default. The institutional purpose is to discipline the market, not to chase capability.

## Implications

- **Two-layer rent picture.** Surplus accrues at the top (hardware/silicon, where multi-year contracts and capital intensity create real lock-in) and at the bottom (implementation, where organizational and regulatory work is the binding constraint). The middle (labs) is the squeezed layer. This is the inverse of the Silicon Valley narrative.
- **Implementation-layer policy matters more than model-layer policy.** For middle powers, the marginal regulatory action with the highest return is one that lets incumbents be displaced by AI-using competitors, not one that subsidizes domestic frontier labs.
- **Consumer surplus, not producer surplus.** The intense competition thesis implies that most of the value created by AI accrues to users (consumer surplus) rather than to labs (producer surplus). This is consistent with the asset-pricing puzzle in [[markets-believe-transformative-ai]] — the Andrews-Farboodi event study showing Treasury yields fall on frontier-model releases is one reading of "AI value flows to users and to the state, not to AI equity."
- **Open weights as competitive policy instrument.** The Garicano-Saa-Requejo argument re-frames open-weight models from an alignment/safety concern (the usual American debate) to an industrial-organization tool — the way a middle power keeps the upstream market competitive without trying to compete in it.
- **Continuity with the two-Europes argument.** This piece is consistent with [[two-europes-divergence]]: the rear of Europe (France, Italy, Spain) won't be saved by a frontier lab; the converging frontier (Poland, Baltics, Nordics) is the part of Europe that might actually do the implementation work. The shared open model is, on this reading, a precondition for whatever growth the rear can still capture.

## Where the argument is strongest and weakest

**Strongest** on the IO of the model layer. The no-network-effects, low-switching-cost, open-weight-ceiling argument is hard to refute and converges with Evans's independent analysis in [[ai-platform-moats]]. The EMI parallel is a real warning about the innovator's trap when the cost of staying ahead rises faster than the rents from being ahead.

**Weakest** on the favorable case for labs (learning curves), which the authors gesture at but don't fully engage with. If recursive self-improvement or agent-trajectory data does produce a flywheel — and coding is the obvious leading candidate — the thesis weakens domain by domain. The article concedes this for coding without quantifying how much of the economy is "coding-like" in the relevant sense.

The middle-power prescription assumes the implementation layer is reachable by European institutions. The HITECH counterexample cuts both ways: it's evidence that implementation is hard, but it doesn't tell you European bureaucracies are better at it than American ones. The argument that Europe doesn't need a frontier model is stronger than the argument that Europe can in fact do implementation well.

## Sources

- Garicano, Luis & Saa-Requejo, Jesús (2026). "Three theses on AI value capture." Silicon Continent. <https://www.siliconcontinent.com/p/three-theses-on-ai-value-capture> — [[2026-05-22-three-theses-on-ai-value-capture|local copy]]
