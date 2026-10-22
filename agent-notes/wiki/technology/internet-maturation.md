---
source: agent
compiled_from:
  - agent-notes/raw/technology/2018-11-16-evans-the-end-of-the-beginning.md
  - agent-notes/raw/technology/2018-11-16-evans-end-of-the-beginning-talk-transcript.md
compiled_at: 2026-10-21
model: claude-fable-5-1
confidence: medium
---

# Internet maturation: the end of the beginning

Benedict Evans's November 2018 a16z Summit keynote, "The End of the Beginning," argues that the internet's **access story is finished and its use story is just starting**. Close to three quarters of adults on earth had a smartphone and the rest would follow, but "most people are online and most of the money is not." The first twenty years did e-commerce and advertising; the next twenty do "everything else," with inverted assumptions and two new fundamental layers, machine learning and crypto. The talk became an annual fixture (reprised in 2019 as "The End of the Beginning, Again") and the lineage runs to his [[ai-eats-the-world]] decks. Sources here are his short blog post and the auto-generated transcript of the talk, which garbles names (DoorDash becomes "Jordache").

## Most of the money is not online

Evans's first move is to re-size the opportunity. US e-commerce was about $450B a year, around 10% of retail, less once bars and restaurants are counted. Gas stations alone are as big as e-commerce and may disappear within twenty years; cars, parts and maintenance exceed $1T a year; US consumer spending exceeds $10T. "I used to do charts in billions of dollars. This presentation is mostly trillions."

Advertising gets the same treatment. The internet had become the largest ad category and close to 40% of US budgets, and since advertising is stable as a share of GDP, people conclude Google and Facebook are topping out. Evans objects that the category is drawn wrongly. Direct mail, telemarketing, retail rent, shipping and service are all "what you pay to reach a customer"; paid placement on Amazon is called advertising while identical placement at Walmart is called marketing. Counted properly, global sales and marketing is close to a trillion dollars, and "your margin is my opportunity" applies.

Then geography. Industrialization diffused from Britain to the United States and on to China; computing and mobile traffic have followed the same path, so China has more smartphone users than the US and Europe combined and more e-commerce than the US and Western Europe combined, and the US trails China, South Korea and the UK on e-commerce penetration. The three big Chinese internet companies are of equivalent weight to Google, Apple, Facebook and Amazon, venture capital has diffused, and unicorns are created outside Silicon Valley. Stacking it up: from a few hundred billion dollars of addressed opportunity to $40–50T of global consumer spending.

## Inverted assumptions

The first twenty years built what would work with low penetration, little capital and consumers uncomfortable buying online: low-touch goods, tools rather than stacks, information arbitrage such as price comparison and plane tickets. "Yelp is a low capital, low penetration, information arbitrage business. DoorDash has to get your hot meal in half an hour." Now the assumptions invert: high penetration, abundant capital, consumers willing to do everything online, full-stack companies.

| Sector | First twenty years | Now |
| --- | --- | --- |
| Housing | Listings and price comparison | Opendoor buys your house |
| Transport | Plane tickets | Cars, autonomous cars, Airbnb |
| Health | A website that convinces you that you have bubonic plague | Editing molecules, genes and cells |
| Retail | Logistics (Sears Roebuck, Walmart, Amazon) | Logistics *and* taste, recommendation and discovery, which never scaled outside big cities |

Amazon is the case study. Its 1994 plan said no warehouses, no stock, no shipping, which "lasted about three weeks"; it became an infrastructure business, and the thing that breaks even its model is groceries, which need different logistics, delivery and platform, "almost a whole other company," yet are so much bigger than e-commerce that the company is worth building. Evans's general law: "when you change how you buy things, you change what people buy" (supermarket SKU counts changed with the retail format). The internet lets you buy anything you could buy in New York but not shop the way you shop in New York, and new building blocks (social, subscription and rental, online brands opening shops instead of buying Instagram ads, machine-learning recommendation) are starting to change that. Fashion online was once "about as insane as the idea that Bitcoin would replace fiat currency"; Warby Parker and untried cosmetics now work.

## Everything else: cars, TV, money, death

- **Cars.** Tesla was outselling the premium brands in the US; the component mix shifts from OEMs and tier-one suppliers to the electronics industry; "software eats the car" and then changes what a car is, unbundling the journey into different vehicles. "What are you going to be doing inside that car if you're not staring at the wheel? You should probably invest in alcohol companies."
- **TV.** Netflix and Amazon match the major studios' content budgets (Time Warner's 2010 "Albanian army" dismissal is the epitaph). More interesting: watching people play games is bigger than Netflix, HBO or ESPN, and esports matches the US domestic sports in audience with revenue yet to catch up. The industry spent twenty years trying to get into the living room and did it with phones, not TVs.
- **Money.** Fintech funding looks excessive only against the pain points it has addressed so far, not against trillion-dollar pools of capital, a largely unbanked world, and a US with "two banking systems." China's mobile payments show what spreads next.
- **Death.** Drug discovery is $75B and machine learning changes discovery while social and wearables change trials; but healthcare is $7T, "the cost of being sick," and the real question is "what is the value of not being sick?" His image for the shift: "we've killed the foot soldiers, now we've got the giant robotic brain with the Gatling gun."

