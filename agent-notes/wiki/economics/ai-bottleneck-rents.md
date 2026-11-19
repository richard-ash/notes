---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-11-07-where-does-baumol-bite.md
compiled_at: 2026-11-19
model: claude-fable-5-2
confidence: medium
---

# Bottleneck rents in the AI stack

A bottleneck rent is the margin an input earns because its supply cannot expand as fast as the demand for it. The AI build-out needs a long chain of inputs, from sunlight and gas at one end to a finished task in the real economy at the other. The question of this article is which link in that chain keeps the rent once every link that can be made abundant has been.

The anchor source is Casey Handmer's essay "Where does Baumol bite?" (7 November 2026, with an edit dated 10 November). Handmer's answer is that almost every rent in the stack is transitional. Researchers held it in 2023; turbine makers and memory fabs hold it today. He argues it ends at electricity, and specifically at the legal permission to generate far more of it. On the demand side he says it ends at goods that a factory cannot make: land in a particular place, and work valued because a person did it.

This is the same question as [[ai-value-capture]] (Garicano and Saa-Requejo) and [[commodity-trap]] (Narayanan and Kapur), and all three agree that the model layer gets squeezed. They differ on where the surplus goes next. Handmer is also the founder of Terraform Industries, which builds solar-powered fuel plants and now solar-powered inference hardware, so his conclusion points at his own product. The section "Reading the essay" covers both points.

## The chain of the argument

**Capability is a power law in compute.** Handmer starts from the Chinchilla fit (Hoffmann et al. 2022): on the compute-optimal path, reducible loss falls as about C^−0.15, so each 10× of training compute removes about 30% of the remaining error. He prices this at about $2 per H100-hour: GPT-3 would cost about half a million dollars to train today, GPT-4 about $30 million, and each further step costs ten times the last. He reads this as slow but completely reliable, which is what matters to whoever writes the next check. This is the investor's version of [[the-bitter-lesson]] and the [[scaling-hypothesis]]. Once computation can substitute for clever people, cleverness stops being the scarce input.

**A power law makes input demand insatiable.** Steady progress in capability needs exponential growth in chips, memory, power and buildings. Handmer cites Epoch AI: frontier training compute up about 5× a year since 2020, the price of a fixed level of capability falling 9× to 900× a year, and the cost of running the frontier still rising. Any input that cannot grow by orders of magnitude becomes the binding constraint.

**Token demand is not capped by human attention.** This is the premise the conclusion depends on. Windows licences stopped growing when everyone who would own a PC had one. If tokens were like that, rent would end with whoever owns the human customer, which is the position described in [[aggregation-theory]]. Handmer's check: all 8.2 billion people reading 16 hours a day could read about 8 × 10^16 tokens a month. Google alone reported 3.2 quadrillion tokens a month in May 2026, about 4% of that ceiling, growing 7× a year. Most tokens are already read by machines. He expects more than 99.99% of valuable activity, in the limit, to run without a human in the loop. With no customer scarcity to own, the constraint is whichever component cannot be built fast enough.

**Baumol turns a speed question into a distribution question.** Baumol's cost disease says a sector that does not get more productive takes a rising share of spending and pulls overall growth down toward its own rate. Handmer follows Aghion, Jones and Jones (2017): when inputs are complements, the economy is a chain as strong as its weakest link. This is the production function behind [[ai-explosive-growth]] and [[weak-link-asymmetry]]. Handmer's addition is that the owner of the weakest link collects a growing share of income. "How fast does AI change the economy" and "who gets paid" are the same question. His string quartets for the build-out are turbine factories, fabs, grid interconnection, permitting, electricians, and deployment into hospitals, warehouses and courtrooms.

## One rule, five routes to it

The rule is: when two things are both needed to make something valuable, the one whose supply is harder to increase keeps the profit. Handmer gives five framings and says they are the same idea.

