---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-07-06-zhang-open-source-enterprise.md
compiled_at: 2026-07-07
model: claude-opus-4-8
confidence: medium
---

# Open Source vs Closed Models in the Enterprise

Jesse Zhang (CEO of Decagon, a customer-service AI-agent company) argues that the widely-cited fact — open-source models fell to **11% of enterprise LLM spend in 2026, down from 19% a year earlier** — is being read exactly backwards. The popular narrative says open source is losing to the frontier labs. Zhang's claim is that the declining share is a **denominator artifact of where enterprise AI sits on a use-case maturity curve**, and that the same force will eventually invert the trend.

The load-bearing idea is the **maturity curve**: whether open or closed wins for a given deployment is not a fixed property of the models — it's a function of how mature the *use case* is. Discovery favors closed frontier models; mature production favors small, fine-tuned open-weights models. The aggregate number moves with the mix of immature vs mature use cases, not with either model class winning on the merits.

## The apparent paradox

Two facts point in opposite directions:

- **Decagon runs ~90% of its workloads on open-source models** (not OpenAI/Anthropic), and Zhang says this is typical of hypergrowth app companies, with large enterprises moving the same way.
- **Enterprise LLM spend as a whole moved *toward* closed** — open-source share fell from 19% → 11% year over year.

If open source were simply winning or losing, these wouldn't both be true. The resolution is that Decagon and the aggregate enterprise are at *different points on the same curve*.

## Why Decagon is 90% open source

Zhang is explicit that the reason was **not cost and not customer demand** — it was that no other option existed for the constraint that binds his product:

- **Latency makes or breaks a live customer-service agent.** An 8-second-per-turn conversation is not a product anyone will use. That forces **small, fast models** — a call answering a support question doesn't need to know the capital of Lithuania or high-school physics.
- **Small models out of the box miss the quality bar.** They only clear it through **heavy fine-tuning on the exact task**.
- **The frontier labs don't sell that combination.** You can't fine-tune their best models the way Decagon needs, and their small models "aren't ours to shape." *Small + fine-tuned means open weights.*

Cost savings are real but **secondary**; enterprise comfort with self-hosted models is a **side effect, not the driver**. This is a sharper version of the open-weights case than the pure-price argument in the [[ai-lab-economics|Shaughnessy bear case]]: there, open weights win because they're ~1/30th the price; here, they win because the *shape of the product* (small + fine-tuned + self-hosted) is one the frontier labs structurally don't offer at all. Price is downstream.

## The use-case maturity curve

The core mechanism:

- **New use case → buy general intelligence.** You don't know the shape of the problem yet — the input distribution, the required behaviors, the failure modes — so you pay a premium for the smartest general-purpose model, including intelligence you may never end up needing. That is the *correct* trade at that stage.
- **Mature use case → the trade flips.** Once the distribution of inputs, the needed behaviors, and the failure modes are known, general intelligence becomes **overhead**. Now you want the smallest, fastest model fine-tuned to do your specific thing extremely well.

Customer service is one of the *most* mature AI use cases in the industry — well-understood workflows, enormous conversation volume, tight quality bars. So Decagon isn't special; it's just **further along the curve** than the average enterprise deployment. The 90%-vs-11% gap is a gap in maturity, not in conviction.

