---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-09-23-dhh-rails-world-2026-keynote.md
compiled_at: 2026-09-24
model: claude-fable-5-1
confidence: medium
---

# The End of Hand-Written Code

David Heinemeier Hansson's (DHH — creator of Rails, co-owner of 37signals) Rails World 2026 opening keynote (Austin, 23 September 2026) is the most forceful statement to date of a thesis that has circled the coding-agent literature for a year: **writing code by hand is over as an economic activity.** 37signals has gone "pencils down." DHH describes himself as having retired from professional programming around March 2026. And he predicts that by the end of 2026, hand-writing code will be economically unproductive for "virtually all domains, virtually all programmers, virtually all companies."

The talk is a manifesto rather than an argument: its evidence is autobiographical, its tone is self-described "AI euphoria," and its closing move is game-theoretic optimism. But it is a useful marker of where the most aggressive practitioner position sits in September 2026, it comes from someone whose prior contrarian calls (see [[local-ci-on-developer-machines]]) later became mainstream Rails features, and it contains several concrete, checkable commitments — HEY's native rewrite, the Rust back-end numbers, the CLI-over-chatbot prescription — that can be evaluated as they ship.

## The photography analogy

DHH frames the moment through his own family. His great-great-grandfather Laurits Tuxen spent three years on an 1886 portrait of the Danish royal family, in a tradition (Reynolds's Waldegrave ladies, 1781; Goya's Spanish royals, 1801) that had been perfecting the same craft for centuries at marginal rates of progress. The camera arrived around 1840, but the inflection was the 1900 Kodak Brownie — mass-produced photography at roughly a dollar a picture. Tuxen and his contemporaries concluded that "depicting reality as perfectly as possible was no longer really an economically viable skill" and pivoted: Picasso to Cubism, the Skagen painters to impressionism. Tuxen himself sat for a photograph in 1921.

Then, DHH stresses, technology "moves in fits, starts and stops." The Leica 1 of 1925 was not very different from the camera that took his handful of 1980s childhood photos; almost eighty years passed with little change. The camera phone made photography frictionless, and volume went parabolic — some two trillion photos a year by 2026.

The mapping he draws: **24 November 2025, the release of Opus 4.5, is the Brownie** — the first time the technology was accessible in a harness ordinary people could afford. What the analogy asserts is that the *craft* is displaced, not augmented, and that practitioners survive by finding a new domain; DHH's version of the new domain is "professional maker of things." What the analogy quietly elides is how many portrait painters actually made that pivot, and the talk never says.

## DHH's timeline of the agent era

- **24 Nov 2025 — Opus 4.5.** "Everything before, and everything after." The model where telling an agent to do something produced output he wanted to merge. This is the same threshold Willison and Karpathy independently dated in [[agentic-engineering]].
- **Shortly after — open-weight parity.** DHH ran Kimi K2.5 in fast mode at ~200 tokens/second and "absolutely loved it."
- **Feb–May 2026 — the trough of disillusionment.** New models (he names Opus 4.6) felt like steps backward; an OpenAI release that barely moved benchmarks triggered a valuation dip and "it's over" talk.
- **June 2026 — Fable 5 and Mythos.** The model where he could hand over *problems and ideas* with no direction on implementation. Mollick's [[patron-not-wizard]] describes the same relational shift on the same model.
- **Sept 2026 — GPT-6 Astra**, ending fears of an Anthropic monopoly on frontier intelligence, and a week later **DeepSeek-4-1 Flash**, ending the assumption that frontier intelligence would stay American.

His point is that the trough lasted four months, not photography's eighty years. Capability jumps are the operative variable; methodology, architecture and language choice are downstream and, he repeatedly admits, unsettled. "This entire thing got kicked off November 24th last year. It hasn't even been a damn year."

## From 10x to 1,000x

