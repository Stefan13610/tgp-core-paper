# Substrate → continuum limit (OP-6, Row 21)

Supports **Row 21 of the numerical-results table** in the core paper and
provides the numerical evidence alluded to by **OP-6** (the rigorous
proofs of CG-1/CG-3/CG-4 are still open; this folder does *not* close
them).

Headline result:

> FRG LPA' + block-spin Monte Carlo give
> $K_{\mathrm{IR}}/K_{\mathrm{UV}} = 1.000$ at the $\alpha=2$ fixed point
> (**8/8 PASS**).

## Scripts

### `a1_alpha2_frg_synthesis.py` — FRG LPA' half (7/7 PASS)

Closed synthesis of the **weak $\alpha = 2$ theorem**:

1. Algebraic Lemma A3 — change of variables $\phi \to \Phi = \phi^2$
   forces the kinetic-operator degree $\alpha = 2$.
2. FRG LPA' flow — $K(\Phi)$ is preserved at one loop; anomalous
   dimension $\eta^* = 0.044$ at the Wilson-Fisher fixed point.
3. Monte Carlo cross-check — block-spin RG on a 1D lattice reproduces
   the same fixed point.

All seven Lemmas A1–A5 + two numerical cross-checks pass.

### `cg_strong_numerical.py` — block-spin Monte Carlo half (1 aggregate test)

Large-volume Monte Carlo with block-averaging; probes the three formally
open theorems in a numerical sense:

- **CG-1** — contraction of the Kadanoff blocking operator:
  $\mathrm{Var}(\Phi_B)$ converges across microscopic $\beta$'s
  (different microscopic Hamiltonians → same fixed point).
- **CG-3** — convergence $\Phi_B \to \Phi$ in $L^2$:
  $\|\Phi_B - \Phi_{2B}\|$ decreases with $L_B$ (CLT-like).
- **CG-4** — correlator $\xi_{\mathrm{eff}}(\Phi)$ shows the linear
  $K \propto \Phi$ relation predicted by $\alpha = 2$.

Status: **numerical evidence, not a proof.** The formal closure of
CG-1/CG-3/CG-4 remains OP-6.

`cg_results.txt` contains the raw Monte Carlo output.

## How to run

```
python a1_alpha2_frg_synthesis.py
python cg_strong_numerical.py
```

Dependencies: `numpy`, `scipy`, `matplotlib`.

## What is still open

The rigorous versions of

- **CG-1** — Banach-fixed-point proof of the Kadanoff blocking operator,
- **CG-3** — homogenization $\Phi_B \to \Phi$ in $H^1(\mathbb{R}^3)$
  (de Giorgi–Nash–Moser / $\Gamma$-convergence),
- **CG-4** — identification $K_{\mathrm{hom}} = K_{\mathrm{TGP}}$,

are stated as **OP-6** in the core paper. The scripts in this folder
show that the *numerical* fingerprint of the expected fixed point is
present, but do not replace those proofs.
