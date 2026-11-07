---
source: agent
compiled_from:
  - agent-notes/raw/law/2017-04-01-deregulation-of-private-capital.md
compiled_at: 2026-11-07
model: claude-opus-5-5
confidence: medium
---

# Decline of the Public Company

The U.S. has fewer public companies than it did in the 1990s, and the ones it has are older and bigger. The usual explanation is that being public got more expensive: Sarbanes-Oxley, Dodd-Frank, litigation, activists. Elisabeth de Fontenay (Duke Law) argues in a 2017 *Hastings Law Journal* article that this has the story backwards. The bigger change, she says, is that being public got *less useful*. Thirty years of private-side deregulation let firms raise large amounts of equity without going public. Meanwhile, private firms lean on the information public firms are forced to disclose, and that reliance makes the arrangement unstable for both sides.

## The original bargain

The 1933 and 1934 Acts split corporate finance into two sides. A firm becomes a reporting company if it (1) offers securities to the general public, (2) grows past a size trigger (assets plus holders of record, under Exchange Act §12(g)), or (3) lists on a national exchange. Reporting companies take on heavy periodic and event-driven disclosure. In return they get the one thing the private side couldn't have: access to the general public, the largest and cheapest pool of capital.

The line was drawn, loosely, by who could "fend for themselves" (*SEC v. Ralston Purina*, 1953). Passive, dispersed investors needed mandated disclosure to value anything. Insiders already had the information, and banks could get it through monitoring and covenants. So the private side was mostly insiders and lenders, and the cost (disclosure) bought a benefit (investors) directly. De Fontenay calls this "disclosure in exchange for investors."

## The decline, as of 2017

| Measure | Earlier | Later | Source cited |
|---|---|---|---|
| U.S. IPOs per year | 310 (1980–2000) | 99 (2001–2012) | Gao, Ritter & Zhu (2013) |
| Small firms' share of IPOs | 53% | 28% | same |
| Total IPO proceeds per year | $28.3B | $28.0B | same |
| U.S. share of global IPOs | 31% (1990s) | 10% (2000s), with flat GDP share | Doidge, Karolyi & Stulz (2013) |
| U.S. exchange-listed firms | 8,025 (1996 peak) | 4,101 (~2016) | NBER via Sorkin |
| Listed firms ÷ all U.S. firms | 1996 peak | down more than half by 2012 | Doidge, Karolyi & Stulz, "listing gap" |
| Median age of VC-backed firm at IPO | 8 yrs (1980s) | 10 yrs (2001–2015) | Ritter |
| Years from first round to IPO | 5.8 (2011) | 7.7 (2015) | Picker, *NYT* |
| Private placements vs registered offerings | — | $2.1T vs $1.35T (2014) | SEC DERA |

Three details stand out:

- **The IPO decline is global. The listing decline is American.** Other developed countries also saw fewer IPOs, but only the U.S. saw listings shrink. Doidge, Karolyi and Stulz call this the U.S. "listing gap."
- **Public firms are net buyers of their own equity.** In 2015, net equity issuance by nonfinancial corporations was about −$128B, so buybacks exceeded new issuance. The public market had stopped raising capital in aggregate (see [[capital-allocation]] on the rise of buybacks).
- **The private figure understates the private side.** It leaves out instruments the law doesn't treat as securities at all, such as the ~$900B leveraged-loan market and commercial paper.

IPOs no longer mainly raise capital. They let insiders cash out once a firm is already large. Facebook is her example: Zuckerberg said there was "no rush" because the company had all the capital it needed. Its eventual IPO was driven mostly by the 500-holder trigger in §12(g), and Facebook's lobbying against that trigger led Congress to raise it in the JOBS Act.

## How the bargain was revoked

De Fontenay calls the liberalization of private capital "arguably the most significant development in securities regulation over the last thirty years" and says the empirical literature on the public-market decline has mostly ignored it.

| Year | Change | Effect |
|---|---|---|
| 1982 | **Regulation D** safe harbors for offerings to "accredited investors" | Became "the exception that swallows the rule." The pool of qualifying institutions grew, and the income and net-worth thresholds were never adjusted for inflation |
| 1988 | **Rule 701** exempts equity compensation | Employee stock no longer pushed firms toward registration |
| 1990 | **Rule 144A** allows unrestricted resale to qualified institutional buyers | Large-scale private syndication, mostly of debt. She dates the start of the listings decline to here, not to 2002 |
| 1996 | **Investment Company Act §3(c)(7)** removes the 100-investor cap on private funds | Made mega-sized PE and VC funds possible |
| 2008-era amendments | **Rule 144** allows free resale of restricted stock after six months or a year | Enabled secondary platforms for private stock (SecondMarket, later Nasdaq Private Market; SharesPost) |
| 2012 | **JOBS Act** | Raised the §12(g) trigger from 500 to 2,000 holders of record (or 500 non-accredited) and excluded employees; lifted the general-solicitation ban for Reg D; created Reg A+ (up to $50M) and crowdfunding |

