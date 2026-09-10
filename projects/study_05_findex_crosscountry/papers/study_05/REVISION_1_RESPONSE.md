# Study 5 — Preregistration REVISION 1 (pre-estimation)

**Date:** 2026-09-09 · **Trigger:** `audit/CODEX_S5_STAGE0_REVIEW.md` (CODEX-S5-STAGE0-001),
verdict `PROCEED_WITH_CHANGES`, §9 (10 required revisions). **No estimation has been run.**
Study 1 untouched.

This document resolves each of Codex's 10 items. `CLAIM_CONTRACT.md`, `VARIABLE_CONTRACT.md`,
`PREREGISTRATION.md`, `H-000500.json` and `CODEX_EXECUTION_BRIEF.md` are edited in place to
match; each carries a "REVISION 1" note. After Codex hash-freezes the revised set, Stage 1 may begin.

---

## Item 1 — Sample count corrected

- `fin22a in {1,2}`: **102,644** valid responses in **98** module economies (310 DK/refused dropped, not 44).
- Under the **revised** complete-case rule (Item 5 removes `emp_in` and `internet_use` from
  mandatory controls), the frozen *expectation* is **~ 97 economies, ~ 100k adults** - Lesotho
  excluded (`inc_q` entirely missing); **China is retained** (it was lost only to the old
  mandatory `emp_in`). Codex reports the exact drop table in Stage 1; any economy that loses
  all observations on a mandatory covariate is excluded and named.
- The "98 economies / 95k-100k" wording is replaced by this.

## Item 2 — Target population fixed; high-income economies retained

- Primary population = **"the economies where the 2024 Global Findex borrowing / digital-payment
  module was administered and complete covariates are available"** (~ 97 economies).
- The 6 module economies labelled `High income` by `regionwb` (Croatia, Poland, Romania, Oman,
  Saudi Arabia, Panama) are **retained in the primary sample**.
- **All "developing / emerging economies" language is removed** from the hypothesis statement,
  claim contract, preregistration, README and (future) manuscript. Excluding the 6 high-income
  economies becomes robustness **M6.3** (z-scores recomputed on the reduced set).

## Item 3 — Weights corrected to match the stated estimand

Replace the `w1`/`w2` formulas with:

```
w_equal_i      = wgt_i / sum_{j in economy(i)} wgt_j        # each economy sums to 1  -> PRIMARY
w_population_i  = w_equal_i * pop_adult_c                    # economy weight proportional to adult population -> robustness
w_unweighted_i  = 1                                          # robustness
```

A single global rescaling constant on any of these is allowed. **Primary weight = `w_equal`.**
**Frozen estimand:** *the average economy-specific (within-economy) association between digital-
payment activity and formal borrowing across the ~ 97 module economies, each economy weighted
equally.* A different estimand (average sampled adult) would require a new dated revision, not
a silent switch.

## Item 4 — Explicit unknown-value truth tables

### `receive_dig` (from `receive_wages`, `receive_transfers`, `receive_pensions`, `receive_agriculture`; each 1=into account, 2=cash only, 3=other way, 4=did not receive, 5=DK/ref, .=missing)

| Condition | `receive_dig` |
|---|---|
| **any** of the 4 == 1 | **1** |
| none == 1 **and** at least one in {2,3,4} | **0** |
| none == 1 **and** all 4 in {5, missing} | **missing** (row dropped for M3 only) |

### `make_dig` (from `merchantpay_dig` in {0,1,.} and `pay_utilities` in {1=from account, 2,3,4 = non-digital/no payment, 5=DK/ref, .})

| Condition | `make_dig` |
|---|---|
| `merchantpay_dig == 1` **or** `pay_utilities == 1` | **1** |
| not the above **and** (`merchantpay_dig == 0` **or** `pay_utilities in {2,3,4}`) | **0** |
| `merchantpay_dig` missing **and** `pay_utilities in {5, missing}` | **missing** (row dropped for M3 only) |

DK/refused never silently becomes 0. `receive_dig` / `make_dig` are used only in M3
(mechanism); rows missing on them are dropped **for M3 only**, not for M1/M2.

## Item 5 — `internet_use` and `emp_in` moved out of the primary adjustment set

