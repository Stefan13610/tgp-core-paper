# Numerical support for the core paper

This directory collects only the subset of TGP numerical work that is
directly referenced in `paper/tgp_core.tex`. For the full, exploratory
research tree (~40 additional subfolders across QM foundations, cosmology,
sector closures, etc.) see the main workshop repository:
https://github.com/Stefan13610/TGP

## Index

| Folder | Supports which claim in the paper | Status |
|--------|------------------------------------|--------|
| [`continuum_limit/`](continuum_limit/) | OP-6 and row 21 of the numerical-results table: FRG LPA' + block-spin Monte Carlo show $K_{\mathrm{IR}}/K_{\mathrm{UV}} = 1.000$ at the $\alpha=2$ fixed point (8/8 PASS). | Numerical evidence; rigorous proof open (OP-6). |
| [`metric_ansatz/`](metric_ansatz/) | Remark 2 (scope of the selection statement for $h(\Phi)=\Phi$): five independent arguments for $p=1$ (substrate density, PPN Cassini+LLR, information budget, volume element, soliton mass ratio). | 11/11 numerical checks PASS; analytic proofs in the paper. |
| [`muon_g_minus_2/`](muon_g_minus_2/) | Closed-branch negative check: the TGP substrate correction to the muon anomalous magnetic moment is $\|\Delta a_\mu\| \lesssim 10^{-12}$, three orders of magnitude below current experimental uncertainty. | Null result — channel closed as near-term falsification avenue. |
| [`thermal_transport_molecular/`](thermal_transport_molecular/) | Closed-branch negative check: TGP-specific correction to the Wiedemann-Franz ratio is $\mathcal{O}(10^{-4})$ at 300 K, 3–4 orders of magnitude smaller than observed bad-metal deviations (cleanly falsifying the hypothesis that TGP explains them). Also shows that TGP recovers the Cahill kinetic floor as a lower bound on thermal conductivity for soft perovskites. | Mixed: positive Cahill-floor recovery + clean bad-metal WF falsification. |
| [`casimir_mof/`](casimir_mof/) | Closed-branch negative check: the TGP correction to Casimir force in MOFs is $10^{-4}$ to $10^{-3}$, below current torsion-balance precision. | Null result — channel closed. |

## How to run

Each folder contains standalone Python scripts that run from the folder
root, e.g.:

```
cd continuum_limit
python cg_strong_numerical.py

cd ../metric_ansatz
python r4_einstein_self_consistency.py

cd ../muon_g_minus_2
python ps01_substrate_vertex_muon_g_minus_2.py
```

Dependencies: `numpy`, `scipy`, `matplotlib`.

## Relationship to the full workshop

The five folders here are a curated, paper-aligned subset. The broader
TGP research tree at https://github.com/Stefan13610/TGP includes:

- additional QM-foundations studies (Born rule, decoherence, measurement,
  spin, entanglement, superposition, statistics),
- cosmology channels (Hubble tension, DESI dark energy, S8 tension),
- additional sector-closure work (neutrino MSW, galaxy scaling, mass
  scaling, particle sector closure, UV completion),
- a long-form companion manuscript (`main.tex`) with the full set of
  appendices not reproduced here.

Those directories reflect work in progress and are not part of the
published record; they are provided for readers who want to see the
broader development of the theory.
