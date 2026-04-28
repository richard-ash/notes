---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2013-06-23-dozen-things-about-business.md
  - agent-notes/raw/business/strategy/2019-09-19-taxonomy-of-moats.md
compiled_at: 2026-04-27
model: claude-opus-4-7
confidence: high
---

# Competitive Moats

A taxonomy of sustainable competitive advantages — what Buffett calls "moats" — and the structural mechanisms underneath them. The central question: what makes a business durably defensible rather than temporarily profitable, and which of these mechanisms are actually available to a startup at founding?

## The four structural sources (Neumann)

Neumann argues that the dozens of named moats in the Porter / Rumelt / Helmer / Greenwald / Mauboussin canon all reduce to **four** underlying mechanisms — three are ways to acquire non-business power, one is a self-reinforcing dynamic. Every moat in the wild is some combination of these:

1. **The state.** Government action — patents, licensing, tariffs, regulatory standards, oligopoly grants, antitrust exemptions, national champions — restricts competition either by direct grant or by enforcing private property and contractual exclusivity (mineral rights, supplier exclusives, distribution lock-ins). Durability is whatever the government says it is.
2. **Special know-how.** Knowledge competitors don't have. Subdivides into:
   - *Closely-held* (recipes, algorithms, designs) — leaks within ~12 months on average per Mansfield's industrial-diffusion study; sustainable only as long as secrecy holds, which is rarely long.
   - *Individual tacit* (the engineer who can fix any process) — non-transferable through writing, but goes down the elevator every night.
   - *Collective tacit* (organizational routines, embedded ways of working between people) — durable, hard to poach, but takes years of organizational maturation to form.
3. **Returns to scale.** Economies of scale (lower unit cost), economies of scope (shared fixed costs across products), supplier bargaining power, network effects (each user makes the product more valuable to all others), two-sided marketplace dynamics, platform ecosystem effects, and risk-pooling (insurance, R&D portfolios).
4. **System rigidity.** The product is embedded in a network of complements, routines, skills, and norms that make switching costly even when a strictly better product exists. Switching costs, complementary-asset lock-in, intentional bundling, complementary-platform dependencies, and even cultural/religious/societal mores favoring incumbents.

Neumann is explicit that he excludes management talent, founder vision, and culture-as-vibe from this list — those are usually surface evidence of *individual competence*, which is a property of the person, not the firm. (Collective tacit knowledge is the form in which culture shows up as a real moat.)

## Why startups almost never have a moat at founding

Neumann's most uncomfortable claim: **none of the four sources is reliably available to a high-growth-potential startup at day one.** Each fails for a different reason:

- **State-granted moats are fungible.** A patent worth $X to a startup is worth $X to an incumbent — so an efficient market should bid the patent price up to its NPV, leaving no surplus for the startup. (The case studies of researchers who *did* capture surplus by founding rather than selling — Page and Brin, biotech founders — are precisely cases where the asset's value was *not* known at the time of founding.)
- **Special know-how leaks.** Closely-held knowledge typically leaks within a year via employee mobility (Samuel Slater memorized the British cotton mill and rebuilt it in Connecticut; Detroit and Silicon Valley genealogies trace through founder movement). Individual tacit knowledge can be poached. Only *collective* tacit knowledge is durable, and by definition it cannot exist before the organization does.
- **Returns to scale require scale.** A company with no users has no network effects. The cost-side advantages don't kick in until volume is large enough.
- **System rigidity requires system embedding.** A new product has no complements, no installed base, no learned routines around it. In fact rigidity *works against* the startup at this stage — the incumbent's product is the one already embedded.

Connection to [[entrepreneurial-profit|Schumpeter's model]]: this is the same observation viewed from the other side. Schumpeter says surplus profit comes from innovation and decays as imitators enter; the moat literature says *which* mechanisms can slow that decay. The four sources are the menu of decay-slowing tools, and the reason most of them are unavailable at founding is that they all need *time* or *money* (for state-granted moats, an existing market price) — neither of which a startup has.

### Uncertainty as the only first-day moat

Neumann's payoff: if the moat options above are unavailable at founding, **what protects the startup from competition during the years it takes to build a real moat?** His answer: uncertainty itself. A startup exists, in his framing, precisely when the founders disagree with the market's valuation of an asset (a patent, a piece of know-how, a market hypothesis). If everyone *knew* the future cash flows, an incumbent would buy the input rather than let a startup form.

So uncertainty is not a nuisance to be eliminated — it is the structural feature that lets a startup exist at all. Once the uncertainty resolves (the product is shown to work, the market reveals itself), the founding-day advantage evaporates and the startup has to have built one of the four real moats by then. **Uncertainty is a *temporary* moat, and the strategic clock starts the moment the market starts to believe.**

This reframes the early-stage question. The job is not "find a startup with a moat" — none have one. The job is "find a startup whose uncertainty window is long enough, and whose path to a real moat is plausible enough, that they survive the transition." Network effects, collective tacit knowledge, and system rigidity are all moats that *grow under cover of uncertainty*. State-granted moats and individual know-how generally don't, which is why they're rarely the foundation of breakout companies.

## The disruption / value-chain wrinkle

System rigidity also runs in startups' favor in one specific configuration: when the *incumbent's* embedded position is itself the constraint. Christensen's *disruptive innovation* and Porter's *value chain innovation* are two formulations of the same point — the incumbent can't imitate the new model without breaking expensive existing relationships (commissioned sales force, dealer network, premium customer base, cost structure tied to legacy assets). Neumann calls this "half a moat": the startup is protected from the incumbent's response but not from other startups or well-resourced lateral entrants.

The discount-brokerage case (Schwab/Fidelity vs. traditional commission-driven brokers) is the canonical example: full-service firms couldn't follow without firing their sales force.

## Practitioner observations (Griffin)

Tren Griffin's 2013 collection of business aphorisms maps onto the four-source taxonomy and adds operator-level observations:

**Moat hierarchy by durability** (Griffin via Wilson and Porter):
1. **Network effects** — the strongest moat. Winner-take-most in markets where each user increases value for all others. (This is Neumann's "scale" source in its strongest form.)
2. **Differentiation through strategic focus** — Porter: "A strategy delineates a territory in which a company seeks to be unique." Strategy is defined as much by what you choose *not* to do as by what you do. (See [[strategy-execution|Vermeulen's "coherent set of choices"]] — focus is the precondition for any of the four sources to compound.)
3. **Operational specialization** — doing a few things extraordinarily well over long horizons, where scale advantages compound when scope stays narrow (Costco, hawker stands, Dick's Drive-In).
4. **Scalable back-end systems** — physical businesses can build moats, but usually only when powered by great software infrastructure (Amazon, Walmart, McDonald's).

**Optionality and asymmetric bets** complement moat-building. Sam Zell's heuristic: low downside + big upside → go; big downside + small upside → run; big downside + big upside → the only case requiring real work. Taleb formalizes this as **convexity** — embrace propositions that benefit from randomness (unlimited upside, capped downside), avoid concave ones. This maps to how Munger sizes bets: concentrate heavily when odds are substantially in your favor.

**Supply, scarcity, and pricing.** Bill Gates: "Supply is the killer of value." Abundant supply creates platforms, but profit accrues only to whoever attaches something *scarce* on top. Griffin calls the belief that supply itself creates value "George Gilder's folly" — Metcalfe himself noted that no one made a nickel on Ethernet itself; profit came from selling things atop the standard.

**Margin pools and the Bezos doctrine.** "Your margin is my opportunity." High margins attract competition. Companies that deliberately keep margins thin and pass value to customers create a self-reinforcing flywheel that *is* a form of moat — competitors find no margin pool to fund entry. This connects to [[aggregation-theory|Aggregation Theory]]'s observation that zero-distribution-cost platforms commoditize supply and own demand.

**Cash as survival.** Harold Geneen: "The only unforgivable sin in business is to run out of cash." Accounting bankruptcy is survivable; actual illiquidity is fatal. Griffin endorses Munger's view that EBITDA should be mentally replaced with the word "bullshit" — interest, taxes, and depreciation are real expenses of the worst kind.

**Customer acquisition.** Bill Gurley: a customer who *chooses* your product is worth far more than one acquired through spend. Marketing must be tracked per-customer, not as a lump sum. This reinforces why moats matter: they reduce CAC to near zero by making the product the obvious choice.

**Hiring.** Peter Schutz (former Porsche CEO): "Hire character. Train skill." Character is the scarce input; skill is the trainable one — the moat logic applied to human capital.

## Implications for early-stage strategy

Combining Neumann's structural taxonomy with Griffin's practitioner heuristics produces a coherent stance:

- **Don't claim a moat you don't yet have.** Pitch decks that list "network effects" or "patent moat" for a five-person company are usually claiming the *eventual* moat as if it already exists. The question to ask is whether the path from current state to that moat is plausible under the uncertainty window the company is operating in.
- **Pick a moat shape compatible with the founding asset.** A startup with a deep-tech innovation has a state-granted (patent) and special-know-how starting position; the strategic task is converting those before they leak into either scale (network effects, learning curves) or system rigidity (workflow integration, complementary asset accumulation). A startup with a market-timing insight (e.g. [[data-content-loops|data-content loops]]) has *only* the uncertainty window — every dollar should buy faster scale.
- **Treat collective tacit knowledge as a real long-run moat.** Goldman Sachs, top consulting firms, the elite hedge funds, and the best operating cultures all have it. It is the moat that doesn't show up in 10-Ks but explains decades of outperformance. It is also the only "culture" that survives the [[strategy-execution|formulation/execution lens]] — culture as a coherent set of routines that make the strategy hard to copy.
- **Use system rigidity *against* incumbents, not as your own moat.** The disruption configuration is a free year or two of cover from the largest competitor. But it's not a moat — and well-resourced lateral entrants can still kill you. Use the cover to build one of the four real moats.

## Temporal notes

The Griffin source is from 2013, the Neumann source from 2019. The taxonomy remains sound; the relative weights have shifted:

- **Network effects have proven even more dominant than anticipated** — winner-take-all in social, search, and major marketplaces. The marketplaces wave Griffin pointed at became the dominant equity-value-creating shape of the 2010s.
- **AI foundation models have introduced an open question** about whether [[ai-platform-moats|model capabilities constitute a moat]] in any of Neumann's four senses, or are rapidly commoditized. Evans's argument is that they have neither the network effects, the collective tacit knowledge, nor the system rigidity of true platforms — which would mean their entrepreneurial-profit window is short despite huge spike heights.
- **The "supply kills value" principle has played out dramatically in content** (journalism, music, video) where infinite digital supply destroyed per-unit pricing and pushed profit to whoever owns scarce *demand* (the [[aggregation-theory|Aggregators]]).
- **Collective tacit knowledge has become more important relative to closely-held knowledge** as employee mobility, public APIs, and open source have accelerated leak rates of explicit knowledge. Hard-to-articulate organizational routines remain the slowest-leaking asset class.

## Sources

- Neumann, Jerry (2019). "A Taxonomy of Moats." *Reaction Wheel*, September 19, 2019. <https://reactionwheel.net/2019/09/a-taxonomy-of-moats.html> — [[2019-09-19-taxonomy-of-moats|local copy]]
- Griffin, Tren (2013). "A Dozen Things I've Learned About Business." <https://25iq.com/2013/06/23/a-dozen-things-ive-learned-about-business-in-999-words/> — [[2013-06-23-dozen-things-about-business|local copy]]
