---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2025-09-29-rodney-brooks-ai-robotics-hype.md
compiled_at: 2026-04-22
model: claude-opus-4-6
confidence: medium
---

# AI and robotics hype cycles

Why do AI and robotics technologies consistently take decades longer to deploy than initial demos suggest? Rodney Brooks — MIT robotics professor turned three-time founder (iRobot, Rethink Robotics, Robust.AI) — argues that the gap between flashy demos and messy reality is structural, not incidental. His career spanning SLAM research in 1985 through warehouse robotics in 2025 gives him an unusually long baseline for calibrating hype.

## The long tail of the real world

Brooks's central claim: "There's a tendency to go for the flashy demo. But the flashy demo doesn't deal with the real environment. It's going to have to operate in — the messy reality."

The autonomous vehicle timeline illustrates this pattern precisely. Brooks attended his first talk on autonomous vehicles in 1979. By 1990, Ernst Dickmanns had a truck driving the Autobahn at 100 km/h and navigating Paris autonomously. After the 2007–2008 DARPA Grand Challenge, the consensus was imminent ubiquity. Almost 20 years later, autonomous driving is available only in small geographic pockets. The "long tail" of edge cases in natural environments — the unusual intersection, the construction zone, the pedestrian behaving unpredictably — is what consumes decades of work after the demo looks solved.

This pattern connects directly to [[the-bitter-lesson]]: scaled computation eventually wins, but Brooks would add that the timescale for "eventually" in physical-world domains is far longer than in purely digital ones, because computation alone cannot close the gap. See also [[agi-timelines]] for Karpathy's more moderate "decade not year" framing — Brooks's timescale is far longer.

## The humanoid robot trap

Brooks argues that a robot's physical form "makes a promise about what it can do." The Roomba's disc shape promised only floor cleaning — achievable. A humanoid form promises everything a human can do — unachievable with current technology.

This creates a funding distortion: VCs are attracted to the humanoid promise because it sells an amazing vision. Brooks reports being asked "Why aren't you doing something sexy?" when pitching warehouse automation carts — a $4 trillion market that will persist for decades, but doesn't photograph well. Malik frames the dynamic precisely: "It's much easier to fund the promise than a real business, because real businesses have limitations on how fast they can grow."

The specific technical gap Brooks highlights is manipulation. Robot hands look dexterous but cannot reproduce what human hands do. Five fingers are an evolutionary accident from the first tetrapods — future dexterous robots might look more like sea anemones with tentacles and cilia than like human hands.

## Human-robot collaboration as design philosophy

Across three companies, Brooks has maintained a consistent design principle: the human stays in control. The Roomba had a handle. Rethink Robotics let workers teach robots by demonstration. Robust.AI's Carta warehouse cart transfers control to any human who grabs the handlebar, amplifying their movements.

This philosophy extends to "simple intelligence" — the cart distinguishes between a person blocking an aisle (wait politely, try to go around) and a pallet blocking an aisle (it won't move on its own, reroute and report). Brooks frames this as "what we can do today and make reliable," explicitly rejecting the attempt to build general intelligence into deployed systems.

## The wrong-substrate argument

Brooks's most radical claim goes beyond timeline pessimism to questioning whether computation is the right substrate for intelligence at all. His analogy: Newton spent half his life on alchemy because he assumed transmutation was chemical. It's actually nuclear — a domain Newton had no access to. Similarly, the four fields born between 1945–1965 (neuroscience, AI, artificial life, abiogenesis) all adopted computation as their primary metaphor. But abiogenesis remained chemical. Brooks asks: are the other three wrong too?

"You can write as big a program as you want, it's not going to get stuff into orbit." Rockets need thermodynamics, not software. If cognition needs something other than computation — some substrate we haven't yet identified — then AGI could be 300 years away.

This is a fundamentally different critique from the [[agi-timelines]] "decade not year" position. Karpathy thinks the direction is right but the timeline is underestimated. Brooks thinks the direction itself might be wrong.

## The orca limit

Brooks uses orcas to challenge the assumption of infinite human cognitive potential. Orcas are genuinely intelligent — they solve novel problems, cooperate in hunting, have cultural transmission. But no one expects them to build a foundry. There is some ceiling on orca cognition that they cannot breach. Brooks asks: why do we assume humans have no such ceiling? "Just like the orcas, we may have limits and we don't like that."

## Hype recurrence in AI

Brooks has watched neural network approaches become ascendant and then get "crushed" four or five times. The current neural dominance is the largest public cycle but follows the same pattern. He points to agentic AI as the latest example: "Now suddenly everyone's got agent-based AI. They didn't have it six months ago." The first paper on agent-based AI was Oliver Selfridge in 1959. Each return of an idea improves on the last iteration, but the recurrence pattern should temper claims of finality.

## Infrastructure overbuild as hidden upside

Despite his skepticism about current hype, Brooks sees a structural upside borrowed from telecom history. Data centers are being massively overbuilt for generative AI training. When the training boom crashes, cheap compute infrastructure will be sitting idle — just as overbuilt fiber networks enabled Google to build search cheaply after the dot-com bust. "If some kid can figure out how to [use them], they're going to be working right now on it in obscurity and poverty and then boom."

## Adjacent predictions

- **3D printing as manufacturing disruption**: Brooks believes 3D printing will eventually break China's supply-chain advantage by reducing manufacturing to raw-materials logistics. This would follow the leapfrog pattern of developing countries adopting mobile payments before credit cards.
- **Nigeria as innovation center**: Brooks predicts Nigeria will be "the center of the technological universe by the end of this century" — population scale creates problems, and problems drive innovation (the same dynamic that drove China's rise).
- **Quantum computing near-term**: Useful quantum computers for the next decade will simulate physical systems, not outperform classical computation. General-purpose quantum computing remains distant.

## Sources

- Malik, Om (2025). "iRobot Founder: Don't Believe The (AI & Robotics) Hype!" <https://crazystupidtech.com/2025/09/29/irobot-founder-dont-believe-the-ai-robotics-hype/> — [[2025-09-29-rodney-brooks-ai-robotics-hype|local copy]]