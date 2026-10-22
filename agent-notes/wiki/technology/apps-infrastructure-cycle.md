---
source: agent
compiled_from:
  - agent-notes/raw/technology/2018-10-01-grant-grossman-myth-of-the-infrastructure-phase.md
  - agent-notes/raw/technology/2021-09-13-mccormick-the-interface-phase.md
compiled_at: 2026-10-21
model: claude-fable-5-1
confidence: medium
---

# Apps-infrastructure cycle

Dani Grant and Nick Grossman of Union Square Ventures argued in October 2018, during a crypto winter, that web3 was not in an "infrastructure phase." Historically, they claimed, apps come first and inspire the infrastructure that lets them scale, which then enables the next apps: "apps beget infrastructure, not the other way around." Packy McCormick picked the essay up in September 2021, at the peak of the NFT boom, and added a third term: new epochs also need new **interfaces**, so the internet runs apps-infrastructure-interface supercycles, and "web3 needs web3 interfaces." Both are venture-investor arguments about crypto, but the pattern is general, and the cleanest test of it since 2021 came from a technology neither essay was watching.

## The USV argument

The puzzle Grant and Grossman start from: founders building crypto infrastructure said their hardest problem was getting developers to build apps on top. If this were really an infrastructure phase, why would that be? Their hypothesis is that platforms "evolve from an iterative cycle of apps=>infrastructure=>apps=>infrastructure and are rarely built in an outside vacuum." The rush to build infrastructure anyway comes from everyone knowing that platforms capture the largest value (Facebook, AWS, Twilio), a belief that is "even more true in the distributed web where value often... accrues in the protocol layer."

Their evidence is a set of sequences:

| Platform | Breakout app | Infrastructure it inspired |
| --- | --- | --- |
| Electricity | Light bulb (1879) | Electric grid (from 1882) |
| Aviation | Airplane (1903) | Airlines (1919), airports (1928), air traffic control (1930) |
| Internet, turn 1 | Messaging (1970), email (1972) | Ethernet and TCP/IP (1973), ISPs (1974) |
| Internet, turn 2 | Portals: Prodigy (1990), AOL (1991) | Search engines and browsers (early 1990s) |
| Internet, turn 3 | Amazon.com (1994) | PHP (1994), JavaScript and Java (1995) |
| Internet, turn 4 | Napster (1999), Pandora (2000), Gmail and Facebook (2004) | NGINX and Rails (2004), AWS (2006) |
| Mobile video | Snapchat (2011), Periscope (2014), Meerkat (2015), Instagram Stories (2016) | Ziggeo and Agora (2014), Mux and Twilio Video (2017), Cloudflare Stream (2018) |
| Crypto | Bitcoin (2008), Silk Road (2011); then ICOs and CryptoKitties (2017) | Sidechains, ERC20, Lightning (2015); Coinbase (2012), MetaMask (2016); Infura (2016), web3.js and Zeppelin (2017) |

Three ideas do the explanatory work. First, Steven Johnson's **adjacent possible**: you can open the door to the next room but not the back door from the front porch, so infrastructure built too far ahead of real apps is speculative and tends to fail. YouTube could be built in 2005 but not 1995 because broadband was laid down after the first hit dot-coms; Chris Dixon's *Dot Bomb* board game mocks ideas that became unicorns a cycle or two later. Second, **falling costs**: each turn makes the next apps cheaper, so building usv.com in 1995 cost orders of magnitude more than it would today, and web3 apps will be far cheaper in fifteen years. Third, the honest caveat that this is a **development framework, not an investment framework**: the cycle explains when something can be built, not when it is a good investment. "No one sold a lot of lightbulbs until the grid was in place."

Why apps first? Because "it doesn't make sense to create infrastructure until there are apps asking you to solve their infrastructure problems." Their October 5 update conceded that the crypto diagram was thin and Ethereum-centric, and added the feedback they liked best: open, interoperable crypto networks blur apps and infrastructure, since any contract can become infrastructure the moment someone builds on it, which only tightens the cycle.

## McCormick's extension: the interface term

McCormick opens with Churchill's 1943 argument for rebuilding the bombed Commons as an adversarial rectangle rather than a horseshoe ("We shape our buildings; thereafter, they shape us") and substitutes interfaces for buildings. Writing while the cycle was visibly turning (OpenSea volume went from $950M in February–July 2021 to $4.8B in the first six weeks of August–September; gas fees over $300 during hot drops; Arbitrum launching and Polygon holding $2.4B in TVL), he argues that infrastructure was catching up but interfaces were not. OpenSea "could have been built in 2015 or even 2010. eBay has been around since 1995."

His history of interface cycles, drawn partly from Murphy's timeline in [[internet-access-history]], is the strongest part of the essay:

