---
source: agent
compiled_from:
  - agent-notes/raw/physics/2026-02-02-nuclear-magic-numbers-spin-pseudospin.md
compiled_at: 2026-04-17
model: claude-opus-4-6
confidence: high
---

# Nuclear Magic Numbers

In nuclear physics, **magic numbers** are specific counts of protons or neutrons (2, 8, 20, 28, 50, 82, 126) at which nuclei exhibit exceptional stability — analogous to noble-gas electron shell closures in atomic physics. Nuclei at these numbers show pronounced discontinuities in binding energies and elevated excitation energies, indicating closed-shell configurations.

## The shell model and spin-orbit coupling

The nuclear shell model, introduced independently by Mayer and by Haxel, Jensen, and Suess in 1949, explained magic numbers by adding a strong **spin-orbit (SO) coupling** term to the nucleon single-particle Hamiltonian. This splits energy levels with the same orbital angular momentum *l* into doublets with *j = l + 1/2* and *j = l − 1/2*, breaking spin symmetry and producing the observed shell gaps. The first three magic numbers (2, 8, 20) follow from a simple harmonic oscillator potential; the higher ones (28, 50, 82, 126) require the SO term.

The Nilsson model extends this to deformed nuclei by adding an *l²* term that lowers high-angular-momentum states. Within this framework, one can characterize shell structure with two parameters: κ (SO strength) and μ (orbital correction strength).

## Pseudospin symmetry

A curious near-degeneracy exists between pairs of single-particle states *(n, l, j = l + 1/2)* and *(n − 1, l + 2, j = l + 3/2)*, called **pseudospin doublets**. These share a "pseudo" orbital angular momentum *l̃ = l + 1*. Ginocchio (1997) showed that this pseudo-orbital angular momentum corresponds to the lower components of the Dirac wave functions, connecting pseudospin symmetry to relativistic nuclear structure. When the Nilsson parameter μ approaches 0.5, pseudospin doublets become exactly degenerate.

In relativistic mean-field models, where nucleons are described by Dirac spinors interacting via meson exchange, the SO potential arises naturally from the interplay of strong attractive scalar and repulsive vector mean fields. Pseudospin symmetry also finds a natural explanation in this framework.

## The microscopic origin: spin-to-pseudospin transition

A key open question has been how phenomenological effective nuclear potentials connect to the realistic nuclear forces derived from quantum chromodynamics. Ding, Wang, Yao, Hergert, Liang, and Bogner (2026) addressed this by tracking how shell structure evolves as a function of momentum resolution, starting from chiral effective field theory (χEFT) interactions and using the **similarity renormalization group (SRG)** to smoothly connect high- and low-resolution scales.

Their central finding for ¹³²Sn: as the resolution scale λ decreases from high momentum to the low-momentum regime (~1.8 fm⁻¹ ), the shell structure undergoes a **transition from spin symmetry to pseudospin symmetry**, during which the conventional magic numbers emerge naturally. At high resolution, spin doublets are nearly degenerate (spin symmetry holds, no familiar magic numbers). At low resolution, pseudospin doublets become nearly degenerate while spin-orbit splittings grow large enough to produce the gaps at Z = 28 and Z = 50.

This establishes, for the first time from first principles, why effective nuclear potentials at "everyday" nuclear-physics scales feature the strong SO coupling that gives rise to magic numbers — it is a natural consequence of running realistic forces down to lower resolution.

## The essential role of three-nucleon forces

Decomposing the contributions to SO splittings reveals that **three-nucleon (3N) forces** are the dominant driver. For EM-family chiral interactions:

- The 2π-exchange component of the 3N force dominates, with the low-energy constant c₃ accounting for 80–90% of the total 3N contribution.
- As λ decreases from 2.8 to 1.8 fm⁻¹, the SO splitting between the 0f₇/₂ and 0f₅/₂ partners increases by ~52–80%, with 3N forces responsible for roughly half to two-thirds of this enhancement.
- 1π-exchange and contact contributions are negligible by comparison.

This confirms and quantifies earlier indications that 3N forces are crucial for reproducing shell structure in calcium isotopes and the oxygen drip line within low-resolution [[ab-initio-nuclear-theory|ab initio]] frameworks.

## Universality across frameworks

The same spin-to-pseudospin transition appears in relativistic Hartree-Fock calculations using one-boson-exchange potentials (OBEPs) with varying momentum cutoffs — even without explicit 3N forces. In this framework, 3N effects are partially captured through virtual nucleon-antinucleon excitations that dress the Dirac mass. As the cutoff Λ decreases, the meson-nucleon couplings converge toward those of successful phenomenological interactions like PKA1, providing microscopic justification for relativistic mean-field models.

The robustness across both nonrelativistic (chiral EFT + SRG/IMSRG) and relativistic (OBEP + RHF) frameworks underscores the universality of this mechanism.

## Implications for exotic nuclei

Analysis of calcium isotopes spanning the magic numbers N = 20, 28, and 50 shows that SO splitting of proton states **decreases monotonically** with increasing neutron number from stable to neutron-rich nuclei. This signals a gradual "melting" of traditional shell structures toward the neutron drip line — consistent with energy density functional studies and relevant to ongoing experiments at radioactive ion beam facilities like FRIB.

The melting of shell closures in neutron-rich nuclei has implications for the [[r-process-nucleosynthesis|r-process]] path that produces heavy elements in neutron star mergers and supernovae.

## Sources

- Ding, Wang, Yao, Hergert, Liang, Bogner (2026). "From Spin to Pseudospin Symmetry: The Origin of Magic Numbers in Nuclear Structure." *Phys. Rev. Lett.* 136, 052501. <https://doi.org/10.1103/8lzc-j1lx> — [[2026-02-02-nuclear-magic-numbers-spin-pseudospin|local copy]]
