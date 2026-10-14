---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-10-05-agent-network-effects.md
compiled_at: 2026-10-14
model: claude-fable-5-1
confidence: medium
---

# Agent Network Effects

Whether personal AI agents have [[network-effects|network effects]], and if so where those effects live: inside the agent product, or in the identity, reputation, and marketplace layers the agent sits on top of. The anchor source is Andrew Chen's *Will agents have network effects?* (2026-10-05), written as a wave of consumer-friendly horizontal agents (Muse, Town, Instinct, Grokbot) forced thousands of vertical-agent startups to ask whether they can survive. Chen's answer is that agents do not inherently have network effects, that the next generation can design them in through viral artifacts and shared context layers, and that the consequential fight is over whether those layers end up proprietary to a few horizontals or open to every agent.

Chen is the a16z general partner whose growth framework is recorded in [[startup-growth-metrics]]. This essay applies that framework's loop taxonomy to a product category he thinks is still at the tool stage.

## The null hypothesis: agents are tools, not networks

Chen opens with the case against winner-take-all. Agents are solo experiences packaged as chat. They do not have the network effects of WhatsApp or the phone system. The right analogy is the email client: one person uses Superhuman, another Outlook, another Gmail, and they still send each other email. If a Muse agent meets an Instinct agent they will build an API or use email and messaging to talk, so there is no advantage to everyone running the same one. Three further points weaken the case for lock-in:

- The underlying model is swappable. Chen cites "the Claude vs Clawdbot saga" as evidence that an agent keeps working when its LLM is replaced.
- Memory and context "are just text files," and AI is good at porting them between systems.
- The new products are themselves thin wrappers: polished, secure, consumer-friendly packaging over the capabilities of OpenClaw and Hermes.

The conclusion he draws is a definitional one. "Better models, UX, integrations, memory, and distribution might create very large companies, but those are not network effects."

## Decomposing the question by KPI

Rather than treat network effects as one amorphous property, Chen overlays them on the metrics a product has to move:

| Effect | "More users" means |
|---|---|
| Acquisition | lower CAC, higher virality, more signups |
| Engagement | higher retention, deeper usage, more frequency |
| Monetization | higher ARPU, higher conversion, more share of wallet |

He adds a footnote that matters for the rest of the argument: "more users" means higher network density and more interconnection, not scale. The essay then works through acquisition and engagement in detail. Monetization appears in the table and nowhere else.

## Acquisition: agentic viral loops

Pre-AI viral loops were driven by users taking actions that pulled in other users, such as sending an invite, sharing content, or being mentioned. Chen's claim is that in the agent era both users and agents can initiate these loops. An agent might offer to organize a family New Year's party, assemble a group chat with siblings and in-laws, build a microsite for RSVPs, and so create a signup opportunity. At work, an agent that helped finish a slide deck might offer to set up the meeting, write the prep doc, take notes, and host it all on a microsite others have to visit.

**What the loop requires.** Access to contacts, enough context to know whom to loop into which project, and access to the communication channels where potential users can be reached. Chen calls those channels "the viral substrate for propagation." The hard part is doing this without being creepy and with enough trust that the agent can reach out on the user's behalf. His negative example is an agent that sends "Andrew would like to get lunch next week" followed by "and sign up for this agent to agree!"

**The content creation loop, replayed.** Many workplace viral loops were content loops: make a thing in Google Slides, share the link, people view it, eventually they make their own. Figma, Notion, spreadsheets, YouTube, and Instagram all run on it. Chen's agentic version: you discuss interior decoration with your agent, it builds you a Pinterest-like board or a mini spreadsheet app with a budget and schedule, and it offers to share that into a group chat, where viewing requires the recipients to get an agent of their own.

**The walled-garden incentive.** Two things follow if the content loop works. First, every agent has an incentive to volunteer visually appealing, shareable artifacts, often, because codegen makes one-off disposable artifacts cheap. Second, the agent should host the artifact itself rather than create a Pinterest board or a Google Sheet, because a self-hosted artifact spreads the agent and a Google Sheet spreads Google. "A properly tuned agentic viral loop will do the former." Chen states this as an incentive, not a recommendation, and it is the seed of the essay's closing section.

**A different viral factor.** Chen's earlier work on viral loops held that getting the viral factor above one depends on reducing friction at each step, inviting enough people, and building on a high-conversion channel. Agentic loops break that model. Friction is near zero, because the agent shares for you. Reach is unbounded, because the agent can pick recipients and in principle publish to millions. The binding constraint moves to the recipient: "the 4th time your sister gets the message 'hey I'm X, andrew's agent, and he wants you to try using an agent too!' you'll get an annoyed text and you'll stop using that agent." The channel itself will degrade as people filter agents and, Chen expects, as agents filter other agents in self-defense. He predicts some products, probably free ones aimed at less sophisticated users, will push past that line and survive the way popup-laden websites do.

