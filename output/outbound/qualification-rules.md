# Qualification Rules: New-Outlet Payments Setup Workflow

**Owner:** Go-to-Market Engineering | **Audience:** GTM engineers and reviewers | **Version:** `qr-0.1` (2026-W46) | **Status:** Draft rules. Untested.
Related: [workflow-spec.md](workflow-spec.md) | [data-schema.md](data-schema.md) | [ICP qualification framework](../../context/icp/icp-qualification-framework.md) | [signal scoring framework](../../context/docs/research/signal-scoring-framework.md) | [signal matrix](../../context/docs/research/signal-matrix.md)

## 1. Summary

These rules turn the ICP and signal documents into steps a person or a script can follow. They do not change the ICP framework. They apply it to this workflow and add one pilot setting. Every value is a starting assumption and will be tested.

The rules run in this order:

1. Entry condition.
2. Suppression and hard gates.
3. Explicit-intent fast lane.
4. Signal score.
5. Capability check.
6. Fit and contactability.
7. Total score and status.
8. Re-checks.

All rules fail closed. If a rule cannot be run, the account does not reach outreach.

## 2. Rules version and change control

- Version string `qr-0.1`. Store it in each qualification row.
- Change a value only with a written reason in the work log and a new version string.
- After the pilot, review each value against outcomes.

## 3. Entry condition

An account enters this workflow only if **all** are true:

| # | Condition | Check |
|---|---|---|
| E1 | Segment is `hospitality` or `food_service` (primary ICP) | Segment field |
| E2 | City is on the approved list | City field |
| E3 | A verified or single-source new-outlet signal exists: SG-01, SG-02 or SG-03, observed within 180 days | Signals table |

Accounts that fail E1 to E3 are not scored in this workflow. Retail (secondary ICP) is held until Product confirms branch and reconciliation capabilities. Explicit-intent signals (SG-16 to SG-18) bypass E3 only.

## 4. Suppression and hard gates

Any failure sets status `EXCLUDED`. Record the failed gate and the date. Do not score.

| Gate | Rule | Fail if | Evidence |
|---|---|---|---|
| S0 Suppression | Business is not on the suppression list | Match on name, domain, phone or social URL | Suppression table |
| G1 Real and operating | Recent activity (posts, reviews, listing updates) | No activity in 180 days, or signs of closure | Public pages |
| G2 In scope geography | City on the approved list | Outside | Address |
| G3 Not simple collection only | Staff-handled counters or several payment channels | Single stall or channel only | Photos, pages |
| G4 Multi-outlet | Two or more outlets, or a verified new outlet bringing the total to two or more | Single outlet with no verified expansion | Outlet evidence |
| G5 Digital payments | Accepts or wants mobile money, card or QR | No sign of any digital payment and no stated interest | Photos, posts, reviews |
| G6 Not an existing customer | Not a Hubtel customer | Match on customer list or visible Hubtel decals | Suppression table, public signs |
| G7 Not a different motion | Not marketplace-only partner, not a large group with central procurement, not a regulated financial institution, not gaming or betting | Any | Listings, group structure |
| G8 Contactable | A business role can be reached through a public business channel | None found | Pages |

**Size check.** More than 15 outlets or more than about 250 employees is a **review flag**, not an automatic fail. A person decides whether the buyer is still the owner.

## 5. Fast lane

If a verified explicit-intent signal exists (SG-16, SG-17, SG-18) and S0 and G1 to G8 pass:

- Status `FAST_LANE`. Skip the score.
- Human review within two working days.
- Capability check still applies before any reply.
- Confirm that the signal came from a business, not a private individual.

## 6. Signal score

Use the base points, recency and verification multipliers from the [signal scoring framework](../../context/docs/research/signal-scoring-framework.md).

```
signal_points = base_points x recency_multiplier x verification_multiplier

within a category:  highest signal counts 100%, every other signal counts 50%
across categories:  all categories count 100%

pain_score    = min(30, sum of stage-3 signal points)
trigger_score = min(20, sum of stage-4 signal points)
signal_score  = pain_score + trigger_score        (maximum 50)
```

Stage 3 signals: SG-04, SG-07, SG-08, SG-09, SG-10. Stage 4 signals: SG-01, SG-02, SG-03, SG-05, SG-06, SG-11, SG-12, SG-13, SG-14, SG-15, SG-19, SG-20.

Same signal seen more than once counts once, using the most recent date. An unconfirmed signal never moves an account to outreach.

## 7. Capability check

Run for the account's strongest pain signal.

| Strongest pain | Maps to | Capability fit |
|---|---|---|
| Slow settlement, provider frustration (SG-08) | Hourly crediting and sweeps (S48) | `pass` |
| Till failures, no-internet need (SG-07, SG-10) | POS and USSD (S50, S51) | `pass` |
| Payment approvals, payroll workload (SG-04, SG-09 where about approvals) | Approval roles and payroll (S46, S47) | `pass` |
| Branch-level reporting across outlets | Not documented | `hold` |
| Per-staff sales tracking | Not documented | `hold` |
| Automated reconciliation | Not documented (planned, S49) | `hold` |
| Audit log | Not documented | `hold` |

