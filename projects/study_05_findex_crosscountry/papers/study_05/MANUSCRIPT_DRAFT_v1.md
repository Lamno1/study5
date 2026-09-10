# Digital Payments and Formal Borrowing Across 97 Economies: A Pre-registered Test of the Credit-Information-Substitution Hypothesis

**Draft v1 — 2026-09-10.** Prepared for the UEH student scientific-research competition.
Author: Nguyen Tran (University of Economics Ho Chi Minh City).

> **Status.** All empirical results are from the frozen pre-registration `EXP-S5-001`
> (`PREREGISTRATION.md`), estimated by Codex (`CODEX-S5-EXP-20260909-002`) and independently
> reproduced by a separate cold implementation (`CLAUDE-S5R-20260910-001`, verdict PASS;
> `audit/CLAUDE_S5_STAGE4_INDEPENDENT_REPRODUCTION.md`). Every empirical sentence below traces
> to evidence ledger entry `E-000068` (the association) or `E-000069` (the moderation test).
> This draft has **not** yet passed `data-table-consistency-audit` or
> `peer-reviewer-simulation-q1`. Numbers shown to 4 s.f.; final typeset copy will carry full
> tables.

---

## Abstract

We ask whether digital-payment activity is associated with formal borrowing among adults, and
whether that association is larger where credit-information coverage is thinner — the
individual-level analogue of the firm-level pattern documented by Galilea, Farazi and Mare
(2026). Using the 2024 Global Findex microdata for 100,560 adults in 97 economies, we estimate
survey-weighted linear probability models with economy fixed effects and economy-clustered
standard errors, following a pre-registered plan. Making or receiving a digital payment is
associated with a 3.62 percentage-point-higher probability of having borrowed from a formal
financial institution in the past 12 months (95% CI 2.60–4.64 pp), conditional on account
ownership, demographics and economy fixed effects. The pre-registered moderation prediction is
**not supported**: the interaction of digital-payment activity with *lower* 2019
credit-information coverage is negative (−1.97 pp per economy-level standard deviation; 95% CI
−2.92 to −1.03 pp), the opposite of the hypothesised sign, and this reversal survives every
pre-registered robustness check and every adversarial re-specification. The registered
receive-versus-make mechanism and the informal-borrowing placebo also fail. We interpret the
results as a cautious, non-causal external-population check that does not reproduce the
credit-information-substitution reading at the individual level, and we discuss why a coverage
floor and the account-access channel are plausible explanations. We report Vietnam's position
in the cross-country distribution for local context.

**Keywords:** digital payments, financial inclusion, formal borrowing, credit information,
Global Findex, pre-registration.
**JEL:** G21, G51, O16, D14.

---

## 1. Introduction

Digital payments have become the most widely held financial service in low- and middle-income
economies: the 2024 Global Findex shows that a majority of adults in the economies it surveys
now make or receive at least one digital payment, often before or without holding other formal
financial products (Demirgüç-Kunt, Klapper, Singer and Ansar, 2022). A recurring policy claim
is that the transaction record such payments generate can serve as an alternative credit
signal, extending formal credit to borrowers whom traditional credit-information systems do
not cover. Galilea, Farazi and Mare (2026) provide the most direct evidence for this idea:
across 101 economies, firms that use electronic payments report weaker credit constraints, and
the association is stronger where credit-information depth is lower — consistent with
electronic-payment records substituting for a missing credit file.

Whether the same pattern holds for *individuals* is not established. Individuals face
different lenders, different products and different information technologies than firms, and
the Global Findex — the natural data source at the individual level — has been used mainly to
describe digital-payment adoption and broad financial-inclusion outcomes rather than to test
this specific moderation. Berg, Burg, Gombović and Puri (2020) show that digital-footprint
variables can predict individual default, which makes the mechanism plausible in principle,
but their setting is a single e-commerce lender in one country. Bazarbash and Beaton (2020)
relate cross-country fintech credit to financial development and information infrastructure
using provider-level data, again not at the individual level.

