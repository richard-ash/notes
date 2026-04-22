---
source: agent
compiled_from:
  - agent-notes/raw/biology/2016-12-30-lactagenesis-warburg-effect.md
  - agent-notes/raw/biology/2026-03-25-lactate-misunderstood-molecule.md
compiled_at: 2026-04-22
model: claude-opus-4-6
confidence: high
---

# The Warburg Effect and Lactagenesis

The Warburg Effect — the observation that cancer cells preferentially ferment glucose to lactate even in the presence of oxygen — has been recognized as a hallmark of cancer since Otto Warburg first described it in 1923. For nearly a century, the *purpose* of this metabolically "inefficient" behavior remained unexplained. San-Millán and Brooks (2017) propose that the answer lies in **lactagenesis**: the highly orchestrated production of lactate is not a byproduct of cancer but its enabling mechanism.

## The paradox of metabolic inefficiency

Cancer cells produce only 2 ATP per glucose molecule (via glycolysis to lactate) instead of ~36–38 ATP via mitochondrial oxidative phosphorylation. This seems irrational for proliferating cells that need energy. But the framing is misleading:

- Cancer cells are parasitic on the host's euglycemia — glucose supply is effectively limitless.
- The metabolic "cost" is externalized: the host provides glucose and absorbs exported lactate and protons.
- The real output isn't ATP — it's **lactate as a signaling molecule and microenvironment shaper**.

This reframing draws on George Brooks' **Lactate Shuttle** hypothesis (1985–2009), which established that lactate is not a waste product but a major fuel, gluconeogenic precursor, and signaling molecule ("lactormone") in normal physiology.

## The five steps of lactagenesis

San-Millán and Brooks identify a five-step orchestrated metabolic reprogramming driven by a triad of transcription factors (HIF-1, c-Myc, p53 suppression):

1. **Increased glucose uptake** — GLUT-1 overexpression (via HIF-1, c-Myc, p53 loss)
2. **Increased glycolytic enzyme expression** — especially LDHA (via HIF-1, c-Myc)
3. **Decreased mitochondrial function** — p53 loss impairs SCO2/cytochrome c oxidase; mitochondrial structural degradation
4. **Increased lactate production, accumulation and release** — mass effect of steps 1–3
5. **Upregulation of MCT1/MCT4 transporters** — enables lactate export and cell-to-cell shuttling (HIF-1 drives MCT4; c-Myc drives MCT1; lactate itself upregulates MCT1 within 1 hour)

The key insight: oncogene and tumor suppressor mutations don't just stop at producing lactate — they also ensure its *export and signaling*, suggesting the entire program exists to generate and distribute lactate.

## Lactate's roles in carcinogenesis

Lactate may be the only single metabolite involved in *all* major hallmarks of cancer progression:

| Process | Lactate's role |
|---------|---------------|
| **Angiogenesis** | Stimulates VEGF expression, increases hyaluronan production |
| **Immune escape** | Inhibits T-cell activation (cytokine production down 95%, cytotoxicity down 50%), blocks monocyte migration, inhibits NK cells, prevents dendritic cell differentiation |
| **Cell migration & metastasis** | Induces TGF-β2 in glioma, increases cell motility concentration-dependently, highly correlated with metastasis incidence |
| **Self-sufficient metabolism** | Regenerates NAD+ for continued glycolysis; glutaminolysis provides secondary carbon source for lactagenesis |
| **Tumor microenvironment** | Creates extracellular acidosis (pH 5.5–7.0) while maintaining alkaline intracellular pH |
| **Exosome signaling** | Low pH increases exosome release/uptake, enabling transfer of oncogenes to candidate cells |
| **Transcriptional reprogramming** | 10 mM lactate upregulates ~4,131 genes in MCF7 cells; activates HIF-1 |
| **Cancer relapse** | Enhances blebbishield sphere formation (cancer stem cells) by 87% |

## The immune escape mechanism in detail

The immune suppression pathway is particularly elegant in its exploitation of the host:

- Cancer cells export lactate + H+ via MCT symporters, acidifying the microenvironment.
- T-cells, when activated for proliferation, also switch to glycolysis and need to export their own lactate via MCTs.
- But MCTs are concentration-gradient-dependent symports — if extracellular lactate/H+ is already high, T-cells cannot export, leading to intracellular acidosis, loss of function, and apoptosis.
- The tumor effectively poisons the immune cells by flooding the shared space with its own metabolic output.

## Exercise physiology parallels

The paper draws heavily on parallels between working skeletal muscle and cancer cells — both are highly glycolytic and produce abundant lactate. The critical differences:

| Feature | Exercise | Cancer |
|---------|----------|--------|
| Lactate exposure | Intermittent | Chronic, continuous |
| Feedback | Negative (self-limiting) | Positive (feed-forward) |
| Mitochondrial response | Biogenesis (doubles reticulum mass) | Degradation |
| Lactate disposal | Rapid oxidation + gluconeogenesis | Accumulation + export |
| Downstream effect | Favorable metabolic adaptation | Carcinogenesis |

This suggests that **chronicity and dysregulation** — not the metabolic pathway itself — are what distinguish cancerous from healthful lactate metabolism.

## Lactate-driven multi-checkpoint immune escape (2026)

San-Millán et al. (2026) extend the immune escape findings significantly. Their most recent work demonstrates that lactate regulates the expression of *multiple* immune checkpoints simultaneously — not just PD-L1, but CD80, CD73, LGALS9, CD47, VISTA, and others — in both breast and lung cancer cell lines. Different cancer cell lines showed strikingly different checkpoint patterns under chronic lactate-producing conditions, revealing a heterogeneous immune escape landscape driven by a shared upstream metabolic state: lactate accumulation.

This has direct implications for immunotherapy. The limited efficacy of single-checkpoint inhibitors (e.g., pembrolizumab targeting PD-1/PD-L1) in many solid tumors may reflect that the tumor has multiple immune escape roads open simultaneously. Targeting [[lactate]] production upstream — rather than individual checkpoints downstream — could potentially shut down multiple immune evasion pathways at once.

## Therapeutic implications

Targeting lactagenesis at various nodes:

- **LDHA inhibitors** (oxamate, siRNA knockdown) — block pyruvate-to-lactate conversion
- **Dichloroacetate (DCA)** — activates PDH, redirecting pyruvate to mitochondrial oxidation
- **MCT inhibitors** — AZD3965 (Phase 1/2, UK), AR-C155858, SR13800, 7-aminocarboxycoumarin (7ACC)
- **CD147 targeting** — RNAi silencing or zinc finger nuclease deletion reduces MCT surface expression
- **Aerobic exercise** — increases mitochondrial density and lactate clearance capacity; may attenuate c-Myc activity; represents an "anti-Warburg Effect"

A challenge: cancer cells develop resistance. When MCT1/2 were inhibited by AR-C155858, cells compensated by overexpressing MCT4.

## Connection to the Lactate Shuttle

See [[lactate]] for the full picture of lactate metabolism and the Lactate Shuttle framework. Brooks' Lactate Shuttle concept (proposed 1985) overturned the century-old dogma that lactate is merely anaerobic waste. Key principles that inform the cancer context:

- Lactate is the obligatory product of glycolysis (produced even at rest, aerobically)
- It serves as a major oxidative fuel (~75–80% of muscle lactate is oxidized during exercise)
- It functions as the primary gluconeogenic precursor
- It signals via GPR81 receptor and CREB/cAMP pathways
- It shuttles between cells (Cell–Cell Lactate Shuttle) and within cells (Intracellular Lactate Shuttle, including mitochondrial oxidation via the mLOC complex)

The cancer cell co-opts this normal signaling infrastructure for pathological purposes: where healthy tissue uses lactate for communication and fuel distribution, cancer uses it for immune suppression, angiogenesis, and metastatic spread.

## Implications and open questions

- If lactagenesis is truly causal (not merely correlative), combination therapies hitting multiple nodes of the five-step program simultaneously may be necessary.
- The exercise connection raises questions about whether regular aerobic training could serve as primary prevention by maintaining robust mitochondrial/oxidative capacity.
- The positive feedback nature (lactate upregulates its own transporters and activates HIF-1 which drives more glycolysis) suggests early intervention matters — once the loop is established, it self-reinforces.
- Cachexia in cancer patients may be explained by the host's desperate gluconeogenic response to feed the tumor's insatiable glucose appetite (proteolysis of skeletal muscle for gluconeogenic amino acids).

## Sources

- San-Millán, I. & Brooks, G.A. (2017). "Reexamining cancer metabolism: lactate production for carcinogenesis could be the purpose and explanation of the Warburg Effect." *Carcinogenesis*, 38(2), 119–133. <https://academic.oup.com/carcin/article/38/2/119/2709442> — [[2016-12-30-lactagenesis-warburg-effect|local copy]]
- San-Millán, I. (2026). "Lactate: The Most Misunderstood Molecule in Biology." *Substack*. <https://substack.com/home/post/p-192080657> — [[2026-03-25-lactate-misunderstood-molecule|local copy]]