Only Product can change a `hold` to a `pass`. Record the date and the person who confirmed it. Until then, `hold` accounts become `MONITOR`.

## 8. Fit score (0 to 40)

Unknown scores the neutral value shown and flags the field for enrichment.

| Criterion | Rule | Points |
|---|---|---|
| Outlet count (max 12) | 2 to 3 outlets | 8 |
| | 4 to 15 outlets | 12 |
| | More than 15 | 6 |
| | Unknown | 6 |
| Payment channels (max 8) | One channel | 0 |
| | Two channels | 5 |
| | Three or more | 8 |
| | Unknown | 4 |
| Staff handle money (max 8) | Evident | 8 |
| | Owner takes all payments | 2 |
| | Unknown | 4 |
| Owner distance (max 6) | Not at every outlet | 6 |
| | Always on site | 2 |
| | Unknown | 3 |
| Operational structure (max 6) | Documented (managers or finance role) | 6 |
| | Informal | 2 |
| | Unknown | 3 |

All unknown gives a neutral fit of 20.

## 9. Contactability score (0 to 10)

| Item | Rule | Points |
|---|---|---|
| Senior decision-maker | Owner or MD identified from a public source | 4 |
| | Not found | 0 |
| Finance or operations lead | Identified | 3 |
| | Not found | 0 |
| Business channel | Verified and active | 3 |
| | Present but unverified | 1 |
| | None | 0 |

Before contact enrichment, contactability is 0. Accounts reach `RESEARCH_NOW` before contacts are found, then are re-scored.

## 10. Total score and status

```
total_score = fit_score + pain_score + trigger_score + contact_score      (maximum 100)
```

Apply in this order. The first rule that matches sets the status.

| Order | Condition | Status | Action |
|---|---|---|---|
| 1 | S0 or any gate G1 to G8 failed | `EXCLUDED` | Record. Do not contact |
| 2 | Verified explicit intent | `FAST_LANE` | Human review within two working days |
| 3 | Entry condition not met | Not in this workflow | Route to other workflow or log |
| 4 | `signal_score` below 10 | `LOG_ONLY` | Record only |
| 5 | Capability fit is `hold` | `MONITOR` | Ask Product. Re-check in 30 days |
| 6 | `pain_score` is 0 (no pain evidence) | `MONITOR` | Re-check at opening date plus 30 days, or in 30 days if the opening has passed |
| 7 | `signal_score` from 10 to 19.9 | `MONITOR` | Re-check in 30 to 90 days |
| 8 | `signal_score` 20 or more, `pain_score` above 0, before enrichment is complete | `RESEARCH_NOW` | Enrich contacts and fit fields. Re-score |
| 9 | After enrichment: `total_score` 70 or more, `pain_score` 10 or more, capability `pass` | `QUALIFIED` | Recommend. Needs HA3 before any message |
| 10 | After enrichment: `total_score` 55 to 69, `pain_score` 10 or more, capability `pass` | `PILOT_REVIEW` | HA2 may approve proceeding. Reason required |
| 11 | Otherwise | `RESEARCH_NOW` (hold) | Fill gaps. Re-check in 30 days |

### Pilot setting

`PILOT_REVIEW` (total 55 to 69) exists because a total of 70 needs near-maximum fit plus real pain evidence plus a fresh trigger, and unknown fields score at neutral values. In the pilot, a reviewer may approve a `PILOT_REVIEW` account with a written reason. This is a pilot setting, not a change to the ICP framework. After the first 20 accounts, either recalibrate the threshold or retire this status. **Confirm with Sales before use.**

### Reviewer overrides

- Allowed only through HA2, with a reason and a name.
- A reviewer **cannot** override: suppression, any hard gate, a capability `hold`, or an unconfirmed signal.
- Log each override. Review all overrides at the weekly meeting.

## 11. Pseudo-code

For a script, a spreadsheet formula set or an n8n Code node. A person must review the code and the test results before use.

```
function classify(account):
    if on_suppression_list(account) or any_gate_failed(account):
        return EXCLUDED

    if has_verified_explicit_intent(account):
        return FAST_LANE

    if not entry_condition_met(account):          # E1, E2, E3
        return NOT_IN_WORKFLOW

    signals = latest_unique_signals(account)
    pain    = min(30, stack(signals, stage="pain"))
    trigger = min(20, stack(signals, stage="trigger"))
    sig     = pain + trigger

    if sig < 10:
        return LOG_ONLY
    if capability_fit(account) == "hold":
        return MONITOR
    if pain == 0:
        return MONITOR                            # recheck = opening_date + 30
    if sig < 20:
        return MONITOR

    if not enrichment_complete(account):
        return RESEARCH_NOW

    total = fit(account) + pain + trigger + contactability(account)
    if total >= 70 and pain >= 10:
        return QUALIFIED
    if total >= 55 and pain >= 10:
        return PILOT_REVIEW
    return RESEARCH_NOW                           # hold, recheck in 30 days

function stack(signals, stage):
    total = 0
    for category in categories(signals):
        pts = sorted(points of signals in category and stage, descending)
        total += pts[0] + 0.5 * sum(pts[1:])
    return total
```

