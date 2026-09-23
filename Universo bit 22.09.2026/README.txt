# Two-Mode Jaynes–Cummings Model of Endogenous and Exogenous Phase Coherence

**Complete Zenodo record with historical development**

**DOI:** [10.5281/zenodo.22904994](https://doi.org/10.5281/zenodo.22904994)

**Authors:** Miguel Angel Percudani (corresponding: miguel_percudani@yahoo.com.ar, ORCID [0009-0007-1748-3212](https://orcid.org/0009-0007-1748-3212)) & Jorge Iván Díaz  
**Affiliation:** Independent Research Collaboration  
**Publication date:** 22 September 2026

**Related records:**
- Binary Universe Ontology: [10.5281/zenodo.18015439](https://doi.org/10.5281/zenodo.18015439) (2025)
- UAT framework: [10.5281/zenodo.17886549](https://doi.org/10.5281/zenodo.17886549) (2025)
- Antifrequency datasets: [10.5281/zenodo.17861265](https://doi.org/10.5281/zenodo.17861265) (2025)

---

## 1. Central paper — read this first

> **`track_A_formal.pdf`** (746 kB, 7 pages)  
> *A Two-Mode Jaynes–Cummings Model of Endogenous and Exogenous Phase Coherence: Falsifiable Predictions for Neural Dynamics*

This is the **formal, falsifiable Track A**. The model contains **no geometric constants** ($\Phi_{\text{UAT}}$, $k_{\text{UAT}}$, $\kappa_{\text{crit}}$). The coupling strength $g_0$ is a free parameter to be fitted to EEG/fMRI data. **This PDF is the one to cite.**

All other files in this record are complementary or supplementary.

---

## 2. Two-track structure

The record is organized in two independent tracks:

### Track A — Formal, falsifiable, testable now

A two-mode Jaynes–Cummings model with Lindblad dissipation and Default Mode Network modulation. The model produces a two-dimensional phase diagram in the plane $(\alpha = g/\delta,\ \gamma_\phi)$ and four falsifiable predictions for EEG/fMRI experiments. All parameters are free and listed in the paper. **Track A remains valid even if Track B is refuted.**

Documents:
- **`track_A_formal.pdf`** (7 pages) — main paper, 4 falsifiable predictions, phase diagram
- **`track_A_field_equations.pdf`** (15 pages) — technical appendix: complete field equations, Hilbert space, operator algebra, Lindblad dissipator, master equation, reduced dynamics, BDF numerical scheme
- **`track_A_Extended_version_full_derivation.pdf`** (20 pages) — extended appendix that **supersedes** the previous one: it contains all the material of `track_A_field_equations.pdf` plus three new sections with full step-by-step derivations:
  - (i) mean-field closure of the reduced dynamics
  - (ii) expansion of the density matrix in the Jaynes–Cummings eigenbasis (dressed states)
  - (iii) linear stability analysis of the Liouvillian superoperator and spectral gap $\Delta$

Both appendix versions are provided for convenience. **The extended version is the recommended reference.**

### Track B — Speculative research program

An ontological interpretation of Track A in terms of the Binary Universe Ontology (Bit 1 = analytic qubit, Bit 0 = substrate oscillator, causal friction = Jaynes–Cummings exchange, homeostasis = Lindblad dissipation, DMN = baryonic filter). Contains the constants $\Phi_{\text{UAT}} = \pi^2/8$, $k_{\text{UAT}} \approx 10.90677$, $\kappa_{\text{crit}} \approx 10^{-78}$ **explicitly labeled as speculative hypotheses, not derived results.**

Document:
- **`track_B_speculative.pdf`** (6 pages) — *Binary Universe Ontology as an Interpretation of Two-Mode Coupling: The Geometric Origin of $k_{\text{UAT}}$ as a Speculative Research Program*

The two tracks are independent. Track A does not use any of the constants from Track B. Track B does not modify the numerical results of Track A.

---

## 3. Figures (stand-alone PNGs for reuse)

- **`v5_run1_rabi.png`** (130 kB) — Rabi oscillation: $\langle \sigma_z \rangle$, $\langle n_0 \rangle$, $S_{vN}$, purity for $g = 17$ Hz, 10 periods
- **`v6_scan2D.png`** (150 kB) — Phase diagram in $(\alpha = g/\delta,\ \gamma_\phi)$ plane, four steady-state observables
- **`v6_cortes1D.png`** (173 kB) — One-dimensional cuts at $\gamma_\phi \in \{0.09, 0.44, 2.26, 11.60\}$ Hz

---

## 4. LaTeX sources (for reproducibility)

- `LaTex_track_A_formal.tex` (16 kB) — source of the central paper
- `LaTex_track_A_field_equations.tex` (31 kB) — source of the 15-page field-equations appendix
- `LaTex_track_A_Extended_version_full_derivation.tex` (45 kB) — source of the 20-page extended appendix
- `LaTex_track_B_speculative.tex` (17 kB) — source of the speculative interpretation

All sources compile with `pdflatex` (two passes required for cross-references). No external dependencies beyond the standard TeX Live distribution.

---

## 5. Code archives (historical development)

The numerical results were developed over six versions. Each `trackA_vN.zip` contains the scripts and data as they were at that stage. Historical versions are included for transparency; **only v5 and v6 are needed to reproduce the published results.**

### Historical / supplementary

- **`trackA_v2.zip`** (326 kB) — v2: manual RK4 integrator, initial dark state $|0,0\rangle$ bug, crashes for $\gamma_\phi \gtrsim 10$ due to stiffness
- **`trackA_v3.zip`** (426 kB) — v3: fix with BDF implicit solver (`scipy.integrate.solve_ivp`), first stable runs
- **`trackA_v4.zip`** (630 kB) — v4: first sweep in $(\alpha, \gamma_\phi)$ plane
- **`trackA_v4_1.zip`** (643 kB) — v4.1: JC coupling corrected (standard Jaynes–Cummings, not anti-JC)

### Final — use these to reproduce

- **`trackA_v5.zip`** (1,626 kB) — **IMPORTANT**: Rabi runs and endogen/exogen contrast at equal Rabi period. Generated `v5_run1_rabi.png`.
- **`trackA_v6.zip`** (510 kB) — **IMPORTANT**: Final 2D scan and 1D cuts, phase diagram, boundary $\alpha_{\text{cruce}}(\gamma_\phi)$, empirical scaling $g_{\text{cruce}} \cdot \gamma_\phi^{0.62} \approx 3.95$. **This is the version used in `track_A_formal.pdf`.**

---

## 6. How to reproduce the central result

### Numerical

```bash
# Main result (phase diagram + Rabi)
unzip trackA_v6.zip && cd trackA_v6
python -m venv venv && source venv/bin/activate
pip install numpy scipy pandas matplotlib
python main.py   # BDF solver, rtol=1e-7, atol=1e-9
# Outputs: v6_scan2D.png, v6_cortes1D.png











