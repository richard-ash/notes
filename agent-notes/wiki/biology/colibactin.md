---
source: agent
compiled_from:
  - agent-notes/raw/biology/2026-03-23-early-onset-colorectal-cancer-rates.md
compiled_at: 2026-04-20
model: claude-opus-4-6
confidence: high
---

# Colibactin

Colibactin is a genotoxin produced by *pks+* strains of *E. coli* that causes interstrand DNA crosslinks — permanent covalent bonds between complementary DNA strands that block both transcription and replication. It is now understood to be a major molecular driver of early-onset colorectal cancer (diagnosed before age 50), a category that has doubled in incidence over the past 30 years and risen ~400% in pediatric cases (though the absolute number in children remains small, ~100 US cases/year).

## Mechanism of action

Colibactin's structure has two key features:

1. **Cyclopropane warheads** at each end — strained three-membered rings geometrically similar to nucleotides but chemically unstable.
2. **A flexible aromatic linker** in the middle that slots into the minor groove of the DNA double helix.

Once seated in the minor groove, the strained cyclopropane bonds snap and react irreversibly with nearby DNA atoms. The result is an interstrand crosslink: two complementary strands superglued together. This is categorically different from the single-strand breaks or base modifications that cellular repair machinery routinely handles. The cell's best option is homologous recombination repair — copying the correct sequence from the other chromosome — which carries a high probability of introducing mutations.

The damage leaves a distinctive mutational signature, **SBS88**, that serves as a molecular fingerprint. SBS88 is highly enriched in colorectal cancers from young patients (Diaz-Gay et al. 2025), providing the epidemiological link between *pks+* E. coli colonization and early-onset disease.

## Why the microbiome matters

The gut microbiome is a competitive ecosystem of hundreds of bacterial species. Factors like diet, obesity, and microplastic exposure can shift its composition toward more aggressive, pro-inflammatory microbes — including *pks+* E. coli. These bacteria dominate by producing toxins that kill competing bacteria and evade immune cells. Paradoxically, immune responses can worsen the problem: *E. coli* thrive in the oxygen-rich environments that activated immune cells create.

The epidemiological rise in early-onset colorectal cancer tracks changes in diet and environmental exposures over the past three decades, though direct comparison is limited because deep microbiome profiling from the 1990s does not exist.

## Therapeutic strategies

### 1. Microbiome modulation

Reducing *pks+* E. coli populations directly. Antibiotics are too blunt — they can paradoxically increase pathogenic bacteria. Probiotics show promise (commensal bacteria competitively exclude *pks+* strains), though early animal studies have stumbled: one probiotic trial inadvertently introduced another colibactin producer. Putrescine supplementation has shown the most targeted results, selectively inhibiting *pks+* E. coli growth. Clinical trials are underway (NCT05816577).

### 2. Colibactin detoxification

*pks+* E. coli protect themselves from their own toxin via an enzyme that cleaves the cyclopropane warhead. Several approaches exploit this biology:

- **Anti-adhesion therapy** (Jans et al. 2024): blocking bacterial adherence to gut epithelial cells dramatically reduces DNA damage, since colibactin requires direct contact to cause harm.
- **Substrate mimicry** (Nature Chemical Biology, 2022): a boron-containing small molecule mimics a biosynthetic precursor, suppressing colibactin production.
- **Engineered scavenger bacteria** (Nature Microbiology, 2025): the *pks+* E. coli detoxifying enzyme is fused to the cell surface of a commensal strain, creating a living "colibactin vacuum cleaner" that degrades extracellular toxin. This points toward a broader synthetic biology paradigm — engineered gut microbes as programmable detoxifiers.

### 3. Direct DNA protection

Colibactin is chemically related to mitomycin C, a crosslinking chemotherapy agent. Amifostine, a cytoprotective drug, has been shown to reduce mitomycin C-induced DNA damage to baseline levels (Camelo et al. 2008). This was originally studied in the context of Fanconi anemia (where crosslink repair genes are mutated), but the principle of pharmacological DNA protection could extend to colibactin-exposed gut epithelium.

## Broader significance

Tomusiak draws a parallel to cardiovascular disease: like colorectal cancer, it is influenced by lifestyle factors (diet, exercise), but the mechanistic insight that cholesterol drives atherosclerosis led to statins — a scalable pharmaceutical intervention. Understanding colibactin's role could enable an analogous "statin moment" for colorectal cancer prevention. The field is early (most cited research dates to 2022-2025), but the proposed interventions — particularly probiotics and engineered scavenger bacteria — are not far from clinical deployment.

This connects to a broader theme in cancer biology: while the [[warburg-effect|Warburg effect]] describes how cancer cells reshape their metabolic environment *after* transformation, colibactin reveals how the microbial environment can initiate transformation in the first place. The two mechanisms can compound — microbiome-driven mutations may give rise to cells that then exploit lactagenesis for growth and immune evasion.

## Sources
- Tomusiak, Alan (2026). "Why are early-onset colorectal cancer rates spiking?" <https://www.communitymorgue.com/p/why-are-early-onset-colorectal-cancer> — [[2026-03-23-early-onset-colorectal-cancer-rates|local copy]]
