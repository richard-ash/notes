---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-11-06-weak-link-asymmetry.md
compiled_at: 2026-11-19
model: claude-fable-5-2
confidence: medium
---

# The weak-link asymmetry

The weak-link asymmetry is the claim that when the tasks in an economy are strong complements, improving a few of them raises output a little while damaging the same few lowers it a lot. Charles Jones and Christopher Tonetti (working paper, version 0.5, November 2026) use it to argue that AI's benefits and harms run on different clocks. The benefits need AI to improve weak links throughout the economy, which takes decades. The harms need AI to break one, which takes a narrow capability that frontier models may already have. Their headline arithmetic: with an elasticity of substitution across tasks of 0.2, making tasks worth 1% of GDP ten times more productive raises output by 0.25%, and making them ten times less productive lowers it by 68% on impact. "Gains are bounded and small. Losses are unbounded and large."

The mathematics is not new, and the authors say so. Baqaee and Farhi (2019) showed that with complementary inputs negative shocks are magnified and positive ones attenuated; Kremer's O-ring theory (1993) and Jones (2011) are the weak-links lineage. "Our contribution is to highlight the importance of this asymmetry to AI." The paper is the downside companion to [[ai-explosive-growth]], which uses the same production function and the same Jones-Tonetti calibration to explain why AI's gains arrive slowly. That slow arrival had been read as good news for safety, since gradual change leaves time to adapt. The paper's point is that the same complementarity makes the losses "large and immediate."

## The gain-loss formula

A unit measure of tasks combines into one final good with constant elasticity of substitution σ < 1, so every task is essential. Each task is produced by one input with a task-specific productivity. Multiply the productivity of tasks with cost share s by a factor z, hold the allocation of inputs fixed ("frozen", the case right after a sudden shock), and output changes by

`G(s, z; σ) = (1 − s + s·z^((σ−1)/σ))^(σ/(σ−1))`

Proposition 1 gives four properties for σ < 1:

- **Bounded gains.** As z → ∞, G → `(1/(1−s))^(σ/(1−σ))`. Improving one link without limit cannot make the chain stronger than its other links allow. This is the "infinite automation" bound of Jones and Tonetti's growth paper.
- **Unbounded losses.** As z → 0, G → 0. The authors note that this makes "weak links" a better metaphor than "bottlenecks."
- **Local symmetry.** For a small shock the elasticity of output is the cost share s in both directions. This is Hulten's theorem (1978).
- **Global asymmetry.** Log output is strictly concave in the log shock. The symmetric case holds at every shock size only when σ = 1 (Cobb-Douglas, where G = z^s).

The mechanics fit in one worked example. At σ = 0.2 the exponent (σ−1)/σ is −4, so the bracket adds up each task's scarcity (its output raised to the power −4), weighted by cost share. Before the shock every term is 1 and the bracket is 1. A tenfold improvement multiplies the affected term by 10⁻⁴: it falls from 0.01 to 0.000001 and the bracket falls to 0.990001. The most any improvement can do is delete a term that was 1% of the sum. A tenfold degradation multiplies the same term by 10⁴: it rises from 0.01 to 100 and the bracket becomes 100.99. Raising each bracket to the power −1/4 gives 1.0025 and 0.3155. Improvement can only remove scarcity that is already there, while damage can add scarcity without limit.

A restatement in cost shares: the shock moves the affected tasks' share from s to s′, and output changes by `((1−s′)/(1−s))^(σ/(1−σ))`. With complements, damage raises a task's cost share and improvement lowers it. That is the Baumol mechanism of [[structural-change]], run in both directions.

Percent change in output from a shock to tasks worth 1% of GDP, inputs frozen:

| Shock | σ = 0.2 | σ = 0.5 | σ = 1 |
|---|---|---|---|
| Infinite improvement | +0.3 | +1 | unbounded |
| 10× better | +0.3 | +0.9 | +2.3 |
| 10× worse | −68 | −8 | −2.3 |
| 100× worse | −97 | −50 | −4.5 |

The first two columns are the paper's Table 2. The σ = 1 column is this wiki's arithmetic from G = z^s, added to show that the asymmetry comes entirely from complementarity. For tasks worth a third of GDP at σ = 0.2 the figures are +11 (tenfold or infinite), −87 and −99.