**Why it can still be tasteful.** A high-retention agent gets many shots on goal. The first invite, to coordinate photos or calendars, can fail. Later the friend shares a genuinely useful microsite for a project or an event, the recipient signs up to leave a comment, and eventually tries the rest.

## Engagement: does your agent get better when others use the same one?

Chen separates two claims that are easy to conflate. Ubiquitous agents will raise engagement in agents generally: scheduling and meeting-note sharing become instant when humans are removed from the loop, and agents that succeed at multi-user coordination get used more. That is a category effect, not a network effect. The network-effect question is narrower: does *your* agent improve when the people around you run the *same* agent?

The argument for no is the email argument again. If every agent runs on a frontier model and can reach every other agent through email, calendars, APIs, and connectors, then organizing a dinner party works fine across heterogeneous agents.

The argument for yes is that some tasks benefit from centralization, because centralization supplies trust, speed, identity, and discovery:

- "Who are 10 people in San Francisco that I should meet?" Agents cannot find an optimal answer by asking each other one at a time.
- "Find me a VP of Engineering who isn't publicly looking, but would leave for a fast-growing startup that pays X in stock." Mixed public and private information, and a passive candidate's agent may lie to an untrusted asker.
- "Who's a trustworthy seller of X?" Reputation can be gamed, so a global source of truth may beat pairwise inquiry.
- "Pick the best dinner in the next 5 minutes for my friends and their +1s, with allergies, schedules, and locations." Real-time solving over shared context.
- All of the above, more so, once some agents lie or exaggerate on their humans' behalf.

For these, Chen can imagine Muse or Town building a shared network-and-context layer: a system of record for identity and trust that does multi-sided matching, understands the relationship between public and private data, and admits only its own agents. Contributors make the network more useful and the network makes their agent more useful. That is a genuine engagement network effect.

His counter to his own counter is that the same layer can be built one level up, by startups shipping agent-facing point solutions: a next-generation eBay any agent can sell through, which holds reputation and identity at that layer rather than inside any one agent. He expects both to happen, as every large company adds chat, commerce, and search while pure plays exist for each. His verdict on that outcome: "more fragmentation than a true winner-take-all."

## Where will the network effects live?

The essay's final move is to replace its title question with a better one. Some agents will have network effects. The consequential question is where those effects sit. Chen sketches two worlds.

**Open-web world.** Identity becomes an open protocol, reputation lives in marketplaces, commerce goes through an agent-native eBay, professional discovery through an agent-native LinkedIn. Agents remain interchangeable clients on top of a constellation of networks, "much as browsers and email clients do today." Enormous network effects emerge around agents without a winner-take-all market for agents. Thousands of agents compete on intelligence, personality, UX, specialization, and price. Vertical agents thrive.

**Walled-garden world.** A few horizontal agents accumulate identity, relationships, private context, reputation, latent intent, and distribution, and keep them proprietary. Switching agents then means leaving your network behind.

Chen's prediction is a fight over exactly this boundary. Every horizontal agent will try to pull network functionality inside its walls: host the artifact instead of creating a Google Doc, execute the transaction instead of sending you to Amazon, make the introduction instead of searching LinkedIn, create the event instead of using Partiful. "Every time it does this successfully, it converts somebody else's network effect into its own." Every incumbent network and a new generation of startups has the opposite incentive, which is to be universally accessible to every agent so that no horizontal can recreate and capture them.

## Reading it against the rest of the wiki

**The direct rebuttal to "one agent each."** Ben Thompson's [[agents-as-aggregators]] predicts that most people will have one agent because agents "operate better the more context they have about you," and that distribution will decide which one. The wiki's note on that essay already observed that per-user context is a switching cost rather than a network effect. Chen makes the same distinction the center of his argument and goes further: the context is text files and AI ports text files, so even the switching cost is thin. Thompson's Aggregator and Chen's walled-garden horizontal are the same company seen from two sides. Thompson describes what it would win; Chen describes the mechanism it would have to run, converting other people's networks one artifact and one transaction at a time, and the counter-incentive every supplier has to stay open. The two essays agree that distribution creates large companies. They disagree on whether that produces one winner, and Chen's answer depends on whether the network layers stay open.

**Groove-in effects, named.** Tren Griffin's taxonomy in [[network-effects]] warns that most software moats are "groove-in effects," Brian Arthur's term for learned-habit switching costs that decay as new tools learn the user automatically. Chen's "memory and context are just text files" is that decay observed in real time. Griffin's tipping criterion also cuts against agent winner-take-all: markets tip when scale economies are large *and* demand for variety is low, and Chen's open-world agents compete on personality and specialization, which is high variety demand. Griffin's Ethernet example, strong network effects that no one captured, is the open-web world in miniature: the effects exist, the standard wins, the clients commoditize.

**Benedict Evans agreed first, at the model layer.** [[ai-platform-moats]] argued that chatbot features like memory give stickiness but no network effect and are copied within weeks. Chen accepts that for the agent as a tool and asks the next question, which features *would* create one. His answer, viral artifacts and shared identity-reputation layers, is a list of things Evans would recognize as real network effects, because they make the product better for each user as density grows rather than merely harder to leave.