Errors in any function return `ERROR` and stop the run. They never return `QUALIFIED`.

## 12. Re-check rules

| Situation | Re-check date |
|---|---|
| `MONITOR` with a new outlet that has not yet opened | Opening date plus 30 days |
| `MONITOR` after opening | 30 days |
| `MONITOR` with score 10 to 19.9 | 60 days |
| `RESEARCH_NOW` (hold) | 30 days |
| Declined | 90 days |
| Opt-out | Never |
| `EXCLUDED` for suppression | Never for acquisition |
| Capability `hold` | When Product confirms, or in 90 days |

Re-score every 90 days at minimum. Recency decay lowers old signals automatically.

## 13. Disqualifying and suppressing signals

| Signal | Action |
|---|---|
| Existing Hubtel customer | Exclude (S0, G6). Route to account management |
| Competitor decal or recent public payments-partner announcement | Suppress for six months, then re-check |
| Business closed or inactive | Exclude (G1) |
| Part of a large group with central procurement | Exclude (G7) |
| Regulatory or legal trouble reported | Hold. Do not contact until reviewed |
| Opt-out request | Permanent suppression |

## 14. Worked examples (hypothetical)

**These examples are hypothetical.** The businesses are invented. Scores illustrate the rules and are not benchmarks. Signal values reuse the examples in the signal scoring framework.

### Example 1: strong signals, short of the Qualified threshold

"Harbour Grill Group" (hypothetical), four-site restaurant group in Accra, fifth outlet announced.

| Step | Result |
|---|---|
| Entry | Food service, Accra, verified SG-01 within 180 days. Met |
| Suppression and gates | All pass |
| Signals | SG-07 8.0, SG-04 6.0 (stage 3). SG-01 6.0 (stage 4). All different categories |
| Pain score, trigger score | 14.0 and 6.0. Signal score 20.0 |
| Capability | Pain maps to POS and settlement. `pass` |
| Status before enrichment | `RESEARCH_NOW` (signal score 20, pain above 0) |
| After enrichment | Fit 40 (4 to 15 outlets 12, three channels 8, staff evident 8, owner not at every outlet 6, documented finance role 6). Contactability 5 (owner identified 4, finance lead not found 0, business channel present but unverified 1) |
| Total | 40 + 14 + 6 + 5 = 65 |
| Final status | `PILOT_REVIEW`. Total 55 to 69, pain 14, capability pass |
| Action | HA2 decides whether to proceed. This shows that even a well-evidenced account can miss 70 |

### Example 2: growth with no pain

"Coastline Hotels" (hypothetical), three-site group, fourth property opened this month in a new city.

| Step | Result |
|---|---|
| Entry and gates | Pass (confirm Hubtel covers the new city) |
| Signals | SG-01 8.0 and SG-02 6.0 in one category (8.0 + 3.0). SG-06 2.25 in People |
| Pain score, trigger score | 0 and 13.25. Signal score 13.3 |
| Status | Rule 6: pain is 0, so `MONITOR` |
| Re-check | Opening date plus 30 days. Look for till complaints or provider mentions |

### Example 3: existing customer

A hypothetical hotel group already on Hubtel's customer list opens a new branch.

| Step | Result |
|---|---|
| Suppression | Match on the customer list |
| Status | `EXCLUDED` (S0, G6) |
| Action | Do not contact for acquisition. Pass the signal to account management as an expansion note |

## 15. Test cases for the scoring script

Before any automation, check that these cases give the expected status. Claude Code can draft the test data. A person reviews it.

| Case | Expected status |
|---|---|
| Suppressed account with strong signals | `EXCLUDED` |
| Single outlet with no verified expansion | `EXCLUDED` (G4) |
| Verified SG-16 from a business | `FAST_LANE` |
| Only SG-01, no pain | `MONITOR` |
| SG-01 plus SG-08, capability `hold` | `MONITOR` |
| Unconfirmed SG-08 only | `LOG_ONLY` or `MONITOR` (below 20) |
| Signal score 20 or more, enrichment missing | `RESEARCH_NOW` |
| Total 70 or more, pain 10 or more, capability `pass` | `QUALIFIED` |
| Total 60, pain 12, capability `pass` | `PILOT_REVIEW` |
| Missing required field | `ERROR` (no progress) |
| Signal older than 365 days | 0 points |
| Two growth signals in one category | Second counts at 50% |

## 16. Confidence

- Rule structure and order: medium.
- Point values, thresholds and the pilot range: low. Untested.
- Capability mapping: medium for the documented items, low for holds, until Product confirms.

## 17. Open items

1. Confirm the pilot range (55 to 69) with Sales.
2. Get Product's confirmed capability list.
3. Get the suppression list.
4. Decide the approved city list.
5. Test the rules on 20 accounts and record how often a reviewer disagrees.