- **Web 1.0.** The pre-web internet was text and "only welcoming to techies." Netscape's graphical browser pulled people in: 16 million internet users at its 1995 IPO, 361 million in 2000, 745 million when Facebook launched in February 2004, a billion by the end of 2005.
- **Web 2.0.** The read-write web needed infrastructure laid by the Web 1.0 bubble (Brian McCullough's figures: $1.6 trillion raised by telecoms, 80.2 million miles of fiber, 76% of all US base digital wiring to that point) plus wifi, but adoption came from the real-time interactive interfaces of Facebook, YouTube and Twitter. Blogger and MySpace were proto-Web 2.0; MySpace peaked just over 100 million users, Facebook passed two billion.
- **Mobile.** WAP (1999) and 3G (2003) were infrastructure; the iPhone (2007) and App Store (2008) were the interface. "Mass users need new interfaces to adopt new computing platforms."

Where web3 stood in 2021: roughly 100 million bitcoin owners, 56 million Coinbase users, 10 million MetaMask wallets. "At best... we're at MySpace usage levels. At worst... we're near 1995 internet adoption levels." Money baked into the protocols let web3 bootstrap demand further ahead of user experience than past paradigms, but not far enough to cross the chasm.

His rubric for a paradigm-shifting interface is reusable independent of crypto. It must:

1. abstract away complexity;
2. give users easy access to most of the new technology's power;
3. wrangle the entropy the new technology creates;
4. create experiences not possible through previous interfaces.

His guesses at the web3 interface were **wallet-first** (the wallet as passport, bank account and portable inventory, after John Palmer's "the internet is now a place where everyone has an inventory"; Playground, Collab.Land, Station, a rolled-up decentralized identifier), **3D spaces and worlds** (Cyber's NFT galleries, Decentraland, The Sandbox, Somnium Space: "the web3 interface will be digital worlds accessed via wallets"), and **physical-digital bridges** (NFTs as a scrapbook of concerts and marathons, social tokens replacing loyalty programs). Desktop first, then a seamless mix with VR and AR. He flagged the caveat himself: "I am not a designer, or an engineer, or even that smart."

## Reading the two essays together

- **The cycle is a demand-discovery mechanism.** Infrastructure is a bet on which app pattern will repeat; the only reliable way to learn the pattern is to watch apps strain. That is why the USV authors insist the cycle "keeps us honest," and why their investment caveat matters: discovering what can be built is not the same as owning what gets built.
- **The interface is where demand is controlled.** Each interface McCormick names (Netscape, Facebook, the App Store) became the aggregator of its era in Thompson's sense ([[aggregation-theory]]). "Web3 needs web3 interfaces" therefore also means "someone will own web3 demand," which sits awkwardly with the decentralization the interface is supposed to serve. McCormick half-notices this with Cyber: ownership decentralized, discovery centralized.
- **Who captures the value is a separate question.** USV's premise that value accrues at the protocol layer held in crypto, where the protocol is the asset. The case studies in [[commodity-trap]] argue the opposite for most infrastructure (fiber, railroads, cloud inference), and [[ai-value-capture]] makes the same argument for AI models. The cycle says nothing about this; it only orders the building.
- **The chicken-and-egg underneath** is the ecosystem-level version of the bootstrap problem in [[network-effects]] and [[multi-sided-markets]].
- **Bubbles lay the infrastructure for the next turn.** McCormick's fiber figures are the Perez point in [[technological-revolutions]]: the frenzy overbuilds, deployment inherits the glut cheaply.

## Temporal notes

- **The web3 interface McCormick forecast did not arrive.** NFT volumes collapsed through 2022 and fell by well over 90% from peak; Decentraland and The Sandbox stayed sparsely populated; Meta's Reality Labs lost more than $10B a year on the metaverse ($13.7B in 2022, rising to $19.2B in 2025) while the company's emphasis moved to AI; Apple's Vision Pro sold roughly 400,000 units in 2024. The crypto products that reached mainstream scale were the most web2-like: Coinbase, spot bitcoin ETFs (January 2024), and dollar stablecoins, which by the end of 2025 had about $300B outstanding, the industry's clearest product-market fit, and federal legislation (the GENIUS Act, July 2025). Those abstracted complexity by removing self-custody, the solution McCormick judged "unlikely to ultimately win."
- **The cycle got its cleanest demonstration from AI.** ChatGPT (November 2022) was the breakout app; the infrastructure wave followed it (GPU clusters, inference serving, vector databases, evaluation and agent tooling; see [[ai-capex-required-returns]] and [[token-pricing]]); and the chat box was a new interface that meets all four of McCormick's criteria. "We shape our interfaces; thereafter, they shape us" applies here too: chat shaped the expectation that AI is a conversation, which [[intelligence-augmentation]] argues under-rates interface design as a lever and which the current fight over messaging and agents ([[messaging-as-ai-interface]], [[agents-as-aggregators]]) is about.
- **Infrastructure ahead of apps did happen in AI.** Compute was built before the applications that would fill it. Grant and Grossman would call that a speculative vacuum; the optimistic readings are Brooks's overbuild-as-hidden-upside in [[ai-robotics-hype-cycles]] and the Perez deployment gift in [[technological-revolutions]].
- McCormick's 4.66 billion internet users (2021) had become roughly 5.5 billion by 2024 ([[internet-access-history]]).

## Sources

- Grant, Dani and Grossman, Nick (2018-10-01). "The Myth of The Infrastructure Phase." Union Square Ventures. <https://www.usv.com/writing/the-myth-of-the-infrastructure-phase> — [[2018-10-01-grant-grossman-myth-of-the-infrastructure-phase|local copy]]
- McCormick, Packy (2021-09-13). "The Interface Phase." Not Boring. <https://www.notboring.co/p/the-interface-phase> — [[2021-09-13-mccormick-the-interface-phase|local copy]]