- **Buffett's looms.** Berkshire's textile mills kept buying cost-saving machines that every rival could also buy. The savings went to customers. A productivity gain available to all competitors raises the bar for survival and does not raise margins. Handmer calls this "a sobering thought for anyone selling tokens, or buying GPUs to sell tokens with."
- **[[commoditize-your-complement]]** (Spolsky, and Grove before him). IBM built the PC from open parts to commoditize its suppliers. The box became the commodity, and MS-DOS and Intel's x86 kept the profit because they had no substitute.
- **[[aggregation-theory]]** (Thompson). The internet made publishing free, scarcity moved to reader attention, and Google sat between the two.
- **7 Powers** (Helmer). Handmer maps each power to a holder in AI: scale economies to TSMC and the hyperscalers, switching costs to Nvidia through CUDA, cornered resources to ASML, interconnection positions and turbine slots, counter-positioning to open-weight releasers. He finds no AI-native holder of network economies, which is the question [[agent-network-effects]] examines. He reads every power as a way of making supply look inelastic to the counterparty. [[competitive-moats]] covers the same taxonomy.
- **Tax incidence.** For complements A and B, A's share of the surplus is roughly ε_B / (ε_A + ε_B), where ε is supply elasticity. Handmer labels this a heuristic and not a theorem. The same demand shock appears as volume on the elastic side and as price on the inelastic side.

The working conclusion is that commoditizing a complement means raising its elasticity: second-sourcing, standard interfaces, open-sourcing, vertical integration, or funding a competitor. Handmer reads Meta's open weights, the hyperscalers' custom chips and Nvidia's backing of neoclouds as this one move aimed in three directions.

He also notes that the usual historical outcome is not a small price drop. The old bottleneck becomes effectively unlimited and the firms built to ration it go to zero: Chilean nitrate after Haber-Bosch, steam locomotive builders after diesel, dock labor after containers, Kodak, Blockbuster.

## Handmer's ratings of each input

Ratings are his, short-run and qualitative.

| Input | Short-run supply elasticity | What is replacing or expanding it | Dissolved yet? |
| --- | --- | --- | --- |
| Frontier research talent | Very low in 2023, rising | AI-assisted research, distillation, people changing jobs | Largely |
| Algorithms and know-how | High | Publication, leakage, distillation | Yes |
| Training data | Low for human text | Synthetic data, RL environments | Largely |
| Accelerator design | Medium | TPU, Trainium, MTIA, Broadcom custom chips | Partly |
| Leading-edge foundry | Low for new fabs | Intel 18A, Samsung | Barely |
| EUV lithography | Very low | Nothing in sight; perhaps ten years at about $10B a year | No |
| HBM and advanced packaging | Low | Capacity expansion | Barely |
| Power generation | Low for gas turbines | Solar plus batteries, engines, fuel cells | Partly |
| Grid interconnection | Very low (over 5 years from request to operation) | Behind-the-meter campuses | Partly |
| Land, water, permits | Low | Jurisdiction shopping, dry cooling | Partly |
| Skilled construction labor | Low | Prefabrication, early robotics | Barely |
| Capital | High so far | Not needed | Not needed |
| Demand and distribution | Low | Agents acting for users | Open |
| Deployment into the physical economy | Very low | Robotics, automated labs, regulatory reform | Barely |

His summary is that the top of the list is being substituted at software speed and the bottom at construction speed. Evidence he cites for the bottom: GE Vernova holds 116 GW of gas turbine backlog and reservations against about 20 GW a year of output, with slots selling into 2031; Microsoft attributes about $25 billion of 2026 capex to component pricing; Google Cloud's backlog passed $460 billion.

## Taking pain

The part of the essay that is most its own is about bargaining. A buyer depends on one or two suppliers who will not expand as fast as the buyer's demand grows. The supplier's caution is rational, because turbine and memory makers have been bankrupted by past booms. Handmer lists nine responses in rising order of pain:

1. Pay up.
2. Take the supplier's risk with prepayments, take-or-pay contracts and paid reservations.
3. Finance the supplier's expansion.
4. Qualify a second source, even a worse one.
5. Design around the input.
6. Open more fronts: fund the supplier's competitor, buy the supplier's supplier, or litigate.
7. Corner the market.
8. Integrate vertically, or credibly threaten to.
9. Change the rules through permitting and policy.

