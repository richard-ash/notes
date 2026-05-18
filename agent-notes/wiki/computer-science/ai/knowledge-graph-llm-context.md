---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-04-20-ortolf-clinical-knowledge-graph-original.md
  - agent-notes/raw/computer-science/ai/2026-04-20-ortolf-clinical-knowledge-graph-iteration.md
compiled_at: 2026-05-18
model: claude-opus-4-7
confidence: medium
---

# Knowledge Graphs as LLM Context

Colton Ortolf's two-post experiment on using a structured knowledge graph as LLM context for clinical recommendations. The durable contribution is twofold: (1) for multi-source reasoning, graph-derived context beats flat [[llm-knowledge-bases|RAG]] beats vanilla LLM; (2) more importantly, **how** the graph is serialized for the LLM matters at least as much as **what** the graph contains — five iterations of prompt engineering on the graph→LLM interface moved the needle more than adding new graph edges did.

## The setup

Ortolf encoded three cardiometabolic clinical guidelines — USPSTF, ACC/AHA, KDIGO — into a Neo4j graph where medications, conditions, and recommendations are structured nodes. Each recommendation carries structured eligibility criteria derived from the guideline text; the graph has a method to evaluate which recommendations fire given a structured patient record. Recommendations decompose into strategies and actions, with edges representing the relationships. Built in three days with Claude Code.

Three arms compared on hand-authored synthetic patient cases designed to test intersections where the arms should diverge:

1. **Vanilla LLM** — patient data only, no guidelines.
2. **Flat RAG** — patient data plus retrieved guideline text chunks.
3. **Graph context** — patient data plus graph-derived context: which guidelines apply, what they recommend, where they agree.

Orchestration is Sonnet running the task; Opus evaluating.

## First-round results (16 patients)

| Arm | Composite |
| --- | --- |
| Graph context | 4.14 |
| Flat RAG | 3.38 |
| Vanilla LLM | 2.98 |

Headline reading: structure beats retrieval. But when Ortolf isolated the hard cases — patients matching multiple guidelines — the graph-vs-RAG margin shrank to only +0.175. Not convincing. RAG can retrieve the right chunks but hopes the model connects the dots across guidelines; the graph's *structural* advantage of knowing three guidelines converge on the same statin recommendation isn't doing much work if the model still has to discover the convergence from the serialized output.

## The serialization iteration

Ortolf left the graph unchanged and rewrote the graph→LLM interface in three specific ways:

1. **Explicit cross-source convergence.** Instead of dumping graph data, the context now includes a structured table: "these 3 guidelines converge on statins for this patient, here's why." The convergence is pre-computed and surfaced as a first-class object in the prompt, not something the LLM has to assemble.
2. **Negative evidence.** The context now tells the LLM what guidelines were *evaluated but did not fire* and why: "KDIGO CKD guidelines evaluated but not applicable — no kidney disease markers present." Most systems optimize for recall (more context); negative evidence improves precision by constraining the reasoning space — the LLM no longer has to ask "did the system consider X?" because the absence is explicit.
3. **Completeness license.** Explicitly tell the LLM it can recommend lifestyle interventions beyond what the graph encodes. The graph is a floor on what's clinically appropriate, not a ceiling on what the LLM is allowed to say.

## Second-round results (22 patients)

| Arm | Composite (multi-guideline) |
| --- | --- |
| Graph context | 4.28 |
| Flat RAG | 3.50 |
| Vanilla LLM | 2.63 |

The graph-vs-RAG margin on the hardest cases jumped from +0.175 to +0.775. The biggest sub-score gains were on *integration* — when you force the LLM to reason about cross-guideline agreement explicitly, it stops dropping interactions.

## The durable insight

> It's not enough to have structured knowledge. How you serialize it for the LLM matters as much as the structure itself.

The five-iterations-on-the-interface-beat-new-edges finding is the load-bearing claim. It generalizes the same pattern that shows up across [[agentic-engineering-architecture|fat-skills agent architecture]] (markdown is the right substrate because the LLM reads markdown well) and the [[agent-harness|agent-harness thesis]] (the harness format, not the underlying capability, is what produces usable agent behavior): the LLM is not consuming raw structure, it is consuming **a textual rendering of structure**, and the choice of rendering is a load-bearing design decision.

The three specific improvements decompose into a checklist that probably generalizes to any structured-context system, clinical or not:

- **Pre-compute the cross-source claims you want the LLM to make.** Don't ask it to discover convergence; surface convergence as a first-class object.
- **Surface what you considered and rejected.** Negative evidence constrains the search space and lets the LLM trust the system's coverage.
- **License completeness outside the structure.** Tell the LLM where the structure ends so it can fill in the parts the structure doesn't cover.

## Caveats

The experiment is exploratory and small-N. 22 synthetic patients, hand-authored by Ortolf specifically to test intersections where he expected the arms to diverge — so the absolute scores are not generalizable, but the *relative* movement of the graph-vs-RAG margin across the serialization iteration is the more credible signal. Opus as judge of Sonnet's output introduces shared-family bias; an independent rubric or human clinician adjudication would tighten the result.

Ortolf also notes (in reply to Shrestha) that he focused on improving the RAG arm of the eval too — flat RAG is good on single-guideline fixtures and only breaks down on multi-guideline cases with conflicting recommendations. So this is not a strawman-RAG comparison; the graph's advantage is specifically in the multi-source-conflict regime.

Babashin's reply flags the practical gap: the "here's why" table unlocks clinician trust *only if* each row links back to the specific guideline section or PubMed paper behind the convergence. The current implementation reportedly does not yet do this, which is a separate axis from the structure-vs-serialization question Ortolf is studying.

## Sources

- Ortolf, C. (2026-04-20). "Can a knowledge graph make an LLM a better doctor?" <https://x.com/ColtonOrtolf/status/2046419930526973963> — [[2026-04-20-ortolf-clinical-knowledge-graph-original|local copy]]
- Ortolf, C. (2026-04-20). "Update on the clinical knowledge graph experiment." <https://x.com/ColtonOrtolf/status/2046971434920996988> — [[2026-04-20-ortolf-clinical-knowledge-graph-iteration|local copy]]