**Graham's lever, from both sides.** Paul Graham's [[startup-power]] tells founders to induce network effects by generalizing the idea (a tool for agents to pay for things becomes a marketplace if agents can pay each other) and to become the platform by proposing standards and shipping APIs for agents. Chen's open-protocol world is that lever pulled by many startups at once. His walled-garden world is the same lever pulled by a horizontal with distribution. Graham's constraint, that every lever must be better for the customer, is also Chen's constraint on agentic virality: the loop only runs while recipients are glad the artifact arrived.

**Content loops with a new author.** Kevin Kwok's [[data-content-loops]] describes publishing a page per entity so that search converts content into free acquisition, as kindling for later network effects. Chen's agentic content loop has the same shape with the agent as the content producer and the group chat replacing search as the channel. The difference is that Kwok's pages are indexed by a neutral third party, while Chen's artifacts are hosted by the agent that made them, which is why the loop pulls toward walled gardens.

**The viral substrate is Moore's affordances list.** Justine Moore's [[messaging-as-ai-interface]] argued that agents need whatever a human in the role would have: a phone number, an email address, a card. Chen's "viral substrate" is the same requirement stated as a growth input. Moore's deliverability point is also the first appearance of Chen's limit: the channel that lets an agent reach your sister is the channel that carrier filters, and later agents, will learn to block.

**Marketplaces and the lying-agent problem.** Chen's engagement examples are marketplace matching, and they pass Griffin's coordination test in [[multi-sided-markets]]: a matching problem that pairwise negotiation cannot solve. The new ingredient is adversarial agents. An agent that lies on its principal's behalf is a reputation problem for the marketplace to solve, which is Chen's case for a central system of record. It is also, from the other direction, the trust question in [[lethal-trifecta]]: an agent that accepts inbound messages from other agents, holds private context, and can act on it is exposed to manipulation, and the agent-filters-agent future Chen predicts is a defense against that as much as against spam.

**Commoditizing the complement without the complement's consent.** [[commoditize-your-complement]] explains why a company cheapens what is bought alongside its product. A horizontal agent hosting its own artifact instead of a Google Doc is commoditizing Google Docs. The incumbents' counter-move, opening every network to every agent, is the same logic reversed: make the agent the commodity and keep the network. Chen's "fight over the boundary" is both sides running Spolsky's playbook against each other.

**The barbell's missing moat.** Mike Vernal's [[software-industry-barbell]] holds that zero production cost erodes replication, switching, and integration moats, leaving only cumulative reinvestment. Chen agrees that models, UX, and memory are not moats and proposes that network effects, which Vernal lists among the eroding ones, can be rebuilt deliberately at the identity and reputation layer. Both leave the same open question, whether that layer belongs to the agent or to a service the agent calls.

## Implications the essay leaves implicit

- **An agent spends its principal's social capital.** Chen's constraint on agentic virality is recipient tolerance, not friction. That makes the viral factor a function of how much goodwill each user has with each contact and how much the agent burns per message. An agent optimizing for growth is drawing down an account that belongs to the user, which is why Chen expects the tasteful version to be gated on retention: a product people keep using is the only one trusted to spend that account slowly.
- **The point-solution bet is a bet on openness.** Chen's agent-native eBay or LinkedIn thrives in the open world and gets absorbed in the walled one. A vertical agent or an agent-facing network is therefore not a hedge against the horizontals; it is a wager that identity and reputation stay outside them. This is an inference from the essay's two worlds, not a claim it makes.
- **Hosting the artifact makes the agent a content platform.** Pulling the microsite, the board, and the event inside the walls brings the moderation, retention, and discoverability obligations of a content host. The essay treats hosting as a growth tactic only.
- **Monetization is the undeveloped third.** Chen lists monetization network effects and never returns to them. The open-world agents he describes compete on price, which suggests the monetization effects, if any, would also live in the marketplaces rather than the agents.

## Caveats

- Single opinionated source. Chen is a venture investor in consumer growth companies and the essay is argued from analogy rather than data.
- The products named (Muse, Town, Instinct, Grokbot, OpenClaw, Hermes) and the "Claude vs Clawdbot saga" are referenced without explanation. Muse is Meta's agent per [[agents-as-aggregators]]; this article repeats only what the essay says about the others.
- The engagement examples assume agents will negotiate with strangers' agents over private information. The essay does not address how a user authorizes that, or what an agent is permitted to disclose.
- "Both will happen" is offered as the most likely outcome for the engagement layer, which makes the essay's two-world framing a spectrum rather than a fork. Chen's own prediction is a contested boundary, not a resolved one.

## Sources

- Chen, Andrew (2026-10-05). "Will agents have network effects?" *andrewchen.substack.com*. <https://andrewchen.substack.com/p/will-agents-have-network-effects> — [[2026-10-05-agent-network-effects|local copy]]