This paper runs a pre-registered individual-level test. We do **not** claim novelty of the
question or of the method; we position the exercise as an individual-level descriptive
analogue and an external-population check of the established firm-level pattern. Three features
discipline the exercise. First, the full analysis plan — sample, variables, specifications,
robustness checks, multiple-testing correction and decision rules — was frozen and
hash-committed before any outcome model was estimated. Second, the primary results were
produced by one implementation and then independently reproduced by a separate cold
implementation that did not see the first; 43 of 45 compared quantities match to 13 decimal
places. Third, the decision rules were written to make a null or contrary interaction a valid,
reportable outcome rather than a failure.

The pre-registration matters because the headline result is a contrary one. We find that
digital-payment activity is positively associated with formal borrowing within economies
(3.62 pp, 95% CI 2.60–4.64), but that this association is **smaller**, not larger, in
economies where 2019 credit-bureau and credit-registry coverage was lower (interaction −1.97
pp per standard deviation, 95% CI −2.92 to −1.03). The sign reversal is robust to
unweighted and population weights, to excluding high-income economies, to adding country-level
macro controls and their interactions, to alternative moderator constructs, to dropping
zero-coverage economies, to leaving out each of seven world regions, and to leaving out each
of the 97 economies one at a time. The registered mechanism split (receiving versus making
payments) and the informal-borrowing placebo also do not behave as the substitution reading
predicts.

Our contribution is therefore an honest, reproducible negative result. At the individual
level, in this cross-section, the cross-country pattern that motivates the
digital-footprint-substitution policy narrative does not appear; if anything the data show the
opposite gradient. We set out the most plausible explanations — a coverage floor in the
thinnest-coverage economies, and the possibility that in those economies digital-payment
activity mainly proxies for basic account access rather than for an incremental credit signal
— and we are explicit about what the design cannot rule out.

## 2. Related literature and positioning

**Firm-level evidence.** Galilea, Farazi and Mare (2026) is the closest paper. Using World
Bank Enterprise Survey data for 101 economies, they document that electronic-payment use is
associated with weaker firm credit constraints and that the association is larger where the
depth-of-credit-information index is lower. Our design mirrors theirs at the individual level:
same broad hypothesis, same moderation logic, different unit and different data.

**Digital footprints and credit.** Berg et al. (2020) show that easily accessible
digital-footprint variables match or exceed a credit bureau score in predicting consumer
default at a German e-commerce lender. This establishes that the *information content* of a
digital trace can be real; it does not establish that the trace expands formal borrowing at
the population level, still less that the effect concentrates where bureaus are thin.

**Cross-country digital credit.** Bazarbash and Beaton (2020) relate the size of fintech and
digital-credit markets across countries to financial development and to information
infrastructure, using marketplace-lending and provider-level data. Their focus is the supply
of digital credit rather than the individual borrower's use of formal credit.

**Global Findex.** Demirgüç-Kunt et al. (2022) and the associated database document the rapid
adoption of digital payments and its correlation with account ownership and with saving and
borrowing behaviour. The database is descriptive by construction. We use it for a specific
pre-registered moderation test rather than for adoption description.

**Positioning.** We claim only an individual-level descriptive analogue and external-population
check of the Galilea et al. pattern. We make no causal, mechanism-identification or novelty
claim.

## 3. Data

### 3.1 Individual data

The individual data are the 2024 wave of the World Bank Global Findex microdata
(`microdata.worldbank.org/catalog/7860`; DOI 10.48529/bk9n-8r43; SHA-256
`ca307a0c…f90fce`). The borrowing and digital-payment module was administered in 98 of the
140 released economies; the reduced questionnaire elsewhere omits the outcome. Our unit of
observation is an adult aged 15 or older within an economy.

- **Outcome** `formal_borrow`: one if the respondent reports having borrowed from a bank or
  another type of formal financial institution in the past 12 months (`fin22a` = 1), zero if
  not (`fin22a` = 2); "don't know" and "refused" are dropped.
- **Exposure** `anydigpayment`: one if the respondent made or received at least one digital
  payment in the past 12 months, zero otherwise.
- **Mechanism split** (secondary): `receive_dig`, one if the respondent received any of wages,
  government transfers, a pension or an agricultural payment into an account; `make_dig`, one
  if the respondent made a digital merchant payment or paid a utility bill from an account.
  Unknown responses are treated as missing, never as zero, and are dropped only for the
  mechanism regressions.
- **Controls** (frozen primary set): account ownership at a financial institution, an
  indicator for female, age centred and its square, three education categories, five
  within-economy income quintiles, and an urban indicator.

