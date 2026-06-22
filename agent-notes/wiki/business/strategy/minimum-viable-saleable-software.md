---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-06-22-minimum-viable-unit.md
compiled_at: 2026-06-22
model: claude-opus-4-8[1m]
confidence: medium
---

# The Minimum Viable Unit of Saleable Software

Brandur Leach's argument for whether a small software business can survive in the LLM age, framed as a revised **buy-vs-build** calculus. The worry he answers: "Anything you ship can be instantly displaced by an internal package built by an LLM." His counter is that LLMs made software *cheaper* to build but not *free*, and that there's a pricing band — a **zone of viability** — where buying still beats building even with capable models on tap.

## The buy-vs-build calculus shifted

For years the default wisdom was: build only inside your core domain, buy everything peripheral, because building was a "very expensive proposition" with huge upfront cost, schedule overruns, and a bottomless rabbit hole. LLMs collapsed the cost of build, making it suddenly plausible to produce substantial software by having models do the work. That reopens the buy-vs-build question for software that was previously unambiguously a "buy."

## Cheap != zero

Leach's load-bearing claim is that LLM-built software still costs money on two axes:

- **Initial build.** A satisfactory result takes dozens of feedback loops — operator runs the model, evaluates, adjusts, re-runs — converging on a compromise between time and quality. A task tracker is "a few weeks" of effort even with gratuitous LLM use.
- **Ongoing maintenance.** Bugs and features never stop. LLMs make changes easier but not free; the expensive element is the **part-time human labor** overseeing and verifying results.

The verification-and-oversight cost is the crux: the human in the loop is the bottleneck, not the model's per-token price. This is the same human-as-bottleneck observation that recurs across the AI-coding literature — see [[ai-native-company-building]] and the agentic-engineering "taste is the bottleneck" framing.

### The Jira worked example

The anecdote that triggers the post: a company rebuilt Jira internally with Claude to escape a $400/mo bill. Leach runs the numbers against it:

- Engineer at $200k/yr → ~$96/hour, $3,850/week, $16.7k/month.
- To beat $400/mo, the engineer can spend **no more than ~4 hours/month** maintaining the clone (400 / 96) — before any context-switching overhead.
- Even charitably assuming 2 hours/month of maintenance, recouping the ~2-week initial build takes **37 months** to break even: `2 * 3846.15 / (400 - 2 * 96.15)`.

Conclusion: the Jira rebuild doesn't pencil out. The $400/mo SaaS bill is *cheaper than the labor* to replace and maintain it.

### The build threshold

Flip the price up and the answer flips. Fully loaded Salesforce at ~$500/seat/mo × 50 seats = **$25k/mo**, which funds ~1.5 full-time engineers (25 / 16.7) on a clone. At that spend a CRM rebuild is "closer to a build decision, even for a smaller company." (Leach notes Salesforce being down 30% YTD as the market arguably agreeing.)

| | Ongoing price | Engineer-equivalent hours/mo | Equivalent eng resources | Verdict |
| --- | --- | --- | --- | --- |
| Jira | $400/mo | 4.2 hours | 0.02 engineers | **Buy** |
| Salesforce | $25k/mo (50 seats) | 260 hours | 1.5 engineers | **Build** |

## The zone of viability

The central concept. For software of arbitrary complexity there's a band — when priced "within reason" — where buy beats build even given capable LLMs. Two conditions define it:

1. **Enough novelty** that an LLM rebuild is non-trivial and carries ongoing maintenance burden.
2. **Pricing not so exorbitant** that it strongly incentivizes a rebuild.

While priced inside the band, cumulative licensing paid is less than the cumulative cost of prompting the initial build plus sustaining it. The **minimum viable unit of saleable software** is the floor of this band: below it, a rebuild is the same or less effort than going through a third-party purchasing process, so the product isn't cost-effective to sell over the long run.

The practical strategic lesson for a vendor: pricing is no longer just a revenue-capture lever, it's the variable that keeps you *inside* the zone. Price too high and you push customers over their own build threshold — the LLM-era version of the [[marketplace-rake]] argument that excessive pricing is strategically self-defeating, now with "the customer rebuilds you with Claude" as the disciplining force rather than a competing platform.

## How this relates to moats

The "novelty" condition is doing a lot of work and maps onto the [[competitive-moats]] taxonomy. A product survives in the zone only if it has something an LLM can't trivially reproduce — Leach's River example leans on **special know-how** baked into API design and performance properties, not on raw feature count. Features are cheap to clone; accumulated design judgment and performance tuning are the durable, hard-to-prompt-back part. This is a sharper, AI-era statement of "software isn't a moat" (the [[snapchat]] thesis) and complements [[ai-platform-moats]]: in a world where the build cost of features approaches commodity, the moat moves to taste, design coherence, and the verification-labor it would take a buyer to match your fidelity.

The argument is also a relative of [[outcome-based-pricing]] — both ask what a customer is actually willing to pay for once raw software production is cheap. Leach's answer is "not having to build and babysit it yourself"; the outcome-pricing answer is "the business result." Both treat per-seat/per-feature pricing as increasingly fragile.

## River as the test case

Leach is taking over [River](https://riverqueue.com/) (a Go/Postgres job queue) full-time and betting it clears the minimum viable unit:

- **Novelty:** open-source core with most features free; Pro reserves advanced features (workflows, sequential jobs, concurrency-limited jobs) and invoice billing. An LLM *could* reproduce these, but the API design and performance work raise the rebuild fidelity bar.
- **Price:** sublinear pricing on **team size, not headcount** — $125/mo for up to 20 developers, scaling to a multiple for an unlimited site license. Deliberately low enough to sit well inside the zone of viability for a small-to-medium team.

The open-core structure is itself a zone-of-viability play: give away the parts cheap to rebuild, charge only for the parts where your accumulated design judgment makes a rebuild genuinely costly.

## Caveats and open questions

- The model is a back-of-envelope, single-author argument (hence medium confidence). The numbers are illustrative, not measured — real maintenance hours, context-switching cost, and build-quality gaps are all assumed.
- It treats the buyer's labor cost as static. If models keep getting cheaper and the human verification burden drops, the zone of viability narrows from the bottom and the minimum viable unit rises over time — a temporal risk Leach acknowledges only implicitly ("the coming months will tell").
- The novelty condition is a moving target: what's non-trivial to rebuild today may be a one-shot prompt next year, so a product's position in the zone is not fixed.

## Sources
- Leach, Brandur. "The Minimum Viable Unit of Saleable Software." <https://brandur.org/minimum-viable-unit> — [[2026-06-22-minimum-viable-unit|local copy]]