Two points she adds:

- **The JOBS Act worked against itself.** It was sold as a way to revive IPOs, but it also made staying private easier, which undid its own on-ramp provisions. Berdejó (2015) found no rise in IPOs among the issuers it targeted. Coates and Pozen estimated that more than two-thirds of public companies at the time could have qualified to stop periodic reporting under the new thresholds.
- **Defining things as non-securities is a hidden form of deregulation.** Leveraged loans, for example, have become functionally close to high-yield bonds but are still treated as non-securities.

Deregulation, new technology and a global glut of capital together gave private firms most of the benefits of being public (capital, some liquidity) with almost none of the costs (disclosure, securities litigation, activism).

## Why the regulatory-cost story falls short

De Fontenay doesn't deny that compliance costs push small firms to go dark (Leuz et al. 2008; Iliev 2010 on SOX §404). She argues the timing and pattern don't fit cost as the main cause:

- Listings peaked in **1996** and the IPO decline started before Sarbanes-Oxley.
- The decline hits **large issuers too**, and compliance costs matter least to them.
- Countries with **lighter regulation** also lost IPOs.
- Other studies find other causes: Bartlett et al. trace the collapse of small IPOs to a 1998 shift in mutual funds' preference for liquidity, and Gao, Ritter and Zhu point to technology pressuring small firms to reach scale quickly through acquisition.

Her methodological point (fn. 103) is the most useful part of this section. Event studies of disclosure rule changes can't tell you the right disclosure policy. That's because the *same* new rule can hurt public firms when most of their peers are private and help them when most are public. Every such study is entangled with where the public-private line happens to sit when it is run.

## The information subsidy

### The puzzle

The standard defense of mandatory disclosure rests on two market failures. The first is **third-party effects**: one firm's disclosures help its competitors, so each firm discloses less than is socially optimal. The second is **agency costs**: managers hide things, such as conflicts of interest, that shareholders would want disclosed. The law-and-economics critique (Easterbrook and Fischel; Stephen Ross's signaling model) asks why investors don't simply punish non-disclosers. The "rough consensus" answer from the 1980s is that mandating disclosure solves a collective-action problem and lowers the cost of capital for disclosing firms as a group.

De Fontenay points to an unstated assumption in that answer: **every comparable firm is bound by the regime.** Once firms can opt out, and once investors can follow them, the model's prediction no longer holds. She stresses that "investor choice is precisely what makes issuer choice meaningful." Some issuer choice has always existed. What changed is that passive capital can now cross the line.

That leaves a puzzle. Theory says not disclosing is a negative signal, so private firms should pay a higher cost of capital or be a pool of adverse selection in Akerlof's sense. Instead, unicorns raise money cheaply. Her example: in January 2016 Uber raised money at $62.5B, and the Morgan Stanley wealth clients it marketed to got *no financial statements at all*. Fidelity and T. Rowe Price mutual funds invested anyway.

### Why debt can contract for information and equity can't

One possible answer is that private investors negotiate for the information they need. That works for debt, and de Fontenay's earlier work on the leveraged-loan market argues that it does. She gives four reasons it doesn't carry over to passive equity:

1. **Maturity.** Equity never matures. Specifying disclosure decades ahead, through changes in accounting, law and the business itself, is too costly. The SEC can revise its rules without asking the issuer. A contracting investor can't.
2. **Collective action.** Debt holders use an agent or arranger at issuance. Dispersed shareholders, especially those buying on secondary markets, have no direct relationship with the issuer.
3. **Ratings.** Credit ratings partly substitute for disclosure on traded debt. Equity has nothing comparable, and analyst reports carry far less weight.
4. **Information sensitivity.** Debt is a fixed claim with priority. Equity's value moves with every piece of news about growth and risk.

VC investors do negotiate information rights (the NVCA Investor Rights Agreement), and large private firms often get audited. But each new funding round, equity grant and secondary trade adds to a "costly patchwork of conflicting information rights, with some investors owed no information whatsoever."

### Her answer: private firms borrow public information

