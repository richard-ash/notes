---
source: agent
compiled_from:
  - agent-notes/raw/health/2026-10-23-general-purpose-llms-outperform-clinical-ai-tools.md
compiled_at: 2026-10-23
model: claude-fable-5-1
confidence: high
---

# Clinical AI tools vs. frontier LLMs

Do specialized clinical AI products — proprietary tools built on LLMs with curated medical corpora and retrieval — answer clinicians' questions better than the general-purpose frontier models they are built on? The first independent, blinded, head-to-head test says no. Vishwanath, Oermann and colleagues at NYU Langone (*Nature Medicine*, 2026) ran [[openevidence|OpenEvidence]] and Wolters Kluwer's UpToDate Expert AI against GPT-5.2, Gemini 3.1 Pro and Claude Opus 4.6 across three stages and found the frontier models ahead on every one. On real physician queries, the clinical tools were statistically indistinguishable from Google Search's auto-enabled AI Overview.

## The three-stage design

| Stage | Items | What it measures | Scoring |
|---|---|---|---|
| MedQA | 500 USMLE-style multiple-choice questions (random seed 62) | Medical knowledge | GPT-4.1 extracts the chosen answer, regex cross-check, manual resolution of disagreements |
| HealthBench | 500 single-turn free-response prompts from OpenAI's benchmark | Alignment with clinician-written rubrics | Three-judge LLM panel (Claude Opus 4.6, Gemini 3.1 Pro, GPT-5.2), majority vote per rubric point, scaled 0–100 |
| Real clinical queries (RCQ) | 100 de-identified questions physicians asked NYU Langone's HIPAA-compliant GPT instance during routine care | Real-world usefulness | 12 blinded US clinicians, 3 raters per model–question pair, four dimensions on a 1–4 scale plus binary harm and hallucination flags; 1,800 annotations |

The RCQ benchmark is the paper's centerpiece and the authors' stated primary evidence: it is free of training-set contamination, judged by humans rather than models, and drawn from what clinicians actually ask. Google AI Overview was added at this stage as a "real-world control" because physicians encounter it whether they mean to or not. The RCQ dataset is not public (institutional data-use agreement); the MedQA and HealthBench subsets are reproducible from the seed.

Frontier models were called via API in February 2026 at temperature 0 with search tools enabled. The clinical tools have no public API, so they were queried by hand through their browser interfaces (OpenEvidence in September 2025 and February 2026; UpToDate Expert AI in November 2025 and February 2026). Response length and formatting were deliberately *not* normalized, on the argument that verbosity and structure are part of the clinical interface and clinicians experience them as such.

## Results

**MedQA (knowledge).** Gemini 97.4%, GPT 94.2%, Claude 90.2%, OpenEvidence 89.6%, UpToDate 88.4%. Gemini beat everything; GPT beat everything but Gemini. Claude Opus 4.6 was not statistically separable from the two clinical tools on this stage — the one place the "frontier beats clinical" headline needs a footnote.

**HealthBench (rubric alignment).** GPT 88.0, Gemini 79.3, Claude 77.0, OpenEvidence 62.6, UpToDate 61.3. GPT led in all seven themes; the clinical tools were last or tied for last in all seven, significantly so in six (the exception was "responding under uncertainty"). The authors downgrade this stage to supplementary because OpenAI built the benchmark and OpenAI's model won it.

**RCQ (blinded clinicians).** Two clean tiers:

| Tier | Model | Mean aggregate (1–4) | 95% CI |
|---|---|---|---|
| Frontier | Gemini 3.1 Pro | 3.62 | 3.56–3.68 |
| Frontier | GPT-5.2 | 3.54 | 3.47–3.61 |
| Frontier | Claude Opus 4.6 | 3.52 | 3.44–3.59 |
| Clinical / search | Google AI Overview | 3.27 | 3.18–3.35 |
| Clinical / search | OpenEvidence | 3.24 | 3.17–3.32 |
| Clinical / search | UpToDate Expert AI | 3.17 | 3.09–3.25 |

