---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2026-07-10-ais-biggest-winners-lowest-margins.md
compiled_at: 2026-07-17
model: claude-opus-4-8[1m]
confidence: medium
---

# Low-Margin Businesses as AI's Biggest Winners

An argument by **@dkfromdk** (a founder of Varick Agents, an AI-services firm) that the largest AI value capture won't accrue to the tech-forward companies everyone watches, but to the thin-margin, labour-heavy operators — manufacturers, trucking carriers, distributors, staffing agencies, field-service and facilities businesses, healthcare clinics — that nobody would call "AI companies." The essay is a vendor thesis (it closes with a pitch), so its structural claims are more durable than its specific numbers, which are illustrative rather than sourced.

## The core argument: profit leverage, not efficiency

AI transformation creates value on three levers — revenue, cost, and risk — and most attention has gone to revenue (better products, faster sales, more productive workers). The author's claim is that for low-margin businesses the decisive lever is **cost**, because thin margins convert small cost reductions into large *profit* swings:

- A software company at 30% margins that gets more efficient stays on the same trajectory — the gain is real but not transformative.
- A business at 3% margins is different: a **<1% cost reduction can be a >25% profit increase**. The math is pure operating leverage — profit is the small residual after a large cost base, so shaving the cost base moves profit disproportionately.

The strategic consequence: early movers *bank* the gain as margin. In a commoditised market, efficiency eventually spreads and competition forces the savings back into lower prices — but the firms that move first capture the earnings uplift and reset their cost position before that happens. This is why the author frames it as a race, not a steady-state opportunity.

## The structural margin trap

Low-margin operators are locked in by three reinforcing conditions: they compete in commoditised markets, have limited pricing power (the market sets the price, not the firm), and carry large operating cost bases that were historically impossible to cut without degrading service. Because they can't move price, **cost is the only lever they control** — and a large share of that cost is labour.

## The specific target: the coordination layer, not frontline labour

The essay's sharpest move is redefining *what* AI attacks. The naive framing is "replace a task / cut headcount / make a worker faster." The author argues the addressable spend, given today's AI capabilities, is the **work behind the work** — the coordination overhead that keeps messy human operations moving: scheduling, dispatching, approvals, exception handling, routing, claims, invoices, back-office reconciliation, and the layer of managers, supervisors, analysts, finance and ops staff who run it.

Why this layer exists: human work is inherently variable — people make judgment calls differently and each carries their own context — so an organisation grows a coordination layer to keep that variance reliable. That layer is the tax on human messiness.

Illustrative unit economics offered:
- Labour ≈ **25% of revenue** in these businesses.
- Roughly a quarter of that labour is coordination/administration ≈ **6% of revenue**.
- For a 3%-margin firm, easing coordination by 10% → **~20% earnings improvement**.
- A logistics client's coordination spend (dispatch, routing changes, customer updates, claims, invoices, exceptions, reconciliation) was ≈ **10% of revenue** — the pool they attacked.

These figures are the author's, unsourced, and should be read as a sizing heuristic rather than measured fact.

## The adoption paradox and the "infrastructure, not tools" thesis

The essay's second half is the more generalizable idea, and it applies well beyond low-margin firms. The paradox: **the companies with the most to gain from AI are the least able to adopt it.** Enterprise AI is mostly sold as a tool that assumes a behaviour change — the employee opens a new interface, remembers when to use it, decides which tasks it applies to, and translates the output back into their existing workflow. That assumption fails even inside tech-forward companies; in a non-technical, change-resistant workforce it fails harder. A tool becomes "another place work has to happen" instead of a thing that removes work.

The prescription — **sell AI as infrastructure, not software**:
- Software asks the employee to adopt a tool. Infrastructure changes the operating layer *underneath* the employee.
- The agent runs across the systems where work already happens — NetSuite, email, PDFs, spreadsheets, inboxes, approvals — rather than adding a new surface. For accounts payable: extract the invoice, match it to the PO, flag the exception, prepare the approval, route to a human *only when judgment is needed*, and learn from the approval feedback over time.
- Value is *engineered into the deployment* rather than dependent on someone remembering to use the AI each day.
- Human control is preserved by exception, not by default: the employee still sees what happened, and the process owner can pause the workflow, change a rule, approve an exception, or pull a person back in.

This is a claim about the *interface* of enterprise AI: the winning form factor is an agent embedded in existing workflows, surfacing to humans only for judgment calls — which rhymes with [[messaging-as-ai-interface]]'s argument that agents should meet people through affordances they already use rather than demanding a new destination app.

## Connections and where this sits

- **Delivery model.** "Sell AI as infrastructure" pairs naturally with [[outcome-based-pricing]]: if value is engineered into the operating layer and doesn't depend on seat-level usage, per-seat/per-token pricing is a poor fit, and charging per realised business outcome (an approved invoice, a resolved exception) aligns vendor and buyer. The essay implies this without naming the pricing model.
- **Which tasks are actually automatable.** The coordination-layer thesis is optimistic about how much of that work AI can absorb. It sits in tension with the labour-economics literature: [[messy-jobs]] argues jobs are bundles where AI substitutes only when a weak component can be *cheaply separated* from the whole, and [[ai-and-relational-scarcity]] argues the residual decision-rights and accountability roles (Arrow's trust, Williamson's hold-up, Hart–Moore authority) are exactly the coordination functions AI structurally cannot yet hold. The author's "route to a human only when judgment is needed" is, in effect, a concession to those boundaries — the durable human role is the judgment residue after the routine coordination is automated. Whether coordination is mostly routine (author's bet) or mostly judgment (the skeptics' bet) is the crux.
- **Task automation vs. paradigm replacement.** The essay is a within-paradigm efficiency story ([[task-automation-vs-paradigm-replacement]]): it does not claim AI reinvents logistics or manufacturing, only that it strips out a coordination cost that was previously treated as permanent. That modesty is a feature — it's why the near-term profit case is plausible.

## Skeptic's read

The thesis is coherent but self-interested (Varick sells exactly this transformation), so weigh it accordingly:
- The **early-mover margin** and the **eventual competition-forces-it-into-price** claims can't both be permanent — the framing is explicitly transitional, which is honest but means the moat is timing, not structure. In a commoditised market with no pricing power, the equilibrium is that the savings become table stakes and the customer, not the operator, captures them. The durable winners in that world may be the AI-infrastructure *providers*, not the low-margin operators.
- The unit-economics numbers (25% labour, 6% coordination, 10% reduction → 20% earnings) are unsourced round numbers doing a lot of work; the mechanism (operating leverage on thin margins) is sound regardless.
- "Route to a human only when judgment is needed" quietly relocates the hard problem into the exception path — the reliability, liability, and error-handling of that boundary is where deployments actually succeed or fail, and the essay treats it as solved.

## Sources
- @dkfromdk (2026). "AI's Biggest Winners Have the Lowest Margins." <https://x.com/dkfromdk/status/2075696599242821979> — [[2026-07-10-ais-biggest-winners-lowest-margins|local copy]]
