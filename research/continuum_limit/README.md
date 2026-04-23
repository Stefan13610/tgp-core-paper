# Substrate → continuum limit (OP-6, Row 21)

Numerical exploration for **OP-6** (rigorous continuum limit of $H_\Gamma$).
This folder provides numerical evidence only; the rigorous closure
of CG-1, CG-3, CG-4 is stated as **OP-6** in the core paper.

> **Status (2026-04):** the "α = 2 synthesis" line of argument
> (`a1_alpha2_frg_synthesis.py`, the A1–A5 lemmata of
> `dodatekQ2_most_gamma_phi_lematy.tex`) is **withdrawn** pending
> an actual derivation; see `../../KNOWN_ISSUES.md`. Theorem
> `thm:alpha2` in the core paper (axiomatic classification under
> (C1)–(C3)) is unaffected.

## Scripts

### `a1_alpha2_frg_synthesis.py` — [WITHDRAWN]

Claimed a "weak α = 2 theorem" via the chain
$\phi \mapsto \Phi = \phi^2$ + FRG LPA' + MC cross-check.
On review, the derivation of the kinetic form has an unresolved gap
(see banner at the top of the script). The file is kept for
transparency; its conclusions should not be cited.

### `cg_strong_numerical.py` — Monte Carlo exploration (CG-1/3/4)

Large-volume Metropolis Monte Carlo with block-averaging on the
1D lattice
$H = -J\sum_{\langle ij\rangle}(\phi_i\phi_j)^2$
equivalently the Ising model in the variables $\Phi_i = \phi_i^2$.
Measures:

- **CG-1** candidate — variance of the block-averaged field
  $\mathrm{Var}(\Phi_B)$ across several microscopic $\beta$.
- **CG-3** candidate — $\|\Phi_B - \Phi_{2B}\|$ vs. block size $L_B$.
- **CG-4** candidate — correlator $\xi_{\mathrm{eff}}(\Phi)$
  scaling.

Status: numerical evidence only, not a proof. The formal closure
of CG-1/CG-3/CG-4 remains **OP-6**. In particular, the scripts do
not attempt to measure the kinetic exponent α.

`cg_results.txt` contains the raw Monte Carlo output.

## How to run

```
python cg_strong_numerical.py
```

Dependencies: `numpy`, `scipy`.

## What is still open

The rigorous versions of

- **CG-1** — Banach-fixed-point proof of the Kadanoff blocking
  operator $T_b$,
- **CG-3** — homogenization $\Phi_B \to \Phi$ in
  $H^1(\mathbb{R}^3)$ (de Giorgi–Nash–Moser / Γ-convergence),
- **CG-4** — identification $K_{\mathrm{hom}} = K_{\mathrm{TGP}}$,

are all stated as **OP-6**. Progress on the reformulation (M1–M5)
is tracked in the development repository
[Stefan13610/TGP](https://github.com/Stefan13610/TGP).
