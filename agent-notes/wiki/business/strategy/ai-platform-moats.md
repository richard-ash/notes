---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-02-19-how-will-openai-compete.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: medium
---

# AI Platform Moats

Do foundation model companies have defensible competitive positions? Or are they building commodity infrastructure without the network effects, lock-in, and ecosystem dynamics that made previous tech platforms dominant? Evans argues that OpenAI's strategic position is far weaker than its scale suggests, and that the platform analogies the company reaches for don't hold up.

## The four strategic problems

Evans identifies four fundamental challenges facing OpenAI (and, to varying degrees, other AI-native companies):

1. **No unique technology.** Half a dozen organizations ship competitive frontier models. They leapfrog each other every few weeks. No known mechanism exists for one company to build an insurmountable lead — unlike Windows, Google Search, or iOS, where market share was self-reinforcing.

2. **Wide but shallow engagement.** ChatGPT has 800-900 million users, but these are weekly actives with thin engagement. Only ~5% pay. 80% sent fewer than 1,000 messages in all of 2025 (roughly three prompts per day at best). OpenAI acknowledges this as a "capability gap" — Evans reads this as a euphemism for lacking product-market fit.

3. **Crossing the chasm without distribution.** Unlike Google or Meta, OpenAI has no existing product base to make AI a feature of. It must compete in one of the most capital-intensive industries ever without legacy cashflows, while incumbents who *do* have them are closing the technology gap.

4. **Research-driven roadmap.** Product leadership at AI labs doesn't set strategy — they receive breakthroughs and turn them into buttons. Fidji Simo (OpenAI's head of product) describes researchers pinging her with "something pretty cool" to figure out how to ship. Evans contrasts this with Jobs's dictum to start with the customer experience and work backwards to the technology.

## The chatbot-as-browser analogy

Evans draws a pointed comparison between chatbots and web browsers: both are fundamentally an input box and an output box. Browsers proved nearly impossible to differentiate — the last meaningful product innovations were tabs and the merged search/URL bar. Chatbot apps face the same problem. Features like "memory" provide stickiness but not network effects, and every competitor copies them within weeks.

The Netscape parallel is instructive. Microsoft used distribution to win the browser war, but winning browsers turned out not to matter — value was created elsewhere. Evans suggests the same dynamic may apply: even if ChatGPT "wins" the chatbot category, the experiences and value capture that matter may be built by others on top of generic model APIs.

## Capex as table stakes, not moat

OpenAI has claimed $1.4 trillion and 30 gigawatts of future compute commitment (no timeline), with 1.9 GW in use at end of 2025. Evans frames this as Sam Altman trying to will OpenAI a seat at a table that may require $200B+ in annual infrastructure spending — an oligopoly driven by rising fixed costs (analogous to Rock's Law in semiconductors, where fab costs doubled every four years even as per-transistor costs fell).

But Evans argues a seat at the table isn't a moat. TSMC has a *de facto* monopoly on cutting-edge chips, yet captures little value further up the stack. Nobody builds "TSMC apps" or "Intel apps." Similarly, end users of AI-powered products don't know or care which foundation model powers them, just as Snap users don't care whether the app runs on AWS or GCP.

## The platform fallacy

OpenAI aspires to be a full-stack platform — chips, infrastructure, models, APIs, app ecosystem — citing Bill Gates's definition that a platform creates more value for partners than for itself. Evans argues this misapplies the platform analogy:

- **Windows/iOS worked** because developers *had* to build for the platform with the users, and users *had* to buy the platform with the developers. This was a genuine network effect.
- **Foundation model APIs lack this lock-in.** If a developer builds a product using OpenAI's API, switching to Gemini or Claude is far easier than porting an iOS app to Android. AI itself may even lower switching costs by generating integration code.
- **The "widget fallacy"** — the recurring tech belief that complex products can be abstracted into simple standard interfaces — tends to fail in practice. Exception cases quickly demand the full product UI. And incentives are misaligned: no company wants to be "someone else's dumb API call."

## Power vs. platform

Evans concludes by reaching for a more precise term than "platform": **power**, defined (via his medieval history professor Roger Lovatt) as the ability to make people do something they don't want to do. Microsoft, Apple, Facebook, and Amazon had this — structural positions that compelled participation regardless of individual preference.

OpenAI does not have this. Foundation models are multipliers that will enable enormous amounts of new creation, but Evans sees no mechanism that forces everyone to build on *one company's* models. Without that, the only advantage is execution — doing it better every day. That's an aspiration, not a strategy.

## Implications

The essay has several broader implications beyond OpenAI specifically:

- **AI-native companies face a structural disadvantage** against incumbents who can make AI a feature of existing products with existing distribution (Google, Meta, Microsoft, Apple).
- **Capital intensity may create an oligopoly** of foundation model providers (analogous to Boeing/Airbus or TSMC), but oligopoly doesn't guarantee margins — it may just be commodity infrastructure sold at marginal cost.
- **The "second step" of AI** — new experiences, products, and business models built on top of raw models — is where value will be created and captured. Who builds that is the real strategic question, and there's no reason to assume it's the model providers.
- **Standards as competitive weapons** (the "embrace and extend" playbook) may give temporary leverage to whoever controls inter-service protocols, but low switching costs between AI platforms undermine durable lock-in.

The analysis connects to [[aggregation-theory]], which addresses how zero-distribution-cost platforms commoditize supply and own demand. Evans is essentially arguing that foundation models don't meet the aggregation test: they can't own demand because the consumer relationship sits elsewhere, and they can't commoditize supply because they *are* the supply being commoditized.

## Sources

- Evans, Ben (2026). "How will OpenAI compete?" <https://www.ben-evans.com/benedictevans/2026/2/19/how-will-openai-compete-nkg2x> — [[2026-02-19-how-will-openai-compete|local copy]]
