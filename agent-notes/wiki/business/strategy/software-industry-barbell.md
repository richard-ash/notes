---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-09-15-moats-barbell-ification-of-software.md
compiled_at: 2026-09-22
model: claude-fable-5-1
confidence: medium
---

# Software Industry Barbell

What happens to the structure of the software industry when the cost of writing software approaches zero? Mike Vernal (@mvernal) argues in a September 2026 essay that it will "barbell-ify" the way newspapers did after the Internet: a handful of very large companies that own an entire buying center or industry, an explosion of tiny software at the other end, and a hollowed-out middle where today's mid-sized point solutions live. The mechanism is that AI erodes the three classic software moats (replication cost, switching costs, network effects), and the only moat left standing is *cumulative reinvestment* — the sheer volume of what you have already built.

## The newspaper precedent

Vernal borrows Ben Thompson's standard analogy (see [[aggregation-theory]]). Pre-Internet newspapers were regional monopolies rooted in distribution infrastructure: it was hard to get the *New York Times* in Des Moines, so you bought the *Register*. When distribution cost went to zero, the market reorganized into a barbell. Vernal's table (subscriber figures are, by his own admission, "courtesy of Claude" and unverified):

| Newspaper | 2002 print circulation | Current subscribers (est.) | Change |
| --- | --- | --- | --- |
| New York Times | 1,113,000 | ~13.4M (2026) | +1,104% |
| Washington Post | 746,724 | ~2.5M | +235% |
| Los Angeles Times | 965,633 | ~243,000 | −75% |
| Chicago Tribune | 613,429 | ~149,000 | −76% |
| San Francisco Chronicle | 512,129 | ~138,000 | −73% |
| Dallas Morning News | 521,956 | ~61,000 | −88% |
| Newsday | 578,809 | 50,000+ | −91% |

