# Study 5 — Digital Payments and Formal Borrowing Across Economies (Isolated Subproject)

Registered **2026-09-09**. Purpose: a cross-country individual-level study for the **UEH
student scientific-research competition** ("mục tiêu là đạt giải"), built from data already
in hand plus one small public add-on.

Runs the full empirical-integrity chain (`docs/EMPIRICAL_INTEGRITY_PROTOCOL.md`) from
scratch. Inherits **nothing** from Studies 1–4.

## Relationship to Study 1

`papers/study_01_rebuild/` (the Vietnam-only descriptive note, N=998) is **frozen and
untouched** — it remains the base for a future journal paper. Study 5 is a **separate**
question at a **different unit** (140 economies, individual level) and must not reuse Study
1's sample, estimates, tables, or text.

## Question (subject to Codex review — see the discovery + data audit)

Among adults in economies where the 2024 Global Findex borrowing/digital-payment module was
administered, is **digital-payment activity** — especially *receiving* payments into an
account — associated with **borrowing from a formal financial institution** (`fin22a`), and
is that association stronger where **2019 credit-information coverage was lower**?

This is the **individual-level analog** of Galilea, Farazi & Mare (2026), *Firm Credit
Constraints and Electronic Payments: A Global Analysis* (101 economies, firm level, World
Bank). Vietnam is positioned within the cross-country distribution for local policy relevance.

## Status (2026-09-09)

- Discovery + data audit: `audit/STUDY_05_DISCOVERY_AND_DATA_AUDIT_2026-09-09.md` — verdict `FEASIBLE`.
- Moderator **acquired + merged** (WB Doing Business credit-info indicators, 2019 snapshot;
  98/98 economies matched, 100%). Files under `data/raw/`, hashes in the manifest.
- **Analysis package + Stage 0 + REVISION 1 done:**
  - `research_council/hypotheses/H-000500.json`
  - `papers/study_05/CLAIM_CONTRACT.md`, `VARIABLE_CONTRACT.md`, `PREREGISTRATION.md` (EXP-S5-001)
  - `papers/study_05/CODEX_EXECUTION_BRIEF.md` — 5 stages
  - `audit/CODEX_S5_STAGE0_REVIEW.md` — Codex Stage 0, verdict `PROCEED_WITH_CHANGES`
  - `papers/study_05/REVISION_1_RESPONSE.md` — Claude's resolution of all 10 Stage-0 §9 items
  - `audit/CODEX_S5_PREBUILD_SEMANTIC_BLOCK.md` — Codex fail-closed pre-Stage-1: `fin24==4`
    bundles FI / employer / private-lender loans, cannot be named a formal-credit outcome
  - `papers/study_05/REVISION_2_RESPONSE.md` — Claude's fix: `emergency_formal` ->
    `emergency_loan_source`, drop code 9, never call it formal credit; BH family size/order unchanged
- **Estimation NOT started.** Next: Codex verifies REVISION 1 + REVISION 2, manifests the 2
  downloaded WDI control inputs, hash-freezes the revised `papers/study_05/*` + `H-000500.json`,
  then Stage 1 (build) -> Stage 2 (estimate) -> Stage 3 (adversarial audit) -> Stage 4 hand
  back to Claude (independent reproduction + English manuscript).
- Manuscript language: **English** (owner). Convert to the UEH competition template once supplied.

## What this study is and is not

- **Is:** a descriptive / correlational cross-country association study with heterogeneity by
  2019 country credit-information coverage. Expected primary complete-case sample: about
  100k adults in 97 module economies; Stage 1 records the exact count.
- **Is not:** causal. Single cross-section, no temporal ordering, and digital-payment
  activity and formal borrowing are mechanically linked through account ownership. Every
  output must carry this caveat.

## Layout

- `audit/` — discovery note, data audit, later Codex reviews.
- `data/STUDY_05_RAW_MANIFEST.json` — hashes + provenance of the Findex file and the
  to-be-acquired moderator file.
- `research_council/` — hypothesis + discovery records once registered.
- `papers/study_05/` — claim/variable contracts once a gate passes.
