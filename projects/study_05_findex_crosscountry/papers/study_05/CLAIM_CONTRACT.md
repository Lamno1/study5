# Study 5 — Claim Contract (FROZEN 2026-09-09, REVISION 1)

**REVISION 1 (2026-09-09, pre-estimation)** per `audit/CODEX_S5_STAGE0_REVIEW.md` and
`REVISION_1_RESPONSE.md`: "developing/emerging economies" removed; moderator renamed and
re-described as *2019 credit-information coverage*; novelty positioning locked. No estimation
has been run.

**Hypothesis:** `H-000500` · **Design:** descriptive cross-sectional association with
country-level moderation · **Causal claim: PROHIBITED.**

Any change requires a dated revision entry and re-freezing; no post-hoc claim may be added
after seeing results.

## C1 — Primary claim (to be estimated, direction not assumed)

> In the pooled 2024 Global Findex sample of adults **in the economies where the borrowing /
> digital-payment module was administered**, making or receiving a digital payment
> (`anydigpayment`) is **associated with** a [sign, magnitude] change in the probability of
> having borrowed from a formal financial institution in the past 12 months (`formal_borrow`),
> conditional on financial-account ownership, demographics, and **economy fixed effects**.

- Reported as an association (percentage points), with an economy-clustered standard error,
  95% CI, and the number of economies and individuals.
- **Not** a causal effect, **not** a policy effect, **not** a statement about credit volume,
  cost, or approval.

## C2 — Moderation claim (the contribution; direction is the hypothesis, not assumed)

> The C1 association is **larger (more positive) in economies that had lower 2019
> credit-information coverage** — i.e. the interaction `anydigpayment x lowcov2019_z` has
> coefficient `b3`, tested against 0.

- `lowcov2019_z` = negative z-score of `any_cov` = max(2019 private credit-bureau coverage,
  2019 public credit-registry coverage), % of adults, archived World Bank Doing Business
  series. It measures **coverage** (share of adults with a credit file), not report quality
  or lender use.
- H-000500 is **supported** only if `b3 > 0`, significant at 5% (economy-clustered), and
  robust per `PREREGISTRATION.md` §6 — including survival when log GDP per capita,
  private-credit/GDP and the economy account-ownership rate (and their interactions with
  `anydigpayment`) are added.
- If `b3 ~ 0`, negative, or fragile -> H-000500 is **not supported**; reported plainly.

## C3 — Mechanism claim (secondary)

> The C1/C2 pattern is **concentrated in digital payments RECEIVED into an account**
> (`receive_dig`) rather than payments MADE (`make_dig`), consistent with incoming payments
> being more visible to a lender (Galilea, Farazi & Mare 2026). Reported as a descriptive
> contrast, **not** as identification of a mechanism.

## C4 — Placebo / contrast

> The C2 moderation is **absent or weaker for informal borrowing** (`fin22b`, from family or
> friends), which should not track formal credit-information coverage.

## C5 — Vietnam positioning (descriptive only)

> Vietnam's location in the cross-country distribution of the 2019 moderator and of the raw
> digital-payment / formal-borrowing rates is described; the fitted association is reported at
> Vietnam's 2019 coverage value. **No causal or counterfactual claim about Vietnam.**

## Novelty positioning (frozen per Stage 0 §8)

Permitted: *"an individual-level descriptive analogue and external-population check of an
established firm-level pattern (Galilea, Farazi & Mare 2026)."*
Related work to cite: Galilea, Farazi & Mare (2026); Berg, Burg, Gombović & Puri (2020);
Demirgüç-Kunt, Klapper, Singer & Ansar (2022); **Bazarbash & Beaton (2020, IMF WP 20/150)**.

## Prohibited statements (must never appear in any Study 5 output)

- "digital payments increase / cause / drive / lead to formal borrowing"
- "effect of", "impact of", "raises", "boosts" (in a causal sense)
- any claim about loan size, interest rate, approval probability, or credit-constraint *levels*
- any firm / SME credit claim (this is individuals)
- "first", "novel", "fills a gap"
- any claim that the interaction **identifies a digital-footprint mechanism**
- any statement that the 2019 moderator is contemporaneous with the 2024 outcome, or that it
  measures the 2024 credit-information system
- "developing / emerging economies" as the population label
- policy recommendations stated as consequences of an estimated effect

## Evidence chain required before any claim is "supported"

`H-000500 -> STUDY_05_RAW_MANIFEST.json -> EXP-S5-001 -> RUN_ID (Codex) -> ARTIFACT_HASHES
-> EVIDENCE_ID -> INDEPENDENT_RUN_ID (Claude reproduction, different run id)`
per `docs/EMPIRICAL_INTEGRITY_PROTOCOL.md`. A PASS using the registering agent or the
original run id is rejected.
