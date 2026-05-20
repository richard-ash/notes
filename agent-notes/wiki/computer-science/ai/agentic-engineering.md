---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-04-29-karpathy-vibe-coding-to-agentic-engineering.md
  - agent-notes/raw/engineering/computer/development/2026-04-02-simon-willison-ai-state-of-union.md
compiled_at: 2026-05-20
model: claude-opus-4-7
confidence: medium
---

# Agentic Engineering

The discipline that has emerged on top of [[vibe-coding-apprenticeship|vibe coding]] now that frontier coding agents reliably one-shot non-trivial code. **Simon Willison coined the term** to name the professional version of building with coding agents; **Andrej Karpathy formalized the framing**: vibe coding raises the *floor* (anyone can build software), while agentic engineering preserves the *ceiling* (professional quality bar) at much higher velocity. Both describe it as a coordinated practice for using stochastic, spiky agents to ship software you'd still defend in code review.

Two independent practitioners date the same threshold-crossing. Karpathy (Sequoia AI Ascent, April 2026): around December 2025 the chunks of code coming back from agentic harnesses crossed a quality threshold, and "I can't remember the last time I corrected it." Willison (Lenny's Podcast, April 2026): GPT-5.1 and Claude Opus 4.5 dropped in November 2025 and were "incrementally better than the previous models, but in a way that crossed a threshold" — coding agents went from "most of the time it mostly works, but you had to pay very close attention" to "almost all of the time it does what you told it to do." That convergent dating is what's pulled the discipline out of vibe-coding hobbyism into something that shows up on hiring scorecards.

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

Willison defends the term against people who use "vibe coding" to mean everything AI-mediated: "The moment vibe coding means everything involved that touches AI, it effectively ends up meaning programming, because we're all moving in the direction where our code is mediated through AI at some point." Reserving "vibe coding" for the not-looking-at-code case and "agentic engineering" for professional work preserves a useful distinction.

This is a direct sibling of [[vibe-coding-apprenticeship|the apprenticeship model]] for interns, but framed from the senior-engineer side: vibe coding is the entry point; agentic engineering is the durable craft.

## The dark factory pattern

Willison's name for the frontier of agentic engineering: software built where **nobody writes the code, and nobody reads it either**, while still meeting professional quality bars. The metaphor comes from factory automation — if a factory is automated enough that no humans are on the floor, you can turn the lights off. What does the analogous fully-dark workflow look like for software?

The "nobody writes code" half is already in practice across the industry. Willison reports producing ~95% of his code without typing it: telling agents "rename that variable, refactor that, add this line" is faster than keyboard input. The "nobody reads code" half is what's new and contested.

His detailed case study is **StrongDM**, a security-software company building identity and access management — exactly the kind of work conventional wisdom says you should never vibe code. From August 2025 onward, StrongDM stopped reading the code their agents produced and instead invested in *how to verify the software works without reading it*. The most interesting answer: a swarm of agent testers simulating end users in a simulated Slack channel, running 24/7, sending requests like "Hey, can someone give me access to Jira?" The cost was ~$10,000/day in tokens — but it produced a robotic QA team that never sleeps.

A second design choice: the surrounding software systems (Slack, Jira, Okta) were *also* simulated. Real third-party APIs have rate limits and can't take 10,000 simulated users at once. So StrongDM had their coding agents read the public API docs and client libraries, then build their own simulations — small Go binaries that sat there at zero ongoing cost, with vibe-coded fake UIs to inspect what was happening.

The general lesson Willison extracts: if you're not reading the code, you need creative new mechanisms to verify the system works. The interesting question isn't *which* coding agent built it — it's the surrounding test/verification regime that lets you trust unread code. This is the architectural problem the dark-factory frontier is trying to solve.

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

## Practitioner practices (Willison)

Where Karpathy frames agentic engineering theoretically, Willison's contribution is a set of concrete techniques he is publishing one chapter at a time on his blog. The unifying insight: **most of the things that make agents write better code also work for humans**. He frames this as "basically writing a book about software engineering and what works well and pretending it's about agents, but it's not."

### Code is cheap → invest the savings into quality

The single biggest mental shift: the thing that used to take the time (typing code) now takes way less time. This is not just a speedup — it changes what every other engineering activity is worth.

- **Prototyping is free.** Instead of designing one solution, build three different versions and compare. Willison reports that prototyping was his career-long superpower; now anyone can do it, and the practice still matters but the moat is gone.
- **Interruptibility flips.** The classic "give engineers uninterrupted 2-4 hour blocks" rule loses force. Willison: "I need two minutes every now and then to prompt my agent about what to do next, and then I can do the other stuff."
- **Don't just take the speedup — convert it into quality.** The mistake is producing the same software faster. The opportunity is producing better software (fewer bugs, more features, more extensible) because the cycle time on every quality investment dropped.
- **Over-testing is no longer expensive.** A library with 100+ tests for 100 lines of code used to be a maintenance disaster ("now you have to update 1,000 lines of tests when code changes"). With agents updating the tests, verbose test suites become a tolerable design choice — the cost they used to impose is now zero.

### Hoarding things you know how to do

A career strategy Willison says predates AI but compounds dramatically with it: build a personal backlog of small experiments — "things you've tried in the past that worked or didn't work" — so when a new problem arrives, you can spot that it's a combination of two techniques you already explored. The value isn't any single experiment; it's the combinatorial library.

How he hoards in practice:
- `simonw/tools` on GitHub — ~193 small client-side HTML/JavaScript tools, most one-file or one-pager. Each one captures *that this is possible*.
- `simonw/research` on GitHub — agent-driven research projects. He prompts Claude Code on his phone: "Download this thing, see how it works, write me a report, try it against this problem." Output is a markdown file in GitHub. Crucial distinction: these are **coding-agent research** (wrote code, ran it, plotted graphs) — not "deep research" reports of unverified web summaries, which he calls "LLM vomit."

How the hoard pays off: paste two GitHub URLs and a problem into Claude Code, tell it to read the source and combine the techniques. "Check `simonw/research` and look at the ones dealing with WebAssembly and Rust, then use that to solve this new task." Coding agents are very good at searching across repositories of small precedents — give them a hard drive and they will surface the relevant examples themselves. Length limits matter much less than they used to because agents do their own retrieval.

Default to public hoarding (GitHub backs up to three continents, plus the Arctic vault), but the same approach works with private GitHub repos or a Dropbox-synced folder. The mechanism, not the host, is what matters.

### Red/green TDD as a five-second prompt

The single most important rule Willison gives for agents: **they must run the code.** "If they haven't run the code, you're back to copying and pasting out of ChatGPT and crossing your fingers." The reliable way to force that is test-driven development.

Tests serve two purposes with agents that map onto their pre-AI rationale:
1. **Existence of any test means the agent ran the code** and caught syntax/runtime errors before claiming success.
2. **A growing test suite is what lets agents change code without breaking unrelated features** — the same logic that makes humans more productive in a tested codebase makes agents far more productive.

Willison's contribution is a five-second prompt: **"use red/green TDD."** Decades-old programmer jargon that means "write the failing test first, watch it fail, write the implementation, watch it pass." Agents know what it means. This compresses a paragraph of instructions into a phrase. The wider lesson: the existence of well-established programming jargon is a *prompting advantage* — short tokens with rich meaning move agents efficiently.

He notes a personal irony: he disliked TDD as a human practice (it slowed him down, he prefers to explore by writing code first). Agents have no opinion about test ordering, so he can impose discipline on them that he wouldn't impose on himself.

### Start projects from a thin template, not a long CLAUDE.md

Coding agents are "phenomenally good at sticking to existing patterns." A single test file is enough to teach an agent your indentation style, your file layout, your testing conventions — it will write the next 100 files in that style without instruction. Willison's preferred starting state: a template with one trivial test (`assert 1 + 1 == 2`), boilerplate laid out the way he likes, and very little else.

The contrast he draws is with people who maintain long `CLAUDE.md` files describing how they like to work. He prefers a thin skeleton because demonstration beats description: agents pick up style faster from one example file than from paragraphs of instruction. (This is consistent with Cherny's "delete your CLAUDE.md and start fresh" advice in [[claude-code]].) He keeps templates on GitHub — one for a Python library, one for a Datasette plugin, one for a CLI tool.

## The exhaustion paradox

A surprising finding from heavy practitioner usage: agents create more free time and *also* exhaust the engineer faster. Willison: "By 11 a.m. I am wiped out for the day." Running four parallel agents requires holding four mental models in your head simultaneously; even without reviewing every line, the supervisory cognition burns out faster than implementation cognition used to.

Compounding the load: agents work 24/7. Willison reports talking to engineers losing sleep because they wake at 4 a.m. to set off more agents, treating the loop "with an element of gambling and addiction." He hopes this is a novelty effect of agents only getting good in the past few months, but flags it as a real risk if management treats agent-mediated workflows as a license to demand 5× output.

The paradox sits underneath an interesting career claim: Willison's New Year's 2026 resolution was the opposite of every previous year's — instead of "focus, do less," he chose "take on more, be more ambitious." His framing: ambition is the bottleneck most people don't realize they have. Jensen Huang's recent take on tech-company layoffs is consistent — companies cutting headcount, in Huang's reading, are revealing they lacked the ambition to absorb the productivity gain. This is a self-serving observation from someone selling capacity to absorb productivity, but it's directionally aligned with what Willison sees in his own work.

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
- **Experienced engineers may benefit most, mid-career engineers least.** A ThoughtWorks roundtable Willison cites concludes that senior engineers have 25 years of mental models to amplify; juniors get the onboarding-friction reduction (Cloudflare and Shopify hired ~1,000 interns each in 2025, citing ramp-up acceleration); mid-career engineers have neither advantage and are most exposed.
- **New artifact classes are the bigger opportunity than faster old artifacts.** Software 3.0 enables programs that couldn't have existed (Menu Gen as a single Nanobanana call, LLM knowledge bases). The "what got faster" framing systematically undersells the paradigm.
- **Verifiable domains outside the labs' RL mix are tractable founder territory.** If you can construct the RL environment, you can fine-tune your way to a moat the labs aren't directly competing with.
- **Aesthetics and simplification will eventually enter the RL loop** — but until they do, those are the human-defended axes. Code review of agent output remains essential.
- **Infrastructure designed for agents first** is currently table stakes for agent-native products and will increasingly be a procurement criterion for infra companies generally.
- **The dark-factory frontier (no one writes code, no one reads it) is where the open research lives.** Once you remove human review, you need new mechanisms to trust the output — simulated end users, simulated dependencies, agentic adversaries — and those mechanisms become the moat. See StrongDM's example above.
- **Security is the binding constraint on personal-assistant agents.** People want an agent with access to their email and the ability to act on it more than they want almost anything else (the OpenClaw phenomenon: first line of code November 2025 to Super Bowl ad in ~3 months, despite known security disasters). But the [[lethal-trifecta]] makes that combination structurally unsafe with current architectures. Willison: "If you can build a safe OpenClaw, that's the biggest opportunity in AI right now. If I knew how, I'd be building it."

## Connections

- [[vibe-coding-apprenticeship]] — the floor-raising side of the same dichotomy, framed from the intern-development perspective
- [[agentic-engineering-architecture]] — Garry Tan's three-layer (fat skills / fat code / thin harness) heuristic for *how* to actually build robust agent systems; the architectural complement to Karpathy's discipline framing
- [[ai-coding-harnesses]] — anatomy of the tool-call loop that powers agentic-engineering tooling like Claude Code and Codex
- [[claude-code]] — Boris Cherny's design philosophy for Anthropic's coding agent; the "build for the next model" principle and thin-CLAUDE.md advice align with Willison's template-over-instructions practice
- [[claude-code-skills]] — the "copy-paste block of text" Karpathy describes as Software 3.0's installer is the same artifact as a Claude Code skill
- [[unattended-coding-agents]] — Stripe's Minions are an enterprise-scale instance of Willison's dark-factory pattern: no human writes the code, agents test against simulated dependencies (devboxes), and review happens at PR boundaries
- [[lethal-trifecta]] — Willison's security framing for why personal-assistant agents structurally cannot be built safely with current architectures; the constraint that bounds where agentic engineering can be deployed
- [[judgment-in-ai-assisted-development]] — Larson's hierarchy (time → attention → judgment → creativity); Karpathy's emphasis on aesthetics, spec design, and oversight is a concrete account of where judgment lives in the agentic-engineering loop, and Willison's "code is cheap" observation is the time-bottleneck-removal Larson describes
- [[agi-timelines]] — Karpathy's deeper "animals vs ghosts" framing and the longer argument that the decade-of-agents shape constrains what the discipline can become
- [[llm-knowledge-bases]] — the understanding-not-thinking tool Karpathy pairs with agentic engineering; the wiki feeds the human-judgment layer
- [[agent-harness]] — the agent-native infrastructure thesis at the SaaS-product layer, complementary to Karpathy's "rewrite everything for agents" framing
- [[the-bitter-lesson]] — Sutton's general-methods-win thesis is the deeper substrate; Software 3.0 is what "leveraging computation" looks like at the application layer once the LLM is the computer
- [[generative-ai-as-pattern-generation]] — Evans's domain-by-error-tolerance framing maps cleanly onto Karpathy's verifiability framing: pattern generation is exactly what the RL loop selects for

## Sources

- Karpathy, A. with Stephanie Zhan (Sequoia Capital, 2026). "Andrej Karpathy: From Vibe Coding to Agentic Engineering." AI Ascent 2026. <https://www.youtube.com/watch?v=96jN2OCOfLs> — [[2026-04-29-karpathy-vibe-coding-to-agentic-engineering|local copy]]
- Willison, S. with Lenny Rachitsky (Lenny's Podcast, 2026). "An AI state of the union: We've passed the inflection point & dark factories are coming." <https://www.youtube.com/watch?v=wc8FBhQtdsA> — [[2026-04-02-simon-willison-ai-state-of-union|local copy]]