Meanwhile a single Substack (Lenny's Newsletter) has over 1.2M subscribers. "The middle disappeared. You're either one of the top newspapers in the world or you're a solopreneur/SMB."

Note the comparison is print circulation vs. digital subscribers, so the percentages are directional rather than exact. The shape is not in dispute.

## Why AI erodes the classic software moats

Vernal says most software companies rest on three pillars, each of which maps onto one of Neumann's structural sources in [[competitive-moats]]:

| Vernal's pillar | Neumann's source | What AI does to it |
| --- | --- | --- |
| Cost and complexity of replicating what was built | Special know-how (closely-held) + scale | Software becomes much faster and cheaper to replicate |
| Switching costs once adopted | System rigidity | Migrations become increasingly automatable |
| Network effects from integrations, human experts, SIs | Returns to scale | Integrations automate; "the AI is a better expert than your p95 human" |

The third erosion is the least obvious and the most interesting. A large part of enterprise software's network effect has never been the software itself; it is the ecosystem of certified consultants, system integrators, and admins who know the product. Salesforce's "Trailblazer" population is a moat. If a model is a better Salesforce admin than the 95th-percentile human one, that ecosystem stops being scarce.

Vernal is careful to say "asymptotically approaches zero," not "is zero." Brandur Leach's [[minimum-viable-saleable-software]] is the necessary corrective on the near term: LLMs made software cheap but not free, and the binding cost is verification and maintenance labor rather than tokens. That means the erosion Vernal describes is a *trend* with a slope, not a switch, and the "zone of viability" where buying still beats rebuilding persists for now.

## The surviving moat: cumulative reinvestment

Vernal's positive claim starts from Amazon. On day one Amazon was "the least-defensible initial premise of the major tech companies" — buying books in bulk and reshipping them in smaller boxes. Thirty years later its moat looks like planes, trucks, and data centers. But another way to see it is 7,500+ days of building, taking the profits, and building more. By year ten a competitor had to replicate nine years of work, because Amazon never took its foot off the gas.

The AI-era version: if the amount of software you can build in a day rises 1,000×, and you build that amount every day for ten years, it still takes competitors years and billions to replicate it. The moat is the *extreme cost of replicating the totality of what you have built*, continuously refreshed.

Vernal then reweights Helmer's 7 Powers for software: **switching costs and network effects become less important; scale economies and branding become more important.** He frames this tentatively ("I suspect"). The prescribed strategy is glibly scale-based: "create an unimaginable amount of software every single day and re-invest the profits to create even more."

This connects to two older ideas in [[competitive-moats]]:

- Neumann's "returns to scale require scale" problem. Vernal's answer is to pick scale economies as the target moat and spend the whole uncertainty window converting into it as fast as possible. It is Neumann's prescription with the moat pre-selected.
- Griffin's Bezos doctrine, "your margin is my opportunity." Reinvesting every dollar into more product denies competitors a margin pool to fund entry. Vernal's loop is that doctrine applied to product surface area rather than price.

It also runs directly against Evans's conclusion in [[ai-platform-moats]] that "doing it better every day" is an aspiration, not a strategy. Vernal is asserting that cumulative execution *is* the strategy once the structural moats are gone. Whether that holds depends on whether the accumulated software actually resists replication, or whether a competitor with the same AI tooling can regenerate ten years of surface area in one. Vernal's bet is that it can't, because the leader's tooling improves at the same rate.

## The barbell prediction

**The heavy end.** A small number of very large software companies:

- In the enterprise, one AI-native system per buying center (Sales, Marketing, Finance, HR, IT).
- For SMBs and mid-market, primarily one all-in-one system, with Rippling as the model.
- One large software company per industry (Legal, Finance, Medicine), analogous to the one dominant trade magazine per industry.

These win on two things: the sheer amount of product they build, and the strength of their go-to-market. "They just need to serve their buying center better than any competitor." The instruction for a venture-backed founder is therefore "do it all" — build the whole thing and completely own the buying center. "I fear there is no safety in the middle."

**The hollow middle.** Most mid-sized point solutions get consolidated or die.

**The light end.** An explosion of "small" software. Most of it is people building for themselves or their own company (the improvised end of Evans's spectrum in [[institutionalized-vs-improvised-software]]). But Vernal also expects a D2C-style wave of small software *businesses*, by analogy to the Shopify-plus-Meta-Ads explosion of the 2010s: if 100M apps get built on tools like Lovable, a power law will make a handful of them thriving SMBs. His footnote is the important caveat — these will mostly *not* be venture-addressable, and founders and investors will be led astray by thinking they are. The successful ones will look like Substacks, where a founder or small team owns and operates the entire business.

**The open question.** What is "the Substack for software"? Vernal expects both an aggregator (the Meta analogue) and a platform (the Shopify/Substack analogue) to emerge, and names Lovable, Bolt, and Wabi as early attempts. He does not have an answer.

## Where the analogy strains

The newspaper barbell was caused by *distribution* cost going to zero. The software barbell Vernal predicts is caused by *production* cost going to zero. Those are different variables, and the difference matters for who wins.

When distribution collapsed, Thompson's [[aggregation-theory]] says the winners were whoever owned demand, because supply had become abundant. Vernal's own account of the winners ("sheer amount of product *and* the strength of their GTM") quietly concedes that distribution has not collapsed for software — if anything it has become the scarce input. This is the same conclusion Evans reaches in [[ai-eats-the-world]] (distribution is the moat in commodity infrastructure) and Spiegel reaches in [[snapchat]] (software isn't a moat; AI makes distribution the binding constraint). Christensen's conservation of attractive profits, discussed under [[scarce-assets]], gives the general rule: when one layer becomes abundant, the adjacent layer becomes scarce. Abundant code makes brand, trust, and access to the buyer scarce. That is why branding rises in Vernal's reweighting, and why "one per buying center" is really a claim about who owns the buyer relationship, not about who has the most features.

So the heavy end of the barbell is defended by two different things at once: cumulative product (Vernal's emphasis) and owned distribution (the thing the newspaper analogy actually predicts). A company with only the first is exposed.

## Where the sides agree

Vernal's picture is consistent with several other agent-notes articles:

- [[commodity-trap]] (Narayanan & Kapur) lists the moats available "up the stack" from raw models: embedding and data gravity, ecosystem, vertical integration, behavioral lock-in, outcome pricing. "Own the buying center" is the SaaS-incumbent version of the same climb, and it implies frontier labs and AI-native SaaS will collide over the same buying centers.
- [[institutionalized-vs-improvised-software]] (Evans) explains why the heavy end doesn't dissolve into the light end: most people aren't builders, knowing what to build is the hard part, and institutional adoption is an org-wide purchase decision. That purchase decision is precisely the GTM half of Vernal's winner formula.
- [[solopreneur-economy]] (Stripe data) shows the light end already forming: solo businesses are being created faster and climbing the income distribution because AI fills capability gaps that used to force hiring.
- [[uncopyable-value]] (Kelly) explains what a small software business sells when the code itself is free: immediacy, personalization, patronage, authenticity. The Substack-shaped software SMB is selling generatives, not code.
- [[low-margin-ai-winners]] and [[outcome-based-pricing]] describe the delivery and pricing models the per-industry winner would plausibly use to "serve the buying center better than any competitor."

## Implications

- **Founders in a mid-sized point solution should assume the middle is the most dangerous place to be**, and choose a direction: expand toward owning the whole buying center, or shrink to a Substack-shaped business with matching capital structure. Raising venture money for the light end is the specific mistake Vernal warns about.
- **"One large software company per industry" is a claim about vertical software.** If it's right, the winner in a vertical (legal, medicine, government) is whoever owns the buyer relationship *and* has the most cumulative product, and the window to become that company is now, while the incumbents' switching-cost moats are still eroding rather than gone.
- **The reinvestment moat is a treadmill, not a wall.** Unlike a patent or a network effect, it only exists while you keep running. This makes capital allocation the central strategic question, which is why Vernal's Amazon framing is about *reinvesting profits* rather than raising them.
- **The "Substack for software" is unsettled.** Whoever becomes the platform or aggregator for the light end captures the same position Shopify and Substack did, and that layer may be the more venture-addressable opportunity than any individual small software business.

## Sources

- Vernal, Mike (2026). "Moats & the Barbell-ification of Software." X, September 15, 2026. <https://x.com/mvernal/status/2099885132379500562> — [[2026-09-15-moats-barbell-ification-of-software|local copy]]
