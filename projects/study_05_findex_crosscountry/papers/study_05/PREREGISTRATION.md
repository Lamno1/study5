# Study 5 — Preregistration (FROZEN 2026-09-09, REVISION 1 + REVISION 2)

**REVISION 1 (2026-09-09, pre-estimation)** per `audit/CODEX_S5_STAGE0_REVIEW.md` §9 and
`REVISION_1_RESPONSE.md`. Changes: weights corrected (§2); primary controls reduced and
`internet_use`/`emp_in` moved to robustness (§3); moderator renamed `lowcov2019_*` and
re-described as *2019 credit-information coverage*; two-way clustering removed (§3 M6);
one multiplicity procedure fixed to BH (§5); FE logit/probit + M2c joint test + weighted
within-R2 specified (§3, §9-notes); "developing/emerging" population language removed.

**REVISION 2 (2026-09-09, pre-estimation)** per `audit/CODEX_S5_PREBUILD_SEMANTIC_BLOCK.md`
and `REVISION_2_RESPONSE.md`. Only change: M4 secondary outcome `emergency_formal` ->
`emergency_loan_source` (M4 bullet + §5 BH family entries 3 & 4); `fin24 == 4` bundles
financial-institution, employer and private-lender loans and is not a formal-credit outcome;
code 9 (Refused) added to its drop rule. BH family size (9) and order unchanged.

**No estimation has been run.**

`H-000500` · `EXP-S5-001` · descriptive, **non-causal**. No specification outside this
document is confirmatory; anything extra is labelled exploratory.

Companion: `CLAIM_CONTRACT.md`, `VARIABLE_CONTRACT.md`, `REVISION_1_RESPONSE.md`,
`../../data/STUDY_05_RAW_MANIFEST.json`, `../../audit/STUDY_05_DISCOVERY_AND_DATA_AUDIT_2026-09-09.md`.

---

## 0. Population

The analysis population is **the economies where the 2024 Global Findex borrowing /
digital-payment module was administered and complete primary covariates are available**
(~ 97 economies; 6 are `High income` by `regionwb` and are retained). No "developing" or
"emerging" label is used.

## 1. Data build (deterministic)

1. Read `F` and `W` at the frozen hashes.
2. Construct every variable exactly per `VARIABLE_CONTRACT.md` (incl. the `receive_dig` /
   `make_dig` truth tables).
3. Left-join `W` onto `F` by `iso3`.
4. Apply the frozen estimation-sample filter; write the **drop table** (rows after each
   filter; economies exited and why).
5. Compute `lowcov2019_z`, `lowcov2019_bmedian`, `lowbureau2019_z`, `lowregistry2019_z`,
   `lowdepth2019_z`, `lowrights2019_z` **on the final estimation economies only** (one value
   per economy, unweighted at the economy level).
6. Compute `acct_own_rate` per economy (`w_equal`-weighted mean of `account_fin`).
7. Freeze the analysis dataset; hash it (in the run receipt).

## 2. Weighting (frozen)

```
w_equal_i      = wgt_i / sum_{j in economy(i)}(wgt_j)     # PRIMARY
w_population_i  = w_equal_i * pop_adult_c                  # robustness
w_unweighted_i  = 1                                        # robustness
```
A global rescaling constant is allowed. **Primary = `w_equal`.** Estimand: the average
economy-specific (within-economy) association, economies weighted equally.

## 3. Specifications

Weighted LPM (OLS on 0/1) with **economy fixed effects `d_c`** and **standard errors
clustered by economy**. For every headline coefficient report: point estimate (pp),
cluster-robust SE, wild-cluster-bootstrap p (Rademacher, 999, fixed seed), 95% CI, N
individuals, N economies, weighted within-R2 (defined below).

**Primary controls `X` (frozen):** `account_fin`, `female_d`, `age_c`, `age_c2`, `C(educ)`,
`C(inc_q)`, `urban_d`.

**Weighted within-R2 (one definition, every LPM):** weighted-Frisch-Waugh partial out `d_c`
and the weighted intercept from `y` and each regressor; then
`within_R2 = 1 - weighted_SSR(residualised full model) / weighted_TSS(residualised y)`.

### M1 — Primary association
`formal_borrow = b1*anydigpayment + b2*account_fin + X + d_c`  ·  weight `w_equal`.
Report `b1` (claim C1).

### M2 — Moderation (the H-000500 test)
`formal_borrow = b1*anydigpayment + b3*(anydigpayment x lowcov2019_z) + b2*account_fin
              + b4*(account_fin x lowcov2019_z) + X + d_c`
- `lowcov2019_z` main effect absorbed by `d_c`.
- **`b3` is the test.** `b3 > 0` => the digital-payment association is stronger where 2019
  credit-information coverage was lower.
- **M2b:** `lowcov2019_z` -> `lowcov2019_bmedian` (interpretable pp contrast).
- **M2c:** two interactions jointly — `anydigpayment x lowbureau2019_z` and
  `anydigpayment x lowregistry2019_z`. **Joint test:** Wald H0 both interaction coeffs = 0,
  economy-cluster-robust VCOV, F-form with G-1 denominator df, plus a wild-cluster-bootstrap
  p. Economies with bureau = registry = 0 are retained.

### M3 — Mechanism split (receive vs make)
```
M3a: formal_borrow = g1*receive_dig + g2*make_dig + b2*account_fin + X + d_c
M3b: formal_borrow = g1*receive_dig + g3*(receive_dig x lowcov2019_z)
                   + g2*make_dig + g4*(make_dig x lowcov2019_z)
                   + b2*account_fin + b4*(account_fin x lowcov2019_z) + X + d_c
```
Prediction (C3): `g1 > g2`; `g3 > 0` and `g3 > g4`. Sample = rows non-missing on both
`receive_dig` and `make_dig` (report the reduced N).