This is the specialization side of the same "AI compresses the middle of the work" family as [[decide-execute-deliver-sandwich|Narayanan's decide-execute-deliver sandwich]]: a mature use case is one where the *decide* layer (what behaviors, what failure modes) has been solved, leaving a narrow, well-specified *execute* task — exactly the thing a small fine-tuned model can absorb.

## The denominator explanation

Zhang's resolution of the paradox: the 11% is a **denominator problem**.

- In 2026, enterprises "stopped building and started buying," and **thousands of brand-new use cases spun up at once**.
- New use cases run on frontier models (per the curve above), so **closed-model share exploded**.
- The pool of *immature* use cases is growing faster than the pool of *mature* ones — so open source's *share* falls even as the absolute number of eventual open-source migrations grows.

Enterprise AI as a whole is at the *very beginning* of the maturity curve. The falling share is a signal of a rapidly-expanding frontier of new experiments, not of open source losing the mature ones.

## Division of labor: discovery vs production

The forward-looking claim, and the durable one worth keeping:

> The frontier labs will keep owning **discovery**. Open source will increasingly own **production**.

Every use case prototyped on a frontier model today is a **future open-source migration**. As a deployment matures, the company does what Decagon did: distill, fine-tune, specialize. This is a specific, testable shape for the [[ai-eats-the-world|"value moves up the stack / models become commodity infra"]] thesis — it says *where* the commoditization happens (mature production workloads) and *where* the premium persists (early discovery), rather than predicting uniform commoditization. It also maps onto swyx's [[ai-lab-economics|model-lab / agent-lab split]]: agent labs like Decagon are the natural operators of the mature-production layer where fine-tuned open weights dominate, while model labs own the discovery layer where general intelligence is worth the premium.

## Why the inflection is years away

Zhang explicitly caveats his own bull case — the open-source share will inflect up, but "it won't happen for many years":

- Most use cases have **not finalized the "shape" of the agent**, so fine-tuning open weights isn't yet worth it.
- **Fine-tuning takes effort and expertise most organizations lack.** The use case has to be very high-ROI *and* already fully deployed at scale to justify it.
- You need **enough data** to verify the small model matches the frontier model on the specific task.
- Otherwise it's simply **easier to plug in a closed frontier model** — no infrastructure to own, and freedom to iterate and experiment.

So the migration is a **trailing** phenomenon: it lags deployment maturity, which itself lags the current buying wave by years. The share number can keep falling for a while before it turns.

## Implications

- **The 11%/19% number is not a scoreboard.** Read it as a maturity indicator: a low open-source share means the enterprise install base is young, not that open weights are inferior.
- **Open source wins on product shape before it wins on price.** Decagon's driver was latency → small + fine-tuned + self-hosted, a combination the frontier labs don't sell. Price is the secondary reason, which complicates the pure-cost version of the [[ai-lab-economics|open-weights escape valve]].
- **Discovery and production may durably split across model classes.** If Zhang is right, the equilibrium isn't "closed wins" or "open wins" but a two-layer market: closed for prototyping unknown-shape problems, open for running known-shape ones at scale.
- **Fine-tuning capability is the gating resource.** The inflection is bottlenecked less by model quality (the closed/open gap is already "low single digits") than by organizations' ability to specialize — data, expertise, and a use case mature enough to justify the effort.

## Connections

- [[ai-lab-economics]] — swyx's model-lab/agent-lab split (agent labs operate the mature-production layer) and Shaughnessy's open-weights escape valve; Zhang's maturity-curve argument is a *complementary* mechanism for why open weights win production, grounded in product shape (latency → small + fine-tuned) rather than price
- [[ai-eats-the-world]] — Evans's commodity-models / value-up-the-stack thesis; Zhang localizes it to *mature production workloads* and preserves a frontier premium for *discovery*
- [[decide-execute-deliver-sandwich]] — a mature use case is one where the *decide* layer is solved, leaving a narrow *execute* task a small fine-tuned model can own
- [[enterprise-agentic-coding-adoption]] — Airbnb's "tool-calling is all you need" choice (re-wrap internal RAG as an MCP tool rather than fine-tune) is a data point on the *other* side of Zhang's curve: even a large, sophisticated org defaulted away from fine-tuning because the use case wasn't yet worth specializing

## Sources
- Zhang, J. (@thejessezhang). "Everyone is wrong about open source AI in the enterprise." *X* (2026-07-06). <https://x.com/thejessezhang/status/2074154325933424861> — [[2026-07-06-zhang-open-source-enterprise|local copy]]
