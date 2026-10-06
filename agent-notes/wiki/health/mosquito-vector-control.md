---
source: agent
compiled_from:
  - agent-notes/raw/health/2026-10-05-mosquitoes-are-a-choice.md
compiled_at: 2026-10-05
model: claude-fable-5-1
confidence: medium
---

# Mosquito Vector Control

Two technologies now exist that can collapse, or disease-proof, a local population of *Aedes aegypti* — the mosquito that carries dengue, yellow fever, Zika, and chikungunya — with minimal environmental cost: Oxitec's self-limiting lethal gene and *Wolbachia*-infected mosquitoes. Maya Rosen's September 2026 *Works in Progress* essay "Mosquitoes are a choice" argues that in the United States the binding constraint on using them is no longer biology but a regulatory system that spent most of fifteen years deciding *which agency* should review an engineered insect. Her title is the thesis: mosquito-borne disease in the US is now a policy choice.

This article is compiled from that single advocacy essay (Works in Progress is a progress-studies publication), so the regulatory framing reflects Rosen's view. The field-trial numbers are drawn from the primary literature she cites.

## Why the US problem is back

- **Dengue, 2024:** almost 4,000 US cases, a 360% increase over the prior decade's average of ~830/year. Florida, California, and Texas all saw locally acquired transmission; Puerto Rico declared a public-health emergency.
- **Malaria, 2023:** ten locally acquired cases, the first in twenty years.
- **Yellow fever:** still absent, but its vector (*Aedes aegypti*) is present.
- **Drivers:** rising temperatures and insecticide resistance.

Rosen's framing claim is that the US is wealthy enough, and its disease-carrying mosquito population small enough, to eliminate the problem entirely inside its own borders — which is what makes the regulatory delay a choice rather than a resource constraint.

## The precedent: the sterile insect technique

Mass release of sterilized insects is not new; it is a mature, public-sector tool the USDA has run since the 1950s. Males are sterilized with radiation, released, and mate with wild females that then produce no offspring, driving the population down.

- **New World screwworm** — a fly whose larvae burrow into the living flesh of livestock. Eradicated from the US in the 1960s and pushed back to the southern tip of Panama, saving American cattle farmers an estimated ~$800M/year. Containment broke in June 2026 when Texas detected the first US case in 60 years (likely via cattle smuggling from Central America, where the pest has resurged); sterile flies are being redeployed.
- **Mediterranean fruit fly** — attacks 300+ crops; sterile releases over California and Florida have kept it out. Re-establishment in California alone is estimated at >$1B/year in crop damage.

The implication Rosen draws is that the *strategy* behind Oxitec's mosquito was already fifty years old and well understood. What was novel was only the *mechanism* — an inserted gene instead of radiation — and the regulatory system treated the mechanism, not the strategy, as the thing requiring classification.

## Approach 1: Oxitec's self-limiting lethal gene

- **Origin (Oxford, 2000):** fruit flies engineered to carry a gene producing **tTAV**, a protein harmless in small amounts and lethal when it accumulates. In the lab, the rearing medium contains tetracycline, which keeps the gene switched off; in the wild there is no tetracycline, the gene switches on, and offspring die before adulthood.
- **In *Aedes aegypti*:** the lethality is tuned to kill only *female* offspring. Males survive and carry the gene for a few generations, so suppression continues for several generations without a fresh "top up" — but the system is **self-limiting**: because the females that inherit it die each generation, the gene steadily disappears from the wild population.
- **Field results:** Cayman Islands, ~80% suppression of the wild population; Juazeiro, Brazil, ~95%.
- **Commercial status:** Oxitec first sought US approval in 2010. As of the essay's writing it still has no commercial registration (see timeline below).

The self-limiting design is worth noting against the gene drives covered in the companion *Works in Progress* essay Rosen links ("The ultra-selfish gene"): a drive is built to spread and persist; Oxitec's construct is built to fade. That is a deliberate trade of persistence for containability — and, ironically, containability bought no regulatory speed. (Compare [[selection-gene-drives]], which applies the same forward-engineer-the-population logic to tumour evolution rather than wild insects.)