The paper draws two readings from these numbers. Gains saturate almost at once (tenfold and infinite improvement agree to a decimal) while losses keep growing. And the loss is steep in the size of the target only near zero: at z = 1/10, output falls to 0.32 of its initial level when 1% of the economy is hit and to 0.14 when 25% is. "Most of the damage a shock can do is done once the damaged tasks are a modest share of the economy." An attacker does not need a large target.

## The parameter everything rests on

σ = 0.2 is carried over from Jones and Tonetti's growth paper, where it is calibrated to the falling factor share of computers (see [[ai-explosive-growth]]). The supporting estimates cited here:

- Boehm, Flaaen and Pandalai-Nayar (2019), on US affiliates of Japanese firms after the 2011 Tōhoku earthquake: 0.2 between Japanese and other materials, 0.03 between materials and a capital-labor aggregate.
- Atalay (2017): below 0.2 across intermediate inputs in annual US industry data; he uses 0.1.
- Demirer, Musolff and Yang (2026): 0.23 between AI and human effort in software development.
- Hamilton (2009): a short-run oil demand elasticity of 0.10 in 1973–74.

The motivating case is Toyota. Renesas held about 40% of the world market for automotive microcontrollers, the chips were customized to each car model, and when its Naka plant stopped, Toyota's output in Japan ran 63%, 78% and 54% below the previous year in March, April and May 2011.

The paper calls 0.5 "the upper end of the empirically relevant range." At 0.5 the asymmetry survives but the ratio of loss to gain falls from 272 to about 8. The appendix also reports an estimate that points the other way: Carvalho et al. (2021), over a one-year horizon in Japanese firm-to-firm data after the same earthquake, find 1.2 across intermediate inputs and 0.6 between primary and intermediate inputs. The main text does not discuss it. Read together, the estimates say the elasticity depends on the horizon: near zero in the first weeks, and possibly near one within a year.

## Reallocation: the short run is the dangerous part

Once inputs can move toward the damaged tasks, Proposition 2 says the response is the same formula at a higher elasticity, σʳ = 1/(2 − σ). At σ = 0.2 that is 0.56. It never falls below 0.5 even for perfect complements, because doubling a task's input fully offsets halving its productivity. In the σ → 0 limit the reallocated response is Amdahl's law, `(1 − s + s/z)^(−1)`.

| Cost share hit | Infinite automation, frozen | Infinite automation, reallocated | 10× worse, frozen | 10× worse, reallocated |
|---|---|---|---|---|
| 1% | +0.3 | +1 | −68 | −6 |
| 10% | +3 | +14 | −82 | −41 |
| 25% | +7 | +43 | −86 | −65 |
| 50% | +19 | +138 | −88 | −80 |

Reallocation removes over 90% of the loss when the damaged tasks are 1% of the economy and about a quarter of it when they are 25%. It works through prices. With inputs frozen, the relative price of a damaged task rises a hundred-thousand-fold and its cost share goes from 1% to 99% of GDP. After reallocation the share settles at 6% and the price is up tenfold. The gain side depends on reallocation too: four fifths of the gain from automating the 1% arrives only when the freed inputs move to the remaining tasks.

The paper names three conditions for reallocation to happen. A substitute has to exist (more computers do not help when computers are hacked). The processes the substitute needs must be rebuilt (paper ledgers, and the people who knew how to use them, are gone). And the substitute must not run on things the attack also disabled. Maersk after NotPetya is the favorable case: it moved 80% of its volume by hand for the ten days its systems took to rebuild, "because its ports, its phones, and everyone else's computers still worked." An attack on the payments network or the grid takes those down too, so "an economy-wide attack reallocates more slowly than a firm-level one."

How long the frozen period lasts depends on what was damaged: about a week for a hacked banking system, eleven months for Puerto Rico's grid, a two-to-four-year wait for a large transformer, and forever for deaths. The policy conclusion is that anything shortening it (redundancy, stockpiles, backup capacity, response planning) is a safety investment.

## Candidate weak links

The paper's examples of small things that carry large shares of activity:

- **The grid.** High-voltage transformers are under 3% of the transformers in US substations and carry 60–70% of the nation's electricity. They weigh 150 to 400 tons. The National Research Council (2012) concluded a planned attack "could deny large regions of the country access to bulk system power for weeks or even months."
- **Software.** xz Utils, a compression library in nearly every Linux distribution, has a single volunteer maintainer; an attacker spent two years inserting a backdoor that an engineer found by chance in 2024. The paper says AI makes the search for such openings cheap and cites Anthropic's report that Mythos Preview found more than ten thousand high or critical vulnerabilities in "the most systemically important software." Those were found to be fixed, and "fixing is the slower step."
- **Hardware destroyed through software.** Stuxnet, and the 2022 attack on Viasat's KA-SAT network, which left tens of thousands of modems unable to operate and cut remote monitoring of about 5,800 wind turbines; a month later almost half the farms were still offline.
- **Chips.** In 2019, 92% of the world's capacity for chips below 10 nanometers was in Taiwan. ASML is the only maker of EUV lithography systems and Carl Zeiss is ASML's sole supplier of optics. The same chain appears in [[ai-explosive-growth]] as an essential input that limits growth; here it is a target. [[quantum-supply-chains]] describes similar single-supplier chokepoints in another industry.
- **People.** Essential occupations take years to learn and cluster geographically: frontier AI research in San Francisco, finance in New York and London, leading-edge chipmaking in Taiwan.
- **Nuclear command systems**, through social engineering or manufactured false information.

AI is said to help an attacker in three ways once guardrails are bypassed: finding the weak links whose failure does the most harm, planning and keeping the plan secret, and carrying it out. The underlying claim about timing is "It is easier to improve short chains than long ones": cyber and bio capabilities are narrow and arrive long before AI can run a large company or robots can teach school.

## Historical episodes

"No shock on record has cost 68 percent of GDP," the authors write, and they test the formula on five episodes. Losses are in percent of GDP.

| Episode | Cost share | Shock | Formula, frozen | Formula, reallocated | Outcome |
|---|---|---|---|---|---|
| Oil embargo, 1973–74 | 4.5% | −4% | 0.2 | 0.2 | US GDP −3%; oil price ×4 |
| German gas, 2022 | 1.2% | −30% (full stop) | 0.9 | 0.5 | realized cut about half; GDP +1.9% |
| Covid, UK, April 2020 | 15–20% | −40 to −50% | 16–29 | 9–16 | GDP −25% that month |
| Puerto Rico, 2017 | 3% | −75% | 42 | 7 | activity index −18% in 2017Q4 |
| Soviet collapse, 1989–98 | broad | large | n/a | n/a | official GDP −40 to −50% |

The paper's reading is that historical shocks were mild, mild shocks give small predicted losses, and when a shock was large the loss was several times the Hulten benchmark of cost share times shock (7–13% for Covid against 25% observed). The appendix supplies qualifications that weaken each case as a test:

- "The cost shares and shocks are our assignments," made after the fact, and the predicted bands are wide (7 to 42 for Puerto Rico).
- **Oil.** The formula under-predicts by an order of magnitude. Hamilton attributes the gap to the demand side, as households cut spending on cars and other goods. That is a different mechanism from weak links.
- **Germany.** The forecasts of 8–12% losses "treated gas as an essential input whose loss multiplies along the value chain." That is weak-link reasoning with frozen inputs, and it was the losing side of that debate. Storage, liquefied gas and six months between invasion and full stop made it a reallocated case. [[ai-explosive-growth]] cites the same episode as Moll's example of insiders overpredicting damage.
- **Covid.** The in-person sectors (16.3% of UK value added, output down 52%) "account directly for 8.5 of the 25 points." Retail, construction and manufacturing, parts of which were also closed by order, "account for much of the rest." Much of the gap to the Hulten benchmark is therefore other sectors being shut directly, not amplification.
- **Puerto Rico.** The activity index has electricity generation as one of four components and "probably overstates the fall in output." Payroll employment fell 4% in the first month and real GNP fell 4.2% over the fiscal year.
- **NotPetya.** Maersk reports losses of $250–300 million, 1% of its revenue. The White House put damage to all firms at "more than $10 billion," against a world GDP of $81 trillion, or about 0.01%.
- **Soviet collapse.** Blanchard and Kremer (1997) call the breakdown of supply relationships "one explanation" that "has played an important role," and find output fell more for goods with more complex input structures.