No significant differences within either tier; all nine significant pairwise differences were between tiers, with rank-biserial effect sizes of 0.5–0.9, meaning the frontier models won on most individual questions rather than merely on average. After adjusting for rater leniency with a cumulative link model, the clinical tools and Google AI had 49–87% lower odds of a higher rating than Gemini (odds ratios 0.13–0.51), or 0.36–0.44 points on the four-point scale in a linear mixed model. All 12 clinicians ranked the models the same way (Kendall's W = 0.65).

The tiers held on each of the four dimensions. Models diverged most on *clarity for clinicians* (W = 0.29) and least on *clinical correctness* (W = 0.14). OpenEvidence had the lowest clarity score of any system (2.84), which the authors read as a communication failure rather than a knowledge failure. Raters' optional free-text notes on low-scoring answers point the same way: OpenEvidence accumulated 52 flagged problems, dominated by incomplete content (15), safety-critical omissions (12) and disorganized responses (13); Google AI Overview 33, heavy on factual errors and incompleteness; GPT 21; UpToDate 20; Claude 19; Gemini 8.

**Refusals and safety.** UpToDate Expert AI refused 19% of real queries, against 1–3% for every other system except Google (6%). Harm and hallucination rates did not differ across models: zero to 3% of responses flagged harmful (Claude Opus 4.6 numerically highest at 3%, not significant), zero to 1.1% flagged as hallucinated, with clinicians agreeing closely on those flags (prevalence-adjusted kappa 0.86 and 0.95).

**Cost (April 2026).** GPT-5.2 at $1.75/$14 per million input/output tokens, Gemini 3.1 Pro at $2/$12, Claude Opus 4.6 at $5/$25; OpenEvidence free to verified US clinicians (ad-supported); UpToDate Expert AI about $699/year for an individual Pro Plus subscription; Google AI Overview free.

## Why the specialized tools lose — the authors' reading

The clinical tools are black boxes, so the paper offers mechanisms rather than proof:

- **Retrieval can hurt.** Both tools almost certainly use RAG over curated corpora. The group's own earlier work ("Medical large language models are easily distracted") and ClashEval show that irrelevant or poorly integrated retrieved material degrades answers. The clarity-not-correctness failure pattern is consistent with stitched-together retrieval. This matches the finding in [[knowledge-graph-llm-context]] that *how* retrieved context is serialized for the model matters more than how much is retrieved, and the production lesson in [[enterprise-rag-architecture]] that naive vector RAG fails at scale.
- **Scale, alignment and iteration speed.** Frontier labs ship faster, train on more, and align harder than any specialist vendor can. The authors frame most medical questions as "knowledge retrieval and reasoning," which is what general models are optimized for — a clinical-domain instance of [[the-bitter-lesson]].
- **A snapshot, not a verdict.** They explicitly hedge: if scaling returns diminish, domain tuning, curated retrieval and clinician-in-the-loop optimization may regain value, and deeply subspecialized tasks (their own CNS-Obsidian neurosurgery model, a cardiology LLM) may already favor adaptation. This is the maturity-curve argument from [[open-source-in-the-enterprise]] applied to medicine: new use cases buy frontier intelligence; mature, narrow ones eventually specialize.

Their policy conclusion is that clinical AI tools "may carry institutional legitimacy and are likely safe for routine use, but ... are not superior to frontier models," with consequences for procurement, reimbursement and regulatory oversight. The path they favor is hospital-specific models trained on institutional data for sensitive tasks, plus frontier models for everything less sensitive — and, above all, independent real-world evaluation before tools reach the bedside, since industry-built benchmarks tend to favor their builders.

## Limitations the paper names

- Browser-only access to the clinical tools: hidden prompts, retrieval behaviour and formatting could not be controlled, and sample size was capped by manual querying.
- MedQA and HealthBench may be in the training data of any of the systems; RCQ is not.
- HealthBench is OpenAI-authored and thinly documented; GPT-5.2's win there is confounded by possible overlap in training data, objectives or rubric design.
- Frontier models were both contestants and HealthBench judges, mitigated by the three-family panel (the same independence logic as the multi-model ensemble in [[ai-code-review]]).
- Latency and citation quality — arguably the clinical tools' selling points — were not measured.
- Item-level inter-rater reliability was only fair (Krippendorff's α 0.10–0.20), though 89–95% of disagreements were adjacent scores and agreement on acceptable-vs-unacceptable was moderate to strong (kappa 0.55–0.83).

## Caveats the paper does not dwell on

- **Search was on.** The frontier models ran with web search tools enabled, so this is not parametric knowledge versus retrieval. It is frontier-model-plus-web-search versus product-RAG-over-licensed-journals. The clinical tools' distinctive asset — NEJM, JAMA, UpToDate's expert-written topics — did not translate into a measurable edge over open-web retrieval.
- **Query provenance.** The 100 RCQ questions are what clinicians chose to ask a general chatbot inside the hospital's GPT deployment. Questions clinicians route to UpToDate (drug dosing, guideline lookups) may have a different shape, and the sample is one institution, 100 items, 12 raters.
- **UpToDate's refusals.** Excluding its 19 refused items means its score reflects only the questions it chose to answer, which could flatter or penalize it.
- **Declared interests.** The senior author consults for Google and holds equity in two health-AI companies; Gemini won two of three stages. The authors disclose this; it does not undermine a blinded design, but it belongs in the record.
- **Model vintage.** All systems are February 2026 snapshots, and the paper itself says the ordering is a snapshot of a rapidly moving landscape. Newer frontier generations (the Claude 5 family among them) postdate the study.

## What it means for the clinical decision support market

This answers, for now, the question Morgan Stanley left open in its [[openevidence|OpenEvidence]] analysis — "can horizontal LLMs compete with verticalized ones?" — and the answer runs against the vertical tools. But it also sharpens *where* OpenEvidence's value sits. Its moat was never a blinded answer-quality test; it is free NPI-gated distribution, inline citations clinicians can check, pharma-ad monetization and an expanding workflow footprint (ambient scribe, dialer). The paper leaves those untouched while removing the "superior clinical performance" plank from the pitch. That is the commodity-models, distribution-is-the-moat thesis from [[ai-eats-the-world]] playing out in healthcare.

The sharper commercial fact is that a free, auto-enabled search feature tied both a product last valued at ~$6B and a $699/year subscription on blinded clinician ratings. For UpToDate, already the incumbent most exposed to usage decline, an AI product that refuses a fifth of real questions and ties Google on the rest is a weak answer to the threat.

For buyers, the operational takeaway is the authors' own: demand independent evaluation on your clinicians' real queries, not vendor benchmarks, before procurement.

## Sources

- Vishwanath, K., Alyakin, A., Ghosh, M., … Oermann, E. K. (2026). "General-purpose large language models outperform specialized clinical AI tools on medical benchmarks." *Nature Medicine*. <https://doi.org/10.1038/s41591-026-04431-5> — [[2026-10-23-general-purpose-llms-outperform-clinical-ai-tools|local copy]]