### M4 — Secondary and placebo outcomes (RHS as M2)
- `mobile_loan_app` (expect `b1 > 0`, `b3 > 0`)
- `emergency_loan_source` (expect `b1 > 0`) — reliance on a loan source (a financial
  institution, an employer, **or** a private lender) as the stated main way to raise
  emergency money, versus self-insurance (savings, work, asset sales) or family/friends.
  **Not** a formal-credit outcome; a secondary contrast only (REVISION 2).
- `informal_borrow` — **placebo**: expect `b3 ~ 0` (C4).

### M5 — Heterogeneity (M2 with one extra 3-way interaction at a time)
`anydigpayment x lowcov2019_z x {inc_q (linear) | female_d | educ (linear) | region}`.
Report all four.

### M6 — Robustness (each changes one thing vs M2)
1. weight `w_unweighted`; weight `w_population`.
2. **dummy-variable** logit and probit; AME of `anydigpayment` and of the interaction in pp;
   economy-cluster delta-method SE (fallback cluster bootstrap). Separation: drop a perfectly
   separated economy from M6.2 only, list it. Convergence: `newton` maxiter 100, retry
   `lbfgs`, record which.
3. drop the 6 `High income` economies (recompute all z-scores on the reduced set).
4. moderator = `lowdepth2019_z`; moderator = `lowrights2019_z`.
5. add country controls `lgdppc`, `privcredit_gdp`, `acct_own_rate` **and their interactions
   with `anydigpayment`**. `b3` must survive (else H-000500 not supported — it was country income).
6. drop economies with retained n < 500.
7. economy-block bootstrap of `b3` (in addition to the wild-cluster bootstrap). *(Two-way
   economy+region clustering is NOT used — only 7 regions.)*
8. add `internet_use` to the primary controls; report M1/M2 with and without.
9. leave-one-economy-out on `b3` (plot ~97 estimates).
10. add `inwork_d` (`emp_in`) to the primary controls; report M1/M2 with and without.

### M7 — Vietnam positioning (descriptive, no model claim)
- Vietnam percentile on `any_cov`, on `depth_credit_info_0_8`, and on raw weighted
  `formal_borrow` by `anydigpayment`.
- Fitted `d(formal_borrow)/d(anydigpayment)` from M2 at Vietnam's `lowcov2019_z`, with a CI.
  Worded as "the cross-country pattern implies X at Vietnam's 2019 coverage level", never a
  Vietnam effect.

## 4. Tables and figures (frozen list)

T1 drop table · T2 descriptives overall + by `anydigpayment` + economy-level moderator
distribution with Vietnam marked · T3 M1+M2+M2b · T4 M3a+M3b · T5 M4 · T6 M6 grid (b1, b3
across variants) · F1 binned scatter (adjusted economy-level `formal_borrow` gap vs `any_cov`,
fitted line, Vietnam labelled) · F2 leave-one-economy-out `b3` · F3 predicted association
across the `lowcov2019_z` range with 95% band, Vietnam + deciles marked.

## 5. Inference and multiplicity (frozen)

- **Primary confirmatory:** `b1` (M1), `b3` (M2). Reported **unadjusted**; exact p-values.
- **Secondary family (BH, q = 0.05), exactly these 9 hypotheses (size and order frozen):**
  1. M4 `mobile_loan_app` b1
  2. M4 `mobile_loan_app` b3
  3. M4 `emergency_loan_source` b1  *(REVISION 2: renamed from `emergency_formal`)*
  4. M4 `emergency_loan_source` b3  *(REVISION 2: renamed from `emergency_formal`)*
  5. M4 `informal_borrow` b3
  6. M5 x`inc_q`
  7. M5 x`female_d`
  8. M5 x`educ`
  9. M5 x`region` (joint Wald -> one p)
- Romano-Wolf is not used.
- The study **stands or falls on M2 `b3`**.

## 6. Decision rules (frozen — mirrors `H-000500.json`)

| Outcome | Reading |
|---|---|
| `b3 > 0`, p < 0.05 (economy-clustered), survives M2b, M2c, M6.1, M6.3, M6.4, M6.5; and M3b `g3 > 0` | **H-000500 supported** — association pattern consistent with (not proof of) the coverage-substitution idea. Non-causal. |
| `b3 > 0` but fails M6.5 (country controls) or M6.9 (driven by < 5 economies) | **Weak / not supported.** Report the fragility. |
| `b3 ~ 0` or `< 0` | **Not supported.** Report the null; discuss (coverage ceiling, account access already absorbing it). |
| placebo `informal_borrow` `b3` ~ as large as for `formal_borrow` | **Coverage-substitution reading not supported** even if `b3 > 0` for formal. |

No result is suppressed. No new specification is added after seeing estimates.

## 7. Out of scope (exploratory only, labelled if reported)

Multi-wave / panel; mediation; IV; ML heterogeneity; any moderator not listed;
country-level-only regression as the headline; B-READY 2024 as a moderator (different
framework, 50 economies — discussion only).

## 8. Environment

Run receipt records: Python, numpy/pandas/statsmodels/(pyfixest or linearmodels) versions,
OS, wall-clock, bootstrap seed, all input hashes, and the resolved `make_dig` / `pay_utilities`
coding decision.