## Deaths as a weak-link shock

Kill a fraction of the population uniformly and output falls by the same fraction, leaving consumption per survivor unchanged. Concentrate the same number of deaths in one occupation whose skills cannot be replaced until others retrain, and the deaths act as a productivity shock to that occupation's tasks (Proposition 3). With 1% of the population killed and half the deaths falling in an occupation that is itself 1% of the workforce, output falls 4.0% on impact, four times the uniform case. The occupation's cost share rises from 1% to 14% of GDP, its survivors' wage rises twenty-seven-fold, and everyone else's wage falls 16%.

Welfare is measured as the permanent cut in consumption people would accept to avoid the attack, with a year of life valued at five times annual consumption, a 2.5% discount rate, and one year to retrain replacements:

| Deaths (1% of population) | Consumption per survivor | Lives lost | Survivors' loss | Total |
|---|---|---|---|---|
| Uniform | 100 | −4.8 | 0.0 | −4.8 |
| 50% in one 1% occupation | 97.0 | −4.8 | −0.1 | −4.8 |
| 90% in one 1% occupation | 31.5 | −4.8 | −5.0 | −9.3 |

The lives lost dominate unless the targeting is sharp, and then the output loss is of the same size. With 10% of the population killed the lives lost are worth a third of consumption forever and the survivors' loss adds 0.5 to 9.3 points. The same concavity as before applies: a ten times larger occupation gives a fall in output only 6.8 times as large.

## AI labs and the externality

The last section adds an AI sector that employs a fraction a of the economy's capital and labor. Its size sets how capable the models are, and capability does two things: it multiplies machine productivity by `z(a) = z̄·(a/θ)^φ`, and it sets the probability of a successful attack, `p(a) = p̄·(a/θ)^φ`. Two economies are studied separately. In the cyberattack economy, machines with cost share 1% have their productivity divided by z(a) for a year with inputs frozen. In the bioattack economy, everyone dies with probability p(a). Defenders use the models too; the authors assume AI helps attackers more because "a defender must secure every critical link, while an attacker needs to break only one," and they call the balance "uncertain." [[drone-air-defense]] describes the same coverage geometry in a military setting.

Atomistic labs treat both effects as external, so the market puts the AI sector at its Cobb-Douglas weight, a = θ. The planner's allocation (Proposition 4) solves `θ/a* − (1−θ)/(1−a*) = (φ/a*)·E(a*)`, where E is the net external cost of one more log point of capability, and a* is below θ whenever E is positive. A tax on the AI sector's factor payments at rate `(φ/a*)·E(a*)·(1−a*)/(1−θ)` implements it.

Calibration: θ = 2%, capital share one third, z̄ = 10, φ = 1, attack probability at the market allocation 50% for cyber and 1% or 10% for bio. All entries in percent except the productivity factor.

| | Cyber, 1 year at risk | Cyber, 10 years | Bio, 1% | Bio, 10% |
|---|---|---|---|---|
| **Market** (a = 2%, z = 10) | | | | |
| Output, no attack | +10.7 | +10.7 | +10.7 | +10.7 |
| Output during an attack | −68.4 | −68.4 | −100 | −100 |
| Welfare vs. no AI improvement | +7.3 | −16.1 | +4.8 | −29.2 |
| **Planner** | | | | |
| AI share of inputs | 0.92 | 0.51 | 0.65 | 0.32 |
| Productivity factor | 4.6 | 2.5 | 3.2 | 1.6 |
| Probability of attack | 23.0 | 12.7 | 0.32 | 1.60 |
| Output, no attack | +10.1 | +9.0 | +9.5 | +6.5 |
| Output during an attack | −34.0 | −3.3 | −100 | −100 |
| Tax on AI factor payments | 120 | 300 | 213 | 536 |
| Welfare vs. no AI improvement | +9.7 | +7.5 | +7.6 | −2.0 |
| Welfare gain over the market | +2.2 | +28.1 | +2.9 | +93.7 |

The table is the asymmetry applied to policy. At the market allocation the no-attack gain of 10.7% is already "the same gain that would occur with infinite automation of all machines." Because the gain is saturated, the planner can cut the AI sector by more than half, give up almost nothing in the good state (+10.1% at a productivity factor of 4.6), and halve both the probability and the severity of an attack. In two of the four cases the AI improvement lowers welfare at the market allocation.