His claim is that power flows to the participant who shows a willingness to take pain. The buyer does not need to succeed at replacing the supplier. Tesla's own 4680 battery cell ramped slowly and Tesla kept buying cells from Panasonic, LG and CATL, but the attempt ended Panasonic's ability to ration supply. In incidence terms, a vertical-integration threat leaves short-run elasticity unchanged. It changes the long-run elasticity the supplier believes it faces, and that belief sets the price. Google's TPUs do not need to beat Nvidia to discipline Nvidia's prices.

Two consequences follow. The first is a refinement of the scarcity rule: the input that ends up holding the rent "isn't necessarily the scarcest one. It's the one whose customers are least willing, or least able, to take pain." The second is his advice to builders: do not plan to hold a rent in anything a factory can make, and keep a hardware integration strategy so that you can negotiate as the bottleneck moves toward metal and electrons. [[startup-power]] makes a related point from the founder's side, that the useful question is what structural position a company holds relative to others.

In the 10 November edit Handmer applies the same lens to Chinese labs. They cannot match the frontier, so they distill American models and release the results as open weights. A closed lab cannot follow them to a price of zero without destroying its own business. He classes this as counter-positioning.

## Where the rent goes next

In 2023 the binding step was trained weights, and a few dozen researchers set the pace. Handmer says a rent does not vanish when its bottleneck dissolves. It moves to the next least elastic step, either up the chain toward steel, electrons and permits, or down it toward distribution, deployment and trust. His late-2026 reading is that layers near the user (apps, model labs) show substitutes and falling prices, and layers near physics (clouds, memory, foundry, power, sites) show backlogs and rising prices. He marks accelerators and aggregators as contested.

He sorts the candidates for a permanent bottleneck into three families: physics (elastic in the long run if manufacturing scales), law (scarce by design, changing at the speed of politics) and people (attention, trust, willingness to delegate). His bets:

- Recursive self-improvement dissolves the model layer's moat and does not entrench the first lab to reach it, because diffusion keeps any lead to months.
- No manufactured input stays inelastic against a demand signal this large and durable.
- Agents neither end aggregation nor become the strongest aggregators. They form economies that mostly trade with each other, where gathering human attention matters less. This disagrees with [[agents-as-aggregators]], where Thompson argues the personal agent is the next and largest aggregator.
- Rent stays with the owner of a scarce input only where there is no substitute, and only while that stays true.

His ten-year outlook has three stages. For about three years the constraints are turbines, transformers, HBM and interconnection. For the next three, the build-out routes around them with behind-the-meter solar and batteries, more custom chips, and fab capacity that catches up. By the end of the decade a token at a fixed capability is priced near the cost of its electricity and amortized silicon, and machines buy most tokens. The scarce inputs are then sunlit land, permits to cover it in panels, and a small remaining slice of human attention and trust.

## The terawatt arithmetic

Handmer's case that permission is the last constraint rests on these numbers:

- A terawatt of solar-powered compute at 15 acres per MW of load covers about 61,000 km², about a fifth of Nevada. About 80% of Nevada is federal land.
- Running compute around the clock on solar needs about 15 times as much panel capacity as load, so 1 TW of compute means about 15 TW of panels.
- Building that in ten years means 1.5 TW a year, about 30 times the current US installation rate and more than double current world production.

He says sunlight is abundant and panels are cheap, and that the constraint is legal permission to put panels on the ground. He calls that hard to change "without something close to a constitutional amendment." Buyers therefore route around permission: behind the meter, into permissive jurisdictions, abroad, and in Musk's case into orbit. Until one of these works at terawatt scale, he concludes, AI transforms the economy at the speed at which power plants are permitted. [[abundance-agenda]] covers the same procedural constraint for housing and transmission.

As evidence that the design works, Handmer reports that Terraform built a 1.8 MW array at its Muroc site at about half the expected $1.40 per watt and ran an H100-scale inference system from it for a week. In his design the GPUs run at about 99.9% utilization and the array and battery at about 30%, which leaves surplus power for a load that tolerates interruption. In Terraform's case that load is its synthetic fuel plant.

## The demand side

