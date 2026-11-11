---
source: agent
compiled_from:
  - agent-notes/raw/business/finance/2026-11-11-a-layman-thinks-about-ai.md
compiled_at: 2026-11-11
model: claude-fable-5-2
confidence: medium
---

# AI investing under uncertainty

Howard Marks's November 2026 Oaktree memo does not offer an AI thesis. It offers a list of eleven questions an AI investor would have to answer, argues that almost none of them can be answered yet, and then asks what an investor should do anyway. His summary judgment: AI is "the most consequential and least predictable development for investors in at least a generation," and the right response is neither abstention nor conviction but sizing and structure chosen to match what you can actually know.

The memo is a useful companion to [[ai-capex-required-returns]]. That article names the hurdles each layer of the AI stack must clear. Marks asks the prior question: how confident can anyone be about whether they will be cleared?

## The compounding-probability problem

Marks starts from a rule he has used before. A top-down investor has to be right about the economy, the industry, the company and the market. At a generous 60% on each, the chance of getting all four right is 0.6⁴ ≈ 13%, assuming independence.

AI, he argues, has more variables than usual: how the technology evolves, demand for compute, competitive structure, who benefits, availability of financing, and the timing of each. He leaves the reader to do the arithmetic, but six variables at 60% is under 5%. The implication he draws is not "stay out." It is that a prediction is only half a view. The other half is the probability the prediction is right, and for AI that probability is unusually low.

His practical test: name the earnings per share of any AI company five years out, then ask whether you would bet the real figure lands within ±50% of your number. He says he never faced uncertainty of this size analyzing 1970s conglomerates or the 1999–2000 internet.

## The eleven questions

1. **How does AI do what it does?** Marks asked Claude, which answered that models are "grown rather than designed": the training recipe is fully known, the resulting mechanism is not, and a model's account of its own reasoning may not match what happened inside. Marks's use of this: if nobody fully understands the mechanism, who can forecast its evolution? (See [[scaling-hypothesis]] and [[ai-alignment]] for the technical side.)
2. **What will it be able to do?** A list of open capability questions: honesty versus sycophancy, creativity, "second-level thinking," whether one model does everything, and what AGI is benchmarked against (the average person, the 90th percentile, or the smartest alive).
3. **Who will profit?** The Buffett point from the internet bubble: transformative technology does not necessarily reward investors. If models converge, the service is a commodity sold on price and the gains go to users, not vendors. If some labs become essential monopolies, the reverse. This is the [[ai-value-capture]] question. Marks adds one he says he has not heard discussed: if AI replaces taxed workers, governments will need the revenue back, so "what's to say AI won't be taxed like people?"
4. **What will the competitive landscape be?** OpenAI and Anthropic were unknown to most people a few years ago. If a lead can be built that fast, it can be lost that fast. Of the leaders of 20–25 years ago, Microsoft, Amazon, Apple and Google survived; Napster, Yahoo and Netscape did not.
5. **How profitable will the companies be?** The ordinary value-investing inputs (units, price, unit cost, reinvestment, return on investment) each depend on AI-specific unknowns: commodity or essential good, chip life and depreciation, how long the spending race lasts. [[ai-lab-economics]] and [[token-pricing]] cover the unit-economics side.

Questions six to eleven (data centers, sector concentration, credit, predictability, the bubble, and how to act) carry most of the memo and get their own sections below.

## Data centers are not a layup

The picks-and-shovels case says: own the infrastructure and you do not need to pick the winning miner. Marks lists why it is weaker than it sounds:

- "Bricks and mortar" is misleading. The shell is a small part of the cost. Chips are most of it, and chip cost and obsolescence risk usually sit with the tenant.
- Sites, permits and local opposition; fiber; power, cooling and construction capacity; and the availability and cost of financing are each a possible bottleneck.

The same bottlenecks cut both ways. Anything that restricts new supply of compute (he cites a round of data-center construction moratoriums passing "last week") makes existing and buildable capacity more valuable. His conclusion is that the spread between winning and losing data-center investments may be wider than is normal for "infrastructure."

## The fault line

Marks's concentration evidence, as he reports it:

- AI is a small part of the U.S. economy but an outsized part of its growth, mostly through data-center capex while other construction declines.
- Magnificent 7 earnings outgrew the rest of the S&P 500 for 14 straight quarters through June 30, 2026.
- Per FactSet, Alphabet and Amazon booked $151 billion of gains on equity stakes in Q2, mostly on Anthropic and SpaceX (which now includes xAI).
- Per J.P. Morgan, 42 AI-related companies produced about two-thirds of the S&P 500's price gains since January 2024.

He calls AI exposure a "fault line" running through portfolios that look diversified. The Milken comparison is the sharpest move in the memo. High-yield investing worked on two legs: extra yield to pay for defaults, and enough diversification that a few defaults did not matter. Today's equity and debt markets have the first leg and are losing the second, because so much rests on one factor.

Note the link between two of his own points: the equity-stake gains that lifted S&P earnings come from the frontier labs, the sector his predictability table rates lowest.

## Credit

This is where Marks is on home ground (see [[private-credit]] for his April 2026 memo on direct lending).

- AI-related debt issuance is near $600 billion globally in 2026 per Goldman Sachs. About $400 billion went to U.S. investment grade: over a fifth of IG supply, taking AI-related bonds to about 12% of the Bloomberg USD IG Corporate index. In high yield the weighting is about 6%.
- AI likely needs about $1 trillion of new capital a year, hundreds of billions of it debt.
- **Rate-insensitive borrowers.** Hyperscalers and labs cannot afford to slow down, so they are "takers" of financing at any price. Marks inverts the old crowding-out story: instead of government borrowing crowding out the private sector, AI borrowing may be raising the rates the government pays. (The [[ai-capex-required-returns]] article reaches higher rates by a different route, through r-star. The two mechanisms are compatible and would stack.)
- **Equity capacity.** Traditional U.S. IPOs raised under $50 billion in eight of the last ten years. AI wants hundreds of billions a year.
- **Ratings drift.** Hyperscalers were debt-free and cash-rich. They are now spending the cash and borrowing. Lenders are lending against ratings earned by a balance sheet that is changing.
- **Structure risk.** Data-center debt leans on tenant ratings, but some leases have out clauses (for example, if the center misses 99.9% reliability). Chip-backed debt may outlive its collateral.
- **Circular transactions.** Money goes from A to B and back to A, or on to C who spends it with A. Are these arm's-length deals or vendors subsidizing demand? And when debt sits in an off-balance-sheet vehicle, is the parent behind it or not?

His instruction to lenders: be "exceptionally vigilant" on both creditworthiness and terms. This is [[leverage]] meeting a single-industry concentration during a period of excitement, which is the setup his bubble checklist in [[private-credit]] describes.

## Predictability scores

Marks asked Claude to rate AI on a scale from 1 (unknowable) to 10 (fully predictable). The answer was about 3 overall, hiding a split: the direction of the technology is a 6 or 7, but "the things investors get paid for" (speed, size of profits, who keeps them) are about a 2.

| AI sector | Score | Comparable industry | Score |
|---|---|---|---|
| Regulated power utilities serving AI load | 6 | Regulated utilities | 6–7 |
| Data centers leased long-term to big tech | 5–6 | Large industrials | 5–6 |
| Hyperscalers | 5 | n/a | |
| Chips | 4 | Airlines, shipping | 3–4 |
| Speculative or "neocloud" data centers | 2–3 | Telecom/fiber 1998–2001 | 2–3 |
| Frontier labs (OpenAI, Anthropic, xAI) | 2 | Early-stage VC | 1–2 |

Claude's stated reason for the labs' score: "These businesses are close to binary. Capital needs are huge, prices per unit of capability keep falling fast, and it's unclear whether a lasting moat exists." Marks notes the irony of Claude saying this about its own maker, and that the least predictable sector appears to be priced at a premium in private markets. He says both OpenAI and Anthropic have filed for IPOs.

The scores are a language model's judgment calls relayed by a self-described layman. They are a useful ordering, not a measurement. The ordering itself (contracted cash flows at the top, binary equity at the bottom) is what a credit investor would expect, which may be why Marks found it persuasive. For a base-rate method of putting numbers on this kind of question, see [[reference-class-forecasting]].