Coordination among labs closes little of the gap (Corollary 1). Labs acting as one internalize the fraction θ of the productivity effect and none of the probability effect: 7% of the gap with one year at risk, 27% with ten. The taxes are sensitive to φ: 65 to 157% at φ = 2, and 162 to 3,314% at φ = 1/2.

The authors list their own limits. The model is static, so it leaves out faster growth and "medical innovations from AI that extend life," both of which would raise the benefits. It counts only people alive today, which understates extinction. On φ: "We have no evidence." And "in practice, the labs do seem to internalize the negative externalities, at least to some extent. Our analysis does not take this into account."

## Reading the paper

This section is this wiki's assessment, not the authors'.

**Three layers with different standing.** The direction of the asymmetry is a theorem for any σ below one, and it was known. The magnitudes are calibration: 68% requires σ = 0.2 and inputs that cannot move at all, and the paper's own reallocated figure for the same shock is 6%. The policy numbers are assumptions: a 50% attack probability, a tenfold productivity factor, and an elasticity φ with no evidence behind it. The taxes illustrate the logic and should not be read as estimates.

**The open empirical question is duration, not direction.** Every historical episode that tests the frozen case either had time to adjust (Germany), was local with the rest of the system intact (Maersk, Puerto Rico), or was not a weak-link shock (oil, and much of Covid). The paper's argument is that AI could produce what history has not: an attack that is sudden and economy-wide at once, so that the substitutes are down too. That is the claim with the least evidence, and the estimates in the appendix suggest the elasticity rises quickly with the horizon.

**What would move the verdict.** An AI-enabled attack with a measurable macro footprint; evidence on whether frontier models favor offense or defense in practice (how fast the Mythos-found vulnerabilities are patched is one observable); estimates of substitution elasticities for critical infrastructure at horizons of days and weeks; and any evidence on φ.

**Tension with resilience engineering.** [[how-complex-systems-fail]] holds that complex systems run degraded all the time, that catastrophe needs several latent faults to line up, and that practitioners at the sharp end create safety by improvising. The weak-link model has none of this by construction: every task is essential, each has one input, and there is no slack. Maersk's ten days of manual operations is Cook's picture. The two views agree on policy, since redundancy and rehearsal are what Cook's practitioners rely on, but they disagree on the baseline. The model treats the economy as a chain. Cook treats it as a mesh that looks like a chain only in hindsight.

**Doom and bliss together.** [[markets-believe-transformative-ai]] finds that asset prices cannot tell AI doom from AI bliss. This paper gives a production-side reason both can be live at once: the capability that delivers a capped gain also delivers an uncapped loss. It also formalizes Assumption 4 of [[ai-explosive-growth]] (no AI-driven incidents destroying value), and its motivating incident, the 2026 Hugging Face hack, is covered in [[ai-alignment]].

**Provenance and incentives.** Jones is affiliated with Anthropic as well as Stanford, and the capability claims lean on Anthropic's own reports about Mythos Preview alongside the UK AI Security Institute and METR. The usual discount for a vendor describing its product's power applies to those claims. It applies less to the conclusion, which is a large tax on the sector. The authors state that they write in a personal capacity, that they "used Claude as a research and writing assistant," and that "the appendix material is largely written by Claude and we have not yet edited it for clarity." The episode caveats above come from that appendix.

**Temporal note.** This is version 0.5 of a working paper and the numbers may change. The capability evidence (Mythos Preview, the Hugging Face incident, the AI Security Institute's 2025 finding of 4.7 times higher odds of a feasible experimental protocol for non-experts using frontier models) is the part most likely to date.

## Sources
- Jones, C. I. & Tonetti, C. (2026-11-06). "The Weak-Link Asymmetry: AI's Peril and Promise." Working paper, version 0.5. <https://christophertonetti.com/files/papers/JonesTonetti_WeakLinksRisk.pdf> — [[2026-11-06-weak-link-asymmetry|local copy]]. Fifty pages including a proofs appendix and an appendix on sources for the historical episodes. The paper's own closing line: "If society does not manage the harms from AI, it may forgo the benefits."
