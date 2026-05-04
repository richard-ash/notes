---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-04-29-karpathy-vibe-coding-to-agentic-engineering.md
compiled_at: 2026-05-04
model: claude-opus-4-7
confidence: medium
---

# Agentic Engineering

Andrej Karpathy's name for the discipline that has emerged on top of [[vibe-coding-apprenticeship|vibe coding]] now that frontier coding agents reliably one-shot non-trivial code: vibe coding raises the *floor* (anyone can build software), while agentic engineering preserves the *ceiling* (professional quality bar) at much higher velocity. Karpathy describes it as "an engineering discipline" — a coordinated practice for using stochastic, spiky agents to ship software you'd still defend in code review.

The underlying claim from Karpathy's April 2026 Sequoia AI Ascent talk: somewhere around December 2025 the chunks of code coming back from agentic harnesses crossed a quality threshold, and "I can't remember the last time I corrected it." That stark transition is what's pulled the discipline out of vibe-coding hobbyism into something that shows up on hiring scorecards.

## Vibe coding vs. agentic engineering

Karpathy's clean formulation of the distinction:

| | Vibe coding | Agentic engineering |
|---|---|---|
| Goal | Raise the floor | Preserve the ceiling |
| Quality bar | "It works for me" | Same as before AI |
| Audience | Anyone | Professional engineers |
| Output | Demos, prototypes, side projects | Production software |
| Constraint | Velocity-only | Velocity *without* sacrificing quality |

The guarantee is symmetric to professional software pre-AI: you're still responsible for the security and correctness of what ships. Vibe coding does not absolve you of vulnerabilities. The question agentic engineering tries to answer is: *how do you coordinate spiky, stochastic agents to go faster without sacrificing the quality bar?*

Karpathy reports the speedup ceiling is much higher than the old "10x engineer" trope. People who are good at agentic engineering "peak a lot more than 10x." This sets up agentic-engineering capability as a hireable skill — and Karpathy notes that most companies have not refactored their hiring loop to test for it. His proposed test: "Give me a really big project. Build a Twitter clone for agents, make it secure. I'll have ten Codex 5 high agents try to break it. They should not be able to."

This is a direct sibling of [[vibe-coding-apprenticeship|the apprenticeship model]] for interns, but framed from the senior-engineer side: vibe coding is the entry point; agentic engineering is the durable craft.

## Software 3.0: prompting as the programming paradigm

Agentic engineering rests on Karpathy's broader **Software 3.0** thesis, which he uses to reframe what programming even is now:

- **Software 1.0** — humans write code in formal languages (C, Python, Lisp). Programming = expressing intent in syntax a deterministic interpreter understands.
- **Software 2.0** — humans curate datasets and architectures; the program is a set of learned weights. Programming = arranging data and objectives so SGD finds the right function.
- **Software 3.0** — humans write natural-language prompts; the LLM is a programmable computer. **The context window is the program.** Programming = composing the right context for the interpreter (the LLM) to do information processing in the digital domain.

Two concrete examples Karpathy uses to make this tangible:

**The Claude Code installer.** A "normal" install script is a fragile bash file that has to handle every OS, shell, and edge case. The Software 3.0 install is a *block of text* you copy-paste into your existing agent. The agent has its own intelligence, looks at your environment, and debugs the install in-loop. The block of text is not a script — it's a skill. (See [[claude-code-skills]] for the design language now coalescing around these copy-paste blocks.)

**Menu Gen.** Karpathy vibe-coded a Vercel app that takes a photo of a restaurant menu, OCRs the items, calls an image generator, and renders pictures next to each item. The Software 3.0 version, which "blew his mind": take the same photo, hand it to Gemini, ask it to use Nanobanana to overlay the dishes onto the menu. Nanobanana returns the same picture with the food rendered into the pixels. *The app shouldn't exist.* The neural net is doing the work end-to-end; the app was an artifact of Software 1.0 thinking.

The implication for builders: don't just look for things to do *faster* in the new paradigm — look for things that **couldn't exist before**, where structured intermediate code is no longer needed because the LLM is the substrate. [[llm-knowledge-bases|LLM-compiled wikis]] are Karpathy's other example: programs that build a knowledge base from arbitrary documents are not faster versions of something that already existed; they are new artifacts the paradigm makes possible.

The long-run extrapolation Karpathy floats: **completely neural computers.** Raw audio/video in, diffusion-rendered UI out, tailored to the moment. CPUs become the co-processor; the neural net is the host. He notes the 1950s–60s computing community wasn't sure whether computers would look like calculators or like neural nets; we went down the calculator path; he expects this to flip.

## Verifiability and jagged intelligence

Why is agentic engineering useful in *some* domains and useless in others? Karpathy's answer is the **verifiability framework**:

- Traditional computers easily automate what you can specify in code.
- LLMs easily automate what you can **verify**.

Frontier labs train models inside giant reinforcement-learning environments. RL only works where the reward is checkable, so training peaks capability in verifiable domains (math, code, chess) and stagnates outside them. The result is **jagged intelligence**: capability that towers on some axes and craters on others, with no smooth interpolation.

Karpathy's concrete example: a frontier model can simultaneously refactor a 100,000-line codebase, find zero-day vulnerabilities, and *also* tell you to walk to a 50-meter-away car wash instead of driving to wash your car. "This is insane." The two skills don't live on the same competence surface.

Two forces that determine where the spikes are:

1. **What's verifiable.** Math, code, chess, and any domain with a checker get RL-pumped. Writing, taste, common-sense physical reasoning don't (yet).
2. **What labs care about / put in the data mix.** The GPT-3.5 → GPT-4 chess jump was not generic capability progress — someone at OpenAI added a lot of chess data. Chess shipped because chess data shipped.

Both factors are partially observable from the outside, which makes Karpathy's practical advice: **figure out which circuits you're in.** If your application sits inside the RL distribution, "you fly." If it sits outside, "you're going to struggle and you have to actually look at fine-tuning and doing some of your own work, because it's not going to come out of the LLM out of the box."

Founder corollary: a verifiable domain that the labs *aren't* directly targeting is a tractable opportunity. You can't compete with OpenAI on math, but if you can construct an RL environment for some valuable domain that's not in the labs' mix, "that's fundamentally technology that just works" — fine-tuning frameworks plus diverse RL environments give you a lever to pull. Karpathy notably declined to name the specific domain he had in mind, calling it the "vape post on stage" he wouldn't make.

On the flip side: ultimately almost everything is automatable, even writing, via councils of LLM judges. The question is not *whether* but *how easy*.

## Aesthetics and taste as the human bottleneck

Today's agents are "intern entities." Remarkable interns: they have perfect API recall (Karpathy admits he no longer remembers `keep_dim` vs `keepdim` or `dim` vs `axis` between PyTorch / NumPy / Pandas), but they will also do absurd things — like Karpathy's Menu Gen agent trying to cross-correlate Stripe and Google funds via email-address matching when there was no persistent user ID, because no human would propose that as the right join key.

So the human role in agentic engineering is concentrated upstream:

- **Spec design.** "Work with your agent to design a spec that is very detailed — basically the docs — and then get the agents to write them." Karpathy is mildly down on plan mode as an isolated feature; the more general move is collaboratively designing the docs and then having agents implement against them.
- **Top-level categories and oversight.** Decide the unique-user-ID is the join key; let the agents handle which framework call expresses it.
- **Aesthetics, judgment, taste.** "When you actually look at the code, sometimes I get a little bit of a heart attack." Bloaty, copy-paste-laden, brittle abstractions. It works, but it's "really gross."

The micro-GPT anecdote is the cleanest illustration of where models hit a wall: Karpathy spent significant effort prompting an LLM to *simplify* his LLM-training code. The models couldn't do it. "You feel like you're outside of the RL circuits — it's like pulling teeth." Simplicity isn't part of the reward; the labs haven't trained for it.

Will the ceiling on taste keep rising? Karpathy's bet is yes — there's nothing fundamental preventing it, the labs just haven't done it yet. But until aesthetics enters the RL loop, taste is a uniquely-human binding constraint. This sits underneath [[judgment-in-ai-assisted-development|Larson's argument]] that judgment is the binding constraint in AI-assisted development: time and attention are increasingly cheap, and the gap is now in the human-judgment layer above the agent.

## Animals vs ghosts (briefly)

Karpathy's "animals vs ghosts" framing — covered in depth in [[agi-timelines]] — gets a softer reading here. Asked whether the framing changes how to build, deploy, or trust agents, he is more cautious: "I don't know if it has real power. I think it's a little bit of philosophizing." The practical takeaway is mindset-level rather than methodological: these are statistical simulation circuits with RL bolted on, not animal cognition; yelling at them doesn't help; expect them to be jagged in ways no animal would be. "It's more just being suspicious of it and figuring out over time."

## Agent-native infrastructure

If LLMs are the new computer, almost every layer of existing infrastructure is misaligned with them. Karpathy's pet peeve: framework and library docs are still written for humans. "Why are people still telling me what to do? I don't want to do anything. What is the thing I should copy-paste to my agent?"

The agent-native re-architecture he sketches:

- **Docs become copy-paste blocks** for agents, not URLs and instructions for humans.
- **Sensors and actuators over the world** — decompose workloads into things the agent can read and things it can act on. The visual analogy comes up explicitly: agents need legible inputs and clean output channels, not GUIs.
- **Agent-legible data structures** — replace human-friendly markup and elaborate UIs with formats LLMs parse cleanly.
- **End-to-end deployment from a prompt.** Karpathy's litmus test for agent-native infra: "I would hope I could give a prompt to an LLM, build Menu Gen, and not have to touch anything — and it's deployed on the internet." Today's bottleneck on Menu Gen wasn't the code; it was the DNS, settings, and Vercel configuration.
- **Agent representation for people and organizations.** "I'll have my agent talk to your agent to figure out some of the details of our meetings."

This is the same thesis [[agent-harness|Bret Taylor]] makes from the SaaS-incumbent side: the web app + REST API is no longer enough; companies need to expose an **agent harness** — skills, docs, rules, context — that lets agents extract real value. Karpathy's framing zooms out from one product to the whole infrastructure stack.

## You can outsource your thinking but not your understanding

Closing the talk on education, Karpathy returns to the human bottleneck: a tweet that "blew his mind" — *you can outsource your thinking but you can't outsource your understanding.*

The argument: even with agents doing the work, *something* has to direct what's worth building, why, and how to evaluate the result. That direction is constrained by *understanding*, which lives only in human heads. "You can't be a good director if you still — because LLMs certainly don't excel at understanding — you still are uniquely in charge of that."

This is why he is bullish on tools that enhance understanding rather than replace thinking — [[llm-knowledge-bases|LLM-maintained personal wikis]] are his primary example, treating each ingested article as "a set of prompts for me to do synthetic data generation over fixed data." Every new projection onto information surfaces insight. The wiki is a thinking tool, not an output tool.

The connection back to agentic engineering: a senior engineer's leverage in this paradigm comes not from typing speed but from the depth of their model of the system. Outsourcing the typing only works if you keep building the model.

## Implications

- **Agentic engineering is a hireable skill** with its own selection problem. Puzzle-style interviews are the wrong test; the right test is "build a non-trivial system end-to-end with agents and defend it under adversarial agents trying to break it."
- **Hiring loops haven't caught up.** Karpathy thinks most companies are still selecting for vibe-coding-era or pre-AI-era capability and are leaving the >10x ceiling on the table.
- **New artifact classes are the bigger opportunity than faster old artifacts.** Software 3.0 enables programs that couldn't have existed (Menu Gen as a single Nanobanana call, LLM knowledge bases). The "what got faster" framing systematically undersells the paradigm.
- **Verifiable domains outside the labs' RL mix are tractable founder territory.** If you can construct the RL environment, you can fine-tune your way to a moat the labs aren't directly competing with.
- **Aesthetics and simplification will eventually enter the RL loop** — but until they do, those are the human-defended axes. Code review of agent output remains essential.
- **Infrastructure designed for agents first** is currently table stakes for agent-native products and will increasingly be a procurement criterion for infra companies generally.

## Connections

- [[vibe-coding-apprenticeship]] — the floor-raising side of the same dichotomy, framed from the intern-development perspective
- [[agentic-engineering-architecture]] — Garry Tan's three-layer (fat skills / fat code / thin harness) heuristic for *how* to actually build robust agent systems; the architectural complement to Karpathy's discipline framing
- [[ai-coding-harnesses]] — anatomy of the tool-call loop that powers agentic-engineering tooling like Claude Code and Codex
- [[claude-code-skills]] — the "copy-paste block of text" Karpathy describes as Software 3.0's installer is the same artifact as a Claude Code skill
- [[judgment-in-ai-assisted-development]] — Larson's hierarchy (time → attention → judgment → creativity); Karpathy's emphasis on aesthetics, spec design, and oversight is a concrete account of where judgment lives in the agentic-engineering loop
- [[agi-timelines]] — Karpathy's deeper "animals vs ghosts" framing and the longer argument that the decade-of-agents shape constrains what the discipline can become
- [[llm-knowledge-bases]] — the understanding-not-thinking tool Karpathy pairs with agentic engineering; the wiki feeds the human-judgment layer
- [[agent-harness]] — the agent-native infrastructure thesis at the SaaS-product layer, complementary to Karpathy's "rewrite everything for agents" framing
- [[the-bitter-lesson]] — Sutton's general-methods-win thesis is the deeper substrate; Software 3.0 is what "leveraging computation" looks like at the application layer once the LLM is the computer
- [[generative-ai-as-pattern-generation]] — Evans's domain-by-error-tolerance framing maps cleanly onto Karpathy's verifiability framing: pattern generation is exactly what the RL loop selects for

## Sources

- Karpathy, A. with Stephanie Zhan (Sequoia Capital, 2026). "Andrej Karpathy: From Vibe Coding to Agentic Engineering." AI Ascent 2026. <https://www.youtube.com/watch?v=96jN2OCOfLs> — [[2026-04-29-karpathy-vibe-coding-to-agentic-engineering|local copy]]
