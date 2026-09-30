---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-09-30-coding-is-not-solved.md
compiled_at: 2026-09-30
model: claude-fable-5-1
confidence: medium
---

# Accountability for AI-generated code

Alex Ewerlöf (reliability engineer and writer, author of *Reliability Engineering Mindset*, two engineering degrees, four years building with and on LLMs including his own harness) published *Coding is NOT solved* on 26 September 2026, three days after DHH's Rails World keynote ([[end-of-hand-written-code]]). It reached #2 on Hacker News (473 points, 476 comments by 29 September, "overwhelmingly positive"), which Ewerlöf reads as evidence that the practitioner majority sits on his side of the argument rather than DHH's. It is the most complete statement so far of the **accountability objection** to the coding-is-solved narrative, and it is worth separating that objection from the polemic it is wrapped in.

The essay is long, discursive and deliberately combative (a self-described "well chunked article with illustrations and memes … optimized for the audience"). Underneath, there are three durable arguments, one economic prediction, and a large amount of opinion about Anthropic and its users that should be read as opinion.

## The core argument: accountability requires understanding

Ewerlöf's central claim is a chain of three propositions:

1. **AI cannot be held accountable.** Accountability means bearing consequences. AI cannot be fined, imprisoned, fired, or made to suffer; "the worst thing you can do to AI is to unplug it," and it does not care. He leans on his earlier accountable-vs-responsible distinction: an agent can be *responsible* for a task (it did the work) but only a human can be *accountable* (they answer for it). The fear of consequences is, he argues, one of the main reasons society doesn't collapse; AI has none.
2. **Therefore a human is accountable for shipped code regardless of how it was produced.** "If you ship a piece of code, you are accountable for it regardless of *how* you produced it. So you better understand it."
3. **You cannot be accountable for what you don't understand.** "AI can explain it to you but it cannot understand it for you." Understanding is what lets you reason about system behaviour and fix it when the AI inevitably fails, and "you cannot be responsible for what you can't control either."