### 3.2 Country moderator

The moderator is the country's **2019 credit-information coverage**: the maximum of the 2019
private credit-bureau coverage and the 2019 public credit-registry coverage, in percent of
adults, from the archived World Bank Doing Business series (`IC.CRED.ACC.PRVT.CRD.ZS`,
`IC.CRED.ACC.PUBL.CRD.REG.COVR.ZS`; snapshot SHA-256 `ef0c67f9…bd06c`). We denote its
negative z-score, computed across the estimation economies, `lowcov2019_z`, so that higher
values mean thinner 2019 coverage. Across the 97 estimation economies the raw coverage
measure has a weighted mean of 41.5%, a median of 40.4%, and a wide spread (24 economies below
10%). The depth-of-credit-information index and the strength-of-legal-rights index, both 2019
vintage, are used as distinct robustness proxies, not as the same construct.

The moderator is measured five years before the outcome. Credit infrastructure is
slow-moving, so this is a defensible historical measure, but we treat the vintage mismatch as
a limitation and never describe the moderator as the contemporaneous 2024 system.

### 3.3 Country controls (robustness only)

For one robustness specification we add, at the economy level, log GDP per capita and domestic
credit to the private sector (% of GDP), each the latest World Bank observation no later than
2023, and the in-sample economy account-ownership rate, together with their interactions with
digital-payment activity. GDP per capita is 2023 for every economy; the private-credit series
has heterogeneous vintages (2008–2023), which we disclose.

### 3.4 Sample construction

Table 1 records the deterministic sample. Requiring a valid formal-borrowing response leaves
102,644 adults in 98 economies. Requiring complete primary covariates removes a further 2,084
adults and one economy (Lesotho, whose income-quintile variable is entirely missing). The
moderator merges to every remaining economy by ISO3 code. The estimation sample is **100,560
adults in 97 economies**; the mechanism sub-sample, which additionally requires non-missing
receive and make indicators, is 90,118 adults in 89 economies. Vietnam contributes 998
respondents.

**Table 1. Sample construction.**

| Step | Adults after | Economies after |
|---|---:|---:|
| Valid formal-borrowing response (`fin22a` ∈ {1,2}) | 102,644 | 98 |
| + non-missing digital-payment, account, sex, age | 102,644 | 98 |
| + non-missing education | 102,245 | 98 |
| + non-missing income quintile | 101,247 | 97 (Lesotho exits) |
| + non-missing urbanicity | 100,560 | 97 |
| + moderator merged by ISO3 | 100,560 | 97 |

Raw rates (survey-weighted): 3.78% of adults with no digital payment have borrowed formally,
against 14.13% of adults with a digital payment — an unadjusted gap of about 10.4 percentage
points, which the regressions below reduce to 3.62 pp once account ownership, demographics and
economy fixed effects are held fixed.

## 4. Empirical strategy

All specifications were frozen in `PREREGISTRATION.md` and hash-committed before estimation.

### 4.1 Primary specification

For adult *i* in economy *c* we estimate, by weighted least squares,

  `formal_borrow_{ic} = β₁·anydigpayment_{ic} + β₂·account_fin_{ic} + X_{ic}′γ + δ_c + ε_{ic}` (M1)

and, for the moderation test,

  `formal_borrow_{ic} = β₁·anydigpayment_{ic} + β₃·(anydigpayment_{ic} × lowcov2019_z_c)`
  `+ β₂·account_fin_{ic} + β₄·(account_fin_{ic} × lowcov2019_z_c) + X_{ic}′γ + δ_c + ε_{ic}` (M2)