Handmer's answer on the demand side matches [[scarce-assets]] and [[ai-and-relational-scarcity]]. Baumol bites wherever AI cannot make more: positional goods such as waterfront and land near the people you love, and anything valued because a human did it in person. He expects the share of spending on live music, a good teacher or "a nurse who knows your name" to keep rising. The string quartet, which he first calls a strange example, is the right one for this end of the chain.

## Reading the essay

**The author sells the conclusion.** The essay ends with "We're hiring, raising, and taking orders." Its conclusion is that the lasting constraint is power, that solar is the answer, and that buyers should integrate into hardware, and Terraform sells exactly that. This is a reason to discount the confidence of the conclusion. It is not a reason to discard the elasticity framework, which is standard and matches the independent sources below.

**Against Garicano on the upstream layer.** [[ai-value-capture]] treats TSMC, the memory makers and Nvidia as durable rent holders, locked in by multi-year contracts and capital intensity. Handmer rates foundry and HBM as "barely" dissolved today and still expects both to go elastic within about six years. The two views agree for the near term and disagree about the long run. What decides it is whether suppliers believe the demand signal enough to build ahead of it. Handmer himself says the caution of turbine and memory makers is rational, which is the best argument for Garicano's side.

**Against Garicano on the downstream layer.** Garicano's main thesis is that intelligence is not the bottleneck and that surplus flows to whoever does the organizational work of deployment. Handmer's own table rates "deployment into the physical economy" as very low elasticity and barely dissolved, the same as interconnection. His conclusion still gives it only a "minuscule slice." The step that removes it is the premise that machines will buy almost all tokens. If most valuable AI work must still pass through human organizations, regulators and liability, as [[messy-jobs]] and [[ai-explosive-growth]] argue, then rent goes down the chain as well as up, and the permit conclusion is half of the answer.

**The unbounded-demand premise has a funding problem.** Handmer shows that machines consume most tokens. That is different from showing who pays for them. [[ai-capex-required-returns]] treats each layer as a ledger that must clear its own required return, and machine-to-machine tokens still need a final buyer with revenue. Handmer's reply is that these workloads produce output that buys more tokens. The essay asserts this loop and does not measure it.

**An unexplained case inside the essay.** Handmer rates the foundry as less elastic than accelerator design, so his rule predicts TSMC keeps more of the rent than Nvidia. He reports the reverse: Nvidia at about $5.6 trillion and TSMC at about $2.4 trillion. He presents this as the Wintel pattern and does not reconcile it with his own ratings. Garicano offers one candidate explanation, that TSMC rations wafers and holds prices below the market-clearing level to grow the market. Switching costs (CUDA) may also matter more than raw supply elasticity, which would mean elasticity alone is too thin a summary of bargaining position.

**"Law" is rated two ways.** In the three-family list Handmer says the speed of politics "isn't fixed" and that a trillion dollars of capex has already moved Washington quickly. In the conclusion he says permitting land at this scale needs something close to a constitutional amendment. His own ninth pain option is "change the rules." By his rule, the permit rent lasts only if buyers are unwilling or unable to take that pain, and the buyers here are the best-funded companies in the world.

**A check on the land figure (compiler's arithmetic, not in the essay).** Fifteen acres per MW of load with a 15× overbuild leaves one acre per MW of panels, or about 247 W per m² of land. Commercial modules are rated at roughly 210–230 W per m² of module area, so this implies panels covering more than all of the ground. Either the land needed is larger than a fifth of Nevada or the overbuild is smaller than 15×. A larger land figure would strengthen his permitting point, so the conclusion survives, but the two inputs should not be quoted together.

**What the essay adds to this wiki.** The other sources here describe where rents sit. Handmer describes how they move: a rent lasts until some buyer accepts enough pain to make supply elastic. That gives a test to apply to any claimed moat in the stack, including the ones in [[ai-lab-economics]] and [[token-pricing]]: who depends on this input, how much pain can they afford, and how long would a substitute take.

## Sources

- Handmer, Casey (2026). "Where does Baumol bite?" <https://blog.caseyhandmer.com/2026/11/07/where-does-baumol-bite/> — [[2026-11-07-where-does-baumol-bite|local copy]]
