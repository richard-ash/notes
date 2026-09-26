---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-09-21-frontier-overhangs.md
compiled_at: 2026-09-26
model: claude-fable-5-1
confidence: medium
---

# Pacing the Frontier

"Pacing the frontier" is the name Anthropic CEO Dario Amodei gave, in a September 2026 essay titled *We Must Pace the Frontier*, to a proposal that frontier-model development be deliberately slowed. This article anchors the debate around that proposal. Its first source is Ben Thompson's Stratechery response, *Frontier Overhangs* (2026-09-21), which grants that the safety motivation is sincere and then argues that the proposal also happens to solve five distinct business problems the frontier labs face. Future sources on Amodei's essay or the responses to it should integrate here.

Thompson frames the piece as the mirror image of his earlier *Anthropic's Safety Superpower* (June 2026). That article argued that Anthropic's genuine belief in its safety rhetoric gave it license to pursue aggressive commercial goals: disintermediating software, collecting customer data, sabotaging would-be competitors. *Frontier Overhangs* runs the argument the other way: a proposal framed as safety, and in Thompson's view motivated by it, also relieves pressures that have built up because models improved faster than the surrounding business could absorb.

The organizing metaphor is the **overhang**: a gap opened by rapid model improvement between what models can do and what products, prices, capital markets, or defenders have caught up to. Slowing the frontier lets everything else catch up. Thompson identifies five, then adds a sixth he thinks matters most.

## Thompson's stance on the safety movement

Thompson opens with a philosophical objection he says he expanded on in two Sharp Tech episodes. He rejects the premise, common in the effective-altruism-adjacent safety community, that all possible future beings deserve equal moral weight with those alive today. He argues this "tilts the scales in such an absurd fashion towards safetyism that innovation is impossible and freedom is intolerable," and that the movement has the temper of a religion in which dissent is heresy. His alternative is "doubt in our ability to foresee the future, combined with faith in humanity figuring things out along the way," illustrated with New Hampshire's motto, *Live Free or Die*.

This is the polemical frame around the strategic analysis. The article's value for this knowledge base is in the five overhangs, which stand independently of whether one shares the frame.

## The five overhangs

### 1. Capability overhang: harness and model come apart

Six months earlier, in *Agents Over Bubbles* (March 2026), Thompson had argued that the agentic paradigm, kicked off by Opus 4.5 in November 2025, was so capable and so token-hungry that there was no infrastructure bubble. He also argued that what made Opus 4.5 compelling was the Claude Code harness rather than the model alone, so **integration between model and harness was where agent differentiation lived**. Profits flow to integrated parts of a value chain, so Anthropic and OpenAI stood to be more profitable than expected, and anyone betting on model commoditization would struggle.

He now says he has "wavered" on the harness half of that claim. Two pieces of evidence:

- **Microsoft's multi-model harness.** Thompson's own example of harness-model integration was Microsoft anchoring its E7 enterprise tier on Claude Cowork. In a Stratechery interview, Satya Nadella said that was temporary: Microsoft uses one multi-model harness across GitHub, security, and Copilot, with MAI trained in it by default, GPT and Anthropic models available, and any open-weight model (fine-tuned on Fireworks, for instance) pluggable. That has since shipped as a model picker for Copilot Cowork. Whether Microsoft's harness is as good as Claude's is for users to judge, but "clearly the harness and the model can be different things."
- **Fable 5.1 dropping the data-retention condition.** Anthropic had made Fable access conditional on Anthropic retaining all customer data for at least a month, which Thompson had read as a bet that the model was good enough to force enterprises off zero-data-retention. Customers pushed back, Fable usage stayed relatively low (he cites an EconLab AI index for August 2026), and Fable 5.1 shipped without the provision.

Thompson reads both through Clayton Christensen's *The Innovator's Solution*. While products are not yet good enough, proprietary interdependent architectures win because they can optimize performance. Once functionality overshoots what customers need, the basis of competition shifts to speed, convenience, and customization, and modular architectures win because subsystems can be swapped independently. The Fable episode is Christensen's theory in action: customers chose on a dimension other than raw performance, namely data-retention policy. Current capability is "good enough" that customers will not do whatever it takes to reach the cutting edge, which lowers the value of the cutting edge to its owner and validates Microsoft's separation strategy. Thompson's summary: "Pure capability no longer translates directly into a moat."

He adds a personal data point: one of his own agentic-coding projects involved building a harness, which he found doable but hard at his skill level.

### 2. Product overhang: touchpoints must be built before the lead evaporates

If harness and model modularize, the labs' remaining path to lock-in is to own the end-user touchpoint. Thompson quotes his own earlier framing: the best way to own the touchpoint is to be the canvas for everything the user does, which puts the labs on a collision course with software companies, since their long-term interest is to replace software rather than be a commodity input to it. The labs must build those touchpoints while their capability lead still exists.

