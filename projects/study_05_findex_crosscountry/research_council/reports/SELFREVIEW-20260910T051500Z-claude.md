# Internal Q1 Referee Report — Study 5, MANUSCRIPT_DRAFT_v2.md

**Record:** `SELFREVIEW-20260910T051500Z` · **Stance:** hostile-but-fair Q1 referee, cold read ·
**Purpose:** self-audit before Codex's independent adversarial review — this does **not** replace it.

**Recommendation: MAJOR REVISION.**
A general-interest Q1 editor would desk-reject on contribution size. For a development-finance /
economics-of-digitalization field journal or the UEH competition — the realistic target — the
paper's transparency (frozen plan, independent cold reproduction, a contrary result reported
straight) is a genuine strength, but four substantive items must be closed before it can call the
sign reversal "robust", and one integrity defect must be fixed.

**None of the findings changes the H-000500 verdict.** The hypothesis is not supported under the
frozen decision rule regardless; the findings bound *how affirmatively the reversal can be
described*, not whether the hypothesis is rejected.

---

## Decision-relevant concerns

### Must fix before Codex

| # | Dimension | The concern | What resolves it |
|---|---|---|---|
| **C2** | Novelty | No Study-5 literature audit exists — the LIT-* on file is Study-1-scoped and never covers Galilea et al. (2026). "Whether the same pattern holds for individuals is not established" (§1) is an unverified "nobody has done this". | Run `literature-review` scoped to H-000500; produce a LIT-* with `search_adequacy`. Check whether Galilea et al. or a WB PRWP already runs an individual-level / Findex version. |
| **C5** | Identification | M2 interacts **only** `anydigpayment` and `account_fin` with the moderator, not the other individual controls. If digital-payment users in thin-coverage economies are disproportionately poor/rural (flatter borrowing slope), the negative β₃ is a compositional artifact. This is the most likely benign explanation and it is untested. | Add `X × lowcov2019_z` for the frozen control set (or at least urban, income quintile, education, age) as a robustness row; report whether β₃ survives. Disclose as post-hoc. |
| **C6** | Data | The moderator is the World Bank **Doing Business "Getting Credit" coverage** series — discontinued in 2021 after an integrity review found irregularities for several economies/years. The manuscript calls it "archived" and never engages this. | Add a paragraph on the DB data-integrity history; identify implicated economies in-sample; show β₃ robust to dropping them; cross-validate 2019 values against an independent source (IMF FAS / live WB API) for a sample. |
| **C9** | Interpretation | Abstract + §5.3: the reversal "survives every pre-registered robustness check and every adversarial re-specification" — but the pre-registered **depth proxy is insignificant** (p≈0.18) and the **legal-rights proxy is positive** (+0.705). A referee who reads Table 2 then the abstract distrusts the rest. | Rewrite: the *significant* reversal holds for the registered coverage moderator across weighting/sample/control-set variation and all 97 LOEO fits; the two alternative institutional proxies are not significant (one same-sign, one opposite-sign). |
| **C13** | Integrity | `H-000500.json` cites evidence IDs `E-S5-0001` / `E-S5-0002`, which **do not exist**. The real ledger entries are `E-000068` / `E-000069` (the manuscript cites these correctly). The CLAIM_CONTRACT evidence chain is broken at the hypothesis node. | Update `H-000500.json` (`verdict` block, `supporting_evidence`, `counter_evidence`, the 2026-09-10 revision entry) to `E-000068` / `E-000069`; append a revision_history note. |

### Should fix before Codex

- **C1 (Contribution).** Sharpen the "so what": name the exact policy-targeting argument that loses
  its individual-level footing, and add a minimum-detectable-effect / equivalence statement — how
  large a positive interaction can the data rule out?
- **C4 (Mechanism evidence).** §7 calls the account-access channel "the explanation we find most
  plausible" on one imprecise sensitivity (account-holders-only, p≈0.22) that conditions on an
  endogenous collider. Downgrade the language or add a proper decomposition with the caveat.
- **C8 (Robustness).** No Oster / coefficient-stability bound for β₃ — the natural summary given
  C5. Add one. Reconcile whether depth, legal rights and coverage are the same "thinness" construct
  (if not, drop the broad "institutional" language; if yes, concede fragility).
- **C14 (Citations).** A 2024-wave fact is cited to the 2021 Findex report (Demirgüç-Kunt et al.
  2022); use the 2025 report. Complete the Galilea et al. / Berg et al. verification.

### Not blocking (revise for the typeset version)

- **C3** theory is derivative and not adapted to individual retail lending; §7 lists rather than
  adjudicates.
- **C7** LPM boundary behaviour undiscussed; the z-scored moderator's "per SD" scale is
  sample-dependent and silently rescales under M6.3.
- **C10** no characterisation of sample composition (income group / region / share from the 24
  thin-coverage economies); a binned scatter of the economy-level slope vs 2019 coverage would help.
- **C11** add one sentence delimiting what the null does *not* imply for policy.
- **C12** Tables 1–2 are hand-transcribed (each value traced by the table audit, but no
  `make tables`); M5 / M7 are single-implementation.

---

## 12-dimension scorecard

| Dimension | Severity | Strongest concern |
|---|---|---|
| Contribution | MAJOR | C1 — descriptive null, no identification; thin for general-interest Q1 |
| Novelty | MAJOR | C2 — no Study-5 literature audit backing the "not established" claim |
| Theory | MINOR | C3 — mechanism imported from firm-level paper, not adapted |
| Mechanism evidence | MAJOR | C4 — preferred explanation rests on one imprecise collider-prone check |
| Identification | MAJOR | C5 — missing control × moderator interactions |
| Data | MAJOR | C6 — Doing Business getting-credit data-integrity history unaddressed |
| Econometrics | MINOR | C7 — LPM bounds; sample-dependent z-scale |
| Robustness | MAJOR | C8 — deep on drop-X, thin on functional form / Oster / proxy agreement |
| Interpretation | MAJOR | C9 — abstract "survives every check" contradicts Table 2 |
| External validity | MINOR | C10 — sample composition not described |
| Policy implications | MINOR | C11 — null not delimited |
| Reproducibility | MINOR | C12 / C13 — tables not script-generated; H-000500.json cites dead evidence IDs |

**Closest paper that could sink the framing:** Galilea, Farazi & Mare (2026) themselves, or a
World Bank PRWP that has already crossed Findex borrowing with Doing Business getting-credit
coverage. C2 is the only way to know.

---
*Registered by Claude (Lead Co-Author, self-audit). This is not Codex's review; if Codex and this
report later disagree, the disagreement stands and evidence decides.*