He formalizes this as **ownership's three pillars**: knowledge (what problem you're solving and how the solution works), mandate (authority to decide without asking permission), and accountability (you're the one on call when it breaks). Remove any one and you have *broken ownership*. The DHH commissioning-owner model, where the business owner holds accountability and someone (or something) else holds the knowledge, is on this framing a textbook broken-ownership pattern rather than a legitimate division of labour. That is the precise point at which the two essays disagree; see below.

His evidence that executives are discovering this the hard way is Shopify's Tobi Lütke: the April 2025 memo mandating AI use before hiring, followed roughly a year later by Lütke coining "slop grenades" for the result. Ewerlöf also quotes an HN commenter's observation that "unaccountability is transitive": teams successfully justify shipped defects with "Claude wrote it," leadership shrugs ("haha, that's AI for you"), and engineers are pressured to deploy business-side vibe-coded tools that "look like they work."

## The risk-tolerance partition

The second durable contribution is a taxonomy of when reading the code is *not* required. Ewerlöf lists four product types:

1. **Personal software**: itch-scratching, automation, DIY patches.
2. **Proof of concept**: demonstrating feasibility or viability.
3. **Throwaway automation**: where the budget only covers validating outputs (e.g. reviewing images, trivially checked by a human).
4. **Weaponized AI**: deliberately pointing the risk at a target (cyber-attacks). He argues even this needs tight controls given the blast radius of an internet-connected agent.

The common factor in the first three is **high risk tolerance**; the fourth *exploits* the risk. Against these he sets the domains that actually hire engineers, which are low-risk-tolerance by construction: healthcare, finance, automotive, defence, power, aviation, manufacturing, "wherever a mistake can cost money, lives or legal consequences."

This partition does a lot of quiet work in the essay and clarifies the DHH dispute. Ewerlöf's own hands-off projects (LinkedOut, a Chrome extension over his LinkedIn export; Garess, a Raspberry Pi harness) are explicitly in the POC/personal bucket, and his LinkedIn reply to DHH concedes that DHH's "experience is valid given the risk tolerance of what you're working on." So the live disagreement is not whether unread code is ever acceptable (both say yes) but **how large the high-risk-tolerance bucket is economically**, and whether a consumer email product like HEY belongs in it. Evans made the same cut from the other direction in [[generative-ai-as-pattern-generation]]: error tolerance by domain determines where generative output is usable at all.

## Why coding specifically resists the current generation

Ewerlöf argues, contrary to the narrative, that coding is one of the *last* areas current LLMs can fully take over, because coding is about logic and "computers don't give a f\*\*\* about how right you think you are." His mechanism:

- LLMs are stochastic. They work on code only because the harness feeds compiler, test and runtime errors back in a loop "until most errors are solved or hidden," and models "can and do cheat" against that loop. This is the same loop [[ai-coding-harnesses]] describes as the reason the harness matters more than the model; Ewerlöf reads it as a workaround for a defect rather than an architecture.
- Accuracy degrades with volume. He puts the *useful* context window at 30–40% of the nominal figure, so a 1M-token window is not a 1M-token capability.
- Capability is on an S-curve with diminishing returns per dollar; humans are "notorious at understanding the S-curve," so "next year" forecasts should be discounted. He is explicit that there is "no guarantee this tech will be 100x better by next year," while also insisting it is not a fad.
- Verification is harder for code than for images. His whiteboard doodle's point: humans spot six-fingered hands at a glance but "even a veteran developer may miss the issue" in code at a glimpse. This is a stronger version of the review-attention argument in [[ai-code-review]].

From this he concludes we are **at least two revolutions away** from eliminating the need to read code: AI that learns in real time (not skills, prompts and memory bolted on at runtime), and AI that reasons in abstract, symbolic terms (he is unpersuaded by the maths results, which he reads as brute-forced with tokens and time, and points at neuro-symbolic research as the unfinished work).

### The compiler criterion and jagged trust

The most useful framing in the essay is his statement of what it would take for him to be comfortable being accountable for AI output with minimal review: **the relationship he has with a compiler**, whose bugs are rare and whose output is deterministic. LLMs fail both tests. "AI has jagged intelligence, I have jagged trust": a model that nailed one case gives no guarantee on the next, whereas humans are *consistently* wrong (and, once they learn, consistently right). The runtime version of the same point is that an AI component in a production system is non-deterministic even at 100% eval pass rate, which is why "you wouldn't want to fly an airplane where the pilot is this AI" (autopilot being a closed control system, "another beast entirely"). [[agent-failure-modes]] gives the arithmetic underneath jagged intelligence: per-step reliability multiplies across steps.

This criterion is worth holding onto because it is exactly what Wilton's [[correctness-oracles]] tries to *manufacture*: reference implementations, contract monitors, generated TLA+ and bytecode analysis are all attempts to build the deterministic, rarely-wrong checker that would let you stop reading. Ewerlöf does not engage with that route beyond noting that "the safest way to discover [conflicting instructions] is to ask your agent to build what you asked for," which is much more expensive than a linter. His position is that no such regime exists today; Wilton's is that building one is now the engineer's job. They agree on what the regime would have to look like.

## The nine fallacies

Ewerlöf's list of counter-narratives, condensed, with the vault articles they push against:

1. **"You can create a full spec upfront."** Impossible except for trivial software; understanding of the problem co-evolves with the implementation. Code is "a side effect of thinking and experimenting." (Contrast [[spec-driven-development]], whose Notion variant is in practice iterative rather than upfront, and [[software-estimation]], which he cites in the same breath as a fantasy.)
2. **"English is the new programming language."** Natural language is vague and self-conflicting; programming languages exist precisely so a compiler or type-checker can flag those conflicts. Controlled natural languages exist but fall short. (This is the direct answer to DHH's "there is a programming language I like better than Ruby, it's called English.")
3. **"I move much faster."** Motion is not progress; SLOC, PR count and feature count are vanity metrics. Measure service levels, "call me when you can prove a margin between token costs and business value."
4. **"I've stopped writing code; next year I'll stop reading it."** If a power user can prompt what you prompt, you have confessed to being redundant. Find value to create *on top of* AI instead.
5. **"Taste is leverage."** "The lie retired chefs tell themselves." Everyone has taste; what was payable was experience, and AI has lowered the bar for producing decent-looking software while raising the bar for what's worth paying for. Bring "taste" to an interview and learn what the market thinks of it. This is a frontal challenge to the taste-as-human-bottleneck line in [[agentic-engineering]].
6. **"Managers delegated to humans, now they delegate to AI."** Humans can be *accountable*; AI can only be *responsible* (see above). Also humans are consistent and models are not.
7. **"Coding is solved but engineering isn't."** His favourite, because it half-concedes. Grunt work is largely solved thanks to feedback loops, but *code remains the source of truth* (what happens and how) and is what you are accountable for. Reading the code gives more control than reading the LLM's explanation of it. Engineering (trade-offs, measurement, isolation, diagnosis, incremental improvement) remains fully applicable, "but coding is NOT solved."
8. **"AI is an equalizer."** It is a *multiplier*: it "gives wings to both stupid and smart people," and the direction of the force vector matters more than its magnitude. Some tasks are cheaper by hand: his agent took 12 minutes and 72 steps to bump five patch-release npm dependencies he could have done in under a minute. Lovable-class tools make it cheaper than ever to fake credibility.
9. **"The agent is the new compiler."** Dismissed with a meme; the substantive rebuttal is the compiler criterion above.

Two further observations belong with these. The **review-volume trick**: run agents in parallel and the diff becomes too large to review, so it gets merged "on trust," the same pre-AI trick as making a PR enormous. And **loop engineering** (agents prompting agents) as something even the labs discover has gone rogue months later. Both are the mechanism [[understanding-as-the-bottleneck]] describes from the inside, and the reason the [[code-review]] legibility check breaks under agent volume.

## Where AI is and isn't good

Ewerlöf's positive taxonomy of current-generation use cases: **mapping** (language-to-language, code-to-code, data-to-code, code-to-data, modality-to-modality), **generation** (creative output, expansion, cohesion from scattered points, prediction), **reduction** (summarization, conversion, extraction from unstructured data, classification), and **search** (progressive discovery, semantic relevance, detection, chunking). Coding sits inside this as a mapping problem with an unusually unforgiving checker.

Where not to use it: anywhere legal accountability would fall on the AI; embedded or low-power devices ("toothbrush with AI"); privacy-sensitive data, where he makes the sharp point that a human-in-the-loop approval step is **compliance theatre** because approval fatigue and attention limits mean nobody is really checking (the standard mitigation in [[lethal-trifecta]] discussions, judged useless in practice); the "kitchen sink," where context is thrown at a model in hope, since AI is more reliable under constraints (guardrails, RBAC, scoped attention) and that pre-work sometimes costs more than doing the task by hand; and anything deterministic code already does faster, cheaper and with predictable edge cases. "If you need regexp or SQL, use them. AI wins in dynamic problems."

## The economic prediction: price collapse and SLAs

The essay's economic section is more interesting than its framing suggests. Even granting solid non-functional requirements and full human understanding, Ewerlöf argues the *economics* of a task decide whether a slow, expensive human belongs on it. If AI output is 2x worse but 1000x faster and 100x cheaper, "slow is fast" is only justified for low-risk-tolerance software. Everything else faces a price collapse.

He draws two consequences:

- **SaaS companies are increasingly in the business of selling SLAs.** You can now prompt a replica of most SaaS products, but when it breaks most businesses would rather call a vendor than debug, AI-caused failures are hard for AI to fix, and scale lets vendors amortize the cost of guarantees. The buy-vs-build line therefore moves to "is this what your business is about, and do you want an SLA or a TCO?" This is the same zone-of-viability argument as [[minimum-viable-saleable-software]] arrived at from the buyer's side.
- **Vendors cannot keep charging human rates for AI output.** He cannot reconcile universal AI adoption with consistently rising software prices and AI-attributed layoffs; the chasm closes as customers realize they can build at a fraction of the cost. The only two ways forward are to accept the price crash (with quality following it down as even more AI is used) or hold price by competing on quality with experienced humans using AI thoughtfully. This is [[software-industry-barbell]] stated as a vendor's choice rather than a market structure.

His "Nordic gold" analogy summarizes the stance: AI output is cheap, technically advanced, and realistic enough to fool a glance; fine if you don't need real gold, and "many use cases don't need gold at all." The mistake is the CEO who sees the surface and asks why the expensive engineers are still on payroll, "as if the act of typing code was the whole value proposition."

## Careers and practice

Ewerlöf's personal rule: **"If I can't do it, I won't ask AI to do it either."** If both can and AI is faster, delegate when in a rush; periodically take over and refactor or debug "the old way" because the brain is a muscle; sometimes "prompt in code" by making the change directly and asking the agent to finish. Mastery "requires us to know the job at a slow speed before we can delegate it effectively at hyper speed." This is [[expertise-as-llm-leverage]] as a discipline rather than an observation, and it is the guardrail logic of [[vibe-coding-apprenticeship]] applied to oneself.

He expects a large fraction of engineers to shift lanes into **technical product managers** (POCs and market fit, handing artifacts to engineers who own them), **AI managers** (herding agent fleets for risk-tolerant or risk-weaponizing automation), **AI deployment engineers** (alignment, reliability, governance, data pipelines) and **AI quality engineers** (taming stochastic products, automating evaluation). Note that three of the four are jobs *about* the accountability gap rather than jobs that assume it away, which is consistent with the essay's thesis and with the decide/deliver layers in [[decide-execute-deliver-sandwich]].

His "AI overdose" checklist (zero tolerance for disagreement, outsourcing anything slightly hard, no longer reading long-form, more time with AI than humans, and "you skim," proven by a deliberately missing item five in the list) is [[ai-judgment-atrophy]]'s friction-erosion thesis in listicle form. He adds a speculative mechanism: neural synchrony, the finding that brain wiring shifts toward the company we keep, which he uses to suggest that some of the *perceived* improvement in models is a perceptual shift in heavy users. That is offered as an observation, not evidence.

## The DHH exchange

The essay's last update records a LinkedIn exchange. Ewerlöf: DHH stopping coding and prioritizing velocity over quality and accountability doesn't oblige the industry to follow; his experience "is valid given the risk tolerance of what you're working on," but "coding is NOT a solved problem" and "please don't run your experiments on me." DHH: "I wish you all the best getting through the five stages of grief. If you're still in denial, there's a way to go … there's only one way out and it's through." Ewerlöf's reply is that DHH can only push this narrative so far before "the people who are responsible for the plane you fly and the car you drive start executing on it," and that he wishes DHH would talk about nuances instead of "going full throttle on your (valid but within a narrow scope) narrative."

Read alongside [[end-of-hand-written-code]], the exchange is a clean statement of the two positions. DHH's implicit answer to the accountability chain is that the commissioning owner has always been accountable for code they couldn't read, and 37signals is just moving the knowledge holder from a contractor to an agent. Ewerlöf's answer is that this only ever worked because the contractor was accountable too, and an agent isn't. Neither side has offered the thing that would settle it: an accounting of what happens at HEY Next's first serious incident in the Rust mail server nobody read.

## Caveats

- **Single, highly opinionated source.** The essay is explicitly a collection of opinions, and its tone (people who disagree are "brain-dead," suffer from "sycophantic AI," or are "overpaid prompt monkeys") is designed to provoke. The arguments above stand or fall independently of it.
- **The Anthropic and Claude material is opinion, not evidence.** Ewerlöf singles out Boris Cherny and [[claude-code]] (three real but cherry-picked GitHub issues: a Bun help-menu bug, a self-deleting installer, extra-usage billing), asserts that "most of those brain-dead narratives come from Claude users," offers as a "working theory" that Anthropic and OpenAI trained their models to make users overestimate them, and claims without a source that "Fable can fall back to Opus without even telling you." None of this is sourced beyond the issue links; he himself invokes Hanlon's razor on the malice question. Treat it as a record of practitioner sentiment in September 2026 rather than as findings.
- **The two-revolutions claim is a forecast.** It rests on his reading of transformers as fundamentally non-symbolic; the essay's own S-curve warning cuts both ways.
- **The cloud-data warning** (labs need "your data in context of doing productive work" and are not to be trusted about retention; he uses cloud AI only for public or open-source material and recommends local models such as Qwen 3.8 27B and Gemma 4 for everything else) is a reasonable privacy stance stated as a certainty about vendor behaviour.
- **He is a reliability engineer**, and the essay's frame (NFRs, SLIs, SLAs, on-call as the definition of accountability) reflects that. Someone building consumer software with a different failure cost will weigh the risk-tolerance partition differently, which is the whole dispute.

## Sources

- Ewerlöf, Alex (2026-09-26). "Coding is NOT solved." <https://blog.alexewerlof.com/p/coding-is-not-solved> — [[2026-09-30-coding-is-not-solved|local copy]]

## Connections

- [[end-of-hand-written-code]] — the keynote this essay rebuts; the commissioning-owner model versus broken ownership is the exact point of disagreement
- [[understanding-as-the-bottleneck]] — Herrengt's rate-asymmetry mechanism; Ewerlöf supplies the accountability frame and the risk-tolerance partition that says where the constraint binds
- [[correctness-oracles]] — Wilton's programme for manufacturing the deterministic checker Ewerlöf's compiler criterion demands
- [[judgment-in-ai-assisted-development]] — the same "judgment, not generation, is scarce" conclusion from the tooling side
- [[ai-code-review]] — the review-side treatment of the volume problem Ewerlöf calls the "old trick"
- [[code-review]] — the legibility check that agent-scale diffs push past its budget
- [[agentic-engineering]] — "taste as the human bottleneck," which fallacy 5 directly contests
- [[spec-driven-development]] — the upfront-spec practice fallacy 1 rejects, and its iterative reality
- [[ai-coding-harnesses]] / [[harness-engineering]] — the feedback loop Ewerlöf credits for LLM coding working at all, read by him as a workaround rather than an architecture
- [[agent-failure-modes]] — multiplicative step reliability as the arithmetic under "jagged intelligence"
- [[generative-ai-as-pattern-generation]] — Evans's error-tolerance-by-domain, the same partition from the product side
- [[minimum-viable-saleable-software]] / [[software-industry-barbell]] — the buy-vs-build zone and the two-ways-forward vendor choice
- [[lethal-trifecta]] — where human-in-the-loop approval sits as a mitigation, and why Ewerlöf calls it compliance theatre
- [[ai-judgment-atrophy]] — the individual-level version of "AI overdose"
- [[expertise-as-llm-leverage]] / [[vibe-coding-apprenticeship]] — "if I can't do it, I won't ask AI to" as practice and as pedagogy
- [[decide-execute-deliver-sandwich]] — the employment-side account his four career lanes are consistent with
- [[software-factory-pattern]] / [[unattended-coding-agents]] — the "software factory" side of the divide he describes
- [[ai-mania]] — the executive environment in which token usage becomes a productivity metric
- [[claude-code]] — the product he uses as the exemplar of the narrative
