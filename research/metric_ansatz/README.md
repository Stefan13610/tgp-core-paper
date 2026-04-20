# Metric ansatz $h(\Phi)=\Phi$ from five independent arguments

Supports **Remark 2** in the core paper (scope of the selection statement
for $h(\Phi) = \Phi$, equivalently the exponent $p = 1$ in
$g_{ij} = (\Phi/\Phi_0)^p \delta_{ij}$).

## The five arguments

The core paper states that $p = 1$ is selected — not merely postulated —
by *five independent arguments* of different character (analytic,
observational, numerical). This folder provides the numerical material
for each. All tests pass.

| # | Argument | Type | Passing tests | Script(s) |
|---|----------|------|---------------|-----------|
| 1 | Substrate density: $\Phi$ is the substrate density $\Rightarrow g_{ij} \propto \psi$ | Analytic (T1–T2) | — | `lk2_metric_from_substrate_propagation.py`, `ex201_antipodal_metric_derivation.py` (T1–T2 portion) |
| 2 | PPN Cassini + LLR: $\gamma = p = 1$, $\beta = 1$ | Observational | 8/8 | `ex206_metric_hypothesis_necessity.py` |
| 3 | Information budget: antipodal condition $f\!\cdot\!h = 1$ | Analytic | 8/8 | `ex201_antipodal_metric_derivation.py` |
| 4 | Volume element: $\sqrt{-g} = \psi^p$ must $= \psi$ | Analytic + numeric | 11/11 | `r4_einstein_self_consistency.py`, `consistency_volume_element.py` |
| 5 | Soliton mass ratio: only $p = 1$ reproduces $r_{21} = 206.77$ | Numerical | 6/6 + 6/6 | `a2_metric_consistency.py`, `a3d_soliton_brannen_r.py` |

Together: *exponential metric* $g_{\mu\nu} = \eta_{\mu\nu}\exp(2\Phi/\Phi_0)$
is the unique ansatz simultaneously satisfying ghost-freedom, positive
kinetic energy, correct Newtonian limit, $\gamma = \beta = 1$ to all PPN
orders, and $\sqrt{-g} = \psi$.

## Scripts

### Argument 1 — substrate density

- **`lk2_metric_from_substrate_propagation.py`** — derives the
  $g_{ij} \propto \psi$ form from substrate-wave propagation.
- **`ex201_antipodal_metric_derivation.py`** (T1–T2 block) — derives
  it from the antipodal $\mathbb{Z}_2$ symmetry.

### Argument 2 — PPN observational

- **`ex206_metric_hypothesis_necessity.py`** — 8/8 PASS. Tests that
  *only* $h(\Phi) = \Phi$ is consistent with the Cassini
  $|\gamma - 1| \le 2.3 \times 10^{-5}$ and LLR
  $|\beta - 1| \le 6 \times 10^{-5}$ bounds; every $p \ne 1$ is ruled
  out by current data.

### Argument 3 — information budget

- **`ex201_antipodal_metric_derivation.py`** — 8/8 PASS. Derives
  $f \cdot h = 1$ (antipodal condition) from the $\mathbb{Z}_2$-symmetric
  information budget and shows that $p = 1$ is the unique solution.

### Argument 4 — volume element

- **`r4_einstein_self_consistency.py`** — 11/11 PASS. Einstein-equation
  self-consistency test: the requirement $\sqrt{-g} = \psi$
  (i.e. the volume element equals the substrate density) forces
  $p = 1$.
- **`consistency_volume_element.py`** — supporting identity checks for
  the same statement.

### Argument 5 — soliton mass ratio

- **`a2_metric_consistency.py`** — 6/6 PASS. Full metric-consistency
  sweep; soliton-mass ratio works only at $p = 1$.
- **`a3d_soliton_brannen_r.py`** — 6/6 PASS. Independent soliton-mass
  computation via the Brannen construction; reproduces
  $r_{21} = 206.77$ only at $p = 1$.

## How to run

```
python lk2_metric_from_substrate_propagation.py
python ex201_antipodal_metric_derivation.py
python ex206_metric_hypothesis_necessity.py
python r4_einstein_self_consistency.py
python consistency_volume_element.py
python a2_metric_consistency.py
python a3d_soliton_brannen_r.py
```

Dependencies: `numpy`, `scipy`, `matplotlib`.

## Remaining (not claimed in the paper)

Two complementary arguments are flagged in the main TGP workshop but are
*not* part of the five-argument statement in the core paper:

- phonon-dispersion relation $c_s(\Phi) = c_0 \sqrt{\Phi/\Phi_0}$
  (a full substrate-phonon derivation),
- an entropic / Bekenstein-Hawking-style derivation giving a metric
  linear in $\Phi$,

together with Lean 4 formalization of the five-argument chain. These
belong to future work and live in the main research repository at
<https://github.com/Stefan13610/TGP>.
