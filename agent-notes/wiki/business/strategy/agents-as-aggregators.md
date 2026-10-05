---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-09-28-apps-agents-and-aggregation.md
compiled_at: 2026-10-05
model: claude-fable-5-1
confidence: medium
---

# Agents as Aggregators

The thesis that a personal or company agent, an AI with its own computer that operates apps on the user's behalf and generates interfaces on demand, is the next Aggregator and also a platform, and that owning it is the largest prize in technology. The anchor source is Ben Thompson's Stratechery essay *Apps, Agents, and Aggregation* (2026-09-28), which extends his own [[aggregation-theory]] from websites to applications: where the web made publishing abundant and discovery scarce, agents make *doing things* abundant and leave volition scarce. Thompson wrote a follow-up Update that is linked from the essay but not yet ingested; it and other sources on the agent-as-interface question should integrate here.

Thompson frames the essay with Steve Jobs's "Are you getting it?" from the iPhone introduction. Jobs presented three products that were one device. Thompson presents three predictions he says are one present-tense reality:

1. Messaging ("chatbots now, natural interfaces later") is how people will communicate with AI.
2. People will not only stop programming computers, they will stop using them. AI will use them.
3. Pre-built UI, "write once, run everywhere, for everyone," is dead.

## Apps were always a means

The essay reaches back to a 2013 argument. When Facebook launched Facebook Home, an Android interface that put friends' activity on the lock screen, Mark Zuckerberg told Wired that "Apps aren't the center of the world. People are." Thompson's reply at the time was that both framings missed the point: phones won because they did more **jobs to be done** for more people in more places than anything before them. His own home screens then held 151 apps covering 80 jobs, with four focused on people.

His phone now holds 689 apps. He treats that number as a measure of what the App Store made possible, a custom interface for every activity, and also of its cost: each app is a service he wanted something from and had to learn to operate. "I'm not a professional app user, I'm just someone who wants to get things done." The apps he opens daily have stayed the same for a decade: messaging, social media, and now ChatGPT and Claude. The number of apps he looks at is "plummeting."

He also recalls his 2014 argument that messaging was mobile's killer app, published the day before Facebook bought WhatsApp, and calls that acquisition "a step back in ambition" from Facebook Home. The essay does not say so outright, but its structure implies that Muse is Home's ambition revived with the organizing principle corrected: a Meta-owned layer over the whole phone, built around jobs rather than friends, and reached through messaging.

## An agent is an AI with a computer

Thompson's definition: agents "are not just AI: they are an AI that has access to a computer." He traces this to his 2023 piece on ChatGPT plugins, which argued that LLMs would not become deterministic but would operate deterministic computers, and adds the ability to write things down (the subject of [[external-memory]]).

Two developments make the definition matter commercially:

- **A computer for every user.** Most people cannot or will not set up a machine for an agent. Thompson says the important part of Meta's Muse launch was not the Muse Spark model but that Meta provisions every U.S. user with a virtual machine (2 cores, 8GB of RAM, 8GB of storage), which he calls "the only way to make agents work for most people."
- **Computer use.** Any app with a command line has been usable by agents for a long time. Thompson says GPT-5.6 Sol made any app with a graphical interface usable, slowly, and that Astra made it fast. His conclusion: "AI can basically use any app or any website that I don't want to."

His worked example is small. Prompted by a friend's use of Muse in a WhatsApp group chat, he asked Muse to organize the recipes he had saved on Instagram. It returned a PDF; he asked for something more accessible; it built him a Recipe Box app. The exchange took five minutes while he walked his dog. He notes the app is imperfect. It currently categorizes videos, and the work of reading captions and watching the videos was still in progress, limited by Instagram's rate limits.

## The infinite app

Thompson calls the recipe app number 690 on his phone and then corrects himself: it is "the infinite app," because an agent can create any app on command, including one with an audience of one. He connects this to his 2024 prediction of on-demand generative UI. What he got is not yet the just-in-time interface he still expects, but it is custom UI with no requirement that anyone else ever use it: "effectively disposable, because it's infinite."

He reads Meta Connect the same way. Meta's glasses and headsets are, in his words, "Muse delivery mechanisms," and the general-purpose computer he predicted wearables would become already exists in the cloud VM Meta gives each user.

## From discovery to inspiration

The central analogy runs through Aggregation Theory:

| Era | What became abundant | What stayed scarce | What the winners solved |
|---|---|---|---|
| Print | — | Publications, which depended on presses and trucks | Owning distribution |
| Web | Publications, once distribution was free | Finding the right one | Discovery (Google, Meta) |
| Agents | Doing things on the web and in apps | Volition | Inspiration |