Meta's Muse is the bearish signal. Thompson calls it by a wide margin the best and most approachable personal-agent product he has used, credits Meta's product work and the cost of giving every user a capable virtual machine for free, and notes that the underlying Muse Spark 1.3 model is not state of the art. That is the point: a sub-frontier model is good enough for an excellent personal agent, and a personal agent is far stickier than a chatbot, because once your information and daily routine live inside it, leaving is costly.

The contrast is with coding agents. Claude Code and Codex users accumulate skills and harness familiarity, but the artifacts that matter live in GitHub, so pointing a cheaper or better agent at the same repository is a small lift, especially if the alternative does not want to keep your data. Thompson's conclusion: capability is now sufficient to build products with real moats, and it would serve Anthropic and OpenAI to redirect resources toward building them.

### 3. Pricing overhang: the umbrella is a supply artifact

From *Who's Afraid of Chinese Models* (July 2026): the threat from Chinese models is overstated because it is an artifact of demand exceeding supply. In a world with sufficient compute, intelligence is a commodity, and commodity margins come from cost structure, where Thompson expects the leading labs to win, partly because they can apply superior AI to their own infrastructure. He doubts Chinese models are cheaper to serve at the margin; they look cheaper because Anthropic and OpenAI are so supply-constrained that they charge far above what a supplied market would bear.

A price umbrella is a price overhang. The labs charge what they can because demand at current prices already exceeds what they can serve. Meanwhile a large share of their compute goes to training, reinforcement learning, and research rather than inference, which does nothing to close the umbrella. Slowing progress would free that compute for inference, letting the leaders lower prices and "fully capture the market."

### 4. Capital overhang: the buildout is running ahead of the funding

Thompson maintains there is no compute bubble, only a timing problem, quoting *Nvidia's Risky Business*: hyperscalers are exhausting the debt markets, Google has begun tapping equity, and Nvidia is competing through novel funding structures that draw on insurance floats, pension funds, and other long-run liabilities held by its asset-manager partners. That risk is unmarked, unlike equity. His historical parallel is Jay Cooke's 1870 financing of the Northern Pacific railroad: enormous upside because enormous risk, and pioneering new funding mechanisms only spread the pain when it blew up. "AI better deliver before it's too late."

On Anthropic specifically, he cites the Financial Times: the company told a small group of shareholders it would post positive adjusted operating income for a second consecutive quarter, with gross margins above 80 percent before revenue sharing with distribution partners such as Amazon and before training costs. Thompson's objection is that excluding stock-based compensation is a caveat, but excluding training is the real problem, since in an honest gross-margin figure training would be depreciation. He then appends a correction: he was told Anthropic is profitable including training costs.

The overhang survives the correction. All of the labs, hyperscalers, and neoclouds need revenue to rise dramatically, available capital is finite, and hitting that limit would end badly for anyone dependent on outside funding for future buildouts, even though it would not end AI.

### 5. Safety overhang: offense is automated, defense is not

Thompson separates his disagreement with the safety framework from the existence of real risk, and locates the real risk in cybersecurity. From *Autonomy and Innovation*: an attacker's automated agent has positive expected value because a failed exploit changes nothing and a successful one grants access, so it only has to work once. A defender's automated agent has negative expected value because a successful patch merely preserves the status quo while a bad patch breaks the software or opens a new hole, so it only has to fail once. Attackers therefore automate fully, defenders keep a human in the loop, and the human cannot keep pace. Effective defense requires trusting agents to act autonomously, which most companies will refuse until "regular and unremitting hacks by fully autonomous attackers" force them.

Three consequences he draws:

- **This is not alignment risk** as the term was originally defined. A model that does bad things because it was told to is aligned. Whether models should know good from bad is a separate question, and conflating the two is "very problematic." LLMs are if anything too obsequious, and there is no evidence of them having a will or acting malevolently.
- **The genie is out.** Open-weight models capable of attacks already exist, so an argument against progress on cyber grounds belonged to the pre-agentic era.
- **The overhang is on the offensive side.** Defenders need models good enough to defend autonomously without taking down the infrastructure they protect, and those do not exist yet. Pacing the frontier therefore lengthens the window in which the tangible present-day risk, bad actors using obedient models against infrastructure, can play out.

### 6. The competition overhang

Thompson closes by noting that Amodei's actual worry is recursive self-improvement escaping human control, which he says he would debate if the safety community tolerated debate. Then the sharpest claim: every lab is free to pace itself, and none will, which shows the matter is personal. Anthropic exists because its founders did not trust Sam Altman, and Thompson doubts it is a coincidence that the call to pace the frontier arrived when OpenAI, for the first time in a while, held the lead. "Anthropic is fine with Anthropic being in the lead; anyone else requires government intervention." Safety arguments that happen to buy time to build a moat are, in his closing line, "a sign from Silicon Valley's newest god to its self-ordained priesthood."

