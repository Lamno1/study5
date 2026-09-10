# Study 5 — Variable Contract (FROZEN 2026-09-09, REVISION 1 + REVISION 2)

**REVISION 1 (2026-09-09, pre-estimation)** per `audit/CODEX_S5_STAGE0_REVIEW.md` §9 and
`REVISION_1_RESPONSE.md`. Changes vs the original freeze: weight formulas corrected; primary
control set reduced (`internet_use`, `emp_in` moved to robustness); explicit unknown-value
truth tables for `receive_dig` / `make_dig`; moderator renamed `weakCIS_*` -> `lowcov2019_*`
and re-described as *2019 credit-information coverage*; sample expectation corrected.

**REVISION 2 (2026-09-09, pre-estimation)** per `audit/CODEX_S5_PREBUILD_SEMANTIC_BLOCK.md`
and `REVISION_2_RESPONSE.md`. Only change: the secondary outcome `emergency_formal` is
renamed `emergency_loan_source`, code 9 (Refused) added to its drop rule, and it must never
be described as a formal-credit outcome (`fin24 == 4` bundles financial-institution, employer
and private-lender loans).

**No estimation has been run.**

Codings verified against `data/external/GlobalFindex2025_DDI.xml`. Raw sources:
- `F` = `data/raw/data_micro_findex_2024_vietnam.xlsx`, sheet `findex_microdata_2025_labelled_`
  (sha256 `ca307a0c3dfd54dc945a18fb03c58b014143bc21c90761f71fe304e6a2f90fce`).
- `W` = `data/raw/wb_credit_information_latest_snapshot.csv`
  (sha256 `ef0c67f9c7d44b67939e088f0aab2e578f7ba0d7f2eeadc4093c0103cc1bd06c`).

## Identifiers / weights

| name | construction |
|---|---|
| `iso3` | `F.economycode` (already ISO3; join key — never join by `W.country` labels, which use Doing Business reference-city names) |
| `economy` | `F.economy` |
| `region` | `F.regionwb` (7 groups) |
| `wgt` | `F.wgt` (Findex within-economy weight) |
| `pop_adult` | `F.pop_adult` |
| `w_equal` | `wgt_i / sum_{j in same economy}(wgt_j)` -> each economy sums to 1. **PRIMARY WEIGHT.** A global rescaling constant is allowed. |
| `w_population` | `w_equal_i * pop_adult_c`. Robustness only. |
| `w_unweighted` | `1`. Robustness only. |

**Estimand (frozen):** the average economy-specific (within-economy) association across the
module economies, each economy weighted equally.

## Outcome

| name | construction |
|---|---|
| `formal_borrow` | `1` if `F.fin22a == 1`; `0` if `F.fin22a == 2`; **drop** rows where `fin22a in {3 (DK), 4 (Refused)}` or missing. Expect 102,644 valid 1/2 responses across 98 module economies. |

## Exposure

| name | construction |
|---|---|
| `anydigpayment` | `F.anydigpayment` (1 = made or received a digital payment; 0 = not). Drop if missing. **Primary regressor.** |
| `receive_dig` | from `F.receive_wages`, `F.receive_transfers`, `F.receive_pensions`, `F.receive_agriculture` (each 1=into account, 2=cash only, 3=other way, 4=did not receive, 5=DK/ref, .=missing): `1` if **any** == 1; `0` if none == 1 **and** at least one in {2,3,4}; **missing** if none == 1 **and** all four in {5, missing}. Used in M3 only. |
| `make_dig` | from `F.merchantpay_dig` (0/1/.) and `F.pay_utilities` (1=from account; 2,3,4=non-digital/no payment; 5=DK/ref; .): `1` if `merchantpay_dig == 1` **or** `pay_utilities == 1`; `0` if not-1 **and** (`merchantpay_dig == 0` **or** `pay_utilities in {2,3,4}`); **missing** if `merchantpay_dig` missing **and** `pay_utilities in {5, missing}`. Used in M3 only. |

DK/refused is never silently coded 0. Rows missing `receive_dig`/`make_dig` are dropped **for
M3 only**, not for M1/M2.

## Country moderator (2019 World Bank Doing Business archived series; merged by `iso3`)

