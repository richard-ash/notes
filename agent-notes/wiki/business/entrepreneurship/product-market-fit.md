---
source: agent
compiled_from:
  - agent-notes/raw/business/entrepreneurship/2026-11-04-superhuman-product-market-fit-engine.md
compiled_at: 2026-11-04
model: claude-fable-5-1
confidence: medium
---

# Product-Market Fit

**Product-market fit (PMF)** is the state in which a product satisfies a market strongly enough that demand pulls it forward without the company pushing. The canonical descriptions are all retrospective: Paul Graham's "make something people want," Sam Altman's "users spontaneously tell other people to use it," and Marc Andreessen's 2007 passage ("customers are buying the product just as fast as you can make it … investment bankers are staking out your house"). Rahul Vohra's contribution, in a 2018 First Round Review essay about Superhuman, is to argue that these are *lagging* indicators that cannot guide next week's work, and to describe a measured, repeatable process for raising PMF before launch. The essay is the reference most later treatments point to, including Migicovsky's YC lecture summarized in [[customer-interviews]].

## The problem Vohra was solving

Superhuman started coding in 2015, was 14 people by mid-2017, and still had not launched. Vohra's prior company, Rapportive, had launched, scaled and sold to LinkedIn in less time. He refused to "throw it out there and see what sticks," arguing that the launch-and-learn approach is fine after a few months of sunk cost but reckless after two years. The post-launch PMF signals were useless to him: fundraising was easy on his track record, press was being avoided deliberately, and user growth was zero by choice because onboarding was gated. He needed a number that worked pre-launch, both to tell the team honestly where they stood and to give them a path out.

## The Sean Ellis question as a leading indicator

The anchor is Sean Ellis's customer-development survey question: *How would you feel if you could no longer use the product?* with three answers, very disappointed / somewhat disappointed / not disappointed. Ellis benchmarked roughly 100 startups and found that companies that struggled to grow almost always had under 40% answering "very disappointed," while companies with strong traction almost always cleared it. Hiten Shah's 2015 open survey of 731 Slack users returned 51%, at a point when Slack had about half a million paying users, which Vohra reads as evidence of how hard 40% is to beat.

Mechanics Vohra adopted:

- **Who to survey.** Users who have experienced the core of the product recently, following Ellis's rule of at least twice in the last two weeks. Superhuman had 100–200 eligible users at the time; Vohra says results become directionally reliable around 40 respondents.
- **Survey each user once.** Re-surveying the same people would distort the comparison against Ellis's benchmark.
- **Four questions**, each of which feeds a later step: (1) the disappointment question; (2) what type of people would most benefit; (3) the main benefit you receive; (4) how can we improve it for you.

Superhuman's first result was 22% very disappointed.

## The engine: four steps

### 1. Segment by the people who already love it, then describe them

Early users are a mixed bag, especially if the product is free or had press. Rather than narrowing the market by preconception, Vohra uses the very-disappointed respondents as the lens. Each respondent is tagged with a persona; the personas that dominate the very-disappointed group (for Superhuman: founders, managers, executives, business development) define the target, and everyone else is temporarily set aside. Recomputing the score on that segment alone moved Superhuman from 22% to 33%, with no product change.

To make the segment vivid for the team he borrows Julie Supan's **high-expectation customer (HXC)**: not the average persona but the most discerning person in the target demographic, who will value the product for its greatest benefit and spread the word (Airbnb's HXC wants to belong, not just travel; Dropbox's wants their life's work safe). The raw material is question 2, "what type of people would most benefit," asked only of very-disappointed users. Vohra's observation is that happy users almost always describe *themselves* in the words that matter to them, so the answers double as a positioning vocabulary. The resulting profile, "Nicole," runs to two paragraphs: an executive or founder reading 100–200 emails a day and sending 15–40, who considers responsiveness part of the job, hits inbox zero two or three times a week, is open to new tools in general but has a fixed mindset about email and is skeptical anything could make her faster.

Vohra defends the narrowness with Graham: a version-one product can be something many people want a little or something a few people want a lot, and nearly all good startups are the latter; and hill-climbing from a small loved product does not get stuck on local maxima because "most fairly good ideas are adjacent to even better ones." See [[organic-startup-ideation]].

### 2. Learn why they love it, and triage everyone else

Two questions drive the step: *why do people love the product?* and *what holds people back?* For the first, question 3 (main benefit) from very-disappointed users goes into a word cloud; Superhuman's themes were speed, focus and keyboard shortcuts.

For the second, the counterintuitive move is to **ignore the not-disappointed group entirely**. Vohra's reasoning: they will request distracting features, present ill-fitting use cases, be loud, and then churn, leaving a muddled roadmap behind. The somewhat-disappointed group is then split by whether *the main benefit the lovers named* (speed) is also their main benefit:

- Somewhat disappointed, speed not the main benefit: also set aside. Even if you built everything they asked for, the core value does not land for them.
- Somewhat disappointed, speed is the main benefit: the only group whose question-4 answers ("how can we improve") are read closely. Something, probably small, is holding them back.

For Superhuman that something was mainly the absence of a mobile app (a deliberate 2015 bet on desktop-first that had run its course), followed by a long tail: integrations, attachment handling, calendaring, unified inbox, better search, read receipts. Vohra notes that calendaring would never have ranked on the team's own intuitions, because an early-stage team barely uses its calendar.

### 3. Roadmap: half double-down, half unblock