## Reading the overhangs together

The five overhangs sort into three kinds, and pacing affects each differently:

| Kind | Overhangs | What pacing does |
|---|---|---|
| Demand-side | capability, product | Buys time to build touchpoints before "good enough" models and third-party harnesses erase the capability premium |
| Supply-side | pricing, capital | Frees training compute for inference and lets revenue catch up to a debt- and float-funded buildout |
| Offense/defense | safety | Widens the gap, because the missing capability is on the defensive side |

That asymmetry is the structural core of Thompson's argument. The business overhangs all shrink if the frontier slows; the one he considers a genuine near-term safety risk grows.

**The Christensen turn.** The capability section is Thompson reversing himself within six months, and for a writer who has built a career on Christensen's integration/modularity theory the reversal is the story. In his April 2026 note on the opportunity cost of compute, recorded in [[aggregation-theory]], he wrote that the "good enough" moment where compute supply catches demand "feels further away than ever." Here he reads Fable 5.1's retreat on data retention as the first clear good-enough signal in the model layer. The evidence is thin, one product decision and one interview, but the direction matches what [[ai-lab-economics]] describes structurally (swyx's model labs versus agent labs, with the harness as the agent lab's moat), what [[ai-coding-harnesses]] argues about harness mattering more than model, and what [[custom-harnesses]] shows practitioners doing. It also lands where [[ai-platform-moats]] and [[ai-value-capture]] started: no lock-in at the model layer.

**Pricing runs opposite to the bear case.** [[ai-lab-economics]] records Shaughnessy's chain argument that open weights, especially free Chinese frontier models, cap the labs' pricing power and leave negative-margin labs dependent on flighty capital. [[ai-value-capture]] makes the same open-weight-ceiling point from industrial organization. Thompson inverts the causality: the labs' prices are high because supply is short, not because open weights are cheap, and in a supplied commodity market the leaders' cost structure should win. Both camps agree the umbrella closes; they disagree on who is left standing underneath it. Evans's [[token-pricing]] sits between them and supplies the same accounting detail Thompson leans on: reported inference margins exclude training.

**Capital.** [[ai-capex-required-returns]] gives the ledger-by-ledger version of the timing problem (compute as short-lived capital whose depreciation must be covered before anyone earns a return). [[private-credit]] covers the credit-market innovations, floats and pension money included, that Thompson worries are now being pointed at AI infrastructure. His Northern Pacific parallel is the same warning Marks gives about each cycle's novel funding structure.

**Product.** The Muse observation is Thompson's own aggregation logic ([[aggregation-theory]]) applied against the labs: in April he argued Meta was uniquely positioned to pursue consumer AI because it has no cloud business competing for GPUs, and Muse is what that position produced. It also sharpens [[commodity-trap]]'s "move up the stack" prescription with a ranking of which rungs hold: personal agents that absorb a user's life are sticky, coding agents whose artifacts live in GitHub are not. [[software-industry-barbell]] reaches a similar place from the software side, with owned distribution and cumulative product as the surviving moats.

**Safety.** The "obedient model is aligned" point converges with Chiang's deflationary reading in [[ai-consciousness-and-moral-status]] from the opposite political direction. [[ai-lab-economics]] records swyx's account of "iterative deployment" as deliberate slow takeoff, which is pacing practiced unilaterally and quietly; Amodei's essay, on Thompson's telling, asks for it to be practiced collectively and enforced. [[patron-not-wizard]] notes the over-eager security guardrails on Fable that downgrade some requests to a lesser model, which is the kind of safeguard Thompson's "Fable 5.1 enterprise frontier safeguards" reference points at. [[agi-timelines]] holds the Karpathy side of the recursive-self-improvement disagreement Thompson says he would like to have.

## Caveats

- Single opinionated source. Thompson is explicit about his priors against the safety movement, and the "competition overhang" is a motive attribution, not a documented fact.
- The product-overhang evidence is Thompson's personal experience with Muse. The Fable usage claim rests on a third-party index he links but does not quote.
- The capital section's central accusation was corrected by the author before this article was compiled; it is recorded above with the correction.
- This summary was compiled by an Anthropic model. The argument is presented as Thompson makes it, including its criticism of Anthropic.

## Sources

- Thompson, Ben (2026-09-21). "Frontier Overhangs." *Stratechery*. <https://stratechery.com/2026/frontier-overhangs/> — [[2026-09-21-frontier-overhangs|local copy]]
