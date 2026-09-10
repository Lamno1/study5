# Study 5 — Preregistration REVISION 2 (pre-estimation)

**Date:** 2026-09-09 · **Trigger:** `audit/CODEX_S5_PREBUILD_SEMANTIC_BLOCK.md`
(CODEX-S5-PREBUILD-BLOCK-001), detected after Revision 1 verification, **before Stage 1 build
and before any outcome model**. **No estimation has been run. No analysis panel written.**
Study 1 untouched.

## The defect

Revision 1 defined a secondary outcome `emergency_formal = 1(fin24 == 4)` and dropped
`fin24 == 8` but not `fin24 == 9`. Per the Findex DDI:
- `fin24` category **4** = *"A loan from a financial institution, an employer, or a private
  lender"* — it does **not** isolate formal credit.
- `fin24` **8** = Don't know, **9** = Refused.

Calling category 4 "formal" misstates the construct; treating code 9 as a valid `0` turns a
refusal into a substantive observation. Both are contract / fail-closed violations.

## Resolution (this is the only change vs Revision 1)

| # | Codex requirement | Applied |
|---|---|---|
| 1 | Rename to a neutral construct | `emergency_formal` -> **`emergency_loan_source`** everywhere |
| 2 | Redefine | `emergency_loan_source` = `1` if `F.fin24 == 4`; `0` if `F.fin24 in {1,2,3,5,6,7}`; **missing / drop** if `F.fin24 in {8, 9}` or system-missing |
| 3 | Never call it formal borrowing / a formal-credit outcome | M4 wording changed to: *"reliance on a loan source (a financial institution, an employer, or a private lender) as the stated main way to raise emergency money, versus self-insurance (savings, work, asset sales) or family/friends."* It is a **secondary contrast only.** |
| 4 | Keep the 9-hypothesis BH family size and test order | Unchanged. Only the **labels** of family members **3** and **4** change: `M4 emergency_formal b1` -> `M4 emergency_loan_source b1`; `M4 emergency_formal b3` -> `M4 emergency_loan_source b3`. Same positions, same tests, same order. |
| 5 | Dated Revision 2; update H-000500 only if it names this outcome; request re-freeze | This file. `H-000500.json` does **not** name this outcome (its `outcome` field is `formal_borrow` only) — a `revision_history` entry is added, no substantive change. |

## Files edited in place (REVISION 2 note added)

- `VARIABLE_CONTRACT.md` — secondary-outcomes row renamed + redefined + neutral-construct note.
- `PREREGISTRATION.md` — M4 bullet reworded; section 5 BH family entries 3 and 4 relabelled.
- `H-000500.json` — `revision_history` entry only.
- `CLAIM_CONTRACT.md` — unchanged (it never named this outcome; C4 is the `informal_borrow` placebo).

## Not changed

- The primary claim (C1), the moderation test (C2 / M2 `b3`), the mechanism split (C3 / M3),
  the placebo (C4 / `informal_borrow`), all weights, controls, moderator, inference, and the
  Vietnam analysis are **exactly as Revision 1**.
- The two WDI country-control raw inputs Codex downloaded under the registered M6.5 plan
  remain; **Codex adds them to `data/STUDY_05_RAW_MANIFEST.json` with hashes and their
  source/vintage before the re-freeze.**

## Status

Revision 1 + Revision 2 together define the frozen preregistration. Awaiting Codex:
verify Revision 2, add the WDI inputs to the manifest, **hash-freeze** the revised
`papers/study_05/*` + `H-000500.json`, then Stage 1 -> Stage 2 -> Stage 3.
