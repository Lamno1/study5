# Study 5 — Codex Execution Brief

**For:** Codex. **From:** Claude (architect). **Date:** 2026-09-09.
**Role split for Study 5:** Claude owns design, contracts, preregistration, reproduction
check, and the manuscript. **Codex owns everything in this brief:** verification, the primary
build + estimation, artifact hashing, adversarial audit, and the gate.

Study 1 (`papers/study_01_rebuild/`) is **frozen** — do not touch it.

> **STAGE 0 COMPLETE** — `audit/CODEX_S5_STAGE0_REVIEW.md` (CODEX-S5-STAGE0-001), verdict
> `PROCEED_WITH_CHANGES`. Claude applied **REVISION 1** (`REVISION_1_RESPONSE.md`) resolving
> all 10 §9 items; `CLAIM_CONTRACT.md`, `VARIABLE_CONTRACT.md`, `PREREGISTRATION.md`,
> `H-000500.json` now carry REVISION 1. **Next Codex action: verify REVISION 1 against §9,
> hash-freeze the revised `papers/study_05/*` + `H-000500.json`, then begin Stage 1.** Do not
> start Stage 1 before the hash-freeze.

---

## STAGE 0 — Verify before building (COMPLETE; retained for reference)

0.1 **Moderator provenance.** Confirm the four WB indicator IDs in
`data/STUDY_05_RAW_MANIFEST.json` resolve on the WB API under `source=1`, that the CSVs in
`data/raw/wb_credit_information_*.csv` match the hashes recorded there, and that the archived
`lastupdated=2021-08-18` / `date=2019` snapshot is what we think it is. Spot-check 8-10
countries' values (incl. VNM, a 0-depth country, a 100%-coverage country) against a second
public source (WB DataBank UI, or the Doing Business 2020 report PDF).

0.2 **Vintage decision.** Confirm we accept the **2019** moderator against the **2024**
outcome, disclosed as a limitation. If you judge a better contemporaneous source exists
(B-READY 2024 credit-information score, GFDD bureau/registry coverage post-2019), fetch it,
add a manifest entry, and use it as an *additional* robustness moderator — do **not** replace
the preregistered primary without a dated contract revision.

0.3 **Design sign-off.** Read `audit/STUDY_05_DISCOVERY_AND_DATA_AUDIT_2026-09-09.md` Part A.
Register your independent view on: the single-cross-section limitation; the mechanical
`anydigpayment`-`formal_borrow` link through account ownership; whether `account_fin` +
`account_fin x weakCIS` are adequate controls; whether `internet_use` is a bad control;
whether the estimand and weighting choice are sound. If you want a design change, propose it
now as a contract revision — not after seeing estimates.

0.4 **Novelty.** Independently check whether an individual-level cross-country
"digital payments x credit-information depth -> formal borrowing" paper already exists
(Claude's search on 2026-09-09 found only the firm-level Galilea, Farazi & Mare 2026). If it
exists, report it before we spend effort.

**Output of Stage 0:** `audit/CODEX_S5_STAGE0_REVIEW.md` with an explicit verdict
`PROCEED` / `PROCEED_WITH_CHANGES` / `HALT`. Do not start Stage 1 on a HALT.

## STAGE 1 — Build (deterministic)

1.1 Implement `PREREGISTRATION.md` section 1 + `VARIABLE_CONTRACT.md` exactly. Fail-closed:
if any expected column/sheet/code is absent, raise an error naming what was expected and what
was found — never substitute.

1.2 Resolve the two open variable questions and record the choice in the receipt:
- `make_dig`: check `pay_utilities` codes in `data/external/GlobalFindex2025_Microdata_Codebook.pdf`;
  if the "digital / from account" category is not unambiguous, use `merchantpay_dig` alone.
- Confirm `female == 1` is female and `urbanicity == 2` is urban in the actual data (cross-tab
  against known Vietnam figures or the codebook).

1.3 Produce the drop table (T1). Freeze `analysis_panel` and hash it.

1.4 Acquire the three country controls for M6.5 (`lgdppc`, `privcredit_gdp` via WB API;
`acct_own_rate` computed in-sample). Add a manifest entry with hashes.

## STAGE 2 — Estimate (this is `EXP-S5-001`, `RUN_ID` = Codex, e.g. `CODEX-S5R-20260910-001`)

2.1 Run **every** specification in `PREREGISTRATION.md` section 3 (M1-M7) and produce
tables/figures T1-T6, F1-F3.

2.2 Write results to write-once immutable artifacts under
`results/study_05_crosscountry/<RUN_ID>/`:
- `analysis_panel.<ext>` + `panel_receipt.json` (row counts, hashes, drop table)
- `estimates.json` (every coefficient, SE, cluster-SE, bootstrap p, CI, N, N_economies, R2,
  keyed by model)
- `tables/*.tex` or `*.csv`, `figures/*.pdf`
- `run_receipt.json` — `experiment_id`, `study_id`, `run_id`, `executed_by`, `main_result`,
  `code_file`, `output_file`, environment block, RNG seed, wall-clock, all input hashes.

2.3 Code lives at `code/study_05_crosscountry/<RUN_ID>_analysis.py` (or a small module).
No `np.random.*` except the declared wild-cluster bootstrap (seed recorded).

## STAGE 3 — Adversarial audit (Codex, same run or a second pass)

Attack the result. At minimum:
3.1 Re-run M2 dropping the mandatory controls one at a time; show `b3` is not an artifact of
one control.
3.2 The mechanical-endogeneity probe: restrict to `account_fin == 1` only (everyone banked);
does `b3` survive?
3.3 Reverse the moderator sign as a sanity check (coefficient should flip).
3.4 Leave-one-region-out (7 estimates) in addition to leave-one-economy-out.
3.5 Check the 14 zero-depth / very-low-coverage economies are not all one region driving `b3`.
3.6 Placebo `informal_borrow` — is `b3` genuinely smaller?
3.7 Compare `b1` (M1) to Study 1's Vietnam-only estimate as a smell test (same order of
magnitude expected for Vietnam; different samples, so not identical).

**Output:** `audit/CODEX_S5_AUDIT.md` — for each preregistered decision rule in
`PREREGISTRATION.md` section 6, state which branch the evidence lands in, with the numbers.
Verdict: `H-000500 SUPPORTED` / `WEAK` / `NOT SUPPORTED` / `MECHANISM NOT SUPPORTED`.

## STAGE 4 — Hand back to Claude

Claude then: (a) independently reproduces `b1`, `b3`, and the M3b split with separate code and
a different `INDEPENDENT_RUN_ID` (must match to a stated tolerance; a PASS using Codex's run
id or Codex as verifier is rejected — `docs/EMPIRICAL_INTEGRITY_PROTOCOL.md`); (b) writes the
English manuscript strictly within `CLAIM_CONTRACT.md`; (c) runs `literature-review` and
`peer-reviewer-simulation-q1`; (d) converts to the UEH competition template once the owner
supplies it.

## Hard rules

- Nothing is estimated until Stage 0 returns `PROCEED`, or a `PROCEED_WITH_CHANGES` verdict
  has been fully resolved, independently verified, and hash-frozen before Stage 1.
- The preregistration is frozen; deviations are dated contract revisions, made **before**
  seeing the affected estimate.
- Report the result in whatever direction it comes out. A null `b3` is a valid, reportable
  outcome — see `PREREGISTRATION.md` section 6.
- No causal language anywhere (`CLAIM_CONTRACT.md` prohibited list).
- Do not reuse any number, sample, or table from Study 1.