Public markets produce two kinds of information. One is **mandatory disclosure**: business, risks, capital structure, audited financials, MD&A, internal controls, governance and compensation, and filed material contracts. The other is **trading prices**: more than a billion NYSE shares a day in January 2016, and each price summarizes the market's whole view of a firm and its environment. De Fontenay sorts the uses third parties make of this information into two groups:

- **The public subsidy (harmless).** Stock indices act as economic indicators for the Fed, legislatures, firms and households, and as benchmarks for more than $1T of S&P 500-linked products. This use doesn't hurt the firms that produce the information, and it is part of the original case for mandating disclosure.
- **The private subsidy (harmful).** Private firms that compete with public firms for capital and customers use the information in two ways:
  - **Competitive spillover.** Filings serve as blueprints for business models, contract terms and pay. Firms clearly worry about this. About 40% of IPO firms got SEC permission to redact parts of their registration filings (Boone et al. 2016). More than 15% of small reporting companies redacted material contracts in a single year, and firms in more competitive industries redact more (Verrecchia & Weber 2006). When a 1999 rule forced firms on the OTC Bulletin Board to report, firms that were *already* disclosing voluntarily saw higher returns and liquidity, because the information finally ran both ways (Bushee & Leuz 2005). Private firms also give themselves away: posting audited financials online would cost nothing, yet they almost never do.
  - **Valuation.** The "valuation chain for private firms above a certain size most often begins with public companies." Comparables valuation needs public peers and their price-to-metric ratios: if peers trade at 8× EBITDA, multiply the private firm's EBITDA by eight. DCF needs a public comparable's beta to set the discount rate. Fidelity's 2016 markdowns of Dropbox and Zenefits followed public rivals' prices, and Baginski and Hinson (2016) find that when one firm stops issuing forecasts, a peer starts, consistent with firms free-riding on each other's disclosures to lower their cost of capital. The benefit runs one way, because private firms give little back.

Dropbox valued by reference to Box is her standard example. Box's stock fell almost 60% in the year after its January 2015 IPO, while its disclosures and price kept helping investors value Dropbox.

She contrasts this with Treasuries. The Treasury market also produces a benchmark that everyone else free-rides on (corporate bonds are priced as spreads over Treasuries), and Treasury officials deliberately issue across the whole yield curve to keep that benchmark complete. The difference is that the government gets the benefit back through growth and tax revenue. A public company gets nothing back for the benchmarks it supplies.

### The A/B unraveling

Her stylized example has two close competitors with strong third-party effects and no agency costs:

| Regime | Firm A | Firm B | Total |
|---|---|---|---|
| Both must disclose | 100 | 100 | 200 |
| B may opt out, keeps disclosing | 100 | 100 | 200 |
| B opts out and goes dark | **90** | **105** | 195 |
| Both opt out | 95 | 95 | 190 |

B gains because it saves compliance costs, keeps learning from A's disclosures without giving any back, and its investors can still value it using A's price. A loses twice: its investors can no longer use B's information to value A, and B now competes with information A doesn't have. Then A defects too. Each firm acts rationally, and investors end up worst off. This is a classic unraveling that only a binding commitment can prevent.

She draws three lessons:

1. A wave of firms exiting disclosure is **not proof that disclosure costs too much**. It may mean the third-party effects are strong.
2. If those effects are strong, a **hybrid regime with heavy mandates and easy opt-out can be worse than either pure option**: light rules with opt-out, or strict rules for everyone.
3. Each defection weakens the private side's information base, so **cheap private capital may be temporary**. It may last only as long as there are enough public firms to borrow information from.

### How this differs from the "publicness" literature

Langevoort and Thompson, and others, criticize disclosures that serve the public rather than shareholders, such as mine safety, conflict minerals and the CEO pay ratio. De Fontenay's claim goes further. Even disclosure plainly designed for shareholders, like financials and stock prices, now increasingly benefits outsiders who compete with the firms producing it.

## Where it ends

De Fontenay sees two opposing forces:

- **Acceleration.** As the public share falls, any given public firm is more likely to face private competitors, so the one-way flow of information costs it more, which pushes more firms to go private.
- **A floor.** Disclosure costs fall relative to size and liquidity benefits grow with it, so the largest firms stay public. The size at which listing makes sense keeps rising, though, so the remaining public market becomes "a holding pen for massive, sleepy corporations."