## Approach 2: *Wolbachia*

*Wolbachia* is a bacterium that naturally infects roughly 60% of insect species. Two properties make it useful:

1. It makes infected mosquitoes **less able to carry viruses**, including dengue.
2. It is **maternally inherited with a reproductive asymmetry**: infected females pass it on through their eggs, and infected males can only produce viable offspring with infected females. An infected male mating with an uninfected female yields eggs that do not hatch. (The standard term for this, which Rosen does not use, is cytoplasmic incompatibility.)

That asymmetry supports two different strategies:

- **Population replacement** — release infected males *and* females so *Wolbachia* spreads through the wild population until most mosquitoes carry it and are virus-resistant, with the resistance inherited by future generations.
- **Population suppression** — release *only* infected males, which then function exactly like the radiation-sterilized males of the sterile insect technique. This is the approach the US deployments use.

Milestones:

- **2009:** Australian researchers successfully introduce a *Wolbachia* strain into *Aedes aegypti* after decades of work, and confirm the male-sterilizing effect.
- **Singapore randomized trial (NEJM, 2025):** releases of *Wolbachia*-infected males cut mosquito populations by **85%** versus control areas and dengue infections by roughly **70%** — city-scale evidence.
- **April 2024:** **MosquitoMate** becomes the first company to receive full nationwide EPA commercial registration for a live mosquito biopesticide — itself after ~15 years in the system. Deployment is subject to local approval; the Florida Keys adopted it in 2025 and the San Gabriel Valley in 2026.
- **June 2026:** Google's **Debug** project requests EPA approval to release 64 million *Wolbachia* mosquitoes in California and Florida, targeting *Culex quinquefasciatus* (the West Nile virus vector). Despite the mechanism already being registered, it must restart the Experimental Use Permit process from the beginning.

Because it involves no genetic modification, *Wolbachia* fit an existing regulatory category (microbial biopesticide) and avoided Oxitec's jurisdictional limbo — though not the EPA's slow pipeline.

## Oxitec's regulatory odyssey

| When | What happened |
|---|---|
| 2010 | Oxitec applies to the **USDA**, the agency that had run mass insect releases for 60 years. |
| ~2011 | After 18 months the USDA rejects the application and redirects it to the **FDA**, which had claimed jurisdiction over GM animals as veterinary drugs ("altered genomic DNA in an animal is a drug … intended to affect the structure or function of the body of the animal"). |
| 2011–2016 | The application sits at the FDA for five years. The FDA cannot fit an engineered mosquito into new-animal-drug rules and issues guidance carving out products "intended to prevent, destroy, repel, or mitigate mosquitoes for population control purposes," sending it to the **EPA** as a pesticide. |
| 2017–2020 | EPA pesticide review (scientific assessments, field-trial requirements). |
| May 2020 | EPA grants an **Experimental Use Permit** — a decade after the first application. Testing allowed; sales not. |
| 2021 | First US field trials in the Florida Keys, where dengue had resurged and local authorities were eager. Trials confirm female offspring die before adulthood. |
| 2022 | EPA extends trials to California, clearing up to 2.4 billion engineered mosquitoes across both states; releases paused after public pushback. |
| April 2024 | Experimental Use Permit expires. Full commercial registration requires a further EPA review of the field data. |
| Nov 2025 | FIFRA Scientific Advisory Panel meeting on the registration is postponed with no new date. |
| Sept 2026 | Registration still pending, 16 years after the first application. |

Andrea Leal, executive director of the Florida Keys Mosquito Control District: "our biggest challenges have been awaiting regulatory approvals."

## Rosen's diagnosis: jurisdiction, not safety

The striking feature of the timeline is that roughly six and a half years elapsed before *any* agency began a substantive safety review. The time was spent on classification. Rosen locates the cause in the structure of US biotech regulation:

- **The 1986 Coordinated Framework** still governs. No major new biotech regulation has passed since the 1980s, and the framework assigns jurisdiction by categories (food, drug, pesticide, plant pest) designed for the previous century's products.
- **Jurisdictional ambiguity routinely costs years** before testing begins (a 2024 GAO report documents this). Cell-cultured meat hit the same FDA-vs-USDA deadlock, broken only when Congress forced a split review in 2019. In Oxitec's case, Rosen argues, a single early inter-agency meeting would have saved years.
- **Harmonization was promised and abandoned.** Biden's September 2022 executive order directed agencies to resolve such uncertainties and update implementation of the Coordinated Framework; almost nothing was delivered, and Trump rescinded the order in March 2025.
- **Capacity, not incentives, is the bottleneck.** The EPA's 2022 Vector Expedited Review Voucher rewards a successful novel-mosquito-product registrant with expedited review on its *next* application — a prize that does nothing about the backlog the first application sits in. The reviewing unit (within the Office of Pesticide Programs' biopesticides division) is a small office that handles everything from biochemical compounds to engineered insects, and reviews live mosquitoes under conventional-pesticide protocols even though they raise different questions (dispersal, inheritance, population effects).

### The proposed fix: fee-funded review capacity

Rosen's model is the FDA's **Prescription Drug User Fee Act (1992)**:

| | FDA human-drug review | EPA pesticide review |
|---|---|---|
| Share of budget from industry fees | ~2/3 | ~1/3 |
| Share from appropriations | ~1/3 | ~2/3 |
| Review time | Median 29 months (late 1980s) → targets of 10 months standard / 6 months priority, met in the large majority of cases | Multi-year, no comparable targets for novel vector products |

Staffing drove the speed-up: review times fell by roughly 3.3 months for every 100 reviewers the FDA added. Rosen's prescription is to grow agency review capacity on the same model rather than add more incentive programs.

## Implications and connections

- **Regulatory category fit, not risk, determined speed.** *Wolbachia* got through faster not because anyone judged it safer, but because it slotted into an existing box. That creates an incentive for firms to choose technologies by regulatory legibility rather than efficacy — the opposite of what a risk-based system should do.
- **The system does not learn.** Google Debug restarting the Experimental Use Permit process for an already-registered mechanism shows there is no platform-level approval: each applicant re-litigates the same questions.
- **Reform vehicle matters.** [[political-economy-of-reform]] finds that technological and administrative reforms (which need only the implementing agency) succeed far more often than legal reforms (which face legislative veto points). Rosen's two fixes map onto that split: an inter-agency agreement and a fee-funded review office are administrative; the cultured-meat precedent, where only Congress could break the deadlock, shows what the high-veto path costs in time.
- **An abundance-agenda case.** This is a clean instance of the [[abundance-agenda]] diagnosis: the technology exists, the money exists, local governments are eager, and delivery is blocked by procedure. It is also an unusually favourable one, since the "losers" from reform are diffuse (no incumbent industry is displaced by killing mosquitoes).
- **The invention-to-impact gap.** [[health-stack]] frames preventive medicine's core failure as the distance between what is invented and what reaches people; [[pharma-industry-economics]] describes the drug-side version. Vector control is the public-health instance, and PDUFA is the one regulatory reform in that literature with a measured before-and-after.
- **What the essay does not address.** Rosen does not engage with the substance of the 2022 public pushback that paused the California releases, nor with the technical limits discussed elsewhere in the literature (e.g., the need for continued releases under self-limiting designs, environmental tetracycline, or *Wolbachia* strain stability under heat). The essay is a case for regulatory reform, not a risk assessment, and should be read as one.

## Sources
- Rosen, Maya (2026). "Mosquitoes are a choice." *Works in Progress*, Issue 26. <https://worksinprogress.co/issue/mosquitoes-are-a-choice/> — [[2026-10-05-mosquitoes-are-a-choice|local copy]]
