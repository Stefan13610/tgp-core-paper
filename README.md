# Theory of Generated Space (TGP) — Core paper

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19670324.svg)](https://doi.org/10.5281/zenodo.19670324)

This repository accompanies the preprint:

> **Theory of Generated Space: A minimal core of axioms, substrate, and effective field**
> M. Serafin, 2026.
> Zenodo DOI [10.5281/zenodo.19670324](https://doi.org/10.5281/zenodo.19670324).

It contains the paper source, the compiled PDF, and the subset of numerical
supporting material that is directly cited in the manuscript.

Companion paper (superconductivity closure):
[Stefan13610/tgp-sc-paper](https://github.com/Stefan13610/tgp-sc-paper)
— Zenodo DOI [10.5281/zenodo.19670557](https://doi.org/10.5281/zenodo.19670557).

The paper defines the minimal axiomatic and field-theoretic content of TGP:
four axioms, a single scalar field $\Phi$ with a kinetic operator
$K(\varphi)=\varphi^{4}$ (coefficient $\alpha=2$) uniquely selected inside
a class of local $\Phi$-covariant second-order operators (C1)–(C3), a
single non-linear potential with two coefficients related by a vacuum
condition, and an algebraically determined effective metric that
reproduces general relativity exactly at the post-Newtonian level.
Fifteen core results are formally proven, six more are numerically
verified, and ten explicit open problems are stated so that the theory is
both well-defined and falsifiable on a clear basis. The derivation of
(C1)–(C3) — equivalently of $\alpha=2$ — from the discrete substrate
Hamiltonian $H_{\Gamma}$ is stated as **OP-6**; see
[`KNOWN_ISSUES.md`](KNOWN_ISSUES.md) for the status of earlier numerical
claims that were withdrawn on internal review in April 2026.

## Repository contents

```
paper/
  tgp_core.tex                 — LaTeX source
  tgp_core.pdf                 — compiled preprint (12 pages)

research/                      — numerical support explicitly cited in the paper
  continuum_limit/             — FRG LPA' + block-spin MC (supports row 21, OP-6)
  metric_ansatz/               — five-argument support for h(Φ) = Φ (supports Remark 2)
  muon_g_minus_2/              — |Δa_μ| ≲ 1e-12 (closed-branch negative check)
  thermal_transport_molecular/ — Wiedemann-Franz null, Cahill-floor recovery
  casimir_mof/                 — 1e-4–1e-3 TGP correction (closed-branch negative check)
```

Each `research/<folder>/` contains its own `README.md` and/or `SUMMARY.md`
describing the problem, scripts and outcome.

## Build

```
cd paper
pdflatex tgp_core.tex
pdflatex tgp_core.tex        # second pass for cross-references
```

Requirements: any modern LaTeX distribution with `amsmath`, `amssymb`,
`amsthm`, `mathtools`, `longtable`, `enumitem`, `hyperref`, `caption`.

## Reproducibility of the numerical support

All Python scripts under `research/` run standalone:

```
python research/continuum_limit/cg_strong_numerical.py
python research/metric_ansatz/r4_einstein_self_consistency.py
python research/muon_g_minus_2/ps01_substrate_vertex_muon_g_minus_2.py
python research/thermal_transport_molecular/ps01_thermal_substrate_diffusion.py
python research/casimir_mof/ps01_casimir_parallel_plates.py
```

(and so on — each folder lists its scripts). Only `numpy`, `scipy` and
`matplotlib` are required.

## For the curious reader — full research workshop

This repository is intentionally pruned. It contains **only** the paper plus
its directly cited numerical support. The broader TGP working repository —
with the full ~500-page long companion manuscript, the exploratory research
directions, sector studies in QM foundations, cosmology, and extensive
appendices — is kept separately at:

https://github.com/Stefan13610/TGP

That is where development happens. This repository is the stable,
paper-aligned snapshot.

## Audit trail (post-Phase 3)

The deposit at DOI [10.5281/zenodo.19670324](https://doi.org/10.5281/zenodo.19670324)
is the immutable timestamped record. Subsequent in-repo audit material:

- [`research/POST_PHASE3_ADDENDUM_2026-04-28.md`](research/POST_PHASE3_ADDENDUM_2026-04-28.md)
  — six structural strengthenings landed in the workshop master after deposit:
  Phase 1 (50/50) + Phase 2 (54/54) + Phase 3 (60/60) closures with grand total
  281; 4-of-4 UV structural compatibility (AS / KKLT / LQG / CDT); B.6 promoted
  ALGEBRAIC → PARTIAL DERIVED (Λ_E = γ/12 sympy-exact); B.4 STRENGTHENED;
  Δ_target = 0.114 placed in heat-kernel a₂ frame; Path B m_σ²/m_s² = 2 preserved
  4/4 UV. **Nothing in the deposit is retracted.**
- [`KNOWN_ISSUES.md`](KNOWN_ISSUES.md) — live audit log; the most recent entry
  records the C5 wording sweep (α=2 selection within class (C1)–(C3),
  2026-04-26).

## Falsification entry points

The full prediction registry — falsification target, experimental horizon,
DOI of the flask that pre-registered each prediction — lives in the workshop
master at
[`TGP_v1/PREDICTIONS_REGISTRY.md`](https://github.com/Stefan13610/TGP/blob/main/TGP_v1/PREDICTIONS_REGISTRY.md).

Quick pointer to the predictions sourced from this paper:

- **Sector 1 — Gravity & WEP** (G1–G3): η_TGP = 3.54·10⁻¹⁷ → MICROSCOPE-2 (~2027–2028)
- **Sector 2 — Gravitational waves** (GW1–GW6): 3 polarization DOF, m_σ²/m_s² = 2
  → LIGO O5 / LISA / pulsar-timing arrays
- **Sector 3 — Photon rings** (BH1–BH3): r_ph^TGP / r_ph^GR = 1.293 ± 0.003%,
  Δb_crit = +14.56% → ngEHT 2030–2032
- **Sector 4 — Dark energy** (DE1–DE5): w = −1.000 exact, Λ_E = γ/12 sympy-exact
  → DESI DR3 / Euclid
- **Sector 7 — UV completion** (UV1–UV7): 4-of-4 structural compatibility
  with AS / KKLT dS / LQG / CDT; long-term research-track item
- **Sector 8 — Foundational locks** (F1–F7): single-Φ, K(φ) = K_geo·φ⁴,
  α₀ = 1069833/264500 sympy-exact rational, 14 founding constraints

## Citation

The `.zenodo.json` file in the root contains the machine-readable metadata
Zenodo uses on each release. A `CITATION.cff` is also provided for GitHub's
native "Cite this repository" widget.

```bibtex
@misc{Serafin2026TGPCore,
  author       = {Serafin, Mateusz},
  title        = {{Theory of Generated Space: A minimal core of axioms,
                   substrate, and effective field}},
  year         = {2026},
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.19670324},
  url          = {https://doi.org/10.5281/zenodo.19670324}
}
```

## License

The paper text and the accompanying numerical code are released under
[CC BY 4.0](LICENSE).
