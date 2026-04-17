---
source: agent
compiled_from:
  - agent-notes/raw/physics/2026-02-17-mond-missing-mass-galaxy-clusters.md
compiled_at: 2026-04-17
model: claude-opus-4-6
confidence: high
---

# MOND and the Missing Mass Problem in Galaxy Clusters

[[modified-newtonian-dynamics|Modified Newtonian Dynamics (MOND)]] successfully explains the rotation curves of individual galaxies without invoking dark matter, but at the galaxy-cluster scale it has long faced a stubborn shortfall: the baryonic mass visible in clusters accounts for only about half to two-thirds of the dynamical mass that MOND itself predicts. This "missing mass problem" has been one of the strongest empirical objections to MOND as a complete alternative to dark matter.

## The problem

Galaxy cluster masses can be estimated independently via hydrostatic equilibrium of the hot intracluster medium (ICM), velocity dispersion of member galaxies, or gravitational lensing. Under MOND, these estimates converge on a dynamical mass roughly twice the observed baryonic mass — a factor-of-two gap that standard MOND cannot explain without invoking some additional unseen component.

Previous attempts to close this gap have included:

- **Extended MOND formalisms** (Hodson & Zhao) — modifying the MOND interpolation function itself
- **Sterile neutrinos** (Angus) — positing 11 eV sterile neutrinos as the cluster-scale missing mass, yielding the nuHDM cosmological model
- **Cluster baryonic dark matter (CBDM)** (Milgrom) — hypothesizing cold baryonic matter heated by x-ray gas processes, possibly traced by ultradiffuse galaxies
- **Virial theorem corrections** (Lopez-Corredoira et al.) — accounting for surface pressure terms in the virial theorem applied to MOND

## The IGIMF resolution

Zhang, Zonoozi, and Kroupa (2026) argue that the gap has been substantially overestimated because previous studies used a canonical, invariant stellar initial mass function (IMF) to convert galaxy luminosities into stellar masses. The integrated galaxy-wide initial mass function (IGIMF) theory — developed entirely independently of MOND — predicts that the IMF varies with the star formation rate, metallicity, and density of the star-forming gas.

For massive elliptical galaxies (which dominate the cores of galaxy clusters), the IGIMF predicts a **top-heavy** gwIMF during their early, intense star-formation epochs. This has two key consequences:

1. **Higher mass-to-light ratios.** The M/L ratios of massive ellipticals are 4-6 times larger under the IGIMF than the canonical IMF, because a top-heavy IMF produces more massive stars that evolve quickly and leave behind remnants (white dwarfs, neutron stars, stellar-mass black holes).
2. **Large stellar remnant populations.** A substantial fraction (~50%) of the total stellar mass in massive early-type galaxies is locked in remnants — compared to only ~15-20% under the canonical IMF.

Spiral galaxies, by contrast, show minimal M/L changes under the IGIMF, so the effect is concentrated in the elliptical-dominated cluster cores.

## Quantitative results

Applying the IGIMF to 46 nearby galaxy clusters (z < 0.1) drawn from WINGS, 2MASS, and NGC 5044 data:

| Mass component | Fraction of MOND dynamical mass |
|---|---|
| ICM gas alone | 52 +4/-3 % |
| Baryonic (canonical IMF) | 67 +4/-3 % |
| Baryonic (IGIMF + IMF ICL) | 81 +5/-4 % |
| Baryonic (full IGIMF) | **88 +5/-4 %** |

The authors note that 88% is likely a **lower bound**, since the galaxy censuses used are incomplete (faint spiral galaxies with high gas fractions are underrepresented).

The residual distribution (baryonic minus dynamical mass, normalized) shifts from a mean of -0.33 under the canonical IMF to -0.11 under the full IGIMF, with the IGIMF residuals much more closely centered on zero.

## Independence of the two theories

A notable feature of this result is that the IGIMF and MOND were developed completely independently. The IGIMF was constructed to explain the variation of stellar populations across different star-forming environments — its parameters are set by observations of embedded clusters, metallicities, and star formation rates, with no reference to gravitational dynamics at the cluster scale. The fact that applying the IGIMF substantially closes the MOND missing-mass gap without parameter tuning is presented as evidence that neither theory requires ad hoc adjustments.

## Open tensions and caveats

The result is not without complications:

- **Lensing masses.** MOND strong-lensing masses within the Einstein radius can be reconciled with IGIMF baryonic masses to within ~10%. However, weak lensing probes larger radii where the spatial distribution of stellar remnants — potentially dispersed by neutron-star kick velocities of ~200 km/s — becomes important and poorly constrained.
- **Radial acceleration relation (RAR).** Brightest cluster galaxies (BCGs) deviate from the standard RAR. Whether the IGIMF's higher M/L ratios exacerbate or help resolve this tension depends on environment-dependent effects not yet modeled.
- **Dynamical mass estimates.** Some studies find that canonical-IMF baryonic masses of massive ellipticals agree with dynamical and lensing estimates. Zhang et al. note that those samples may have lower alpha-element ratios (indicating slower, later star formation), which would produce lower IGIMF M/L ratios closer to the canonical case.
- **Gravitational-wave merger rates.** If massive ellipticals indeed contain far more neutron stars and stellar-mass black holes than canonical IMF predictions suggest, this should be testable via gravitational-wave merger rate statistics.

## Implications

If confirmed, this work shifts the MOND missing-mass problem from a factor-of-two discrepancy to a ~12% residual — within observational uncertainties for many individual clusters. The remaining gap could plausibly be explained by incomplete galaxy surveys, ICL modeling uncertainties, or modest amounts of non-luminous baryonic matter, rather than requiring exotic physics or new particles.

More broadly, the result highlights how assumptions about the stellar IMF propagate through cosmological inferences. The canonical invariant IMF is a foundational assumption in most extragalactic mass estimates; if the IGIMF is correct, stellar masses throughout the universe have been systematically underestimated for massive early-type galaxies, with implications extending well beyond MOND to dark matter profiles, baryon fractions, and galaxy formation models.

## Sources
- Zhang, Zonoozi, Kroupa (2026). "Revisiting the missing mass problem in MOND for nearby galaxy clusters." *Physical Review D* 113, 043027. <https://doi.org/10.1103/PhysRevD.113.043027> — [[2026-02-17-mond-missing-mass-galaxy-clusters|local copy]]
