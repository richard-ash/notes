---
source: agent
compiled_from:
  - agent-notes/raw/health/2026-04-10-openevidence-morgan-stanley-deep-dive.md
compiled_at: 2026-04-10
model: claude-opus-4-6
confidence: medium
---

# OpenEvidence

OpenEvidence is an AI-powered medical search and clinical decision support platform, founded in 2022 by Daniel Nadler (ex-Kensho, acquired by S&P Global in 2018) and Zachary Ziegler (Harvard ML/NLP researcher). It answers clinical questions with citations from peer-reviewed literature, and has since expanded along the clinician workflow into ambient scribing (Visits) and a HIPAA-secure Dialer. By early 2026 it had reached a ~$6B valuation and was positioned as the central competitive debate in the clinical decision support (CDS) market, threatening incumbents Doximity (DoxGPT) and Wolters Kluwer's UpToDate.

## Product and distribution model

OpenEvidence is free to any U.S. clinician who verifies their National Provider Identifier (NPI). This "viral," doctor-centric distribution bypasses the long institutional procurement cycles typical of healthcare software — monetization happens instead through targeted pharma advertising inside the product, modeled on the HCP-marketing channels pioneered by Doximity and Medscape. Morgan Stanley estimates the total U.S. pharma marketing TAM at ~$33B (~$23B HCP-directed, ~$10B DTC).

Core capabilities:
- **Evidence-grounded search** over PubMed (>39m citations/abstracts) plus full-text content from multi-year agreements with NEJM Group (Feb 2025) and JAMA Network (Jun 2025), and guideline content from NCCN, ACC, ACEP, ADA.
- **DeepConsult** — an autonomous literature-synthesis agent for more complex cross-referenced questions.
- **Visits** (Aug 2025) — ambient scribe that transcribes patient visits, drafts notes, and enriches them with evidence citations.
- **Dialer** (Dec 2025) — HIPAA-secure iOS/Android dialer with practice caller-ID and optional Visits integration to auto-generate a clinical note from the call.
- **Enterprise distribution** via embedding into Microsoft Dragon Copilot.

Usage (late 2025): ~300–400K monthly active users overall, 100K+ U.S. physicians monthly (~10–25% of ~1M U.S. physicians). The company claims daily use by "over 40% of physicians in the United States." Annualized ad revenue reached $50m in July 2025, with reports of a materially higher run rate exiting 2025.

## The competitive triangle: OpenEvidence vs. DoxGPT vs. UpToDate

Morgan Stanley frames a three-way convergence between products that started from different anchors:

| | OpenEvidence | DoxGPT (Doximity) | UpToDate (Wolters Kluwer) |
|---|---|---|---|
| Anchor | Evidence-grounded search + citations | Workflow assistant inside a physician network (650K prescribers) | Expert-authored curated topic reviews since 1992 (13,000+ topics, 7,600+ authors) |
| Content model | Licensed journals + PubMed | Pathway's structured dataset + 2,000+ journals (via Research Solutions referral) | Proprietary curated content maintained by subject-matter experts |
| Price | Free to verified clinicians | Free within Doximity | Paid subscription (individual + enterprise) |
| Userbase | 300–400K MAU | 650K prescribers | 3M+ clinicians in 190+ countries |
| Monetization | Pharma advertising | Pharma advertising | Subscription revenue (CDS is ~10% of WKL group) |

MS argues these three "will converge" toward a common platform layer that combines **high-trust content + AI-native synthesis + in-workflow activation**. OpenEvidence's 2025 push into ambient scribe + dialer is the clearest signal of that convergence — moving from a standalone answer engine toward owning more of the end-to-end clinician workflow.

Related: horizontal LLMs like [[agi-timelines|general-purpose frontier models]] (e.g., ChatGPT) could in principle answer clinical questions competitively with verticalized models, which MS flags as a key "market value" question for the CDS space.

## AlphaWise usage data: what the numbers say

Morgan Stanley's AlphaWise Web Intelligence data through December 2025 paints a nuanced picture:

- **Web unique visitors**: Doximity steady at ~4M/month; OpenEvidence risen from near-zero (Aug 2024 launch) to 1.3M; UpToDate down ~55% to 2.4M.
- **Total visits converged** to ~7M across all three — OpenEvidence has the highest re-visit intensity.
- **Avg visit duration**: OpenEvidence 7.5 min, ~2× Doximity (5 min) and UpToDate (5 min).
- **App MAUs**: OpenEvidence 1.1M (Dec 2025), ~3× Doximity's 430K; UpToDate ~400K and declining.
- **App downloads**: OpenEvidence peaked at ~87K/month in July 2025, ~52K in December. Cumulatively still just 52K (vs. Doximity's ~2M and UpToDate's ~2.3M cumulative since 2012).
- **Sessions/day**: OE 3.4, Doximity 3.2, UpToDate 2.1.

The key reading: **Doximity is not losing share** — its web and app metrics are stable. **UpToDate is the one bleeding usage intensity.** OpenEvidence appears to be expanding the pie (for now) rather than displacing Doximity's engaged prescriber base.

## Monetization reality check — pharma buyer perspective

MS spoke with execs at two top-10 pharma companies and multiple ad agencies. Their framing:

**On Doximity:** default performance channel. 10-15% script-lift on new prescriptions. Reported 3:1 to 5:1 ROI. Sampled quotes: *"Doximity is a key player"*, *"Seeing attractive 3:1 to 5:1 ROI...very differentiated"*, *"Pathway Medical gives AI efforts more teeth."* The budget rebalancing story is "from in-person reps and Medscape → digital, and Doximity takes the lion's share."