| name | construction |
|---|---|
| `bureau_cov` | `W.credit_bureau_cov_pct` (0-100), 2019 |
| `registry_cov` | `W.credit_registry_cov_pct` (0-100), 2019 |
| `any_cov` | `max(bureau_cov, registry_cov)` = **2019 credit-information coverage** (share of adults with a credit file at a bureau or registry). Measures COVERAGE, not report quality or lender use. |
| `lowcov2019_z` | `-1 * zscore(any_cov)` across the estimation economies (higher = lower 2019 coverage). **PRIMARY MODERATOR.** |
| `lowcov2019_bmedian` | `1` if `any_cov` < median(`any_cov`) across estimation economies, else `0`. Robustness (M2b). |
| `lowbureau2019_z` | `-1 * zscore(bureau_cov)`. Used jointly in M2c. |
| `lowregistry2019_z` | `-1 * zscore(registry_cov)`. Used jointly in M2c. |
| `lowdepth2019_z` | `-1 * zscore(W.depth_credit_info_0_8)`. **Distinct robustness proxy** (M6.4): "2019 depth-of-credit-information index". |
| `lowrights2019_z` | `-1 * zscore(W.legal_rights_0_12)`. **Distinct robustness proxy** (M6.4): "2019 strength-of-legal-rights index". |

All z-scores are computed **on the final estimation economies only**, one value per economy
(unweighted at the economy level). Vintage of every moderator: **2019** (Doing Business 2020) —
disclosed limitation; prose must never imply it measures the 2024 system.

## Individual controls

**Primary adjustment set (frozen):** `account_fin`, `female_d`, `age_c`, `age_c2`, `C(educ)`,
`C(inc_q)`, `urban_d`.

| name | construction | DDI coding |
|---|---|---|
| `account_fin` | `F.account_fin` (1/0) | "Has an account at a financial institution". **Mandatory.** |
| `female_d` | `1` if `F.female == 1` else `0` | 1 = Female, 2 = Male |
| `age` / `age_c` / `age_c2` | `F.age`; `age_c = age - mean(age)` over final sample; `age_c2 = age_c**2` | 15-99 |
| `educ` | `F.educ`, 3-level categorical, base = 1 | 1 = primary-, 2 = secondary, 3 = tertiary+ |
| `inc_q` | `F.inc_q`, 5-level categorical, base = 1 | within-economy household income quintile |
| `urban_d` | `1` if `F.urbanicity == 2` else `0` | 1 = Rural, 2 = Urban |

**Robustness-only controls (added in named specs, not in the primary estimand):**

| name | construction | spec |
|---|---|---|
| `internet_use` | `F.internet_use` (1/0) | M6.8 |
| `inwork_d` | `1` if `F.emp_in == 1` else `0` | M6.10 |

## Country controls (robustness M6.5; by `iso3`, latest <= 2023)

| name | source |
|---|---|
| `lgdppc` | `log`(WB `NY.GDP.PCAP.CD`), latest <= 2023 (fixed at build time, recorded) |
| `privcredit_gdp` | WB `FS.AST.PRVT.GD.ZS` (domestic credit to private sector, % GDP), latest <= 2023 |
| `acct_own_rate` | `w_equal`-weighted mean of `account_fin` per economy, computed in-sample |

## Secondary / placebo outcomes

| name | construction |
|---|---|
| `mobile_loan_app` | `1` if `F.fin20 == 1`; `0` if `== 2`; drop {3,4}/missing |
| `emergency_loan_source` | `1` if `F.fin24 == 4`; `0` if `F.fin24 in {1,2,3,5,6,7}`; **drop `F.fin24 in {8 (DK), 9 (Refused)}` and system-missing**. **REVISION 2:** `fin24 == 4` = "a loan from a financial institution, an employer, **or** a private lender" — this does **not** isolate formal credit. It measures reliance on a loan source (vs self-insurance: savings, work, asset sales, or family/friends) as the stated main way to raise emergency money. **Never call it formal borrowing / a formal-credit outcome.** Secondary contrast only. |
| `informal_borrow` | `1` if `F.fin22b == 1`; `0` if `== 2`; drop {3,4}/missing. **Placebo/contrast.** |

## Estimation sample (frozen definition)

Keep a row iff **all** of: `fin22a in {1,2}`; `anydigpayment` non-missing; `account_fin`,
`female`, `age`, `educ`, `inc_q`, `urbanicity` non-missing; `iso3` merges to `W`.

**Frozen expectation:** ~ 97 economies, ~ 100k adults. Lesotho excluded (`inc_q` entirely
missing). China retained (was lost only to the old mandatory `emp_in`). Codex reports the
exact drop table (rows after each filter, economies exited and why) in Stage 1; any economy
losing all observations on a mandatory covariate is excluded and named.
