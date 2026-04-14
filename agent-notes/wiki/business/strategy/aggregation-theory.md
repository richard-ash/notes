---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2015-07-21-aggregation-theory.md
  - agent-notes/raw/business/strategy/2026-04-13-mythos-muse-opportunity-cost-compute.md
compiled_at: 2026-04-14
model: claude-opus-4-6
confidence: high
---

# Aggregation Theory

Aggregation Theory is Ben Thompson's framework for understanding how the Internet has restructured value chains across consumer industries. Introduced in 2015 on Stratechery, it has become one of the most cited mental models in tech strategy, explaining the dominance of Google, Facebook, Amazon, Netflix, Uber, Airbnb, and their successors.

## The core framework

Thompson observes that every consumer market has three layers: **suppliers**, **distributors**, and **consumers/users**. Outsize profits come from either monopolizing one layer or integrating two layers for a vertical advantage.

**Pre-Internet:** distribution was scarce and expensive. Incumbents integrated backward into supply — newspapers owned content creation, publishers controlled authors, taxi companies owned medallions and cars, hotels bundled brand trust with rooms. Because there were always more consumers than suppliers, and transactions were costly, controlling the supplier relationship gave distributors their leverage.

**Post-Internet:** two shifts inverted this dynamic:

1. **Distribution of digital goods became free** — neutralizing the advantage of backward integration with suppliers.
2. **Transaction costs went to zero** — making it viable to integrate forward with consumers at massive scale.

The result: competition shifted from exclusive supplier relationships to **user experience**. The best aggregators win the most users, which attracts the most suppliers, which further improves the experience — a virtuous cycle. Suppliers are commoditized; the consumer relationship becomes the scarce asset.

Thompson draws on Clay Christensen's *Conservation of Attractive Profits*: when one layer of a value chain is modularized (made interchangeable), profits shift to an adjacent layer that becomes integrated. Aggregators are the companies that modularize supply and integrate with demand.

## The pattern in practice

Thompson identifies a consistent two-step move across industries:

| Company | What they modularized | What they integrated |
|---------|----------------------|---------------------|
| **Google** | Individual pages/articles (previously bundled in publications) | Search results + user profile data → advertising |
| **Facebook** | Advertisements (targeting users directly, not via publisher proxy) | News feed inventory + profile data → advertising |
| **Amazon** | Book distribution (e-commerce, then e-books) | Customer data + payments + distribution |
| **Netflix** | Broadcast availability (full library, any time) | Content purchases + subscriber management |
| **Uber** | Fleet management (independent drivers replace owned fleets) | Dispatch + customer management |
| **Airbnb** | Vacant rooms (reputation system replaces brand trust) | Property management + customer management |

Thompson notes three waves of aggregation: **digital content** first (Google, easiest because content was always monetized by proxy), then **user-generated content** (Facebook, which uniquely has exclusive access to its supply), then **physical-world industries** where a critical function — trust, dispatch — could be digitized even though the underlying product couldn't (Uber, Airbnb).

## Winner-take-all dynamics

A key corollary: aggregators exhibit strong winner-take-all effects. They can serve every consumer on earth, and they get *better* with each additional user. This is why consumer tech companies command such high valuations — the ceiling is the entire addressable population.

Thompson proposes three diagnostic questions for identifying aggregation opportunities:

1. What is the critical differentiator for incumbents, and can some aspect of it be digitized?
2. If digitized, does competition shift to user experience — giving new entrants a structural advantage?
3. Can the winner generate a virtuous cycle where user ownership attracts suppliers and further improves the experience?

## The AI challenge: opportunity costs, not marginal costs

Writing eleven years later (2026), Thompson revisited Aggregation Theory in light of AI. Doug O'Laughlin (Fabricated Knowledge) argued that reasoning models like o1 broke the paradigm by reintroducing meaningful marginal costs — each inference costs real compute, unlike the zero-marginal-cost Internet era.

Thompson argues this framing is wrong. AI compute is still a fixed cost: chips are purchased regardless, electricity is a fraction of chip cost, and no one with AI accelerators is leaving them idle. The real constraint is **opportunity cost** — compute allocated to one workload cannot serve another.

This distinction matters enormously:

- **Microsoft** missed Azure growth targets not from lack of demand but because it prioritized internal workloads (M365 Copilot, GitHub Copilot) with higher margins. CFO Amy Hood noted Azure KPI would have exceeded 40% growth if all new GPUs had been allocated to Azure.
- **Anthropic** withholds its most advanced model (Mythos) not because serving it would be unprofitable per-query, but because the compute has higher-value uses and the company is already capacity-constrained.
- **Every hyperscaler** faces the same balancing act: Microsoft (Azure vs. its own software), Amazon (AWS vs. e-commerce vs. Anthropic/OpenAI investments), Google (GCP vs. consumer products vs. Anthropic investment).

## Distillation as a competitive weapon

Frontier labs face a second strategic pressure: open-source models that undercut pricing power via **distillation** — training cheaper models on frontier model outputs. Anthropic identified industrial-scale distillation campaigns by DeepSeek, Moonshot, and MiniMax involving 16 million exchanges through 24,000 fraudulent accounts.

Thompson observes a double incentive for frontier labs to combat distillation: protecting margins is obvious, but there's a second-order effect. If open-source models become less capable (because they can't distill), the compute that would have run them becomes less valuable to enterprises — and therefore cheaper for frontier labs to acquire. Stopping distillation is simultaneously revenue-protection and compute-acquisition strategy.

## Meta's structural advantage

Thompson argues Meta occupies a uniquely advantaged position because it is the only major player without an enterprise/cloud business creating opportunity-cost tension. Every GPU Meta deploys serves its consumer products — no competing internal demand from a cloud division.

Combined with Meta's advertising engine, this means Meta can pursue consumer AI with full focus while Anthropic and OpenAI are increasingly tempted to prioritize lucrative enterprise and [[agentic-engineering-architecture|agentic]] workloads. Thompson suggests Meta should open-source its Muse model family: a widely available frontier-quality open model would erode competitors' pricing power and make the consumer market less attractive for them — leaving it to Meta.

## Does Aggregation Theory survive the AI era?

Thompson's conclusion: yes, with caveats. The two preconditions — zero distribution costs and zero transaction costs — still hold. The company that builds the most compelling product wins the most users, generating revenue to acquire compute.

The nuance is that compute constraints create a period where companies *cannot serve everyone* — serving one customer base imposes a real opportunity cost. This won't last forever; eventually AI will be "good enough" for enough use cases that compute supply catches up. But as of early 2026, Thompson notes that theoretical future "feels further away than ever."

The open question: does supply-side advantage (OpenAI's bet — more compute, better models) ultimately determine demand-side dominance? Or does demand-side momentum (Anthropic's trajectory) generate the cash flow to acquire sufficient supply? Thompson bets on demand but acknowledges the circularity.

## Sources

- Thompson, Ben (2015). "Aggregation Theory." <https://stratechery.com/2015/aggregation-theory/> — [[2015-07-21-aggregation-theory|local copy]]
- Thompson, Ben (2026). "Mythos, Muse, and the Opportunity Cost of Compute." <https://stratechery.com/2026/mythos-muse-and-the-opportunity-cost-of-compute/> — [[2026-04-13-mythos-muse-opportunity-cost-compute|local copy]]
