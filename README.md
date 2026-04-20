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
four axioms, a single scalar field $\Phi$ with a geometrically fixed kinetic
operator ($\alpha=2$), a single non-linear potential with two coefficients
related by a vacuum condition, and an algebraically determined effective
metric that reproduces general relativity exactly at the post-Newtonian
level. Fifteen core results are formally proven, six more are numerically
verified, and ten explicit open problems are stated so that the theory is
both well-defined and falsifiable on a clear basis.

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

## Citation

Once Zenodo has minted a DOI for this repository, please cite it in addition
to the paper proper. The `.zenodo.json` file in the root contains the
machine-readable metadata that Zenodo uses on each release.

## License

The paper text and the accompanying numerical code are released under
[CC BY 4.0](LICENSE).
