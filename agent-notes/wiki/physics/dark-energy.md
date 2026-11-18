---
source: agent
compiled_from:
  - agent-notes/raw/physics/2026-11-17-what-makes-up-the-cosmos.md
compiled_at: 2026-11-17
model: claude-opus-5-5
confidence: medium
---

# Dark Energy and the Cracks in Lambda-CDM

**Dark energy** is the name for whatever drives the accelerating expansion of the universe. Since 1998 the standard model of cosmology, **Lambda-CDM**, has treated it as **lambda**: a constant energy of empty space. The universe in that model is about 70% dark energy and 30% matter, and most of the matter is slow-moving "cold dark matter" (CDM). For about twenty years every new survey fit this picture. Since 2024 the fit has started to slip. In May 2026 the **Dark Energy Survey (DES)** released its final combined analysis ([arXiv 2605.27221](https://arxiv.org/abs/2605.27221)). Combined with DESI, the CMB and supernovae, it shows a **three-sigma preference for dark energy that has weakened in recent eons** over a constant lambda. Simone Ferraro (Lawrence Berkeley National Laboratory) put the mood plainly: "There appear to be cracks in that model... There's something that doesn't fit."

## How lambda got in

Charlie Wood (*Quanta*) frames cosmology as building a dossier on someone's life from scattered records, then telling the story that fits them all. Before 1998 the story was matter only. Galaxy rotation implied dark matter around every visible galaxy, and there seemed to be just enough matter in total to slow the expansion forever without stopping it. Some records didn't fit. Some stars looked older than the universe, and models worked better with an extra energy term. Joshua Frieman (then at Chicago, now at SLAC) was studying that "missing energy" as a niche idea. His 1997–98 workshop went from a few dozen sign-ups to TV cameras once two supernova teams announced in early 1998 that the expansion is speeding up. The Blanco 4-meter telescope in Chile, which later carried the DES camera, played a role in that discovery.

The 1998 case rested on a thin file: a blurry CMB, a few million galaxies and a few dozen supernovae. DES was built to thicken it. Fermilab physicists started planning in 2003 and built the 570-megapixel Dark Energy Camera. They observed for 758 nights from 2013 to 2019, a year longer than planned to make up for El Niño cloud cover, and catalogued hundreds of millions of galaxies with a collaboration of more than 400 scientists in seven countries. Each interim analysis came back consistent with Lambda-CDM.

## The four kinds of record

The probes measure different things, which is what makes the result hard to wave away:

| Probe | What it records | Who |
|---|---|---|
| **Cosmic microwave background** | A snapshot of the early universe; sets the starting conditions | Planck and successors |
| **Baryon acoustic oscillations** | Sound waves in the early plasma left shells of slightly denser matter, all the same physical size. How big a shell looks gives its distance, which traces the expansion over roughly the last 10 billion years | DESI (Kitt Peak, thousands of fibers that each swivel onto one galaxy) |
| **Type Ia supernovae** | Explosions of near-known brightness; distance versus redshift traces recent expansion | DES (1,600 supernovae, reprocessed) and other catalogs |
| **Matter clumping** | The tug of war between gravity pulling matter together and dark energy pushing it apart. DES measures it from how galaxies cluster (each one marks the center of a dark-matter cloud) and from how foreground matter distorts the shapes of background galaxies (weak lensing), comparing pair after pair across hundreds of millions of galaxies | DES |

An agent-drawn distinction the article implies but doesn't name: the first three mostly constrain the **expansion history**, how fast space grew. Clumping constrains the **growth history**, how fast structure formed against that expansion. A changing dark energy has to fit both, so the two are independent handles on the same question.

## Timeline of the crack

- **2024 — DESI's first-year results.** Adding baryon acoustic oscillation distances to the CMB and supernova data, Lambda-CDM no longer fit everything. A dark energy that weakens over time fit better.
- **2025 — DESI's second analysis** with more data found the same preference.
- **Early 2026 — DES's final clumping results** after seven years of analysis. Ferraro, who isn't in DES, called it "a real tour de force" that "pushed the analysis to a new level."
- **May 2026 — DES's combined final analysis**, merging its clumping map, reprocessed supernovae, DESI's shells and the CMB: a three-sigma preference for weakening dark energy. Seshadri Nadathur (DESI) said that spring he trusted the reprocessed DES supernovae "much more than... any other supernova dataset." Since then, per *Quanta*'s correction, other teams have reanalyzed their supernova catalogs and the leading catalogs now agree closely, so the supernova input is no longer the obvious weak link.

## Why "no single item to toss" matters

The strongest point in the DES result is structural, not statistical. If Lambda-CDM is right, the CMB disagrees with the matter maps, the matter maps disagree with the supernovae, and the supernovae disagree with the CMB. A tension driven by one dataset with a hidden error would go away when that dataset is dropped. This one doesn't: every pair is a little off. That makes "one instrument has a calibration bug" less likely and "the model is missing something" more likely. It isn't proof. Several small systematic errors, or a wrong assumption shared by all the probes, could produce the same pattern, but it's a much harder story to tell.

Two pieces of outside context, not from the article:

- The matter-maps-versus-CMB leg matches the long-running **S8 tension**, where weak-lensing surveys including earlier DES releases found the universe slightly less clumpy than the Planck CMB predicts under Lambda-CDM. The final DES result places that old anomaly inside a larger pattern.
- In DESI's published fits, the best-fitting evolving dark energy uses the two-parameter w0–wa model, and it appears to cross the w = −1 line that separates ordinary fields from "phantom" behavior. Simple scalar-field models struggle to do that, so even a confirmed signal wouldn't point to an obvious replacement theory.

## How much three sigma means

Three sigma means data this lopsided would show up by chance about 0.3% of the time if Lambda-CDM were exactly right. Five sigma, physics' bar for a discovery, is about one in 3.5 million. The article says three sigma is "significant enough to make people pay attention" but "far short" of a discovery. Agent caveats: the competing model has extra free parameters, so some improvement in fit comes for free, and several 3-sigma excesses in physics have dissolved with more data. What sets this one apart is that it has held across DESI's 2024 and 2025 releases and the DES final analysis, with different instruments and partly independent data.

## Three ways to read it

1. **Dark energy really is weakening.** Many theorists resist this. Explaining why the vacuum's energy is so tiny is already the cosmological-constant problem, the source of multiverse arguments. A changing dark energy adds a second puzzle: why that tiny amount is "evaporating at a mysteriously slow rate."
2. **Lambda is fine and another assumption is off.** Ferraro and collaborators showed in 2025 ([arXiv 2504.16932](https://arxiv.org/abs/2504.16932)) that if **reionization**, when early stars and other bright objects burned off the neutral hydrogen fog, happened about 200 million years earlier than Lambda-CDM's ~700 million years after the Big Bang, Lambda-CDM fits the data better. "This number is crucial," Ferraro says. "However, it's extremely hard to measure." Agent note: this connects to [[jwst-early-universe-puzzles]]. JWST's too-bright, too-many early galaxies and early black holes are exactly the kind of sources that could ionize the universe sooner. So the "fix lambda" route and the JWST anomalies may be one story seen from two ends, though the article doesn't make this link.
3. **Dark energy and dark matter are coupled.** Some theorists are exploring a dark energy that shifts together with the mass of dark matter.

The two "dark" parts of Lambda-CDM are under pressure from different directions. [[modified-newtonian-dynamics]] and [[mond-galaxy-cluster-missing-mass]] challenge the CDM half at galaxy scales. This result challenges the lambda half at cosmic scales. Option 3 would tie the two together.

## What would settle it

Ferraro: "It's certainly enough to make you either uncomfortable or excited." Field-level confusion after two decades of stability is how the 1998 discovery started too. The plan is a thicker dossier:

- **DESI** keeps observing until at least 2028.
- The **Vera C. Rubin Observatory** on Cerro Pachón, about six miles from DES's telescope, began survey operations in 2026 with the world's largest digital camera. It's expected to catalog about **10 billion galaxies** and millions of supernovae, compared with the few dozen behind the 1998 discovery. DES veterans are moving to Rubin to repeat the pair-by-pair analysis.

The next signal to watch is whether these surveys push the preference toward five sigma or back toward zero. A better independent measurement of reionization timing would separate reading 1 from reading 2.

## Sources
- Wood, Charlie (2026). "What Makes Up the Cosmos? A 20-Year Survey Hints That Something Is Missing." *Quanta Magazine*. <https://www.quantamagazine.org/what-makes-up-the-cosmos-a-20-year-survey-hints-that-something-is-missing-20261116/> — [[2026-11-17-what-makes-up-the-cosmos|local copy]]
