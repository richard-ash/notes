---
source: agent
compiled_from:
  - agent-notes/raw/business/finance/2022-03-18-accounting-for-saas-and-swords.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: medium
---

# Revenue Recognition

Revenue recognition is the accounting process by which a business determines when money received from customers actually counts as "revenue." The concept rests on a deeper insight: money has *colour* — the same dollar amount can represent fundamentally different things depending on context, timing, and obligations.

## The Three Tests

Accounting broadly requires three conditions before money qualifies as revenue:

1. **Known amount** — the exact sum to be collected is determinable.
2. **Performance complete** — the product has been delivered or the service fully rendered.
3. **Collectibility** — there is reasonable confidence the money will actually be received.

The rationale is that accounting should perceive the world as it actually exists. A business that has fulfilled its obligations to a creditworthy customer has earned revenue regardless of whether the payment has literally arrived. Conversely, money received for work not yet performed is not revenue — it is a **liability**.

## Revenue Recognition in SaaS

SaaS companies commonly track monthly recurring revenue (MRR), a non-GAAP metric that McKenzie notes accountants find distasteful precisely because it conflates different colours of money. The practical difficulties compound when companies offer annual plans at a discount (e.g., 12 months for the price of 10):

- **Common MRR bugs**: booking the full annual payment as a single month's MRR (massive overstatement); counting the undiscounted monthly rate (ignoring the discount); or showing an artificial MRR dip during the "free" months despite no change in the customer relationship.
- **Accounting's answer**: recognize revenue *daily*, ratably over the commitment period. Revenue for a 12-month annual plan accrues each day across those 12 months, regardless of when cash arrives.

Money received but not yet recognized becomes **deferred revenue** — a balance-sheet liability representing unperformed obligations. This distinction matters acutely for [[capital-allocation|valuations and acquisitions]]: when McKenzie sold his SaaS business, the buyer valued annual-contract revenue lower than monthly MRR because the annual contracts carried months of unperformed service obligations. At small scale, annual contracts can actually be worth less than monthly ones — the reverse of the conventional wisdom at larger SaaS companies where reduced churn risk makes annuals more valuable.

IFRS 15 (effective 2018) formalized much of this by requiring companies to align revenue math with economic substance of contracts.

## Revenue Recognition for Virtual Goods

The question gets stranger when applied to in-game purchases. McKenzie argues that when a player buys premium currency (e.g., gems), they are not paying for the currency itself — they are paying for future access to in-game items and services. The implicit contract includes "you will continue running this game so I can spend these gems."

This creates an embedded service element that forces a potions-vs-swords distinction:

### Consumables ("Potions")

Temporary items — speed boosts, level skips, single-use buffs — can have revenue recognized at the moment of consumption. Performance is complete when the potion is "drunk."

### Durables ("Swords")

Permanent items must have revenue recognized ratably over their **economically useful life**. Since there is little accounting precedent for estimating the useful life of an imaginary sword directly, companies typically use the player's predicted remaining engagement with the game as a proxy. This causes bookings (cash received) to diverge sharply from recognized revenue, depressing reported financials.

### Game Mechanics as Accounting Optimizations

McKenzie makes a striking observation: gacha-game mechanics that require "burning" multiple copies of an item to upgrade it may partly function as accounting optimizations. When a Sword of Slightly Less Awesome is sacrificed to forge a Sword of Awesomeness, the sacrificed item has no remaining useful life — its deferred revenue liability can be recognized immediately. This reduces the drag of unearned revenue on the balance sheet, making the company appear more valuable. "Accounting standards have destroyed more imaginary swords than all the rust monsters in all the prime material planes combined."

### The Goblin's Perpetual Bond

A mobile game offering an in-game "bank" that pays 10 gems/day forever for a 1,000-gem purchase is not actually creating a perpetual bond liability — the bond is fiction, and accounting is concerned with reality. The economic substance is a prepaid variable discount on future purchases. Revenue is recognized ratably over the player's predicted remaining lifetime in the game.

## The Colour of Money — Broader Implications

McKenzie frames revenue recognition as one instance of a general principle: money has colour (provenance, obligations, regulatory status), and systems that handle money must perceive those colours accurately. Other dimensions include KYC status, risk ratings, and regulatory classification.

This has two practical consequences:

1. **For builders**: financial systems that model money as "just numbers" will eventually need to be rebuilt as they encounter more colours. The apparent simplicity of money math is deceptive.
2. **For policymakers**: every new regulatory colour (classification, reporting requirement) is implicitly a vote for fewer, larger systems capable of perceiving it — which can conflict with goals like promoting competition and avoiding systemic concentration.

The concept connects to Matthew Skala's "colour of bits" — the idea that identical data carries non-inspectable metadata (provenance, intent, legal status) that society treats as meaningful even when computers cannot distinguish it.

## Temporal Notes

This article was published in March 2022. Since then, IFRS 15 adoption is mature and no longer novel. The broader principles — deferred revenue as liability, ratable recognition over service periods, the colour-of-money framework — remain fully current. [[startup-growth-metrics|SaaS growth metrics]] continue to use MRR despite the accounting tensions McKenzie describes.

## Sources

- McKenzie, Patrick (2022). "Accounting for SaaS and swords." <https://www.bitsaboutmoney.com/archive/accounting-for-saas-and-swords/> — [[2022-03-18-accounting-for-saas-and-swords|local copy]]