- **Primary controls (frozen):** `account_fin`, `female_d`, `age_c`, `age_c2`, `C(educ)`,
  `C(inc_q)`, `urban_d`. (Matches Study 1's control set and keeps China.)
- `internet_use` -> robustness **M6.8** (add to primary; report M1/M2 with and without).
- `emp_in` (`inwork_d`) -> robustness **M6.10** (add to primary).
- `account_fin` stays mandatory; the `account_fin == 1` restriction remains an essential
  sensitivity analysis (Stage 3.2), explicitly not a fix for endogeneity.

## Item 6 — Two-way (economy + region) clustering removed from confirmatory robustness

- Deleted from M6.7. Confirmatory inference = **economy-clustered SE + wild-cluster bootstrap
  (Rademacher, 999)**.
- **Leave-one-region-out (7 estimates)** stays as adversarial sensitivity in Stage 3 only,
  never as a confirmatory inference method.

## Item 7 — One multiplicity procedure

- **Benjamini-Hochberg (BH) at q = 0.05**, applied to a **frozen 9-hypothesis secondary family**:
  1. M4 `mobile_loan_app` b1
  2. M4 `mobile_loan_app` b3
  3. M4 `emergency_formal` b1   *(renamed `emergency_loan_source` in REVISION 2 — same test/position)*
  4. M4 `emergency_formal` b3   *(renamed `emergency_loan_source` in REVISION 2 — same test/position)*
  5. M4 `informal_borrow` b3 (placebo)
  6. M5 heterogeneity interaction: x `inc_q` (linear)
  7. M5 heterogeneity interaction: x `female_d`
  8. M5 heterogeneity interaction: x `educ` (linear)
  9. M5 heterogeneity interaction: x `region` (joint Wald across region dummies -> one p-value)
- **Primary confirmatory tests M1 `b1` and M2 `b3` are NOT in the family** - reported
  unadjusted as the two pre-declared primary tests.
- Romano-Wolf is not used (its implementation is not independently validated here).

## Item 8 — Fixed-effect logit / probit implementation (robustness M6.2)

- **Unconditional (dummy-variable) logit and probit**: economy fixed effects entered as
  dummies; ~97 dummies over ~100k observations.
- **Separation policy:** if an economy is perfectly separated on the outcome, or the
  `anydigpayment x outcome` cell is degenerate, that economy is dropped **from M6.2 only** and
  listed in the receipt.
- **Convergence:** statsmodels `method="newton"`, `maxiter=100`; on non-convergence retry
  `method="lbfgs"` and record which was used.
- **AME:** average of individual marginal effects of `anydigpayment` (and of the M2
  interaction, evaluated across the `lowcov2019_z` range), reported in **percentage points**,
  with SE by economy-cluster delta method (fallback: cluster bootstrap). Compared to the LPM
  `b1`/`b3` for sign and rough magnitude only.

## Item 9 — M2c joint test and weighted within-R2

- **M2c** enters two interactions jointly: `anydigpayment x lowbureau2019_z` and
  `anydigpayment x lowregistry2019_z` (each = -1 x z-score of the 2019 coverage series).
  **Joint test** = Wald test H0: both interaction coefficients = 0, using the
  economy-cluster-robust VCOV, reported as an F statistic with G-1 denominator df **and** a
  wild-cluster-bootstrap p-value. Economies with both bureau and registry coverage = 0 are
  retained (low extreme of both z-scores - informative, not missing).
- **Weighted within-R2 (one definition, reused for every LPM):**
  partial out economy fixed effects (and the weighted intercept) from `y` and every regressor
  by weighted Frisch-Waugh; then
  `within_R2 = 1 - (weighted SSR of the residualised full model) / (weighted TSS of residualised y)`.
  Computed identically across M1/M2/M3.

## Item 10 — Construct renamed to what is actually measured

- Everywhere: **"credit-information systems" -> "2019 credit-information coverage"**, defined as
  the **maximum of the 2019 private credit-bureau coverage and public credit-registry coverage
  (% of adults)** from the archived World Bank Doing Business series.
- Variable renames (frozen): `weakCIS_z` -> **`lowcov2019_z`**; `weakCIS_bmedian` ->
  **`lowcov2019_bmedian`**; the M2c pair -> `lowbureau2019_z`, `lowregistry2019_z`.
- `depth_credit_info_0_8` and `legal_rights_0_12` are **distinct 2019 robustness proxies**
  (M6.4), not the same construct - labelled "2019 depth-of-credit-information index" and
  "2019 strength-of-legal-rights index".
- The moderator measures **coverage** (share of adults with a credit file), **not** report
  quality or actual lender use. Prose must say so.

## Novelty positioning (Stage 0 section 8 - frozen)

Permitted: *"an individual-level descriptive analogue and external-population check of an
established firm-level pattern (Galilea, Farazi & Mare 2026)."*
Prohibited: "first", "novel", "fills a gap", and any claim that the interaction identifies a
digital-footprint mechanism. Add to the literature: **Bazarbash & Beaton (2020, IMF WP
20/150)** "Filling the Gap: Digital Credit and Financial Inclusion".

---

## Post-revision status

| Item | Status |
|---|---|
| 1 Sample count | resolved (~97 economies; Codex confirms in Stage 1 drop table) |
| 2 Target population | resolved (module-administered economies; 6 high-income retained; no "developing" language) |
| 3 Weights | resolved (`w_equal` primary, formulas fixed, estimand frozen) |
| 4 Unknown-value truth tables | resolved (tables above) |
| 5 `internet_use` / `emp_in` | resolved (both -> robustness; primary controls frozen) |
| 6 Two-way clustering | resolved (removed from confirmatory) |
| 7 Multiplicity | resolved (BH, 9-hypothesis family enumerated) |
| 8 FE logit/probit | resolved (dummy-variable; separation + convergence + AME policy) |
| 9 M2c joint test + within-R2 | resolved (definitions above) |
| 10 Construct name | resolved (`lowcov2019_*`; "2019 credit-information coverage") |

Awaiting Codex hash-freeze of the revised `papers/study_05/*` + `H-000500.json`, then Stage 1.

## Codex consistency correction before freeze

Before estimation, Codex found and mechanically corrected three stale descriptions outside
the substantive contracts: the README population/sample wording, the raw-manifest coverage
note, and the execution brief's hard-rule wording for a resolved `PROCEED_WITH_CHANGES`
verdict. These corrections do not alter the estimand or specification.