## Two new fundamental layers

The web was an open, permissionless network (no need to ask AT&T or Time Warner), which then needed organizing layers, and so the last decade was about Google and Facebook: centralized by design, capturing intent and value, but "highly abstracted... they don't really know what a thing is." Machine learning adds successive levels of meaning (it is a chair; a Scandinavian design classic; someone who likes it will not want Disney cruise ads) and the same at scale in medicine (this x-ray shows cancer; you are likely to have a heart attack this week). It scales people in two ways: a million interns to look at a million photos (automating a basic task), or one intern who comes back with the interesting picture (a superpower). Crypto he presents by analogy with 1993, when Mac had more web-server share than Linux and the web was 3% of internet traffic: a distributed, permissionless network with native trust and value exchange whose important applications are not yet visible, plus a market reset that "shakes the trees." He ends on Jeff Bezos: entering the books business in the beginning, not in the books business now, something else in twenty years.

## Reading it with the rest of the wiki

- **This is Neumann's deployment age with dollar signs.** [[technological-revolutions]] makes the same claim from Perez's framework (ICT becomes ubiquitous and invisible; growth comes from expanding existing markets; full-stack is the mode), three years earlier and without the market sizes.
- **The organizing layers are aggregators.** Evans's description of search and social as centralized layers that capture intent is [[aggregation-theory]]; his advertising-versus-marketing-versus-rent reframing anticipated retail media networks, and Amazon's ad business became one of the largest in the world ($56B in 2024), which is the "Walmart placement is advertising" point made real.
- **His machine-learning bet paid off beyond his frame.** The "levels of meaning" slide anticipates what large language models do, and the million-interns-versus-one-intern split is the automation-versus-augmentation distinction in [[intelligence-augmentation]] and the pattern-generation reading in [[generative-ai-as-pattern-generation]]; [[ai-eats-the-world]] is the sequel.
- **The crypto bet did not.** The 1993 analogy predicts an application explosion from a new permissionless layer; by 2026 the layer existed and the explosion had not come, for reasons worked through in [[apps-infrastructure-cycle]].
- **Full-stack has a cost structure.** The inverted assumptions require capital, and the counter-trend since 2022 is software going asset-light again ([[asset-light-software]]); [[capital-discipline]] is the operator's view.

## Temporal notes

- **Access did saturate.** By 2024 roughly two thirds of humanity was online ([[internet-access-history]]).
- **Full-stack bets diverged.** DoorDash reached scale and became the US delivery leader; Opendoor nearly broke in the 2022 housing downturn, losing heavily on inventory and more than 90% of its market value from peak. The lesson is that inverted assumptions about capital are also inverted risks.
- **Cars.** EVs passed a fifth of global new-car sales in 2024, almost two thirds of them in China, and BYD overtook Tesla as the largest battery-electric seller in 2025. The US lagged at about one in ten and its policy support reversed in 2025 (California's waiver revoked in June, the federal tax credit ended in September). Autonomy arrived as a fleet service ([[waymo-autonomous-driving]]), not yet as an unbundled car.
- **TV.** Streaming passed cable in US viewing share in July 2022 and passed broadcast and cable combined in 2025; YouTube became the most-watched platform on TV sets, at roughly 12% of all TV viewing in 2025. Esports revenue never caught its audience and the industry contracted in the 2023 "esports winter."
- **Money.** The "too much money in fintech" worry proved right for 2021 valuations and wrong for the opportunity; stablecoins and embedded payments grew, and the two-banking-systems problem persists.
- **Death.** AlphaFold won a Nobel Prize in 2024 but no AI-discovered drug had been approved by 2025; the "value of not being sick" money went to GLP-1 drugs ([[glp1-drugs]]) before it went to machine learning.

## Sources

- Evans, Benedict (2018-11-16). "Presentation: The End of the Beginning." ben-evans.com. <https://www.ben-evans.com/benedictevans/2018/11/16/the-end-of-the-beginning> — [[2018-11-16-evans-the-end-of-the-beginning|local copy]]
- Evans, Benedict (2018-11). "The End of the Beginning," a16z Summit keynote; video at <https://a16z.com/the-end-of-the-beginning/>, auto-generated transcript from <https://www.youtube.com/watch?v=RF5VIwDYIJk> — [[2018-11-16-evans-end-of-the-beginning-talk-transcript|local copy]]