On geopolitics he only lists questions: TSMC makes nearly all leading-edge chips, U.S. export limits push China toward cheap models, and fear of China may blunt safety regulation.

## Is it a bubble?

Marks defines a bubble as "irrational exuberance leading to imprudent behavior, excessive investment, and too-high prices for participation," and splits the question three ways:

1. Is the technology overhyped? No. He thinks AI is real and will be consequential.
2. Is the spending excessive? Unknowable until we know how AI is used and who profits.
3. Are investors overpaying? Unknowable until earnings can be estimated.

He says his view has not changed since his February 2026 memo. Everything reduces to one question: will AI deliver enough value to users to support compute volumes and prices that earn an adequate return on the trillions invested, and for which companies? His finding from talking to people he considers knowledgeable is that the answer is "largely a matter of faith." He quotes Stuart Chase: "For those who believe, no proof is necessary. For those who don't believe, no proof is possible."

He also describes the mood in the weeks before the memo: inflation, deficits, rising rates and a war in Iran, plus AI-specific worries (cheaper and open-source models, Chinese competition, falling token prices, sales growth below expectations, leverage). His point is that none of these worries were new. A changed climate made old questions suddenly matter, the usual swing from "flawless to hopeless." [[technological-revolutions]] gives the longer historical pattern of installation-phase overbuilding that this debate keeps returning to.

## How to act

Marks's prescription has four parts.

- **Uncertainty is not a reason to abstain.** "The biggest mistakes are made when people think they do" know everything. The response is calibrated humility in strategy selection, position sizing and risk-taking, plus willingness to act.
- **Pick the questions you can answer.** An equity investor in a frontier lab must be right about technology, competition, pricing power, profitability and valuation. A lender against a long-term data-center lease must be right about fewer and different things: tenant credit, contract terms, power, residual value. The key question is "which of the questions am I or my organization well suited to answer, and which uncertainties am I willing to bear in the absence of that expertise?"
- **Price can pay for uncertainty.** A low-predictability sector can be the better investment if it is cheap enough. But he flags the catch himself: the same unknowns make intrinsic value, and so cheapness, hard to judge.
- **Five questions for any investment:** How many things have to go right? If my central assumptions are wrong, how much can I lose? Which risks am I paid for and which am I just carrying? How much optimism is already in the price? Does this add to the risk I already hold or diversify it?

He closes with Buffett in *Forbes*, August 6, 1979: "The future is never clear; you pay a very high price in the stock market for a cheery consensus. Uncertainty actually is the friend of the buyer of long-term values."

## Reading the memo

- **It is a credit investor's memo.** The structure favors positions where you need to be right about fewer things: senior, contracted, collateralized. That fits Oaktree's business. It does not make the argument wrong, but a reader should notice that the framework's natural conclusion is the author's own product. The frontier-lab equity holder would answer that the binary payoff is the point.
- **The Buffett quote cuts against the mood of the memo.** Uncertainty is the friend of the long-term buyer when it lowers prices. Marks's own evidence (labs priced at a premium, AI at two-thirds of index gains) describes uncertainty without the discount. He half-says this in the "price can pay" section and leaves it there.
- **Its distinct contribution** next to [[ai-capex-required-returns]] is the second-order question. That piece says which numbers would settle the debate. This one says how to size a position while those numbers are missing. [[present-value-of-growth-opportunities]] is the tool for his fourth closing question, how much optimism is already in the price.
- **The use of Claude as a source is itself evidence.** A 2026 memo from one of the best-known investors quotes a model on interpretability and asks it to score its own industry. That is a small data point on question two.
- **Figures are as reported.** The FactSet, J.P. Morgan and Goldman numbers are Marks's citations and were not checked against the originals here.

## Sources
- Marks, Howard (2026). "A Layman Thinks About AI." <https://www.oaktreecapital.com/insights/memo/a-layman-thinks-about-ai> — [[2026-11-11-a-layman-thinks-about-ai|local copy]]