On the web, whoever solved discovery aggregated demand, gained power over suppliers, and in the cases of Google and Meta built very large advertising businesses. Thompson argues the same thing is about to happen one layer up. "The companies who solve inspiration will gain power over every entity that has things that need to be done." Once the user is focused on a problem, each app and service involved becomes "an implementation detail," a supplier "facing the fate of publications under Aggregators," and the Agent becomes "the ultimate gatekeeper of not just user demand, but desire."

## Platform and Aggregator at once

Thompson's second exhibit is Microsoft's redesigned Copilot "super app," as reported by The Verge. It bundles chat, a Code tab that lets any employee build an app, tracker, dashboard, or automation and share it as a cloud-hosted internal app, and Autopilot, a "digital teammate" (formerly Scout) that keeps running while the user sleeps. Microsoft VP Jared Spataro's description: Autopilot "lives in your tenant with its own identity, memory, computer, and workspace," is built on Microsoft IQ, shows up in Teams and Outlook where it can be @mentioned like a colleague, and has "permissions, audit, and governance behind it."

Thompson reads this as Microsoft's standing strategy, which Satya Nadella restated on X as being the OS for work, and as the successor to what he once called Teams as the OS for SaaS: own the interface and make everyone else integrate on your terms. He notes the structural similarity to Muse, down to the cloud computer per agent, with enterprise controls added.

The prize, on his account, is larger than either earlier category: "not just a platform like Windows, or an Aggregator like Facebook" but both. The agent is the only interface a user needs, it uses a computer on their behalf, it generates whatever UI they want, and it does things "without you but for you the rest of the time."

## Who wins: the distributors

Thompson concedes that all of this is obvious only to people who already use agents, and that many do not. He expects that to change. Nobody wants apps for their own sake, and nobody wants enterprise UI at all, which he describes as "inscrutable interfaces" that exist to expose arcane functionality and lock people in. With computer use, the agent does not depend on "an underdeveloped and intentionally limited API."

Three claims follow:

- **Suppliers will try to charge for access, and it will not hold.** Thompson says Salesforce, at its most recent Dreamforce, set out to charge "a three-digit premium" for making its flagship product a Claude plugin. He calls it a cash grab in the face of computer use that will mean "the Salesforce UI is never interacted with by a human again."
- **One agent each.** "Models are relatively substitutable; agents, however, operate better the more context they have about you, and the more access they have to things like your logins and files." Context and access make agents sticky, so "most people and companies will only have one agent, not multiple."
- **Distribution decides it.** The first two companies to ship agent products that fit the use case (broad exposure to a person's or employee's life, an established messaging service, a computer per agent) are the two with distribution and practice at using it. "Meta reaches nearly every person on earth; Microsoft reaches nearly every employee."

## Reading it against the rest of the wiki

**A third cost goes to zero.** [[aggregation-theory]] rests on two costs collapsing: distribution and transactions. The implicit third here is the cost of *operating* software. When that falls, the layer that gets modularized is the application's interface, and the layer that integrates is the agent plus the user's accumulated context. Thompson's 2015 diagnostic questions map cleanly: the incumbent differentiator being digitized is the UI and the workflow lock-in built around it. One difference from the original theory deserves notice. Classic Aggregators had a cross-side flywheel, where users attracted suppliers and suppliers improved the experience. With computer use, suppliers do not need to show up at all, so the agent's flywheel is per-user: more context and more credentials make it better for that one person. That is closer to a switching cost than a network effect, which means the "one agent" prediction leans more on lock-in and distribution than on the winner-take-all dynamics the original theory described.

**Computer use is commoditizing the complement without its consent.** [[commoditize-your-complement]] describes companies deliberately cheapening what is bought alongside their product. Here the complement is every app, and the agent does not need the app maker's cooperation. That puts Thompson at a slightly different point from Bret Taylor in [[agent-harness]], who argues that companies will need to expose a harness of skills, documentation, and rules because an API alone is too thin, and that harness quality will become a procurement criterion. The two views combine into a narrower choice for suppliers than either states alone: being intermediated is not optional, but being a well-documented supplier the agent uses well, rather than one it scrapes badly, still is. Taylor's distinction between decaying systems of engagement and durable systems of record, and Sierra's "the agent is the UI, the system of record the backend" in [[company-wide-agent]], say what survives on the supplier side: the ledger, not the screen. Sierra's account also arrives at Thompson's two framings independently, from inside one company: "Agent, singular," and "companies are a collection of jobs to be done."

**Salesforce is squeezed from two directions.** Brandur Leach's arithmetic in [[minimum-viable-saleable-software]] already put fully loaded Salesforce (about $25k a month for 50 seats) on the *build* side of the buy-versus-build line. Thompson adds a second pressure that applies even to customers who keep paying: they stop touching the product. A plugin premium is a toll on a road that computer use routes around.

