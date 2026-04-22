---
source: agent
compiled_from:
  - agent-notes/raw/biology/2026-03-25-lactate-misunderstood-molecule.md
compiled_at: 2026-04-22
model: claude-opus-4-6
confidence: high
---

# Lactate

Lactate is the obligatory end product of glycolysis, a universal metabolic fuel, a hormone-like signaling molecule, and — in cancer — a driver of carcinogenesis. For over two centuries it was mischaracterized as a toxic waste product of anaerobic metabolism. The modern understanding, built primarily on the work of George A. Brooks at UC Berkeley from the 1970s onward, reveals lactate as one of the most important molecules in human physiology.

## The historical misunderstanding

Lactate's reputation as metabolic waste traces to three accidents of history:

1. **Discovery in sour milk (1780).** Carl Wilhelm Scheele isolated "lactic acid" from curdled milk — the name stuck, associating the molecule with spoilage.
2. **First detection in human blood under pathological conditions (1843).** Johann Joseph Scherer found it during autopsy in cases of septic and hemorrhagic shock. Its presence was immediately associated with dying.
3. **The Meyerhof model (1922 Nobel Prize).** Otto Meyerhof showed glycogen-lactate coupling in electrically stimulated, oxygen-deprived frog muscle preparations. This cemented the paradigm that lactate = oxygen lack = failure. The problem: the model was built on dead tissue in a dish, not living organisms.

This three-Nobel-Prize intellectual lineage (Warburg → Meyerhof → Krebs, all connected through the Kaiser Wilhelm Institute in Berlin) mapped the machinery of cellular energy production with precision, but left lactate mischaracterized as a dead-end metabolite.

## Terminology: lactate, not lactic acid

At physiological pH (~7.4), the molecule exists almost entirely in its dissociated ionic form: **lactate** (the conjugate base), not lactic acid. This is chemically meaningful — lactic acid essentially does not exist in the body under normal conditions.

## The biochemistry

Glycolysis converts glucose to pyruvate in ten cytosolic steps. At step six, NAD⁺ is reduced to NADH. For glycolysis to continue, NADH must be reoxidized. Lactate dehydrogenase (LDH) performs this essential function:

> pyruvate + NADH + H⁺ → lactate + NAD⁺

This reaction simultaneously:
- **Regenerates NAD⁺** — maintaining the redox ratio essential for continued glycolysis
- **Consumes a proton** — providing a mild buffering effect against cytosolic acidosis

The "burn" athletes feel during intense exercise is not caused by lactate. It results from protons released during ATP hydrolysis (ATP → ADP + Pi + H⁺). Lactate appears alongside acidosis because both increase with exercise intensity, but lactate is "at the scene of the crime, not the criminal" — it is actually helping by consuming protons.

## The Lactate Shuttle

Brooks formalized the **Lactate Shuttle Hypothesis** in 1985, now proven and considered one of the most important frameworks in metabolic physiology. The core finding: lactate is produced continuously under fully aerobic conditions (not just during oxygen deprivation) and circulates as a primary fuel.

### Intracellular shuttle

Through MCT1 (monocarboxylate transporter 1), lactate enters mitochondria, where mitochondrial LDH converts it back to pyruvate. Pyruvate enters the Krebs cycle via acetyl-CoA, feeding the electron transport chain for ATP production. Brooks' lab characterized the **mitochondrial lactate oxidation complex (mLOC)** — MCT1, mitochondrial LDH, and cytochrome oxidase organized as a dedicated molecular machine on the inner mitochondrial membrane. The cell built specific infrastructure to oxidize lactate — not what you do for waste.

### Cell-to-cell shuttle

Fast-twitch (type II) muscle fibers produce lactate rapidly and export it via MCT4. Slow-twitch (type I) fibers, rich in mitochondria, take it up via MCT1 and oxidize it as fuel. The same exchange occurs between working muscle and the heart, brain, kidneys, and other organs. When lactate enters mitochondria via MCT1 (an H⁺/lactate symporter), it co-transports a proton — actively removing the acidifying protons from the cytosol.

### Clinical and athletic implication

