---
source: agent
compiled_from:
  - agent-notes/raw/physics/2002-04-30-mond-alternative-dark-matter.md
compiled_at: 2026-04-17
model: claude-opus-4-6
confidence: high
---

# Modified Newtonian Dynamics (MOND)

Modified Newtonian Dynamics (MOND) is an empirically motivated modification of Newtonian gravity (or inertia) proposed by Mordehai Milgrom in 1983 as an alternative to dark matter. Its central claim is that the mass discrepancies observed in galaxies and larger structures are not caused by unseen matter but by a breakdown of Newton's laws at very low accelerations.

## The core idea

MOND introduces a single new physical constant: a critical acceleration scale a_0 ~ 1.2 x 10^-8 cm/s^2. At accelerations well above a_0, standard Newtonian dynamics applies. Below a_0, the effective gravitational acceleration transitions to g = sqrt(g_N * a_0), where g_N is the Newtonian value. This can be expressed either as a modification of gravity:

> g * mu(|g|/a_0) = g_N

or as a modification of inertia:

> m * a * mu(a/a_0) = F

where mu(x) -> 1 for x >> 1 (Newtonian regime) and mu(x) -> x for x << 1 (MOND regime). The two formulations differ in principle and practice, but both produce the same low-acceleration phenomenology.

A suggestive coincidence noted by Milgrom: a_0 ~ cH_0/6, tying the acceleration scale to the Hubble constant and hinting that MOND may reflect cosmological influence on local dynamics.

## Key predictions and successes

Sanders and McGaugh (2002) catalogued MOND's phenomenological achievements across scales:

### Rotation curves of spiral galaxies

MOND's signature success. In the low-acceleration regime, v^4 = G*M*a_0 for a point mass, so all isolated galaxies have asymptotically flat rotation curves and obey a baryonic Tully-Fisher relation M ~ V^4. With a_0 fixed, MOND fits the detailed rotation curves of ~100 galaxies using a single free parameter per galaxy — the mass-to-light ratio (M/L) of the stellar disk. In the K-band, the fitted M/L ~ 0.8 with ~30% scatter, meaning MOND can nearly predict rotation curves with zero free parameters.

The theory naturally explains the difference between high surface brightness (HSB) and low surface brightness (LSB) galaxies: HSB galaxies are mostly in the Newtonian regime and show declining rotation curves that flatten, while LSB galaxies are entirely in the MOND regime with continuously rising rotation curves. Milgrom predicted this LSB behavior before these galaxies were discovered.

### Surface density thresholds

MOND implies a critical surface density Sigma_m ~ a_0/G ~ 860 M_sun/pc^2. This explains:

- **Freeman's law**: the observed upper limit on spiral galaxy surface brightness (~22 mag/arcsec^2) — systems above Sigma_m are Newtonian and unstable to bar formation
- **Fish's law**: a characteristic surface brightness within the effective radius of elliptical galaxies

### Pressure-supported systems

For nearly isothermal, self-gravitating systems, MOND predicts finite mass (unlike Newtonian isothermal spheres which have infinite mass) with a mass-velocity dispersion relation (M/10^11 M_sun) ~ (sigma/100 km/s)^4. This single relation spans:

- **Molecular clouds** (~5 km/s) — surface densities near Sigma_m
- **Globular clusters** — internal accelerations above a_0, no mass discrepancy expected or observed
- **Elliptical galaxies** — reproduces the Faber-Jackson relation and fundamental plane
- **Dwarf spheroidals** — Milgrom predicted M/L ratios of 10-100 before kinematic data confirmed it
- **Galaxy groups** — M/L values reduced from ~100 (Newtonian) to ~3 (MOND)
- **Galaxy clusters** — discrepancy reduced from factor 5-10 to factor ~2 (see [[mond-galaxy-cluster-missing-mass]])
- **Superclusters** — Perseus-Pisces filament: MOND M/L ~ 10, consistent with little or no dark matter

### The external field effect

A distinctive and non-Newtonian feature: the internal dynamics of a sub-system are affected by the external gravitational field in which it sits. A system with internal accelerations below a_0 will behave Newtonianly (with a renormalized G) if the external acceleration exceeds a_0. This violates the strong equivalence principle but preserves the weak equivalence principle (universality of free fall). It explains why open star clusters in the Galaxy do not show mass discrepancies despite having internal accelerations below a_0.

## Known difficulties

### Galaxy clusters

