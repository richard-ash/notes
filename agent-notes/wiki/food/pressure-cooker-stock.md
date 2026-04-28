---
source: agent
compiled_from:
  - agent-notes/raw/food/2026-04-28-michelin-stock-60-minutes.md
compiled_at: 2026-04-28
model: claude-opus-4-7
confidence: high
---

# Pressure-Cooker Stock and Consomme

Chris Young — formerly of Heston Blumenthal's Fat Duck restaurant in the early 2000s, co-author of *Modernist Cuisine*, and founder of Combustion Inc. — argues that the classical French rules for stock-making (whole carcasses, large vegetables, 8+ hour simmer) are a heritage compromise that pressure cooking and surface-area maximization render obsolete. A two-quart roast chicken stock from a $5 Costco rotisserie chicken can match a Michelin-grade simmered stock in 40 minutes.

## The technique

1. Sweat aromatics — half a carrot (thinly sliced), half an onion (thinly sliced), 2 smashed garlic cloves — in chicken fat or neutral oil.
2. Strip and **shred all meat** off a Costco rotisserie chicken; keep skin and bones. Use the meat — Young insists great stock should taste like meat, not bones, and at the Fat Duck stocks were heavy on meat to mimic roasting juices.
3. Add chicken (meat, skin, bones) and 2 quarts of *boiling* water to the pressure cooker.
4. Pressure-cook **40 minutes** on high.
5. Release pressure **slowly** — never quick-release (super-heated water flashes to a boil and re-emulsifies fat).
6. Yield is *more than* 2 quarts because juices are extracted from the meat.

## Why pressure cooking works: two physics principles

### Fick's law of diffusion (surface area dominates)

Extraction rate scales with the surface-area-to-volume ratio. Young uses the coffee-bean analogy: a whole bean produces flavorless water; ground fine, a few beans make strong coffee. Same logic for stock — shredding meat removes the diffusion barrier that whole carcasses preserve. Escoffier's fear that small pieces would "muddy" the stock was correct *under boiling*, but pressure cooking removes that constraint (see below).

### Arrhenius equation (temperature exponentially accelerates extraction)

A sealed pressure cooker reaches ~250 °F instead of 212 °F. As Young puts it, **every 10 °F increase makes stock develop ~45% faster**, so 250 °F is roughly 4× faster than simmering. This follows from the Arrhenius rate equation governing collagen→gelatin conversion.

### Why pressure-cooked stock comes out clear

Boiling is a turbulent process — vapor pressure pushing up overcomes atmospheric pressure pushing down, and the resulting churn emulsifies fat and breaks particles into a cloudy suspension. Inside a sealed pressure cooker, steam pressure rises until it equals the would-be boiling pressure, and the liquid goes **dead calm**. No agitation, no emulsion, no clouding. This is why classical stock-makers' fear of muddiness doesn't apply to pressure cooking.

## Two-stage extraction (Young's measured data)

Young instrumented the process: he simmered and pressure-cooked identical stocks, sampled hourly for 12 hours, centrifuged each sample, and measured dissolved solids with a refractometer.

- **1 hour pressure-cooked ≈ 6 hours simmered**
- **2 hours pressure-cooked ≈ 9 hours simmered**

A single diffusion equation doesn't fit the curve — it takes two terms, indicating two parallel processes:

| Phase | What's extracted | Why |
|---|---|---|
| **Fast step** | Sugars, salts, soluble proteins, peptides, fats — the *flavor* | Easily washed out of shredded meat fibers |
| **Slow step** | Collagen → gelatin from skin/bones; proteoglycans from cartilage — the *body and silky mouthfeel* | Big bushy molecules that take time to unwind |

Stovetop simmering takes hours to complete the slow step; the pressure cooker collapses it under an hour.

## The sweet spot — and why longer is worse

Counterintuitively, the extraction curve keeps rising but the stock gets **worse** past ~3 hours of pressure cooking:

- **Metallic taste** — bone structure breaks down and dumps calcium and magnesium into the liquid.
- **Bitter taste** — proteins fragment into short bitter peptides.
- **Won't gel** — gelatin "ropes" get chopped into pieces too short to form the tangled mesh that traps water. Young shows side-by-side photos: 1-hour stock gels solid; 12-hour stock is a sloppy mess.

Young's recommended times by source:

| Stock | Pressure-cook time | Reason |
|---|---|---|
| Chicken | 30–90 min (40 min default) | Collagen extracts easily |
| Beef | ~2 hours | Beef collagen is tougher |
| Other animals | Somewhere between | — |

## Extension 1: Pressure-cooked consomme (myosin raft)

The classical consomme method whisks pureed meat, vegetables, and egg white into stock, simmers gently for an hour to form a fragile "raft," then ladles out the clear liquid beneath without breaking the raft. Young replaces this with the **smoothie-from-hell** method:

1. Blend a portion of the cooled stock with raw chicken in a high-speed blender. The violent shearing releases **myosin** (a sticky muscle protein that behaves like egg-white albumin) and whips in thousands of air bubbles.
2. Pour the slurry back into the stock, bring to high pressure, **turn off the heat, and let cool naturally**.
3. Myosin denatures as the stock heats — uncoiling into sticky strings that net oil droplets and particles. Whipped-in air bubbles get trapped in the coagulating protein and float the whole mass to the surface as a buoyant **raft** that scrubs the stock as it rises.
4. The raft is solid — pour through a sieve, even squeeze it, no risk of breaking the gel as in the classical method.

Result: consomme brunoise (clarified consomme garnished with fine-diced vegetables) without the babysitting.

## Extension 2: Ice filtration (gel filtration consomme)

Even pressure-cooked-and-rafted consomme cloudbacks when chilled — fat droplets clump and solidify into opaque flecks that defeat clarity. Young's brute-force attempts (centrifuges, 0.2-micron membrane filters at $30 per cup) failed.

The fix came from German gel chemist Gerard Clarke at a lunch with Heston Blumenthal and Albert Adrià: **let the stock clarify itself.**

1. Freeze stock into ice cubes/blocks. The expanding ice crystals stretch the gelatin mesh.
2. Place blocks on a strainer in the fridge and walk away.
3. As the ice slowly thaws, melt-water carries small flavor molecules out through the stretched gelatin mesh.
4. The cold keeps fat droplets solid (they can't flow through), and the gelatin net traps haze proteins (too big to pass through).

Drip-by-drip output:
- **Crystal-clear, twice as concentrated** as the original stock — the intensity you'd normally get from boiling down (which loses aromatics to evaporation), but lossless.
- The gelatin-rich "gunk" left behind on the strainer is essentially a demi-glace — save for sauces.
- Because gelatin is filtered out, this consomme **won't set on its own**. Add 0.5–1% purified gelatin by weight if a jelly is wanted.

## Connections to other techniques

- Young's instrumentation philosophy ("you can't improve what you don't measure") drives the same multi-sensor predictive thermometer used in [[reverse-searing]]. The Costco-stock data and the rib-eye phase-temperature data come from the same project.
- The pressure-cooker insight that *boiling clouds, calm-liquid clarifies* is the inverse of the searing insight that *evaporative cooling protects the interior* — both rely on understanding which surface phenomena dominate at which temperature.

## Sources
- Chris Young (2025). "$6 Michelin Stock in 60 Minutes (Costco Hack)." <https://www.youtube.com/watch?v=3k20zFlbFfE> — [[2026-04-28-michelin-stock-60-minutes|local copy]]
