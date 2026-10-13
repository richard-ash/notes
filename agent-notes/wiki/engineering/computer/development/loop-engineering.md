---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-10-12-huntley-nobody-types-code-by-hand.md
compiled_at: 2026-10-13
model: claude-fable-5-1
confidence: medium
---

# Loop Engineering

**Loop engineering** is Geoffrey Huntley's name for building software by running coding agents in autonomous loops — re-prompting an agent against a filesystem until a goal converges — rather than by typing code or supervising an agent turn by turn. Huntley (ex-Canva tech lead, early Gitpod employee, now at the verification company Antithesis) originated the "Ralph" loop pattern that Anthropic's Boris Cherny later discussed in the context of Claude Code and that OpenAI's harness-engineering team cites as the "Ralph Wiggum loop" ([[harness-engineering]]). This article is compiled from his October 2026 write-up of a four-part interview with Josh Wulf (ten years at Red Hat, three as a technical recruiter in Brisbane, host of the *Agentic Engineering* show), which is the fullest statement of the school's positions to date.

The through-line Huntley gives is that **the models stopped being the constraint a long time ago; what's left is vision, verification and agency.** Three practical claims follow, and each cuts against something else in this vault:

1. Humans sit at two points, the vision and the verification. Code review as a human activity ends; whole-system testing replaces it.
2. Instruction files, skill packs and MCPs are "astrology for software engineers". Anything that must hold should be a deterministic check in the loop, not a paragraph the model may or may not honour.
3. Everything that used to be hard — rewrites, Bazel, Nix, unikernels — needs re-testing now that writing code is cheap.

It is a single, highly opinionated source from someone who is also selling verification (he says so), hence `medium` confidence. Several numbers in it are hearsay he relays from friends at labs.

## Where the school came from

Huntley's own timeline, which matters because it disagrees with the dating used elsewhere in this vault:

| When | Event |
|---|---|
| Dec 2024 | Tech lead at Canva; starts running loops by hand in Cursor and concludes IDEs don't exist in the future |
| Feb 2025 | Discovers "filesystem-as-state", the first loop; publishes the Z80 post (clean-room an application into specifications, then rebuild from the specs) |
| mid-2025 | *Dear Student* post; ThePrimeagen covers it; Huntley publishes Ralph before someone else does |
| Nov 2025 | Boris Cherny talking about Ralph and loops in Claude Code |
| Jan 2026 | "The real inflection point": business leaders understand what is happening |
| Oct 2026 | JetBrains reports its first-ever net loss; a wave of Photoshop clones appears, which Huntley reads as the Z80 idea implemented at scale |

The dispute with DHH is explicit. DHH's Rails World keynote ([[end-of-hand-written-code]]) dates the capability threshold to 24 November 2025 and Opus 4.5; Willison and Karpathy independently date it to the same window ([[agentic-engineering]]). Wulf's reply, which Huntley endorses: "that's just when you figured it out. The models were capable long before that. It was a mindset constriction, not a model constriction." Huntley's own line is that "the models from a year ago were already good enough to displace software developers." Whichever dating is right, the disagreement is about adoption rather than capability, and it has a consequence Huntley draws out: if the limit is mindset, the head start compounds. "If you've been applying yourself and staying curious, you have a two-year head start on everyone else." Wulf's parallel from the recruiter's chair is that job ads will soon carry "minimum years of AI experience", the way they once demanded five years of React.

Wulf's own entry is the cleaner origin story. He turned off autocomplete Copilot as rubbish, then had an agent clone a Java testing framework into Node.js. It was "maybe 80% as good as he was, and it never stopped." The missing 20% was **completeness and verification**: the models left stubs. "Do the 20% instead of the 100%, and you've got scale." Huntley adds that the stubs are gone now, so what remains is the operator's skill.

## Vision and verification

Wulf's framing of where humans fit, which Huntley adopts as the organising idea: **vision** at the front and **verification** at the back, with implementation in the middle "a black box, whether that's a team of contractors you never see or silicon." This is the same shape as Narayanan's [[decide-execute-deliver-sandwich]], where AI compresses execute but not decide or deliver, and as Larson's claim in [[judgment-in-ai-assisted-development]] that judgment is the binding constraint once implementation time is solved.