The risk is to the private side. Ever fewer, ever larger public firms make worse comparables for growth-stage private firms, so information costs rise, valuations fall, and capital may be misallocated at scale. She cites Zenefits and Theranos as early examples but says anecdotes don't predict outcomes. She is cautiously optimistic that institutional investors will build private alternatives, such as listing standards on private-stock exchanges and data vendors like Sageworks. But she sees a limit on how much passive equity holders can obtain on their own, and calls the height of that ceiling "a key unknown."

## Policy position

She explicitly takes no side on how much public companies should disclose. Her claim is that the current path undermines itself on the SEC's own terms. If investment information is a public good that private ordering underproduces, then piling more disclosure on public firms while letting investors move into the "disclosure-lite" private markets wears down the very thing the SEC wants produced. She prefers either end of the spectrum to the middle: **cut public-company disclosure sharply, or redraw the line so more issuers and investors are confined to the public side.** She rejects the alternative of mandating disclosure for all widely traded firms based on public float (proposed by Coffee, Ritter and Rodrigues). Private firms of comparable size would still benefit from public firms' information without giving any back.

## Implications and connections

- **This is a Hayekian argument about prices.** In [[use-of-knowledge-in-society]], prices compress knowledge spread across many people into a single signal. De Fontenay treats exchange prices the same way, as a public good whose production is shrinking while more firms consume it. Fewer listed firms means less information gets aggregated into prices.
- **It is the same capital wave Damodaran describes.** The "gray market" in [[scaling-vs-profitability]], where mutual funds, sovereign funds and SoftBank pour money into late-stage private firms, is the "retailization" de Fontenay saw beginning in 2016. Damodaran's Ritter data (higher age, revenue and market cap at IPO; the share of IPO firms that are profitable falling from over 80% to under 25%) continues her "fewer and bigger" trend. The two arguments also connect. If private valuations are borrowed from public multiples, Damodaran's weakening reversal in public markets doesn't stay public. Any mispricing in the comparables passes straight into private marks.
- **The debt side grew in the same deregulated space, but more safely.** Her debt-versus-equity argument explains why [[private-credit]] could grow on negotiated covenants and information rights while private equity holders could not. Marks's warning about retail-distributed BDCs is the debt version of her concern about pushing retail money into illiquid private assets.
- **Read as a commons problem, the policy choice follows.** Public-company information works like a shared pasture that private firms graze without paying. A commons survives either through enclosure (lighter mandates, so each firm discloses what it is paid for) or through compulsory membership (move the line so the grazers have to contribute). That is her binary, and it explains why she finds the middle position unstable rather than merely a compromise.

## Temporal notes

The article was written in early 2017, and much has happened since:

- **Every unicorn she names has gone public or failed.** Dropbox listed in March 2018 at roughly $9B, below its $10B private mark. Lyft listed in March 2019, Uber in May 2019 (about $82B, well below the ~$120B bankers had floated), and Airbnb in December 2020. Theranos shut down in 2018. Down-priced listings like these fit her valuation-chain argument: an IPO is where a borrowed private mark meets a price set directly by the market.
- **The 2022 repricing is consistent with the valuation-chain argument.** When public software multiples collapsed in 2022, private marks followed with a lag, through down rounds such as Klarna's (from $45.6B to $6.7B) and Stripe's (from $95B to $50B).
- **The window has opened and closed.** The 2020–21 SPAC and IPO boom briefly reversed the "drought." Direct listings (Spotify 2018; NYSE primary direct listings approved in December 2020) offered another route in, and the window shut again in 2022–23. By mid-2026 the largest listings dwarf any she imagined. Per [[scaling-vs-profitability]], SpaceX listed at $1.8T in June 2026. That fits her prediction that firms will go public only once they are behemoths.
- **Private-side deregulation continued.** In 2020 the SEC widened the accredited-investor definition to include holders of certain professional licenses (Series 7, 65 and 82) and "knowledgeable employees," without inflation-adjusting the wealth thresholds. It also raised the Reg A+ cap from $50M to $75M and the crowdfunding cap from $1.07M to $5M. The 2025 executive order directing regulators to open 401(k)s to private equity and private credit takes the retailization she flagged much further.
- **The listing-gap paper she cites as a manuscript** was published in the *Journal of Financial Economics* in 2017 (Doidge, Karolyi & Stulz, "The U.S. Listing Gap").

## Sources
- de Fontenay, Elisabeth (2017). "The Deregulation of Private Capital and the Decline of the Public Company." *Hastings Law Journal* 68:445. <https://ssrn.com/abstract=2951158> — [[2017-04-01-deregulation-of-private-capital|local copy]]
