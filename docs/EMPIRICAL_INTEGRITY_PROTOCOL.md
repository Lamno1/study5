# Empirical integrity protocol

No empirical claim is manuscript-eligible until its evidence status is `VERIFIED`.

The enforced chain is:

`STUDY_ID -> DATA_MANIFEST -> EXPERIMENT_ID -> RUN_ID -> ARTIFACT_HASHES -> EVIDENCE_ID -> INDEPENDENT_RUN_ID`

Rules:

1. Data manifests are immutable, study-scoped, and contain source, extraction date,
   license, codebook, observational unit, coverage, and a SHA-256 artifact hash.
2. An experiment cannot be approved without registered manifests and explicit gate
   checks for the hypothesis, specification, variables, leakage, and study isolation.
3. Unknown or rejected experiments cannot submit results. There is no auto-approval.
4. Result artifacts must exist inside the workspace and are hashed at admission.
5. Random calls must be declared as bootstrap, permutation test, simulation, or test
   fixture and must not construct or alter the estimand. Undeclared randomness fails.
6. Estimation creates `UNVERIFIED` evidence. A different agent and different run ID
   must reproduce it before the experiment becomes `COMPLETED`.
7. `FAILED` and `UNTESTED` are valid terminal research outcomes. Agent agreement does
   not substitute for any evidence gate.

## Operator status

Run `python -m orchestrator.main status`. The agent table is authoritative for live
activity: `RUNNING` requires a live PID and a recent heartbeat; after 90 seconds without
either it is displayed as `STALE`. A terminal global phase is normalized to
`COMPLETED` with no active agent, even when a legacy state file contains contradictory
fields.

Required result payload fields are `experiment_id`, `study_id`, `run_id`, `executed_by`,
`main_result`, `code_file`, and `output_file`. A result-audit receipt must contain
`experiment_id`, `verdict`, and `independent_run_id`. A `PASS` using the original
run ID or the registering agent is rejected.
