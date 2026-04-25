# Known issues

This file documents known gaps and retractions in the TGP core paper
(Zenodo DOI [10.5281/zenodo.19670324](https://doi.org/10.5281/zenodo.19670324)).
It is updated as issues are identified during internal review, so that
every claim in the paper has a traceable status.

## 2026-04-25 — M9.1 (statyka + PPN): pure power-form metric falsified by β_PPN

### Status

**TGP gravity sector with metric `g_tt = -c²/φ`, `g_rr = φ` and full
nonlinear Φ-EOM is falsified at the post-Newtonian level.** Numerical
solution of the Φ-EOM for a static spherical source produces an
asymptotic expansion `ε(r) = a₁/r + a₂/r² + a₃/r³ + ...` with
`c₂ := a₂/a₁² = -0.992 ± 0.005` (analytic limit `-1` exactly), giving
**β_PPN = 2(1 − c₂) = 3.98 ± 0.01**. Observation: β_PPN = 1.000 ±
1·10⁻⁴ (Mercury, Cassini, LLR). Deviation `~3·10⁴` σ.

OP-2b therefore remains **open**, but the path forward is no longer a
purely numerical RG cross-check (closed by M3–M8 at scheme-independent
level) — instead it is a structural question about the **metric ansatz
itself** versus the substrate.

### Evidence

| Probe | File | Signal |
|---|---|---|
| Foundational ontology | `TGP/TGP_v1/TGP_FOUNDATIONS.md` | Single-Φ Z₂ substrate immovable; gravity = collective fluctuation effect (Sakharov / Verlinde / Volovik tradition); GR target = numerical analog "in the limit", not analytic isomorphism. |
| Analytical setup | `TGP/TGP_v1/research/op-newton-momentum/M9_1_setup.md` | Φ-EOM linearization → γ_PPN = 1 (exact, by metric ansatz); β_PPN = 2 in linear power form, β_PPN = 1 in exponential reparametrization; whether full nonlinear Φ-EOM dynamically picks one is THE question. |
| Numerical solver | `TGP/TGP_v1/research/op-newton-momentum/m9_1_static.py` | scipy.solve_bvp on Φ-EOM with v(r)=r·ε(r) substitution; tests T1–T5. |
| Convergence study | `TGP/TGP_v1/research/op-newton-momentum/debug_rmax.py` | c₂ vs R_max: 100→-0.71, 200→-0.87, 400→-0.97, 800→-0.992 (analytic -1.000). |
| Pipeline sanity | `TGP/TGP_v1/research/op-newton-momentum/debug_t3.py` | Same fit pipeline on linearized solver gives \|a₂\| ~ 10⁻¹¹ (clean noise floor). |
| Verdict | `TGP/TGP_v1/research/op-newton-momentum/M9_1_results.md` | T1, T2, T4, T5 PASS; T3 FAIL (β_PPN ≈ 4 vs observed 1, ~3·10⁴ σ). |

### Implications

1. **Cannot improve via tighter numerics.** Analytic asymptotic series
   is exact; numerical c₂ converges to -1 to 1% at R_max=800. The
   prediction β_PPN = 4 is a structural feature of TGP in its current
   formulation, not a calculational artefact.
2. **OP-2b path forward (M9.1′ — metric ansatz audit).** Three options
   without breaking single-Φ Z₂ substrate:
   - (a) Alternative metric reparametrization: e.g., `g_tt = -c²·exp(-η)`,
     `g_rr = exp(+η)`. Compatible with `f·h = 1` substrate budget but
     requires η ≠ ε; needs derivation from substrate.
   - (b) Matter back-reaction: stress-energy of matter modifies Φ-EOM
     at higher order. Not yet axiomatized in TGP.
   - (c) M9.2 (momentum / Lenz back-reaction) might inform: if inertia
     forces a different metric structure, c₂ may shift.
3. **Cycle M9.2 and M9.3 are gated by M9.1′.** Without GR-compatible
   statics, momentum (M9.2) and GW radiation (M9.3) tests of TGP
   gravity are premature.
4. **Substrate is NOT renegotiated.** Per `TGP_FOUNDATIONS.md` §1.2 +
   §5: TGP = single fundamental scalar Z₂ + gravity-as-collective-
   fluctuation. Multi-component substrate or fundamental graviton
   would constitute a different theory.

### Cross-connection to M3–M8

M3–M8 closed the FP-universality question (β/γ < 0 at WF FP, scheme-
independent under NPRG cross-check). M9.1 closes the broken-phase
classical PPN question (β_PPN = 4, falsified). Both negative at the
mathematical level **for current TGP formulation**, both leave room
within the ontology (single Z₂ scalar + emergent gravity) for
structural revisions of the metric/source coupling.

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
  ~~Now leading candidate for OP-2b after Test A negative.~~
  → **Completed 2026-04-25 as M5; see entry below. NEGATIVE.**
- **P3.2 GL-bond operator in MK-RG:** bond flow, not just on-site.
  ~~Now leading candidate for OP-2b after Test A negative.~~
  → **Completed 2026-04-25 as M6 (Track A) + M7 (Track B); see entries
  below. M6 closure-in-principle at unphysical J_GL ≈ 5.89; M7 shows
  J_GL is strongly irrelevant at the M3 FP. NEGATIVE.**
- **P3.3 OP-7 (tensor sector):** 2 polarisations for GR-matching GW.
  Now the only remaining structural path for restoring β = γ at
  criticality after M3–M8.
- **P3.4 NPRG:** last-resort cross-check.
  → **Completed 2026-04-25 as M8; see entry below. CONFIRMS M3–M7
  verdict at scheme-independent level (β/γ at FP minimum is
  universally negative).**

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

## 2026-04-25 — Test C (M6): GL bond closes OP-2b *in principle*, outside the perturbative regime

> **Update 2026-04-25 (post-M7):** M6's closure-in-principle is
> **resolved in the negative** by the M7 eigenvalue test (entry
> below). The crossing at `J_GL ≈ +5.89` is **not** realised under
> proper RG flow: J_GL is strongly irrelevant at the M3 fixed
> point (|λ_GL| ≈ 0.07 ≪ 1). M6 below preserved as historical
> record of the candidate-screening sequence.

### Status

OP-2b status moves from **open** to **closure-in-principle**. The v2
axiom-level GL bond
`H_GL = J_GL · Σ A_ij Φ_i Φ_j (Φ_j − Φ_i)²`,
treated as a first-order perturbation of M3's bilinear bond on the
on-site `V'(s)` update (Track A), drives M3's gap
`diff = B*/Γ* − 1/v*²` monotonically through zero at
**`J_GL_* ≈ +5.89`**. This is the **first** of the three
single-channel candidates (after H-S Jacobian and Z_Φ both failed)
that produces a sign change in `diff` at all.

However, the crossing is **outside the perturbative regime**. At
`|J_GL| ≲ 1` Track A's first-order truncation is justified, and the
GL bond closes only ~9 % of the M3 gap. Reaching closure requires
`|J_GL| ~ 6`, where the per-step GL correction is comparable to the
M3 polynomial sector itself — Track A's `O(J_GL)` truncation
quantitatively breaks down.

### Evidence

| Probe | File | Signal |
|---|---|---|
| Analytical setup | `TGP/TGP_v1/research/op1-op2-op4/M6_glbond_derivation.md` | Track A: GL bond → on-site `ΔV(s)` via `−J_GL ⟨bond_12⟩(K_eff·s)` at `s_3=0` projection. Decision criteria. |
| Implementation | `TGP/TGP_v1/research/op1-op2-op4/mk_rg_glbond.py` | Extension of `mk_rg_bgamma.py`. Computes `M_n(K_eff·s)` at outer s grid via inner s_2 quadrature, projects `ΔF` onto even-power basis up to `s^{2 N_ops}`. `J_GL=0` reproduces M3 to 5 decimals. |
| J_GL coarse scan | `mk_rg_glbond_results.txt` | `J_GL ∈ [-2, 10]` step 0.25; `B*/Γ*` climbs from -0.85 (J=-2) through -0.57 (J=0) and 0 (J≈2.7) to +4.5 (J=10); `1/v*²` mildly increases from +1.18 to +1.44 over the same range. |
| Crossing | same | Sign change of `diff` in `J_GL ∈ [+5.85, +5.90]`, linear interp **`J_GL_* = +5.8933`**, min |diff| = 0.0039 at `J_GL = 5.90`. |
| Perturbative-regime closure | same | At `J_GL = 1`, |diff| = 1.640 (closes 9 % of the M3 gap); at `J_GL = 0.5`, |diff| = 1.722 (4 % closed). Linear extrapolation in J_GL within Track A's domain of validity does NOT reach zero. |
| Verdict | `M6_results.md` | **CLOSURE-IN-PRINCIPLE only** (M6 §6 criterion 2). GL bond is the unique mechanism among {H-S, Z_Φ, GL} that drives `diff` through zero, but the value at which it does so is outside Track A's perturbative regime. |

### Implications

- **No paper edits yet.** OP-2b status in v2 paper remains "open"
  pending non-perturbative confirmation. A possible future v3 patch
  could move OP-2b to "closure-in-principle, awaiting NPRG" if Track B
  or NPRG corroborate.
- **Candidate ordering after M4+M5+M6:**
  1. ~~P3.1 — `Z_Φ`~~ ruled out by M5.
  2. P3.2 — GL bond, **closure-in-principle** at `J_GL ≈ 5.89`,
     outside perturbative regime. Strongest single-channel candidate.
  3. P3.2-Track-B — `J_GL` flowing alongside `(r,u,B,Γ,…)` under MK,
     including operator-mixing `O(J_GL²)` contributions. Promoted to
     next step.
  4. P3.4 — NPRG (Wetterich) with full Z_Φ + GL kinetic ansatz.
     Resolves the perturbative-regime ambiguity at all orders.

### Why this is qualitatively different from M4 / M5

M4 and M5 each ruled their channel OUT: the relevant deformation
parameter (`μ` for H-S, `η` for Z_Φ) failed to close the gap
*at any value*. M6 is the opposite: the gap *does* close, just
not safely within Track A's domain.

The physical direction is correct: positive `J_GL` (gradient bond
favouring smooth `Φ`-configurations) pushes `B/Γ` toward the
`v² = β/γ` Lorentz-locking value, exactly as expected for the
mechanism that produces local Lorentz invariance from coarse-graining.

## 2026-04-25 — M7 (Track-B sketch): J_GL is **strongly irrelevant** at the M3 FP — M6 closure-in-principle does NOT lift

### Status

OP-2b returns to **OPEN at the level of single-channel single-site
MK-RG**. M7 computes the J_GL eigenvalue under one MK step
linearised at the 3D Ising WF fixed point (the M3 FP), addressing
M6's central caveat. Result:

```
|λ_GL| ≈ 0.07     (L² norm projection onto O_GL, robust across
                   n_outer ∈ {20,30,40,50}, n_max ∈ {8,12,16})
```

**Strongly irrelevant** (|λ_GL| ≪ 0.5 in all sub-extractions). Bare
J_GL decays by a factor of ~14 per MK step at the M3 FP. M6's
closure at `J_GL ≈ +5.89` is therefore **not** realised under
proper RG flow: any small bare J_GL flows to zero in the IR
before reaching the closure value.

This **resolves M6's central caveat** ("Track A's first-order
J_GL truncation is not trustworthy near the crossing") in the
negative direction: the crossing exists in Track A but is washed
out under proper RG flow. The GL bond, treated as an MK-flow
operator at the M3 FP, **cannot** close OP-2b.

### Evidence

| Probe | File | Signal |
|---|---|---|
| Analytical setup | `TGP/TGP_v1/research/op1-op2-op4/M7_glbond_eigenvalue.md` | λ_GL = ∂J_GL_post_bar / ∂J_GL_pre_bar at (cb_M3*, J_GL=0). Uses 2D F(s_1, s_3) extraction; first-order linear response = `dF/dJ_GL_pre = -4·⟨bond_12 + bond_23⟩(s_1,s_3)`. Multiple decision criteria (relevant / irrelevant / strongly irrelevant). |
| Implementation | `TGP/TGP_v1/research/op1-op2-op4/mk_rg_glbond_eig.py` | Vectorised inner s_2 quadrature (n_quad=1200) over 2D outer (s_1, s_3) grid; three independent eigenvalue extractions (monomial-basis lstsq, L² norm projection onto O_GL, finite-difference numerical perturbation); robustness scan over n_outer × n_max. |
| Numerical result | `mk_rg_glbond_eig_results.txt` | M3 FP reproduced to 5 decimals. Bilateral symmetry to 1e-8. **L² projection: λ_GL_norm = +0.0704** (stable to 4 digits across all robustness configs). Monomial (2,6) extraction: 0.028–0.094 (basis-dependent). Canonical baseline: 4/K_new⁴ = 0.0048. |
| Operator-mixing diagnostic | same | Shape ratio c(4,4)/c(2,6): expected −2 for pure GL; numerical −2.08 (n_max=16, n_outer=50) → −3.5 (n_max=12). Sub-leading mixing into "(s_1+s_3)^8 cross" operator; mixing-corrected eigenvalue still ≪ 1. |
| Verdict | `M7_results.md` | OP-2b **back to open**. M6's closure-in-principle resolved in the negative. All three single-channel candidates (H-S, Z_Φ, GL) now exhausted at the level of single-site MK-RG. |

### Implications

- **No paper edits.** M7 confirms the v2 paper's "OP-2b open"
  disposition. The flirt with closure-in-principle (M6) does not
  survive proper RG flow.
- **All three single-channel candidates from M3 §6 are exhausted**:
  - M4: H-S Jacobian — bounded |diff| ≥ 1.62 above zero (no closure).
  - M5: Z_Φ via η-deformation — bounded |diff| ≥ 1.69 above zero.
  - M6+M7: GL bond — closure exists in Track A at unphysical
    J_GL ≈ 5.89, but J_GL is strongly irrelevant under proper RG flow.
- **Candidate ordering after M3+M4+M5+M6+M7:**
  1. **P3.4 — NPRG (Wetterich)** with full Z_Φ + GL kinetic
     ansatz. Promoted to leading remaining test. Resolves
     ambiguities of single-site MK-RG at all orders.
  2. Full operator-basis Jacobian at the extended FP (P3.2-Track-B
     extended). Tests whether off-diagonal mixing among irrelevant
     bond operators produces a relevant *eigenvector* of the full
     operator-space Jacobian (a relevant direction not aligned with
     any single channel).
  3. Document OP-2b as a **genuine open problem** of single-site
     MK-RG; closure requires NPRG-level treatment.

### What this proves and what it does not

**Proves:** The diagonal projection of the J_GL response at the M3
FP is strongly irrelevant. M6's Track-A closure is not realised
under proper RG flow.

**Does not prove:** That J_GL is irrelevant at *every* fixed point
of the extended flow (a different non-WF FP could host a relevant
J_GL); that off-diagonal mixing in the full operator basis cannot
produce a relevant eigenvector with non-trivial GL component;
that single-site MK-RG is the right framework (NPRG is the
gold-standard cross-check).

## 2026-04-25 — M8 (NPRG/Wetterich, P3.4): non-perturbative cross-check **CONFIRMS** M3–M7 verdict on OP-2b

### Status

OP-2b is **CONFIRMED OPEN** at the level of single-component scalar
Z₂ field theory. The non-perturbative gold-standard cross-check
(Wetterich exact RG in LPA with Litim regulator, polynomial
truncation around `ρ̃ = 0`) reproduces the 3D Ising Wilson–Fisher
fixed point with literature precision and yields a **same-sign**
result on the scheme-independent observable `β/γ` evaluated at the
FP minimum:

```
ν_LPA(N=10) = 0.6492        (literature: 0.6496, agreement to 0.05%)
β/γ at FP minimum (NPRG):    -0.326
β/γ at FP minimum (MK-RG):   -0.444   (same formula, evaluated at MK FP)
```

Both schemes give `β/γ < 0`, confirming that the OP-2b gap is a
**universality-class feature of 3D single-component scalar Z₂
field theory**, not an artefact of the Migdal–Kadanoff scheme. All
five investigations (M3, M4, M5, M6, M7) and the non-perturbative
cross-check (M8) now agree at the scheme-independent level.

A subtle but important second finding: the **polynomial-coefficient
ratio** `B*/Γ* = (3/2)(a_3/a_4)` taken literally as the "same"
observable across schemes has **opposite signs** in NPRG and MK-RG
(NPRG: `+0.367` at N=10, MK-RG: `−0.5687`). This is a scheme
convention difference (Taylor expansion at `ρ̃ = 0` vs. derivatives
at the FP minimum), not a physical disagreement. Quantities of the
form `β/γ` should be read at the FP minimum, where they are
LPA-invariant; polynomial-coefficient ratios at `ρ̃ = 0` mix
short-distance shape information with vacuum-point physics.

### Evidence

| Probe | File | Signal |
|---|---|---|
| Analytical setup | `TGP/TGP_v1/research/op1-op2-op4/M8_NPRG_setup.md` | LPA flow eq. for Litim regulator in d=3, polynomial truncation around `ρ̃=0`, FP equations (3-k)·a_k = c·[1/(1+m²)]_k, mapping to MK-RG (a_3/a_4 = (2/3)(B/Γ)), validation gate ν ∈ [0.55, 0.70], decision matrix on `a_3/a_4`. |
| Implementation | `TGP/TGP_v1/research/op1-op2-op4/nprg_lpa_3d.py` | Polynomial-truncation FP solver via fsolve; structured grid of initial guesses (MK-RG-inspired alternating signs + 20 random fallbacks); WF validation (residual < 1e-6, exactly 1 positive eigenvalue, ν gate). Scheme-independent β/γ at FP minimum via brentq for `v'_*(ρ̃_0) = 0` plus chain-rule on derivatives. |
| Numerical result | `nprg_lpa_3d_results.txt` | N=2 analytic seed reproduced (a₁ = -1/13, ν = 0.5427). WF FP found at N = 4, 5, 6, 7, 8, 10 (unique distinct a₃/a₄ at each N). N=10: a₁ = -0.1859, a₂ = +2.4322, a₃ = +11.08, a₄ = +45.26, ν = 0.6492. N ≥ 12: no WF root (small radius of convergence around ρ̃=0). β/γ at ρ̃₀ = 0.0306: NPRG -0.326, MK -0.444 (both negative). |
| Verdict | `M8_results.md` | Two-level analysis: (i) polynomial ratio is scheme-dependent and flips sign across schemes; (ii) scheme-independent `β/γ` at FP minimum has same sign in both schemes. OP-2b confirmed open at universality-class level. |

### Implications

- **No paper edits beyond what was already in place.** The v2 paper
  already lists OP-2b as open after M3-M7; M8 confirms this
  disposition at the non-perturbative level. The result strengthens
  rather than changes the v2 disposition.
- **`thm:beta-eq-gamma-triple` is genuinely unrescuable at the level
  of single-component scalar Z₂ field theory.** All four channels
  considered (bilinear bond, H-S Jacobian, Z_Φ, GL bond) plus the
  non-perturbative gold-standard treatment fail to produce `β = γ`
  at the WF FP. Closure requires multi-component physics (tensor
  sector / OP-7), composite-operator mixing beyond LPA, or a
  fundamentally different substrate ansatz.
- **Subtle pedagogical point on observable choice:** quantities
  reported as "ratios of polynomial coefficients at the origin"
  should be replaced by "ratios of derivatives at the FP minimum"
  whenever cross-scheme comparison is intended. M3-M7 implicitly
  used the former; the M8 cross-check shows that the latter is the
  correct invariant. Future M-series tests should use the FP-minimum
  observable directly.
- **Candidate ordering after M3-M8:**
  1. **OP-7 (tensor sector, P3.3)** — only remaining structural path
     for restoring `β = γ` at criticality, via multi-component or
     tensor-mediated mechanism. This is the natural next investment.
  2. Full operator-basis Jacobian at the extended FP (P3.2-Track-B
     extended) — would search for relevant eigenvectors not aligned
     with any single channel, but is now lower-priority since M8
     already confirms the universality-class verdict at the
     non-perturbative level.
  3. LPA' (anomalous-dimension `η` flow) and broken-phase
     polynomial expansion as quantitative refinements (M9 if
     percent-level accuracy on β/γ is wanted).

### What this proves and what it does not

**Proves:** The Wetterich LPA with Litim regulator at d=3 has a WF
FP with literature-matching `ν`, and at that FP the
scheme-independent observable `β/γ` is negative, agreeing in sign
with MK-RG. The OP-2b gap is a feature of 3D Ising universality at
single-component scalar level, not of the MK scheme.

**Does not prove:** That the result holds beyond LPA (`η ≠ 0`
corrections); that it holds in multi-component / tensor extensions
(OP-7); that the polynomial truncation around `ρ̃ = 0` would extend
to N ≥ 12 (it does not, due to radius-of-convergence issues — but
N = 10 already locks in `ν` to four significant digits). The
Litim regulator was the only one tested; regulator-independence at
LPA level is expected for sign-of-`β/γ`-at-FP-minimum but was not
explicitly verified.

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
