# Known issues

This file documents known gaps and retractions in the TGP core paper
(Zenodo DOI [10.5281/zenodo.19670324](https://doi.org/10.5281/zenodo.19670324)).
It is updated as issues are identified during internal review, so that
every claim in the paper has a traceable status.

## 2026-04-25 — external review: six critiques (C1–C6), disposition

External reviewer audit delivered 2026-04-25. Full response plan in
`TGP/TGP_v1/research/external_review_2026-04-25/review_response_plan.md`.
Priority-1 patches land in this commit; P2/P3 tracked as open work.

| # | Critique | Severity | Disposition |
|---|----------|----------|-------------|
| C1 | "Substrate stable at s=0 → no SSB" | — | **Reviewer misread**: axiom explicitly has `m₀² < 0` in ordered phase. But a **deeper v2-specific point is real**: GL gradient bond vanishes on uniform configurations, so SSB depends entirely on `m₀² < 0` axiomatically (no J-driven alternative as in v1). **Patched** via new remarks `rem:B-ssb-v2` (dodatek B) and `rem:GL-breaking-axiomatic` (sek01). Also corrected `v² = (Jz − m₀²)/λ₀` → `v² = |m₀²|/λ₀` in the v2 map (P1.1). |
| C2 | `U(φ) = β/3 φ³ − γ/4 φ⁴ → −∞` at large φ | Real presentation issue | **To be patched (P1.2)**: U(φ) is Taylor truncation of V_eff(Φ) around Φ₀, valid for `|φ−1| ≪ 1`. Full V_eff bounded below by bare `λ₀/4 Φ²`. Apparent unboundedness is truncation artefact. |
| C3 | "All 10 PPN = GR" overreach | Real | **To be patched (P1.3)**: restrict to `γ_PPN = β_PPN = 1` from static/isotropic/weak-field ansatz. Full 10-PPN requires OP-7 (moving matter + tensor sector). |
| C4 | `c_GW = c₀` overreach | Real, physically serious | **To be patched (P1.4)**: scalar-φ fluctuations on `g_eff` are luminal, but 2 tensor GR polarisations require OP-7. GW150914-class detections are NOT yet a closed TGP prediction. Potential falsification via LIGO/Virgo scalar-mode bounds (< few %). |
| C5 | α=2 pivot = "moving the goalposts" | Partly real | **To be patched (P1.5)**: α=2 is a *selection* within GL-substrate ansatz (conditions C1–C3), not a derivation from minimal bilinear substrate (latter falsified, see 2026-04-24 entry below). Paper text must reflect this at every α=2 assertion. |
| C6 | `p=1` defence mixes external and internal arguments | Minor | Folded into P1.5 commentary and M2c reality-check text. No separate patch. |

### Cross-connection: OP-2b and C5

Reviewer's C5 ("pivot moved physics from result to assumption") is
logically coupled to the user's conjecture that MK-RG in ŝ-variables
loses the composite-field Jacobian — both are cases where a
variable/axiom choice silently absorbs physical content that used to
be dynamical. Test A (MK-RG in Φ-variables,
`research/op1-op2-op4/mk_rg_phi.py`) is the minimal experiment.

### Open items after P1 batch

- **P2 Test A (OP-2b):** MK-RG in Φ-variables with explicit `ln Φ`
  tracking. ~~If μ-term is marginal/relevant at WF, `thm:beta-eq-gamma`
  is salvageable. If μ → irrelevant, OP-2b is fundamentally open.~~
  → **Completed 2026-04-25; see entry below.**
- **P3.1 Z_Φ in MK-RG:** wave-function renormalisation of composite.
  Now leading candidate for OP-2b after Test A negative.
- **P3.2 GL-bond operator in MK-RG:** bond flow, not just on-site.
  Now leading candidate for OP-2b after Test A negative.
- **P3.3 OP-7 (tensor sector):** 2 polarisations for GR-matching GW.
- **P3.4 NPRG:** last-resort cross-check; can verify P3.1+P3.2.

## 2026-04-25 — Test A (M4): H-S Jacobian does NOT close OP-2b

### Status

OP-2b stays **open**. The Hubbard–Stratonovich Jacobian `Φ^{-1/2}`
(translated to ŝ-variables as `μ ln(s²+ε²)` with `μ_HS = 1/2`) does
not close the M3 gap `B*/Γ* − 1/v*² ≈ -1.80`. The minimum
`|B*/Γ* − 1/v*²|` over the entire convergent regime
`μ ∈ [0, 0.45]` is **≈1.62** at `μ ≈ 0.32`, with **no sign change**
and trend reversing for `μ > 0.32`.

Reviewer C5's conjecture (concurrent with the user's diagnostic)
that "M3 missed the H-S Jacobian" is therefore experimentally
**falsified at the single-site MK-RG level**.

### Evidence

| Probe | File | Signal |
|---|---|---|
| Analytical setup | `TGP/TGP_v1/research/op1-op2-op4/M4_phi_variable_derivation.md` | μ exactly marginal under MK with bilinear bond (decimation, bond-move, bar-rescaling); μ labels FP families. Convergence boundary at μ=1/2. |
| Implementation | `TGP/TGP_v1/research/op1-op2-op4/mk_rg_phi.py` | Extension of `mk_rg_bgamma.py`; weight `(s²+ε²)^{-μ} exp(-V_poly)`. μ=0 reproduces M3 to 5 decimals. |
| μ-scan @ ε=0.10, N_ops=8 | `mk_rg_phi_results.txt` | `B*/Γ* ∈ [-0.84, -0.57]`, `1/v*² ∈ [+0.81, +1.23]`, both move but signs never align. |
| Cross-checks (ε ∈ {0.10, 0.05, 0.01}, N_ops ∈ {6, 8}) | same | min `|diff| ≈ 1.62 ± 0.02` robust across regulator and truncation. |
| Verdict & next-step list | `M4_results.md` | OP-2b **confirmed open** via §6 negative criterion; `Z_Φ`, GL-bond, NPRG promoted to leading candidates. |

### Implications

- **No paper edits.** P1.1 already left `thm:beta-eq-gamma-triple`
  Route 3 in the open-problem column; M4 narrows the candidate
  list but does not change the disposition.
- **Candidate ordering for OP-2b post-M4:**
  1. P3.1 — `Z_Φ` wave-function renormalisation of the composite
     field. Inserts anomalous dimension into β/γ flow.
     → **Tested 2026-04-25, see M5 below.**
  2. P3.2 — GL-bond operator promoted to a tracked coupling in
     MK-RG (highest expected impact, hardest to implement; the
     v2 GL bond is intrinsically two-site/momentum-dependent and
     not captured by single-site MK moments).
  3. P3.4 — NPRG (Wetterich) cross-check with `Z_Φ` + GL kinetic
     ansatz. Independent estimate from a different RG scheme.

## 2026-04-25 — Test B (M5): Z_Φ does NOT close OP-2b

### Status

OP-2b stays **open**. The wave-function renormalisation of the
composite field, modelled as an η-deformation of the MK bond
rescaling `K_eff(η) = b^{d-1+η} K`, does not close M3's gap
`B*/Γ* − 1/v*² ≈ -1.80`. Minimum `|diff| ≈ 1.694` at `η ≈ -0.55`,
no sign change anywhere in `η ∈ [-1, 2]` (full convergent regime).

The 3D Ising bootstrap value `η_Φ ≈ 2 η_φ ≈ 0.072` actually makes
the gap **slightly worse** (|diff| = 1.825 vs M3's 1.796).

### Evidence

| Probe | File | Signal |
|---|---|---|
| Analytical setup | `TGP/TGP_v1/research/op1-op2-op4/M5_zphi_derivation.md` | η enters through bond rescaling factor; analytic estimate of min |diff| ≈ 1.18 (achieved numerically at 1.694). |
| Implementation | `TGP/TGP_v1/research/op1-op2-op4/mk_rg_zphi.py` | One-line modification of `mk_rg_bgamma.py`'s K_eff. η=0 reproduces M3 to 5 decimals. |
| η-scan @ N_ops=8 | `mk_rg_zphi_results.txt` | `B*/Γ* ∈ [-1.05, -0.14]`, `1/v*² ∈ [+0.70, +4.63]`, both move smoothly but signs never align. |
| Bootstrap-η reading | same | At η=0.07: B*/Γ* = -0.5435, 1/v*² = +1.281, diff = -1.825 (worse than M3 by 1.6%). |
| Verdict | `M5_results.md` | OP-2b **confirmed open** also under η-deformation; GL-bond (P3.2) is the SOLE remaining single-channel candidate. |

### Implications

- **No paper edits.** P1.1's disposition stands unchanged.
- **Candidate ordering for OP-2b post-M4+M5:**
  1. ~~P3.1 — `Z_Φ`~~ ruled out by M5 within natural η range.
  2. **P3.2 — GL-bond operator** in MK-RG. Now the **sole**
     remaining single-channel candidate. The v2 axiom-level GL
     bond is intrinsically non-local (2-site, momentum-dependent)
     and is qualitatively different from the on-site / field-
     strength sectors that M4+M5 exhausted.
  3. P3.4 — NPRG (Wetterich) cross-check with full GL kinetic
     ansatz; can also test combined `Z_Φ + GL bond`.

The deeper analytical reason `Z_Φ` alone fails: the η-deformation
shifts `B*/Γ*` and `1/v*²` by similar magnitudes in **opposite**
directions, so the gap |diff| is bounded below by ~1.6 even at
the optimum |η| ≈ 0.5. See `M5_results.md` §5 for the analytic
estimate and §6 for the comparison table with M4.

## 2026-04-24 — OP-6 closed via axiom pivot (v2 change)

### Status

OP-6 ("rigorous continuum limit of H_Γ, specifically the derivation
of `K(φ) ∝ φ⁴` from v1's bilinear-bond H_Γ") is **closed**. The
outcome is **negative for the v1 derivation path** and is resolved
by a **pivot at the axiom level** (M1-A′) for v2.

### Evidence that rules out the v1 derivation

Three independent lines of investigation were completed in
`TGP/TGP_v1/research/op6/` between 2026-04-22 and 2026-04-24:

| Probe | File | Signal |
|---|---|---|
| M2-a: analytical (standard RG mechanisms) | `M2a_analytical_sketch.md` | All four mechanisms (LPA, LPA' with Z_k(ρ), derivative expansion, extended operator basis) fail to produce K(φ)∝φ⁴ from the v1 bilinear H_Γ. |
| M2-b: 1D envelope-RG MC of v1 H_Γ | `M2b_results.md` | Measured `K_eff(⟨Φ⟩) ∝ ⟨Φ⟩^(-0.28 ± 0.43)`. TGP target p=+1 rejected at 3σ. |
| M2-c: reality-check on the pivot target | `M2c_H3_reality_check.md` | Identifies that the GL functional H_GL (not the bilinear H₃) is the object that actually gives α=2; numerically confirmed at 5.5σ. |
| M3-a: 1D block-RG of v1 H_Γ, 4 octaves | `M3a_results.md` | `p_B = -0.52 ± 0.28` uniformly across B ∈ {1,2,4,8,16}. TGP target p=+1 rejected at **5.5σ** at every block size; `C_B ∝ 1/B` confirms block-RG is genuine. |
| M3-c: scaling dimensions at 3D Ising WF | `M3c_scaling_dimensions.md` | Using conformal-bootstrap Δ_ε = 1.413, ratio `K^{(1)}/K^{(0)} ~ k^{1.41} → 0` in the IR. `K_*(φ) → const`, not `K_*(φ) ∝ φ`. Also rules out tricritical / higher-derivative / O(N) / long-range / two-field / gauged-Z₂ minimal extensions. |

**Bottom line:** the v1 claim that MK coarse-graining of the bilinear
bond of H_Γ generates the GL coupling `K_ij = J(φ_iφ_j)²` is
numerically and analytically excluded. The M1–M5 programme announced
in the previous entry (below) does not close on the original plan.

### Resolution: pivot at the axiom level (M1-A′)

The substrate Hamiltonian in `eq:H-Gamma` of the paper has been
changed from the v1 bilinear bond to a Ginzburg–Landau gradient bond
in the Z₂-even composite `Φ_i = ŝ_i²`:

    v1:  H_Γ = Σ [...on-site...] − J Σ_⟨ij⟩ A_ij ŝ_i ŝ_j

    v2:  H_Γ = Σ [...on-site...] + J Σ_⟨ij⟩ A_ij ŝ_i² ŝ_j² (ŝ_j² − ŝ_i²)²

**Preserved from v1:**

- Microscopic Z₂-odd amplitude ŝ_i (ontological chain
  "nothingness + Z₂ → matter" unchanged).
- On-site structure (π²/2μ, m₀², λ₀).
- All four axioms (ax:N0, ax:substrate, ax:source, ax:P3).
- Prop `prop:substrate-action` in dodatekB (already used H_GL form
  since 2026-03-24).
- Theorem `thm:alpha2` in Sec. 4 (its proof is axiom-independent).
- The three-level ontology (Γ → Φ → g_μν).

**What changes in v2:**

- The bond is now GL-in-φ rather than bilinear-in-ŝ. Physical
  content: empty substrate (ŝ=0) supports no geometric bond, so
  "no substrate ⇒ no geometry" becomes a property of the axiom
  rather than a derived consequence.
- α=2 is now a direct algebraic consequence of the axiom via
  Prop `prop:substrate-action`, not an open derivation problem.
- `thm:alpha2` retains its meaning as an independent uniqueness
  statement: among all local Φ-covariant kinetic operators, the GL
  form is the unique choice satisfying (C1)–(C3). In v2 this is a
  consistency check of the axiom; in v1 it was the *only* supplier
  of α=2.
- The Migdal–Kadanoff coarse-graining remark in the substrate-to-
  field section is restated as: the continuum of the v2 bond is
  directly the GL functional (Prop. `prop:substrate-action`).

### Impact

- **v1 (Zenodo DOI 10.5281/zenodo.19670324):** unchanged. The v1
  release remains on Zenodo with its original axiom. This file is
  the authoritative note of its OP-6 status (now resolved by pivot
  rather than by derivation).
- **v2:** in preparation. All source files in `tgp-core-paper/` have
  been updated to use the GL bond as axiom. A v2 release to Zenodo
  will be made once the companion-paper impact is audited and the
  full v2 diff is cross-checked.
- **Companion papers:** impact audit pending. The v2 axiom is a
  refinement at the bond level; none of the companion papers
  (tgp-qm, tgp-leptons, tgp-sc) use the specific form of the bond,
  only the coarse-grained φ dynamics (which is unchanged).
- **Scripts:** `a1_alpha2_frg_synthesis.py` remains WITHDRAWN
  (previous entry still applies). `cg_strong_numerical.py` still
  legitimate. New OP-6 scripts (`m2b_envelope_stiffness_1d.py`,
  `m3a_block_rg_1d.py`) are the authoritative numerical record.

### Why this is not "moving the goalposts"

The v1 theorem `thm:alpha2` was always a *classification* result
(uniqueness inside (C1)–(C3)), never a derivation from H_Γ. The
open item in v1 was the derivation of (C1)–(C3) from the bilinear
H_Γ; three independent probes now rule this out. A substrate
Hamiltonian that *does* supply (C1)–(C3) exists — the GL bond —
and has been the working target in `prop:substrate-action` since
2026-03-24. The pivot simply states this explicitly at the axiom
level and makes the chain of inferences traceable end-to-end.

---

## 2026-04 — Withdrawal of the "α = 2 from H_Γ" numerical synthesis

### Scope

The following claims in earlier versions of the paper are **withdrawn**
pending a complete derivation:

- Table of numerical results, row 16: *"FRG fixed point α = 2,
  |α\* − 2| < 10⁻³"* (earlier phrasing).
- Table of numerical results, row 21: *"Block-spin Monte Carlo and
  FRG LPA' on a 1D substrate chain show K_IR/K_UV = 1.000 at the
  α = 2 fixed point (8/8 PASS)"* (earlier phrasing).
- Script `research/continuum_limit/a1_alpha2_frg_synthesis.py` and its
  companion `dodatekQ2` lemmata chain (A1–A5) as a closure of the
  "weak α = 2 theorem".

### What is retained

- **Theorem `thm:alpha2`** in Sec. 4 of the core paper — the
  classification result *"within axioms (C1)–(C3), K(φ) = φ⁴ is the
  unique kinetic operator and α = 2"* — stands as stated. It is an
  axiomatic classification theorem, not a derivation from H_Γ.
- **Row 16** is retained in a narrower form: FRG LPA' at the
  Wilson–Fisher fixed point preserves the kinetic structure
  K(ρ) ∝ ρ with η\* ≈ 0.044. This is a continuum-level statement
  and does not extract α from H_Γ.
- **Row 21** is retained as a numerical exploration
  (`cg_strong_numerical.py`) of block-averaging on a 1D chain,
  consistent with a non-trivial fixed point but not determining α.
- **OP-6** remains open as stated.

### Nature of the issue

Reading of `a1_alpha2_frg_synthesis.py` (lines 540–640) shows the
author deriving K₁(Φ) = Z₀/(4·Φ) from the change of variables
Φ = φ² and concluding that this gives α_K = 0 in the
g = √(Φ/Φ₀) variable, contradicting the value α = 2 used
throughout the soliton code (`f_kin(g) = 1 + 2α·ln g`). The
script then comments:

> I think I'm going down a rabbit hole. The key point is: alpha = 2
> IS established (both in the theory and verified numerically) and
> Lemma A3 provides the algebraic justification. The EXACT mechanism
> (power law vs log) involves subtle convention issues that are
> already resolved in the formal theory (sek08 + dodatekQ2).

and proceeds with the seven test cases on that assertion. On review:

1. The derivation of the log-form kinetic term
   f_kin(g) = 1 + 2α · ln g from H_Γ is not completed inside this
   script, nor in `dodatekQ_coarse_graining_formal.tex`, nor in
   `dodatekQ2_most_gamma_phi_lematy.tex`. The reference chain is
   circular: the script defers to `dodatekQ2`, which in turn treats
   α = 2 as following "algebraically" from the variable change,
   which in the script gives α = 0.
2. The tests T3–T7 that run after the `# CONTRADICTION!` comment
   consist of: T3 a tautology (ODE with α = 2 differs from ODE with
   α = 0); T4 a restatement of CG-2 FRG results from a different
   script; T5 an algebraic identity 1/Φ₀ · Φ₀ = 1; T6 an MC reading
   α = 6.48 ± 3.82 (error bar covers α ∈ [−1, 14]); T7 a table of
   claims rather than a test.
3. Therefore the "8/8 PASS" aggregate is performative: it does not
   establish α = 2 from H_Γ.

### What we are doing about it

- The core paper text has been corrected to reflect the actual
  scope of the numerical results (this commit).
- The script `a1_alpha2_frg_synthesis.py` is kept in the repository
  for transparency, with a WITHDRAWN banner added at the top.
- A fresh attempt at OP-6 is tracked as milestones M1–M5 in the
  development repository [Stefan13610/TGP](https://github.com/Stefan13610/TGP):
  - M1: explicit H_Γ (Hilbert space, couplings, symmetries,
    order parameter) consolidated in a single document.
  - M2: clean derivation of K₁(Φ) from H_Γ — resolving the
    power-law vs logarithmic form and the sign of α.
  - M3: numerical FRG in LPA' for 1D H_Γ, measuring α directly
    (not imposing it) and the anomalous dimension η.
  - M4: effective action for Φ from expansion around the fixed
    point.
  - M5: Γ-convergence (or Banach contraction) in a simplified
    model.
- If M1–M5 succeed, a revised version 2 of the core paper will
  be released with α = 2 derived from H_Γ. The current version
  (v1) remains on Zenodo; this note is the authoritative record
  of its known issues.

### Impact on companion papers

Audited independently:

- `tgp-qm-paper` (emergent QM) — independent of A1–A5; no change
  required.
- `tgp-leptons-paper` (charged leptons / Koide / Cabibbo) —
  independent of A1–A5; no change required.
- `tgp-sc-paper` (superconductivity) — independent of A1–A5; no
  change required (separate review of that paper is in progress
  for unrelated issues).

## Reporting new issues

Please open an issue at
https://github.com/Stefan13610/tgp-core-paper/issues, or email the
author. Issues listed here are tracked against concrete corrections
in the paper source.