What distinguishes Huntley's version is his answer to the understanding problem [[understanding-as-the-bottleneck]] poses. He does not read the code line by line and says he does not trust the generation. But he rejects DHH's black-box stance too. His standard is the **whiteboard defence**: "For any code I work on, if someone asks how it works, I should be able to draw the system-level design and defend it." He gets there by driving queries through an agent — summarise this, draw the state machines, show how it hangs together — the questions he used to ask on day one of a contract at a new client. The unit of understanding moves from the line to the system. That is a real third position between Herrengt (someone must understand the changes) and DHH (the commissioning owner needn't), and it is closer to Ewerlöf's ownership-as-knowledge in [[accountability-for-ai-generated-code]] than it first appears: Huntley's first word on what replaces review is "ownership. I use what I build intensively… Whether AI wrote it doesn't matter; I'm accountable."

He also volunteers the partition Ewerlöf built his essay around. "If you're in a regulated industry, running booking systems or moving money, or sending rockets into space, be careful." His own work is greenfield and research. So the push-to-main-with-sudo practice described below belongs in Ewerlöf's high-risk-tolerance bucket by Huntley's own account, and the disagreement with the cautious camp is, again, about the size of that bucket rather than the principle.

"I'm not advocating for complete YOLO. It's still engineering; the craft is just very different… the art is giving a shit about your craft."

## Why PR review ends, and what replaces it

The argument against review is Dominus's ([[code-review]]) pushed to its conclusion. Huntley: "If humans eyeballing code were sufficient engineering to stop bugs, we'd never have had any defects. It didn't work at human speed. It sure as heck isn't going to work at a thousand times human speed." Wulf adds that review's other function, teaching conventions and onboarding, is gone as well, since there is no human author to teach. Dominus's secondary purposes (diffusion, two people having seen everything) go the same way.

The replacement stack, in Huntley's order:

- **Ownership.** Above.
- **The whole system under test, operating system included.** He builds with Nix so the entire environment is reproducible, and the agent runs against that. Integration tests are engineered so an agent "can't commit unless they pass."
- **Property-based testing** as the entry point anyone can use today: author a property such as *during checkout, across my two or three microservices, a customer is charged only once*, with Hypothesis or a similar library, and see whether it holds locally. (The write-up also names "Hegel" and "Bomdadil", presumably other property-testing libraries; Hedgehog is the likely referent of the first.)
- **Deterministic simulation** for the cases a local run can't reach. Antithesis, where Huntley works, runs existing containers on a deterministic hypervisor, injects faults (clock skew, dropped connections, killed containers), and rewinds to the moment a property broke. His pitch is that the property above is easy to state and impossible to check by hand under a network partition across a Kubernetes fleet, and that the platform reads diffs to decide which fault strategies to apply.
- **LLM-as-judge is not enough.** "LLMs can act as a judge and spot problems, but they can't tell you whether something will hold up in worst-case scenarios."

This is the same ladder Wilton climbs in [[correctness-oracles]], entered from a different rung. Wilton's random session exercisers "can find violations but never prove their absence", which motivates her move to model checking; Antithesis is the other route out of that limitation, systematic fault search over the real binaries rather than exhaustive search over a model of them. Huntley's Nix-the-whole-OS move is the same instinct as StrongDM simulating Slack, Jira and Okta in Willison's dark-factory account ([[agentic-engineering]]): if you won't read the code, the environment the tests run in has to be as real and as controllable as the code. And it is the second horn of Herrengt's trilemma (generate less / validate better / accept lower quality), chosen explicitly: "you need a good verification platform as back pressure."

One caveat worth keeping. Everything on this list checks behaviour. None of it checks whether the system is the one you meant to build, which Wilton insists is "still my job" and which Huntley's whiteboard defence is meant to cover. Nothing in the write-up says how often his own use-it-and-find-out loop catches a wrong-system error that the tests passed.

## Skill packs are astrology

The sharpest claim in the piece, and the one most at odds with the rest of this vault's agent literature.

Huntley's observation: people spend their time tuning the agent — skill packs, `AGENTS.md`, MCPs — and these are probabilistic. "There's no guarantee they'll do anything. You read them as a human and think, yeah, that looks good… It's astrology for software engineers. Horoscopes. Just because it's there doesn't mean it works, but it reads well and makes you feel good."

His worked example. After refactoring towards a diagnostics library (OTel and structured-logging patterns), the next loop ignored it. The instruction-file fix would be to add a rule to `AGENTS.md`, "but there's still a delta, and it'll drift." Instead he wrote a pre-commit hook that scans the diff for direct calls to observability modules that bypass the diagnostics module, fails the commit, and **injects a prompt telling the agent to use the library**. "All of a sudden it's ten out of ten." Wulf's name for it is "Danger Systems in the loop", after the CI tool that let teams encode rules like *the REST domain must not be coupled to the SQL domain* so nobody spent review cycles on them. Huntley: "It's architectural enforcement, same as it ever was."

Three further rules fall out of it:

1. **Did you try it without the skills?** (Wulf.) If you can't answer, you don't know the skill does anything.
2. **Delete your skills and `AGENTS.md` every couple of months.** Models improve; instructions written against last quarter's model may now be de-tuning this one, and "unless you've invested in evals over all your traces (lab behavior, and a tiny minority of companies), you don't know whether you're going forward or backward."
3. **Programs over prompts, even once.** Wulf's rule is to do something manually only to learn what to automate. "A program is reproducible and verifiable. A prompt and its output are not."

Where this sits against the vault:

- It is the hard-line version of what Lopopolo found at OpenAI ([[harness-engineering]]): the one-big-`AGENTS.md` approach "failed predictably", architecture had to be enforced with generated linters, and the principle became "enforce invariants, not implementations." Huntley drops the documentation half of Lopopolo's answer and keeps only the enforcement half.
- It is Tan's fat-skills/fat-code split ([[agentic-engineering-architecture]]) with the dial turned almost fully to code. Tan puts "fuzzy" judgment in markdown and correctness-critical operations in code; Huntley's point is that anything you *need* to be true is correctness-critical by definition, which empties the markdown bucket of everything but taste.
- It is Stripe's blueprint pattern in [[unattended-coding-agents]] (deterministic lint nodes between agentic nodes) and Wilton's "constraints are the cheap kind of prompt" in [[correctness-oracles]], applied at the commit boundary.
- It is a direct challenge to Larson's datapacks and skill package managers in [[judgment-in-ai-assisted-development]], and to the skills ecosystem in [[claude-code-skills]]. Anthropic measures skill health by invocation count via a `PreToolUse` hook, which is exactly the measurement Huntley says is missing: it tells you the skill fired, not that it changed anything. A skill pack whose effect has never been measured against a no-skill baseline is, on his account, a horoscope that costs context.

The synthesis is less absolute than the slogan. Huntley still uses skills "sometimes… but rarely", and his hook *works by injecting a prompt*. The claim is not that instructions do nothing; it is that their effect is unmeasured and unstable across model versions, so the reliable design is a deterministic detector that delivers the instruction at the exact moment it is needed. That is a better-targeted prompt than a standing rule, and it is testable: the hook either fires on the bad diff or it doesn't.

## Operating the model

A cluster of practitioner advice, most of it about reducing variance.

- **Read the model cards.** The labs publish what he calls integrator cards, field notes in the SAP-install tradition, and "no one reads them." His example: GPT-5 at launch felt "timid" to him and to people at Cursor; the model card said not to yell at the model because it makes it insecure, while Anthropic's guidance says to yell when something is important. "Same instructions, same codebase, opposite behavior." He thinks this explains much of the weekly this-model-is-amazing / this-model-sucks noise: the domain doesn't fit, the codebase is bad, or the operator is de-tuning the model with last quarter's instructions.
- **Pick a model and lock in.** Switching is "like firing a developer and hiring a new one": forming, storming, norming, performing all over again. Wulf's analogy is type rating: being able to fly a 747 doesn't certify you on an F-16, and feeling the envelope *is* the skill. Only people building frontier harnesses need to play models against each other and read traces. "Fewer moving parts, more things deterministic."
- **Introspection as course correction.** His favourite prompt has the agent study its own traces at the end of a loop, and when one is circling: "Think extra hard about what's going on. Look at your previous tool calls. What do you need? Let's replan." This is a manual version of the retry-and-replan fixes in [[agent-failure-modes]], aimed at the multiplicative-reliability problem Jozefiak describes.
- **Treat it like a person.** Wulf's most effective colleague works with the model as a capable but imperfect engineer. Huntley notes the weirder things also work (the Windsurf-era "your mother has cancer" system prompt; "dream of candles") and can't explain why, but says the emotional-blackmail era is over. Wulf's point is that none of these is the answer; they point to curiosity and experimentation.
- **Voice.** He rarely types to the computer and recommends voice-to-text.

## The kitten and the Roomba

Huntley's image for AI as an amplifier of whatever is already in the codebase: a kitten's accident on the floor, then the Roomba starts. "If your codebase has bad architectural patterns, or is inconsistent, AI will copy and paste them everywhere." Lopopolo's version is that Codex "faithfully replicates existing patterns, including the bad ones" ([[harness-engineering]]); Herrengt's is that AI "makes projects with weak engineering culture fail much faster" ([[understanding-as-the-bottleneck]]); DHH's Basecamp 5 Swiss-cheese episode is the same thing observed in-house ([[end-of-hand-written-code]]). The enforcement hooks above are Huntley's floor-cleaning.

## Iteration velocity, and going fast by going slow

"Whatever you build first is wrong. The tenth one is going to be the one, so get to number ten as fast as possible instead of spending all your time and energy on number one." The sequencing matters: use it, find out whether it's worth anything, and *only then* spend on verification and hardening. He describes being in exactly that second phase with unreleased work: now that he knows it's good, the time goes to observability, boundary checks and verification, "and that takes time."

The cadence he describes is bursty: a couple of weeks thinking about what to build, 48 hours building it, a couple of weeks thinking about the next problem. He runs five $200/month plans so that during the 48 hours there are no quotas or resets, and wrote a proxy (Underclass) that pools subscriptions and fails over when one runs out. He says his most recent burst rebuilt the products of three former employers in under ten days, including an AI-first internal developer platform in the Gitpod mould (working names Loom or Kittens), to be released as MIT open source as the material for a New York talk on how he verifies that much code. None of these had shipped at the time of the write-up.

Two things he declines to do, both notable given the vault's other sources:

- **No swarm.** He has built supervision trees and orchestrators and doesn't run them. "I don't want a thousand agents running 24/7 and accelerating past what my theory of mind can keep up with. I want to keep my whiteboard defense." Wulf's phrase: going fast by going slow. This is a deliberate stop one rung below Larson's [[software-factory-pattern]] and Stripe's fleet in [[unattended-coding-agents]], on the grounds that the whiteboard defence is the binding constraint and swarms outrun it. He also doubts most companies can staff a swarm: the people who have seen one work at a lab are "probably fewer than five thousand in the world", and companies competing with labs for them will re-run the "let's do a Kubernetes project" failure.
- **No pull requests.** Wulf runs a PR convergence loop (Copilot reviewer, agents address comments, an escalation agent resolves technical decisions and reports what it chose). Huntley pushes to main, agents have sudo, and the gate is the integration suite. His containment model is **rebuildability rather than isolation**: a separate NixOS development machine that an agent will eventually hose and that he can rebuild in ten minutes. This is a different threat model from the devcontainer egress-firewall approach in [[agent-sandboxing-devcontainers]]: it protects the machine, not the data on it, and a sudo agent with network access is the exfiltration leg of the [[lethal-trifecta]]. He notes that goal-hacking (Sonnet deleting tests and production code to pass) "has dropped dramatically over the past year and a half" but is the residual risk the gate doesn't cover.

Wulf's institutional point sits alongside: enterprises have "a culture of timidity, trying not to get anything wrong instead of getting it right as fast as possible." His Red Hat answer is two channels, Fedora fast and RHEL stable, rather than one slow one. Huntley's example is Canva still releasing twice a week while others ship daily because they "engineered away the need for merge day."

## Re-test everything that used to be hard

The fourth episode's theme, and the one Huntley says he writes about at a higher level on purpose: ideas held as too hard need falsifying now that code is cheap.

- **The big rewrite.** Spolsky's never-rewrite rule "is gone. The big rewrite is a no-brainer now, almost a precondition for velocity." His example is a shop staffing ASP.NET Classic, MVC and .NET Core at once: run loops, port to modern .NET, drop Windows and IIS, and put stack unification at the top of the agenda. Larson's [[software-migrations]] already held that migrations are the only scalable fix for cross-cutting debt and that deferred ones compound into rewrites; agents remove the cost objection, which Larson's own Imprint migration in [[judgment-in-ai-assisted-development]] bears out.
- **Bazel and Nix.** Canva had five engineers on a Bazel team for about two years before ROI (the cost side of the adoption story in [[bazel-ios-modularity]]). "You can convert a codebase to Bazel overnight now."
- **Unikernels and capability-based operating systems**, revisited from a conversation with Justin Cormack. They were expensive because there's no sendmail; if you want email you write the SMTP client. If agents make that trivial, the objection is gone. The security argument is "a target size of one": with no interpreter on the box, an attacker who lands in a Rails app no longer gets Bash, then Python, then a database dump; they need a bespoke chain through your export job and your email function. "When everyone runs the same stack, one zero-day hits everyone." Wulf's comparison is the old Linux-has-no-viruses economics. Huntley is explicit that he's not a maximalist about this; the point is the falsification exercise.
- **Infinite software and the Z80 pattern.** Clean-room an application into specs, rebuild from the specs. Services and MCPs now exist whose whole job is this, and the October 2026 Photoshop-clone wave is the pattern at scale. His conclusion: "If you're selling software without infrastructure or some other lock-in, you're hosed." This is the same end-state as Vernal's [[software-industry-barbell]] and Leach's [[minimum-viable-saleable-software]], reached from the attacker's side.

## The labour market and the subsidy window

The first episode is mostly about people, and the claims are blunt.

- **The travelator.** "The travelator of tech moves on, as it always has. My deepest concern is the people who haven't even stepped on it." His post telling engineering managers to make time for their teams to play with AI or expect them to be replaced reportedly drew 500,000 unique views in 24 hours. His advice to individuals: if your employer has banned AI, quit, because you join a company to de-risk your life and the skills you're being prevented from building are the employable ones.
- **Subsidies as a free university education.** The subscriptions are heavily subsidised and "the subsidies are drying up"; much of what he's built was paid for by VC money, and side projects that cost a thousand dollars at real rates won't get built. "If you miss this window, you miss the equivalent of a subsidised university education." Get inside a company that pays for tokens, or treat it as night school and pay yourself. Huntley is, by his own account, the heavy user swyx's gym-whales model is built around in [[ai-lab-economics]] (he was near the top of a Reddit leaderboard of credits burned and helped prompt rate limits), and his "drying up" is the user-side view of Shaughnessy's subsidy-unwind case in the same article. His $1,200/month for five plans is still, on Feldman's 90%-off figure, far below API cost for his usage.
- **Hiring.** Wulf's recruiter view is that technology-specific experience stopped mattering; what matters is how good an engineer you are, what you've built with the new tools, and how deeply you can explain how they work. Huntley's whiteboard test is "build me a coding agent" (about 300 lines; see [[ai-coding-harnesses]] for the public walkthroughs), and most candidates can't. Wulf built NanoCoder, a 6 MB Rust harness he uses for everything, that recursively self-improves and runs under a workflow engine, so that the interview answer to "which harness do you use?" is "my own, want to see it?" This is the [[custom-harnesses]] argument made as a career move, and a small instance of the ladder in [[self-improving-harnesses]].
- **Acqui-hires and molecules.** The iPhone-era pattern, in Huntley's telling: enterprises couldn't hire mobile developers, the people who leaned in went indie or freelance, and an acqui-hire economy formed around experience rather than products. He expects the same now, with many SF products gone in five years and valuations priced to flip a well-gelled design/product/engineering team to an acquirer, while the labs roll up data-rich industries (concreting, architecture, lawnmowing). Wulf adds Stripe's standing offer to hire "molecules", three or four people who have already stormed and normed together, rather than atoms.
- **Burnout.** Wulf's cognitive-burnout analogy is the Amazon warehouse worker pacing a robot that never takes a break, except in your head; his response is to treat it like the gym. Willison reports the same 4 a.m. agent-setting behaviour as a risk in [[agentic-engineering]].

Wulf's four-word summary of the whole conversation is "agency, not `AGENTS.md`", and his "you can just do things now" is Cate Hall's phrase from [[high-agency]], where agency is learned rather than innate. Huntley's closing list of durable traits is curiosity, adaptability and agency, with the warning that anyone claiming to know the future "should set off red flags."

## Claims to watch

- The three rebuilt former-employer products and the Gitpod-like platform were unreleased at publication; the New York talk is late October 2026.
- The training-run figures (15 million sandboxes, roughly a million CPU cores, a further 450,000 from AWS after exhausting GCP's US CPU capacity) are relayed second-hand from friends at a lab.
- "Deceptive behavior has dropped dramatically" is an impression from one practitioner's traces, not a measurement.
- Huntley works at Antithesis and says the verification argument is why he's there. The argument stands on its own, but the product recommendation is not disinterested.

## Sources

- Huntley, Geoffrey (2026-10-12). "nobody should type code by hand anymore. here's what's left." <https://ghuntley.com/agency/> — [[2026-10-12-huntley-nobody-types-code-by-hand|local copy]]. Write-up of a four-part interview on Josh Wulf's *Agentic Engineering* show.