**Stickiness, and who is missing from the winners' list.** A week earlier, in the essay recorded in [[pacing-the-frontier]], Thompson argued that Muse showed a sub-frontier model is good enough for an excellent personal agent, that a personal agent is far stickier than a chatbot, and that coding agents are not sticky because their artifacts live in GitHub. This essay generalizes that into "one agent each" and names the beneficiaries. Neither is a frontier lab, which fits the earlier essay's "product overhang": the labs have to build touchpoints before their capability lead stops mattering. Benedict Evans's objection in [[ai-platform-moats]] is the counterweight. He grants that features like memory provide stickiness but argues they provide no network effect and are copied within weeks. Thompson's implied answer is that an agent's hold comes from accumulated context, delegated logins, and a provisioned computer, not from a feature. [[commodity-trap]] describes the same mechanism as "embedding moats" and "digital workers" that effectively cannot be fired, and treats the resulting lock-in as the thing regulators should worry about. Thompson describes the same outcome as a prize to be won, with Meta and Microsoft rather than the labs as the likely holders.

**Distribution and messaging.** Evan Spiegel's claim in [[snapchat]] that AI shrinks the cost of producing a product and does nothing to deliver it is the general form of Thompson's closing section, and Evans's point in [[ai-platform-moats]] that incumbents with distribution can make AI a feature is the same prediction from the skeptic's side. Justine Moore's [[messaging-as-ai-interface]] argued that the consumer agent will live in a message thread and that agents need human affordances such as phone numbers, cards, and email addresses. Its main caveat was that outside the United States, WhatsApp already occupies that slot. Thompson's essay is that caveat promoted to the main argument: Meta owns WhatsApp, Microsoft owns Teams and Outlook, and Autopilot's "identity, memory, computer, and workspace" is Moore's list of affordances in enterprise form.

**The skeptical case from the same month.** Evans's essay in [[institutionalized-vs-improvised-software]] rebuts precisely the claim that apps as a category are dead. His objections are that most people are not tool-builders, that knowing what to build is harder than building it, and that adoption inside companies is an organizational decision. Thompson's essay half-concedes each. His scarce resource, volition, is Evans's first two objections restated as an opportunity: if people do not know what to ask for, whoever supplies the asking wins. His own recipe app needed a friend's example to prompt it and a follow-up to turn a PDF into something useful. And Microsoft's version, with shared internal apps, permissions, and audit, is in Evans's terms the paving of improvised tools into institutionalized ones, not the end of institutionalized software. The disagreement that remains is about pre-built UI for the long tail, where Thompson expects generated interfaces to replace it and Evans expects most people never to ask.

**An answer to the barbell's open question.** Mike Vernal's [[software-industry-barbell]] predicts an explosion of small software and leaves open what "the Substack for software" will be, expecting both an aggregator and a platform to emerge. Thompson's answer is that the agent is both. It also shrinks the part of Vernal's light end that could be a business: software my agent builds for me in five minutes is software I do not buy from anyone.

**What "solving inspiration" would mean.** In the essay behind [[external-memory]], Thompson held that what AI lacks is volition, which is consistent with volition being the scarce input here. But a company that "solves inspiration" is supplying the inputs to volition, which is to say suggesting what to want. That is the feed business in a new position, and Meta is the company with the most practice at it. Thompson does not spell out the business model, but the Aggregation analogy he draws ends in advertising, and suppliers "scrapping for crumbs from the Agent" suggests paid placement in the agent's choices. This is an inference from the essay, not a claim it makes. It also connects to [[scarce-assets]] and [[uncopyable-value]]: Kevin Kelly observed that findability accrued to the aggregators, not the creators, and Thompson's sequence puts volition next in line for the same capture.

## Caveats

- Single opinionated source, argued largely from personal experience. The central demonstration is one recipe app that Thompson himself describes as unfinished.
- The supplier in that demonstration, Instagram, is owned by the agent's maker and still rate-limits the agent. Other suppliers can throttle, block, or litigate against computer-use agents. The essay treats computer use as settling the question of supplier cooperation, and its own anecdote shows the question is open.
- "One agent each" is asserted, not argued in detail, and the essay's own framing yields at least two per person: Meta's for the individual and Microsoft's for the employee.
- The essay acknowledges that giving an agent access to a computer, logins, and files "is scary" and moves on. Security and delegation risk are not addressed.
- Apple and Google, who control the phone operating systems these agents and generated apps must reach users through, do not appear.
- Product references (GPT-5.6 Sol, Astra, Muse Spark, Microsoft IQ) are named without detail. This article repeats only what the essay says about them.

## Sources

- Thompson, Ben (2026-09-28). "Apps, Agents, and Aggregation." *Stratechery*. <https://stratechery.com/2026/apps-agents-and-aggregation/> — [[2026-09-28-apps-agents-and-aggregation|local copy]]