where `X` is the frozen control set, `δ_c` are economy fixed effects (which absorb the
moderator's main effect), and weights `w_equal` make each economy sum to one, so the estimand
is the average within-economy association with economies weighted equally. Standard errors are
clustered by economy (97 clusters); we also report Rademacher wild-cluster-bootstrap p-values
(999 replications). **`β₃` is the pre-registered test.** `β₃ > 0` would mean the
digital-payment/formal-borrowing association is stronger where 2019 coverage was thinner.

### 4.2 Pre-registered decision rule

The frozen rule (`PREREGISTRATION.md` §6): H-000500 is *supported* only if `β₃ > 0`,
significant at 5%, and robust to the below-median moderator contrast, the bureau/registry
joint test, alternative weighting, dropping high-income economies, the depth and legal-rights
proxies, and country-level controls, and if the mechanism split shows the receive interaction
positive. `β₃ ≈ 0` or `β₃ < 0` means *not supported*, to be reported plainly. A non-null
placebo interaction for informal borrowing also undermines the substitution reading.

### 4.3 Secondary and robustness specifications

The plan specifies: a below-median moderator contrast (M2b); a bureau/registry joint test
(M2c); the receive-versus-make mechanism split (M3); three secondary outcomes with
Benjamini-Hochberg control over a frozen nine-hypothesis family (M4); four heterogeneity
interactions (M5); a ten-branch robustness grid (M6, including unweighted and population
weights, dummy-variable logit/probit, dropping high-income economies, the depth and
legal-rights proxies, country controls, a minimum economy-size filter, an internet-use
control, an economy-block bootstrap, a leave-one-economy-out sweep and an employment control);
and a descriptive Vietnam-positioning exercise (M7). Adversarial checks (drop each control,
restrict to account holders, drop zero-coverage economies, drop the lowest coverage quartile,
leave out each region, and a moderator sign-reversal algebra check) were run after estimation.

### 4.4 Interpretation limits

The design is a single cross-section. Economy fixed effects remove all fixed cross-country
confounding but do not identify the effect of digital-payment use or of the moderator, and do
not make the cross-level interaction causal. Digital-payment activity and formal borrowing are
mechanically linked through account ownership, which we condition on but which is itself a
possible common consequence. We therefore use associational language throughout and prohibit
causal, policy-effect and mechanism-identification claims (`CLAIM_CONTRACT.md`).

## 5. Results

### 5.1 The association (C1)

Digital-payment activity is associated with a **3.617 percentage-point** higher probability of
formal borrowing (M1; economy-clustered SE 0.514 pp; p ≈ 3 × 10⁻¹⁰; 95% CI 2.597–4.638 pp;
wild-cluster-bootstrap p = 0.001; 100,560 adults, 97 economies). Against a sample formal-
borrowing rate of about 9.2%, this is an association of roughly 40% of the mean. It is a
within-economy, covariate-adjusted association, not a causal effect. [E-000068]

### 5.2 The pre-registered moderation test (C2 / H-000500)

The moderation prediction is **not supported, with the interaction carrying the opposite
sign**. In M2 the interaction of digital-payment activity with lower 2019 credit-information
coverage is **−1.975 percentage points** per one economy-level standard deviation
(economy-clustered SE 0.474 pp; p ≈ 6.8 × 10⁻⁵; 95% CI −2.916 to −1.033 pp;
wild-cluster-bootstrap p = 0.001). The digital-payment/formal-borrowing association is
therefore *weaker*, not stronger, in economies with thinner 2019 coverage — the reverse of the
credit-information-substitution prediction. The below-median contrast (M2b) agrees: the
association is 3.958 pp smaller in economies below the coverage median (SE 0.970 pp;
p ≈ 9.3 × 10⁻⁵). [E-000069]

Under the frozen decision rule this places H-000500 in the *not supported* branch. We do not
relabel the reverse pattern as a confirmation of a different hypothesis; it was not
pre-registered.

### 5.3 Robustness of the sign reversal

The negative interaction survives every pre-registered robustness branch (M6) and every
adversarial re-specification, always with the same sign and always significant at
conventional levels except where noted:

**Table 2. The M2 interaction `β₃` across specifications (percentage points per SD).**

| Specification | `β₃` | Note |
|---|---:|---|
| M2 baseline | −1.975 | p ≈ 6.8e-5 |
| Unweighted | −2.129 | |
| Population weights | −2.783 | |
| Drop 6 high-income economies (z re-computed) | −2.050 | 94,682 adults / 91 economies |
| Moderator = depth-of-credit-information proxy | −0.525 | p ≈ 0.18 (imprecise, same sign) |
| Moderator = legal-rights proxy | +0.705 | p ≈ 0.24 (imprecise) |
| + country controls and their digital-payment interactions | −2.354 | p ≈ 0.003 |
| + internet-use control | −2.048 | |
| + employment control | −1.896 | 96,925 adults / 96 economies |
| Restrict to account holders | −0.803 | p ≈ 0.22 (imprecise) |
| Drop zero-coverage economies | −2.121 | 99,059 adults / 95 economies |
| Drop lowest coverage quartile | −2.880 | 76,108 adults / 72 economies |
| Leave out each of 7 regions | −2.187 … −1.412 | all negative |
| Leave out each of 97 economies | −2.164 … −1.737 | all negative |
| Moderator sign reversed (algebra check) | +1.975 | exact negation, as expected |

Dummy-variable logit and probit give negative interaction average marginal effects
(approximately −1.35 and −1.36 pp); the sign, not the precise magnitude, is the informative
quantity from the non-linear models. The only specifications that do not reach significance
are those that also lose precision by construction — the account-holders-only restriction and
the two alternative moderator proxies — and none of them reverses the sign toward the
hypothesised direction.

### 5.4 Mechanism and placebo

The registered receive-versus-make mechanism (M3) does not behave as the substitution reading
predicts. In M3a the making-payment coefficient (5.172 pp) exceeds the receiving-payment
coefficient (4.080 pp), contrary to the prediction that incoming, lender-visible payments
matter more. In M3b the receive interaction is essentially zero (−0.269 pp, p ≈ 0.59) while
the make interaction is −2.021 pp (p ≈ 6 × 10⁻⁵). The informal-borrowing placebo (M4) also
fails: the interaction for borrowing from family or friends is **positive** (+1.736 pp,
p ≈ 0.005; Benjamini-Hochberg q ≈ 0.010), where the substitution reading predicts it to be
approximately zero. Taken together, the secondary results give no support to a
credit-information-substitution interpretation even though some of the individual coefficients
are statistically distinguishable from zero. [E-000069]

### 5.5 Independent reproduction

The primary and robustness results were produced by one implementation
(`CODEX-S5-EXP-20260909-002`) and then reproduced by a separate cold implementation written
from the frozen contracts alone (`CLAUDE-S5R-20260910-001`). Of 45 compared quantities, 43
match to an absolute difference below 5 × 10⁻¹³, including M1, the M2 interaction, M2b, the
mechanism split, every secondary outcome, the full robustness grid, and every adversarial
check. Two non-primary diagnostics — the M2c joint-test statistic form and the non-linear
interaction marginal effect — differ in magnitude but not in sign or conclusion. The
reproduction verdict is PASS (`audit/CLAUDE_S5_STAGE4_INDEPENDENT_REPRODUCTION.md`).

## 6. Vietnam in the cross-country distribution

This section is descriptive; it makes no claim about a Vietnam-specific effect. Vietnam's 2019
credit-information coverage is 59.4% (public registry 59.4%, private bureau 20.6%), above the
97-economy median of 40.4% — Vietnam is a *higher-coverage* economy on this measure, with a
maximum-score depth-of-credit-information index of 8. Evaluated at Vietnam's value of the
moderator, the fitted M2 slope of formal borrowing on digital-payment activity is
approximately +5.07 pp (95% CI 3.89–6.25 pp). This is the cross-country pattern read at
Vietnam's 2019 coverage level, not an estimate of what digital payments do in Vietnam.

## 7. Discussion

**Why might the association be weaker, not stronger, where coverage is thin?** Three
explanations are consistent with the evidence and with the design's limits.

*A coverage floor.* In the 24 economies with 2019 coverage below 10%, credit-information
systems are close to absent for everyone; there is little cross-sectional room for a
digital-payment record to "substitute" at the margin, and formal borrowing in these economies
is low and concentrated among a small, selected group. Dropping the zero-coverage economies
and the lowest coverage quartile does not remove the negative interaction, which argues
against this being the whole story, but a non-linear coverage relationship remains plausible.

*The account-access channel.* Where formal financial infrastructure is thin, holding an
account and using digital payments may principally mark inclusion in the formal system at all,
rather than an incremental, lender-legible signal on top of an existing credit file. The
account-holders-only restriction shrinks the interaction toward zero and renders it imprecise,
which is consistent with composition — including non-account holders — accounting for part of
the gradient. This is the explanation we find most plausible, and it is the opposite of the
firm-level substitution reading.

*Supply-side heterogeneity.* Lenders in thin-coverage economies may not have the systems to
act on a digital-payment history even when it exists; the firm-level result may reflect
relationship-lending technologies that individual retail lending in these settings lacks. We
cannot test this with Findex.

**Reconciling with Galilea et al. (2026).** The unit differs (firms versus individuals), the
outcome differs (self-reported credit constraints versus realised formal borrowing), the
moderator differs (depth index versus coverage), and the lending technologies differ. A
contrary individual-level cross-section does not contradict their firm-level finding; it
bounds its external validity.

**Limitations.** (i) One cross-section; no temporal ordering; formal borrowing can itself
induce account opening and digital activity. (ii) The moderator is 2019, five years before the
outcome, and is a non-random country characteristic. (iii) `account_fin` is conditioned on but
is a possible common consequence; the account-holders-only check is a sensitivity analysis,
not a fix. (iv) The private-credit robustness control has heterogeneous vintages. (v) The
Global Findex provenance is verified-reconstructed, not original-download verified. None of
these is resolved by the design, and all are why the language stays associational.

## 8. Conclusion

In a pre-registered individual-level test across 97 economies, digital-payment activity is
positively associated with formal borrowing, but the credit-information-substitution
prediction — that the association is larger where credit-information coverage is thinner — is
not supported. The interaction has the opposite sign and is robust to every pre-registered and
adversarial check, and the registered mechanism and placebo tests give no support to the
substitution reading. We read this as an external-population check that does not reproduce the
firm-level pattern at the individual level in this cross-section, most plausibly because
digital-payment activity in the thinnest-coverage economies marks basic formal-system access
rather than an incremental credit signal. The value of the exercise is in its transparency: a
frozen plan, an independently reproduced result, and a contrary finding reported as such.

---

## Reproducibility statement

Raw inputs, code and results are under `projects/study_05_findex_crosscountry/`. The frozen
pre-registration (`papers/study_05/PREREGISTRATION.md`, `VARIABLE_CONTRACT.md`,
`CLAIM_CONTRACT.md`) and hypothesis (`research_council/hypotheses/H-000500.json`) were
hash-committed before estimation (`CODEX-S5-REVISION2-FREEZE-001`). Primary estimation:
`code/study_05_crosscountry/*_codex.py`, run `CODEX-S5-EXP-20260909-002`. Independent
reproduction: `code/study_05_crosscountry/CLAUDE-S5R-20260910-001_reproduce.py`
(SHA-256 `2e7a43db…60f`), run `CLAUDE-S5R-20260910-001`, verdict PASS. Evidence ledger:
`E-000068` (association), `E-000069` (moderation test), both `INDEPENDENTLY_REPRODUCED`.
Input SHA-256: Findex microdata `ca307a0c…f90fce`; 2019 credit-information snapshot
`ef0c67f9…bd06c`.

## References

- Bazarbash, M. and Beaton, K. (2020). *Filling the Gap: Digital Credit and Financial
  Inclusion.* IMF Working Paper WP/20/150. International Monetary Fund.
- Berg, T., Burg, V., Gombović, A. and Puri, M. (2020). On the Rise of FinTechs: Credit
  Scoring Using Digital Footprints. *Review of Financial Studies*, 33(7), 2845–2897.
- Demirgüç-Kunt, A., Klapper, L., Singer, D. and Ansar, S. (2022). *The Global Findex Database
  2021: Financial Inclusion, Digital Payments, and Resilience in the Age of COVID-19.* World
  Bank.
- Galilea, G. W., Farazi, S. and Mare, D. S. (2026). Firm Credit Constraints and Electronic
  Payments: A Global Analysis. World Bank. *(reproducibility package
  reproducibility.worldbank.org/catalog/430; verify final citation details before submission.)*
- World Bank (2025). *Global Findex Database 2025 Microdata (2024 wave).* World Bank Microdata
  Library, catalogue 7860. DOI 10.48529/bk9n-8r43.
- World Bank. *Doing Business archived indicators* (Getting Credit: credit-bureau and
  credit-registry coverage, depth of credit information, strength of legal rights), 2019
  snapshot.

> **Citation-verification note for the next pass.** Confirm before submission: (i) Galilea,
> Farazi and Mare (2026) exact author order, title, outlet and year; (ii) the Global Findex
> 2025 report citation (Demirgüç-Kunt et al. year may need updating to the 2025 report);
> (iii) Berg et al. (2020) volume/pages. `peer-reviewer-simulation-q1` and
> `data-table-consistency-audit` still to run.
