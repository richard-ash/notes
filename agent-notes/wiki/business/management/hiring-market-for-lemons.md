---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2026-04-28-danluu-hiring-market-for-lemons.md
compiled_at: 2026-04-28
model: claude-opus-4-7
confidence: medium
---

# The Developer Hiring Market and the Lemons Problem

Dan Luu's response to Joel Spolsky's "Finding Great Developers" thesis. Spolsky's claim — that great developers apply to roughly four jobs in their entire career and are nearly always retained by their current employer — has hardened into industry conventional wisdom. Luu argues the model is internally inconsistent, contradicted by what he actually sees in the market, and that the reasons hiring managers struggle are not "great devs don't exist" but four mundane and fixable problems.

## Spolsky's "great devs are sticky" model

Spolsky frames developer hiring as a near-zero-supply market for high-quality candidates. The model rests on two assumptions:

1. **Prospective employers can recognize "great" developers quickly** — i.e., quality is observable.
2. **Once recognized, current employers will do anything to keep them** — i.e., great devs accumulate offers internally and never need to test the market.

The result, in his telling: a 1000-resume pile contains ~970 incompetents, ~30 "solid" people, and maybe one great developer. Hiring is impossible because the genuinely good are simply not in the pool.

## Luu's structural critique

Luu's first move is to point out that Spolsky's two assumptions undermine each other. **If prospective employers can identify a great dev cheaply, they can simply outbid the current employer** — Luu reports having seen offers at 2× existing comp succeed exactly this way. A market for lemons in [the Akerlof sense](https://en.wikipedia.org/wiki/The_Market_for_Lemons) requires asymmetric information; Spolsky's model explicitly denies asymmetry, then assumes the consequences of asymmetry anyway.

The deeper inversion: **information asymmetry often runs the other direction.** Luu's "Bob" archetype — the engineer whose work prevents catastrophes that therefore never happen — is invisible to internal management but legible to a peer network that has seen the work up close. External offers can therefore exceed internal comp by 2× because outside management has *better* information than inside management about productivity. This is the same "credit-taker captures the visible work, the load-bearer is undervalued" dynamic that recurs across organizations.

## Why "good teams retain forever" doesn't survive contact with reality

Spolsky's stickiness story implicitly assumes companies can manufacture environments good devs want to stay in. Luu offers two empirical pushbacks:

- **Bad environments are abundant.** He polled developers at a conference: "Do you know any company that isn't highly dysfunctional?" Zero respondents answered yes. "Do you know a great team that's hiring?" Almost nobody. Good teams are full because everyone forwards their network into them; the team that lost 3 of 7 people in a year is the one with open seats. The mechanical consequence: **a randomly chosen open role is disproportionately on a churning team.**
- **Good environments aren't stable.** The "Marc Yun" anecdote: a great manager leaves a great team, and over two years every person Luu knew there exits. One leadership change converts an entire low-attrition group into searchers. Acquisitions accelerate this. Stickiness assumes stationarity that the modern industry doesn't deliver.

## The four real reasons hiring is hard

Luu's central practical claim: every hiring manager he's seen struggling with hiring has at least one of four problems, all of which are fixable.

### 1. Pay is too low
A 6× compensation spread between companies hiring for the same role in the same metro, with nearly every company believing it pays competitively. Spolsky himself, as a case study: praising Fog Creek's pay in 2007, then complaining a few years later that Google overpays new grads. **Luu's claim is that "we pay competitively" is a near-universal delusion** — companies anchor on peer comp, not market comp, and confuse the two. Oracle and Alibaba's Seattle cloud hiring success is the existence proof: pay above market and the hiring problem disappears, even with a hostile employer brand.

### 2. Filters reject good devs
Luu's resume math is the inverse of Spolsky's: a 1000-resume pile has ~400 solid people and ~20 strong ones, but everyone uses the same filters and competes for the same ~30 candidates the filters surface. He cites a [law-firm recruiting study](http://www-2.rotman.utoronto.ca/facbios/file/RiveraTilcsik.pdf) where "high-class" hobbies (sailing, polo, classical music) plus being male produced a 4× lift in interview invites with no other resume changes — the filters are tracking class signals, not job-relevant skill. Counter-examples: his first employer Centaur ran an onsite easier than Google's phone screen and produced the highest-productivity team Luu has worked on; Matasano famously broke from convention and got results. The dominant strategy is the IBM safety: pedigree-screen, run the standard interview, deny that anything was missed.

The class of people most affected: **devs who don't look like the cultural template** ("nontraditional" backgrounds, bad-at-interviewing-but-strong-at-work, work that doesn't generate visible artifacts). Luu names two patterns in particular:
- People like "Bob" whose work prevents incidents and therefore registers as nothing.
- People who are simply terrible interviewers (his "Jeshua Smith" example) — top performer for a decade, references universally glowing, can't pass a screen.

### 3. Rare skill combinations
Standard answer: hire someone with a third of the requirements and train. Luu notes this advice rarely meets resistance.

### 4. Dysfunction the manager doesn't see
The hardest case. Some teams' anti-referral rate exceeds their referral rate — current employees actively warn friends away. Founders and VPs are systematically last to know. Luu doesn't claim a fix; if he had one he says he'd be a manager.

## The implicit symmetry: lemons run both ways

Luu's strongest analytical point is that the lemons frame is partial regardless of which direction you apply it. Both candidates and employers operate under incomplete information about each other:

- Candidates can't tell good teams from bad before joining, so they cling to existing roles, which makes hiring harder.
- Employers can't tell good candidates from bad without expensive sampling, so they fall back on cheap proxies (pedigree, interview performance) that miss most of the real signal.

What counts as "the lemons problem in dev hiring" depends on which side you stand on. Luu's takeaway is asymmetric: **finding a good team is genuinely hard with no replicable strategy, but hiring well is straightforward with replicable fixes** — pay properly, change your filters, train for combo-skills, address dysfunction. The asymmetry is what produces his lack of sympathy for hiring managers who complain.

## How this contrasts with other hiring philosophies

[[deliberate-want]] (Rands) and [[hiring-for-curiosity]] (Shapiro) both operate inside Spolsky's premise — they assume the hard part is competing for scarce strong candidates and offer levers (deliberate communication, role customization around curiosity) to win that competition. Luu's argument is that those frames misdescribe the problem: the candidate pool is *not* mostly empty, it's full of people the standard filters reject. Rands optimizes the closing mechanics of an offer; Shapiro optimizes the filter. Luu's diagnosis is closer to Shapiro's in spirit — both argue that conventional filters miss a lot — but Luu pushes further, claiming the average hiring manager's "we have a high bar" self-conception is the actual problem rather than a partial solution.

This connects to [[scaling-people]]'s argument that management is fundamentally a series of people decisions: if Luu is right, the leverage point isn't sourcing harder, it's questioning the inherited filters that decide who gets a real evaluation. It also connects to [[truth-telling-leadership]]'s observation that organizations resist hard truths — "we filter out a lot of people who do great work elsewhere" is exactly the kind of self-assessment that almost no team is willing to make.

## What's load-bearing in Luu's argument vs. anecdote

The core analytical claims are robust:
- Spolsky's two premises are mutually inconsistent.
- Information asymmetry runs both directions, and often favors prospective employers.
- The supply of good environments is much smaller than the supply of dev jobs, which inverts the stickiness intuition.

The four-causes taxonomy is presented from one developer's vantage at a small number of large companies (the "company that's notorious for being dysfunctional in this exact way" Luu mentions in the post is widely understood to be Microsoft, where Luu worked at the time). Compensation spreads, filter homogeneity, and the dysfunction-blindness of senior leadership are claims that ring true to almost everyone in industry, but they're sourced to Luu's network rather than systematic measurement. Confidence is **medium** — the structural critique of Spolsky is hard to escape; the practical taxonomy is plausible but anecdotal.

## Sources

- Dan Luu. "Hiring and the market for lemons." <https://danluu.com/hiring-lemons/> — [[2026-04-28-danluu-hiring-market-for-lemons|local copy]]