Blood lactate at a standardized workload is a direct readout of mitochondrial function. Two cyclists at 300 watts: one at 1.5–2 mmol/L (mitochondria clearing lactate as fast as it's produced — zone 2 equilibrium) versus one at 7 mmol/L (shuttles overwhelmed, lactate escaping to blood, protons accumulating). The difference is not effort — it is mitochondrial capacity. This single measurement can index fitness, predict competitive performance, and guide training.

## Lactate as a lactormone and exerkine

Brooks coined the term **lactormone** to describe lactate's hormone-like properties. It functions as an endocrine, paracrine, and autocrine signaling molecule across multiple organ systems.

### Fuel partitioning

Lactate orchestrates the shift from fat to carbohydrate oxidation during high-intensity exercise through two mechanisms:
- **GPR81 (HCAR1) binding** in adipose tissue — suppresses lipolysis (fat breakdown)
- **CPT1/CPT2 inhibition** — reduces fatty acid import into mitochondria for oxidation (demonstrated by San-Millán and Brooks in neonatal rat cardiomyocytes)

### Brain effects

Lactate crosses into the brain, serving as both fuel and signaling molecule in astrocytes and neurons:
- Stimulates **BDNF** (brain-derived neurotrophic factor) production — supporting synaptic plasticity and neuroprotection
- Promotes **hippocampal neurogenesis**
- Acutely improves **executive function**

This may be one of the most important molecular explanations for the cognitive and mood-enhancing effects of aerobic exercise.

### Epigenetic regulation

Zhang et al. (2019) discovered **histone lactylation** — lactate directly modifies histone lysine residues, altering gene expression programs. Lactate reaches inside the nucleus and changes which genes are transcribed, with implications in both normal physiology and disease.

## Lactate in cancer

See [[warburg-effect]] for detailed coverage of the lactagenesis hypothesis. Key developments from San-Millán's ongoing research program:

- **Oncometabolite status confirmed.** In MCF7 breast cancer cells, lactate upregulates oncogenes and transcription factors while suppressing tumor suppressors. It is not merely present — it regulates the genetic machinery of carcinogenesis.
- **EMT regulation.** Lactate controls expression of genes driving epithelial-to-mesenchymal transition (invasion and metastasis). Silencing LDHA suppresses EGFR and HIF-1α within 48–72 hours.
- **Histone lactylation in tumors.** The same epigenetic mechanism discovered in normal physiology drives pro-survival and immune-evasion gene programs in cancer cells.
- **Multi-checkpoint immune escape (2026).** San-Millán et al. show lactate regulates expression of *multiple* immune checkpoints simultaneously — not just PD-L1 but CD80, CD73, LGALS9, CD47, VISTA, and others. Different cancer lines show heterogeneous checkpoint patterns, all driven by a shared upstream metabolic state: chronic lactate accumulation. This may explain why single-checkpoint immunotherapy (pembrolizumab) has limited efficacy in many solid tumors — blocking one road while the tumor has many.

### Exercise lactate vs. cancer lactate

The critical distinction: **transience vs. chronicity**.

| Feature | Exercise lactate | Cancer lactate |
|---------|-----------------|----------------|
| Duration | Transient (minutes) | Chronic (24/7) |
| Purpose | Fuel distribution, signaling | Carcinogenic program |
| Clearance | Rapid via mitochondrial oxidation | Trapped in tumor microenvironment |
| pH effect | Buffered, returns to baseline | Sustained microenvironment acidosis |
| Downstream | Adaptation, neuroprotection | Immune escape, metastasis, angiogenesis |

Exercise-induced mitochondrial adaptations (greater oxidative capacity, enhanced lactate clearance, upregulated MCT1) may represent a biological defense against the pathological lactate accumulation that characterizes cancer.

## The intellectual lineage

The article traces the Kaiser Wilhelm Institute connection: Warburg (1931 Nobel, cellular respiration) → Meyerhof (1922 Nobel, glycolysis-lactate coupling) → Krebs (1953 Nobel, TCA cycle). Three Nobel Prizes, one institutional address, all touching the pathway lactate sits at the center of — yet none fully resolving lactate's role. Brooks, working from Berkeley since 1971, completed the picture.

San-Millán describes meeting Brooks at a California bike race after years studying his papers. Their subsequent 15-year collaboration produced the lactagenesis hypothesis (rejected 8 times before publication) and the ongoing cancer metabolism research program.

## Sources

- San-Millán, I. (2026). "Lactate: The Most Misunderstood Molecule in Biology." *Substack*. <https://substack.com/home/post/p-192080657> — [[2026-03-25-lactate-misunderstood-molecule|local copy]]