**On OpenEvidence:** experimental phase, smaller budgets. *"Best version of AI in healthcare"*, *"We are in a nascent, exploratory phase"*, *"View it as complementary to Doximity"*, *"Narrow use cases"*, *"Data set is lacking"*, *"If you can't provide data (tracking and measurement)...will be at a disadvantage."* OE has been on an "aggressive push to hire sales people in the past 6 months."

The bottleneck: OpenEvidence's measurement suite is weaker than incumbent ad platforms. Pharma buyers want replicable, scalable ROI proof points comparable to Doximity's closed-loop attribution. And any pharma-sponsored content must clear **Medical Legal Review (MLR)** — an internal compliance gate ensuring promotional materials are accurate, balanced, and legally compliant. OpenEvidence must keep sponsored placements (pre-approved modular content) clearly delineated from factual clinical answers, or risk regulatory exposure and loss of trust with clinicians.

## Fundraising and investors

Roughly $545M raised by October 2025. Most recent round: Series C on 20-Oct-2025, $200M at a $5.8B pre-money ($6B post), led by GV with participation from Coatue, Blackstone, BOND Capital, Thrive, Sequoia, Kleiner Perkins, and Craft Ventures. A $210M Series B in July 2025 closed at a $3.55B post — **valuation ~70% in three months**. Earlier backers include Sequoia, Greycroft, Conviction, Xfund, Ziff Davis, Jim Breyer, Brian Sheth, and Ken Moelis. Board investors: Mamoon Hamid (Kleiner Perkins), Patrick Grady (Sequoia), Sangeen Zeb (GV).

## Legal: OpenEvidence vs. Doximity and Pathway

In 2025, OpenEvidence sued both Doximity and Pathway Medical under the Defend Trade Secrets Act and Lanham Act, alleging impersonation of physicians to access the platform and steal system-prompt code. Doximity then **acquired Pathway for $63M in August 2025**, folding its structured evidence dataset and full-text journal access into DoxGPT — the single most important upgrade to Doximity's AI capabilities. OpenEvidence dropped the Pathway case in October 2025 (Doximity case status as of MS publication: ongoing; Doximity hired a new general counsel in mid-August 2025).

## MS's four key open questions

1. **Will AI-CDS competition intensify?** Yes — OE's early growth occurred in a near-vacuum. UpToDate Expert AI only launched Oct 2025; DoxGPT got its Pathway-powered upgrade in Q3 2025. The uncontested period is over.
2. **Is there a durable moat around AI-synthesis in CDS?** Three sub-questions: (a) curated corpora (UpToDate's approach) vs. broad-scrape AI synthesis — which wins on answer quality? (b) will AI synthesis "stick" in CDS or will accuracy issues drive a rollback? (c) can horizontal LLMs compete with verticalized ones?
3. **Will OE need to formalize institutional routes to market?** Today OE bypasses healthcare institutions — clinicians self-onboard via NPI verification. Ambient scribe ambitions may force contractual relationships with hospitals, where Doximity has a structural head start. International expansion tightens this further.
4. **Will monetization change?** Viral free-for-use has great unit economics (no sales/marketing spend). But if OE has to build institutional workflows and formal contracts, operating margin compresses and subscription/enterprise models may enter the mix.

## The knowledge-half-life argument

OpenEvidence's internal framing: medical-knowledge doubling time has collapsed from ~50 years (1950) to ~5 years today, making up-to-date evidence at the point of care structurally more valuable — and making static, periodically-updated tools like traditional UpToDate look obsolescent. This is the strategic narrative behind the company's "free for every U.S. doctor" distribution bet.

## Publisher–platform content deal precedents

MS surveys content-licensing precedents to frame how OE's journal partnerships might evolve. The structures are highly heterogeneous — training rights vs. display rights, fixed minimums vs. variable upside tied to how often content surfaces:

- Google → Reddit: ~$60M/yr (training)
- OpenAI → Reddit: ~$70M/yr (training + display)
- OpenAI → News Corp: $250M over 5 years (cash + OpenAI credits)
- OpenAI → Dotdash Meredith: $16M/yr fixed + variable upside
- OpenAI → Axel Springer: "tens of millions" of euros, 3-year fixed + variable
- Microsoft et al → Informa (Taylor & Francis): >$75M+ non-recurring in 2024
- Unnamed tech firms → Wiley: $44M, no opt-outs
- Apple News → TIME: seven figures/yr (distribution)
- Meta → WSJ/NYT/CNN: $10M / $20M / $3M (news tab, terminated 2024)

The implication for OE: medical-journal deals will likely blend training-data rights with product-feature rights (branded evidence summaries, prominent citations), and economics will flex between fixed minimums and KPI-linked upside. The analogous model is OE directing verified reader traffic to journals while preserving publisher brand credibility.

## Implications for incumbents

**Doximity (DOCS.N)** — MS values at 26x EV/EBITDA on CY27 $445M adj. EBITDA. Downside risks explicitly include "rising competition from companies like OpenEvidence." The Pathway acquisition is defensive.

**Wolters Kluwer (WLSNc.AS)** — UpToDate is ~10% of group revenues. MS values WKL via 10-year DCF, ~9% WACC, ~3% terminal growth. Downside risks explicitly cite "Competition debates (e.g. OpenEvidence)." UpToDate is the most exposed of the three — it's the only product already losing measurable usage intensity, and its subscription model is the one most vulnerable to being undercut by a free, AI-native alternative.

## Sources

- Morgan Stanley Research (2026-01-12). "Private Company Research Series: A Deeper Dive into OpenEvidence." Transforming Healthcare | North America. — [[2026-04-10-openevidence-morgan-stanley-deep-dive|local copy]]