As of 2002, galaxy clusters remained MOND's most significant empirical challenge. Even after applying MOND, clusters showed a residual factor-of-two mass discrepancy, particularly concentrated in the central regions detectable through strong gravitational lensing. Sanders and McGaugh note that this could mean either MOND fails at this scale, or the baryonic mass census of clusters is incomplete. Subsequent work using the IGIMF theory has substantially reduced this discrepancy — see [[mond-galaxy-cluster-missing-mass]].

### NGC 2841

The most difficult individual galaxy for MOND rotation curve fits. MOND prefers a distance of ~19 Mpc versus the Hubble distance of ~10 Mpc. A Cepheid distance of 14.1 +/- 1.5 Mpc does not fully resolve the tension.

## Theoretical foundations

### The Bekenstein-Milgrom theory (AQUAL)

Milgrom's original prescription, applied naively to N-body systems, violates conservation of momentum. Bekenstein & Milgrom (1984) resolved this with a non-relativistic Lagrangian-based theory using a modified Poisson equation. This "aquadratic Lagrangian" (AQUAL) theory conserves energy and momentum, and has a notable mathematical property: the Bekenstein-Milgrom field equation is conformally invariant in three spatial dimensions.

### Relativistic extensions

Creating a covariant (general-relativistic) version of MOND has proven difficult:

- **Scalar-tensor theories** (AQUAL, PCG): suffer from either superluminal propagation, unstable vacua, or failure to predict observed gravitational lensing
- **Stratified theories**: can reproduce lensing by breaking Lorentz invariance, but are contrived
- **As of 2002**: "there is no satisfactory covariant generalization of MOND as a modification of general relativity. But this does not imply that MOND is wrong any more than the absence of a viable theory of quantum gravity implies that general relativity is wrong."

(Note: Bekenstein's TeVeS theory, published in 2004, partially addressed the lensing problem but has since faced its own challenges.)

### MOND as modified inertia

Milgrom (1994, 1999) explored the possibility that MOND modifies particle inertia rather than gravity. Such a theory must be strongly non-local — the motion of a particle depends on its entire past trajectory. This connects to Unruh radiation and the cosmological constant: if inertia arises from vacuum interaction, and Lambda modifies the vacuum temperature, one can derive a_0 = 2c * sqrt(Lambda/3), linking MOND's acceleration scale directly to the cosmological constant.

## MOND cosmology

In the absence of a complete relativistic theory, only tentative conclusions can be drawn:

- MOND is most consistent with a purely baryonic universe (Omega_m = Omega_b, no CDM)
- The early universe (radiation-dominated era) would be identical to the standard Big Bang
- After recombination (~z = 3-4), the entire universe becomes MONDian
- Structure formation would be greatly enhanced: galaxy-mass objects could be in place by z ~ 10
- McGaugh (2000) showed that a purely baryonic universe matches the CMB acoustic peak structure (particularly the low second peak observed by Boomerang)

## Temporal notes

This review was written in 2002, before several important developments:

- **TeVeS** (Bekenstein 2004): the first relativistic MOND theory that could handle gravitational lensing, though it has since been largely ruled out by gravitational wave observations (GW170817 showed gravitational and electromagnetic waves travel at the same speed)
- **The Bullet Cluster** (Clowe et al. 2006): widely cited as evidence against MOND, though MOND proponents argue it is not definitive
- **Planck CMB data**: provided much tighter constraints on cosmological parameters, creating challenges for purely baryonic cosmologies
- **IGIMF theory** (Kroupa et al.): substantially reduces the cluster missing-mass problem — see [[mond-galaxy-cluster-missing-mass]]
- The Pioneer anomaly, which Sanders and McGaugh found "provocative," was later explained by anisotropic thermal radiation pressure, not new physics

Despite these developments, MOND's core phenomenological success — predicting individual galaxy rotation curves from the observed baryonic distribution alone — remains unmatched by CDM, which requires fitting dark matter halo parameters for each galaxy. The radial acceleration relation (RAR), established observationally by McGaugh, Lelli & Schombert (2016), provides a modern, precise statement of the MOND phenomenology.

## Sources
- Sanders, McGaugh (2002). "Modified Newtonian Dynamics as an Alternative to Dark Matter." *Annual Review of Astronomy and Astrophysics*. <https://arxiv.org/abs/astro-ph/0204521> — [[2002-04-30-mond-alternative-dark-matter|local copy]]