Vohra's rule for resolving the tension: *if you only double down on what users love, the score will not rise; if you only address what holds users back, competitors will overtake you.* So half the roadmap deepens the loved benefit (sub-50ms UI response, instantaneous search, more and pipelined keyboard shortcuts, Snippets for automating typed text, hundreds of small design touches) and half removes blockers for the speed-loving fence-sitters (mobile app, integrations, attachments, calendar, unified inbox, search, read receipts). Prioritization within each half is a low/medium/high cost-versus-impact grid, starting with low-cost high-impact items so improvements ship immediately. Impact on the unblock half is read off request counts; impact on the double-down half has to be intuited, which is where the HXC profile earns its keep.

### 4. Repeat, and make the score the only key result

New users are surveyed continuously (each once), with the very-disappointed percentage tracked weekly, monthly and quarterly through custom tooling, and the product team's OKR had a single key result: that percentage. Trajectory: 22% in summer 2017, 33% after segmenting, 58% within three quarters of roadmap work. Vohra reports that NPS rose alongside it, users became louder advocates, and existing investors began asking to put in more money ahead of rounds.

He also warns the score can *fall* as you grow: early adopters forgive missing features for the sake of the core benefit, while later users demand parity with what they already use. Network-effect businesses get a rising core benefit for free; a SaaS product has to keep improving, so Superhuman rebuilds its roadmap quarterly with the same process.

His two closing takeaways: investors should stop pushing growth ahead of PMF, and once the target score is hit, "push the pedal all the way down and grow as fast as you can."

## Assessment

- **The score measures depth of attachment among the retained, not breadth of the market.** The eligibility filter (used twice in two weeks) already removes anyone who bounced. Forty percent therefore means "of the people still showing up, this share would miss you," which is a different quantity from the flattening retention curve that [[startup-growth-metrics]] treats as the PMF signal. The two are complementary: Chen's curve says how many stay, Ellis's question says how much the stayers care. A product can pass one and fail the other.
- **Segmenting raises the number by construction.** Selecting the personas that already answered "very disappointed" and recomputing is selection on the dependent variable; the 22%→33% step is a target-market decision, not an improvement. Vohra is candid that it took "minimal effort," and as strategy it is exactly what [[design-partners]] recommends (churn cohorts until you find the segment with urgency). The honest baseline for the three-quarter improvement is 33%, and the discipline the method needs is to freeze the segment definition before you start chasing the number, since further narrowing can always manufacture a higher score.
- **Small samples cut both ways.** Forty respondents gives a confidence interval of roughly ±15 points on the headline figure, and the cell that matters most (somewhat disappointed, main benefit resonates) may be a handful of people. The method is defensible as a trend instrument with repeated surveys; a single reading should not be over-read in either direction.
- **It is Mom Test compatible, with one exception handled well.** Questions 1–3 ask about present experience and present benefit, not hypotheticals. Question 4 ("how can we improve") is the kind of feature-request question [[customer-interviews]] warns against, and Vohra's answer is to ask it of everyone but *read* it only from the segment whose core benefit already lands. That filter is what turns feature requests into roadmap evidence.
- **It is a counterexample to MVP orthodoxy, and says so.** Two years and 14 people before launch is the opposite of [[minimum-viable-product]]. Vohra's defense is that sunk cost changes the calculus and that a gated onboarding queue can stand in for the market as a test population. The engine is a controlled-release substitute for learning-by-launching, and the waitlist it required later became part of Superhuman's brand.
- **Distribution is absent.** The framework measures and raises love; it says nothing about how the product reaches people, which [[snapchat]] argues is the binding constraint for consumer products and [[category-creation]] argues should be worked in parallel with the product. The second takeaway, "floor it," assumes a channel exists. For a $30/month prosumer email client sold through a waitlist and word of mouth, that assumption held; it will not hold everywhere.
- **The half/half rule is an exploit/explore split.** Doubling down protects the differentiator from being commoditized while blockers are fixed; unblocking converts the fence-sitters that doubling down alone would never move. The rule is a heuristic, and Vohra's reasoning for why neither half suffices on its own is the transferable part.

## Temporal notes

- The essay first ran on First Round Review in November 2018; the clipped copy is the republication on Superhuman's own blog, which has been revised to say "Superhuman Mail" throughout. That is the product name adopted after Grammarly acquired Superhuman (announced July 2025, terms undisclosed) and, in late 2025, renamed the combined company Superhuman, with Grammarly, Superhuman Mail and Coda as product lines. The 2018-11-27 date in the frontmatter is the original publication date, not the date of the text as it now reads.
- Superhuman launched publicly, invite-only at $30 a month, in 2019, and raised a Series B that year and a Series C in 2021, so the "we're not done" framing describes a company roughly two years from launch and seven from exit.
- Vohra's interactive version of the engine lives in a Coda doc, which is now a sister product inside the same company.
- Ellis's 40% test has since become standard founder vocabulary, largely through this essay; the number itself still rests on his original benchmark of about 100 companies and should be treated as a strong heuristic rather than a calibrated threshold.

## Sources
- Vohra, Rahul (2018). "How Superhuman Built an Engine to Find Product-Market Fit." First Round Review, republished on the Superhuman blog. <https://blog.superhuman.com/how-superhuman-built-an-engine-to-find-product-market-fit/> — [[2026-11-04-superhuman-product-market-fit-engine|local copy]]