The 10x-programmer debate traces to a 1968 ACM study (commonly identified as Sackman, Erikson and Grant's *Communications of the ACM* paper) that found a 5x–30x spread between the worst and best programmers, roughly 10x on average. DHH says the industry spent 45 years arguing whether that was real and has now leapt past it: a 100x gap between the worst programmer without agents and the best with them is "not a very controversial statement," and 1,000x "sounds about right." Karpathy's "peak a lot more than 10x" in [[agentic-engineering]] is the milder cousin.

His own numbers, all self-reported in lines of code, a unit he concedes is "weird, fuzzy, malleable":

| Period | Output |
|---|---|
| Previous 21 years | ~30,000 lines of production Ruby per year; over half his work was Ruby |
| Past 20 months | half as much code as the previous 21 years combined |
| 2026 | Ruby is ~3% of his output |
| August 2026 | ~150,000 lines in one month, ~60x his long-term average |
| Hand-written code | none for ~5 months, since roughly March 2026 |

The lines-of-code caveat does real work: most of the August volume is Rust he never reads, and he explicitly lets the agent "spit out more than was necessary, in a way I would never tolerate from my Ruby code." So the 60x partly measures relaxed editorial pressure, not delivered capability. The NBER figures in [[decide-execute-deliver-sandwich]] (8x more code, 30% more releases) are the outside view of the same measurement problem.

He replays his 2005 Rails demo — "look at all the things I'm not doing" — and calls this "the Rails moment" again. The exuberance then and now is about elided work; the amount elided is just vastly larger.

## Pencils down at 37signals

A couple of weeks before the talk, 37signals decided that writing code by hand is no longer the normal course of business. Hand-written code is now an **exceptional state**: "like seeing a bug in Sentry. Something here went wrong. Why was the agent not able to produce what we wanted?" You might patch by hand once, "but then we fix the machine. We fix the factory."

This is the same forcing-function logic as OpenAI's zero-hand-written-code experiment in [[harness-engineering]] (every failure becomes a "what capability is missing?" question rather than a write-it-yourself escape hatch) and the direction of Larson's [[software-factory-pattern]]. DHH's contribution is presenting it as company-wide policy rather than an experiment, and as a *recognition* of what already happened: a show of hands in the Rails World room for "still writing material amounts of code by hand weekly" produced about five people.

### The Basecamp 5 counter-example

In spring 2026, 37signals tried this on Basecamp 5's final features by having designers vibe-code them. Individually, the PRs "seemed reasonable." Twenty or thirty of them together "left the architecture looking a little like a Swiss cheese." The team concluded the technology wasn't ready and reverted to programmers reviewing everything. DHH now calls that the wrong conclusion, for two reasons: waiting "five minutes" for Fable would probably have made it work, and in any case "there is only one serious question in this moment of software development: how do you get the most out of this intelligence explosion? Every other question is below that in the stack of values."

Two things are worth noting. First, the Swiss-cheese episode is exactly the mechanism Herrengt describes in [[understanding-as-the-bottleneck]] — locally reasonable changes degrading global structure faster than anyone drains the damage — observed inside 37signals. Second, the resolution is a capability bet, not a process fix: it holds only if the next model tier produces architecturally coherent output across dozens of independent PRs, which is precisely what the next project will test. Basecamp 5 shipped agent-accelerated but with substantial hand-written code; DHH calls that hybrid "the old way of working that was just retired 5 minutes ago."

## HEY Next: native front end, Rust back end

**Front end.** The new version of HEY (working title "HEY Next") will stop being a web app. DHH's argument is that HEY "never really wanted to be a web app"; it was one because a small team could only be productive on the web. React Native and Hotwire Native existed to let small teams approximate native while accepting a fidelity hit. With native development cost "gone to damn near zero," he distinguishes **web apps of necessity** (team size, resources, programmer preference), which will go native, from **web apps of choice**, where install-free ephemeral use is the product — Basecamp's guests who just need a file. Six native apps were kicked off about a week before the keynote; the first Windows prompt produced something "not quite shippable," and a redirected version landed 20 minutes later. He cites Shopify's Shop app, rewritten native by roughly six people to replace a React Native codebase, as evidence he is not alone.

**Back end.** Rust. DHH calls it "the ugliest programming language that has been invented in probably the last 40 years" and "like pouring acid in my eyes" — but "agents like Rust," and he loves the outcomes if he never has to look at it. With no HTML to render, HEY's back end becomes "the mail server that it really is at its core." The claimed result:

| Metric | Claim |
|---|---|
| CPU | 99% less |
| Memory | 95% less |
| Hosts | 10, only for redundancy |
| Peak traffic | servable on a single Raspberry Pi (back of envelope) |

These are projections for a rewrite that started a week earlier, not measurements of a shipped system.

**The black-box stance.** "I don't know any Rust at all. I consider that a feature." He evaluates "the Rust box" from outside, "as any business owner in history who's ever commissioned a group of programmers" — "who now holds that responsibility has changed, but not the phenomenon." He warns people who know too much about computers against being over-prescriptive; a beginner's mindset yields higher-level prompts.

This is the sharpest point of disagreement between the talk and the rest of this vault. Andreessen ([[ai-and-the-future-of-work]]) holds that "if you can't read the code the bots produce, you can't debug it." Herrengt makes understanding the binding constraint. Wilton ([[correctness-oracles]]) and Willison's StrongDM dark-factory case ([[agentic-engineering]]) both argue you may stop reading code only once you have built the verification regime that replaces reading. DHH describes no such regime beyond outcomes and the Rails agent evals; his implicit answer is that the commissioning-owner relationship has always worked without one, and that whoever holds the understanding, it needn't be him.

## Working asynchronously

DHH says the best way to work with agents is asynchronously — hand off a task "like you would a coworker," go away, review when something is ready — not in a chat interface waiting for tokens. 37signals is trying this with an agent ("Chef Marie") inside Basecamp. He is candid that nobody knows the methodology yet: the ability to assign *outcomes and problems* rather than tasks "is only a couple of months old." This is the same delegated slow loop as [[unattended-coding-agents]] and, at the goal level, [[software-factory-pattern]].

## Where Rails fits

For HEY the answer is native plus Rust. But the web "never asks anyone to install anything," a million businesses are built on that, and Rails stays in play there. DHH's pitch: 25 years of convention over configuration "leads directly to things like token efficiency," and the one-person-framework focus matches an era where single developers go much further. Valim, in [[programming-languages-for-agents]], argues the opposite direction over a longer horizon — that optimizing syntax for token efficiency is "building around today's limitations" — so DHH's claim is best read as a near-term positioning of Rails, not a durable law.

The Rails Foundation has Evil Martians running **agent evals** that implement feature cards against reference applications. The first version saturated quickly (agents reaching ~95% completion) and had to be made harder. DHH expects "a lot of elevation of the things we ask the agents to do."

## English as the programming language

"There is actually a programming language I like better than Ruby. It's called English." More expressive, "a little more vague," "a little more or less deterministic," and "an absolute joy." He notes he started programming because he wanted outcomes, fell in love with code, and now retires from it — with joy rather than regret. Karpathy's Software 3.0 in [[agentic-engineering]] is the formal version of the same claim: the prompt is the program.

He is explicit that the retirement is a *career* claim, not just a personal one: hand-writing code "is no longer an economically productive enterprise for the vast majority of programmers working at the vast majority of companies. That's today." On the other side he sees "a new career … as a professional maker of things," and rates the moment bigger than the internet.

## Rethinking architecture: abstractions as choke points

DHH's one concrete architectural claim: abstractions were built partly to avoid repetition, but "if you suddenly have hundreds or thousands or tens of thousands of conscious processes trying to mutate an application, you kind of don't want these choke points that abstractions represent." The price of repetition "has gone to near zero," and so has the price of keeping copies in sync. He calls this a fundamental revaluation of computer science with no blueprint yet, and lists the open questions — methodology, cycle length, who specifies what.

Metz's [[wrong-abstraction]] already argued for duplication over the wrong abstraction on human grounds; DHH's version drops the "wrong" — the cost side of DRY itself has changed. Note the unresolved tension with his own Basecamp 5 story: parallel agents mutating a codebase also need *some* structure to avoid the Swiss-cheese outcome, and Wilton's architecture-boundary assertions in [[correctness-oracles]] pull in the opposite direction from abstraction-as-choke-point. The talk doesn't reconcile them.

## Bring your own agent: every app needs a CLI

The talk's one prescriptive demand. DHH rejects the embedded chatbot ("I don't want to use your concierge … save your tokens, bro"). He has his own agent that connects Basecamp to HEY to everything else via CLIs, and wants to interact with every application that way: "if your app doesn't have a CLI, I want to see it by next Friday." His example: HEY uses Elasticsearch, which is "serviceable" but "very often does not find what I'm looking for." Through the HEY CLI, an agent found a five-year-old email about sneakers and a podcast when he remembered neither sender, company, nor year — concept search rather than keyword search. "How did it do it? I still don't fully know."

This is the minimalist form of Taylor's argument in [[agent-harness]] that businesses need an agent-facing layer alongside the web app and the API, and it aligns with Taylor's preference for plain tools over MCP-style protocols. It is also [[outcome-first-design]] arriving from the user side: the search UI was a tool, the found email is the outcome, and the user brings the model that bridges them.

## Omarchy and one-shot apps

"We can fix everything" extended to the whole computer. Omarchy, DHH's Linux distribution, has raised about $20M. Install time went from 3m33s (demoed at Rails World 2025) to 35s (an AMD engineer on a Strix Halo laptop) to 9s in the lab — "there's computers that don't even boot in 9 seconds." His stock justification, borrowed from Mitchell Hashimoto: "The pursuit of excellence does not need justification."

One-shot apps he has built without reading the code: a Qt/C++ calculator theme-matched to Omarchy (from a ChatGPT-generated mockup screenshot; seven minutes to app, fifteen to public repo, then a new ISO), a writing app replacing iA Writer, a video trimmer, and **Hype**, Markdown-based presentation software written during keynote prep, with a half-megabyte binary.

## The performance payoff

Twenty years of hardware progress were spent on programmer productivity — "the right choice" — which made software "slow, bulky, fat and lazy" (Spotify's 1.2 GB music player) because a programmer hour was too expensive to spend on payload optimization. Now "every optimization is within reach … every model can run overnight and deliver 10, 30x improvements." The implication is that the developer-time-over-machine-time tradeoff behind high-level languages and [[choose-boring-technology]] inverts once developer time is tokens — which is why DHH, of all people, is happy with a Rust back end.

## Concerns, predictions, and P(bloom)

DHH concedes security: agents "maybe know their expiration date" and "sometimes they're gonna try to do bad things"; a recent Rails CVE in a C image library motivated a quarantine effort (HotCell). "We have the tools. Get ready." (Compare [[lethal-trifecta]] for the structural version of the problem.)

Otherwise his argument is that prediction fails. Economists can't call the stock market six months out. ATMs in the 1950s were supposed to eliminate 30,000 bank tellers within 18 months; instead cheaper branches meant more branches and roughly 40,000 tellers by 2010 (his Jevons example). Truman dismissed Oppenheimer's dread and the Cold War stayed cold; nuclear power was then "pissed away" for forty years. Hence P(bloom) over P(doom), and pure game theory: if it goes well, sadness was wasted; if it doesn't, "you should have spent your last day being a little more cheery." "Agent Luther is going to disintermediate the cleric class" and let everyone program — competition Rails developers should welcome. The next generation has "no 500 layers of things to unlearn."

Two notes on the ATM parable. Oks's [[task-automation-vs-paradigm-replacement]] shows it has a second act DHH's version omits: teller employment fell from 332,000 (2010) to 164,000 (2022) once mobile banking replaced the branch paradigm. And DHH's own thesis — a paradigm (hand-coding) replaced, not a task automated — is the kind of change Oks says *does* displace. So the talk's optimism about programmers rests on the painters' pivot, not on the teller precedent. Narayanan ([[decide-execute-deliver-sandwich]]) reaches optimism about employment by a different route — execute is compressed but decide and deliver are not — and DHH's "commissioning business owner" is, in that model, the human who still holds decide and deliver.

## Sources

- DHH / Ruby on Rails (2026). "Rails World 2026 Opening Keynote - DHH." <https://www.youtube.com/watch?v=vDjW_dRyKXY> — [[2026-09-23-dhh-rails-world-2026-keynote|local copy]]
