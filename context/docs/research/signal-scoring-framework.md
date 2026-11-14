# Signal Scoring Framework

**Owner:** Go-to-Market Engineering | **Audience:** GTM, Sales and leadership | **Version:** 2026-W46
Companion: [signal-matrix.md](signal-matrix.md) (signal IDs SG-01 to SG-20). Feeds stages 3 and 4 of the [ICP qualification framework](../../icp/icp-qualification-framework.md). S# = source ID in the [source register](source-register.md).

## Summary

The framework turns observed signals into one number and one decision: **does this account deserve more research now, later or not at all?** It is a method, not a verdict. Every weight and threshold is our starting assumption and will change after the first accounts are reviewed.

How it works:
1. Classify each signal: explicit intent, strong, weak, or interesting but not actionable.
2. Check hard gates first. An account that fails a gate scores nothing.
3. Score each signal: base points, adjusted for how recent it is and how well it is verified.
4. Combine signals. Signals from different categories add in full. Several signals in the same category add less.
5. Convert the **Signal Score** (maximum 50) into a research decision.
6. Add fit and contactability from the qualification framework. Only the full score decides outreach.

## Signal classes

| Class | Definition | Can justify research alone? | Points |
|---|---|---|---|
| **Explicit intent** | The business is asking for a solution (SG-16, SG-17, SG-18) | Yes. Goes to the fast lane | Not scored |
| **Strong** | Points to a problem or imminent change Hubtel can address (SG-01 to SG-04, SG-07 to SG-11, SG-19) | Yes, with verification | 3 to 10 base points |
| **Weak** | Context only (SG-05, SG-06, SG-12 to SG-15, SG-20) | No. Counts only alongside another signal | 2 to 4 base points |
| **Interesting, not actionable** | Awards, follower growth, general press and similar | No | 0. Logged only |

## Gates first

Before scoring, run gates G1 to G8 from the qualification framework. Key gates for signals: real and operating business (G1), approved geography (G2), two or more outlets or a credible expansion plan (G4), not on Hubtel's customer list (G6), not a different motion (G7). A gate failure sets status to Excluded and the signal is logged without points.

## Scoring formula

**Signal points = base points × recency multiplier × verification multiplier**

### Base points

Stage 3 (pain evidence) is capped at 30. Stage 4 (triggers and timing) is capped at 20. These caps match the qualification framework.

| Stage | ID | Signal | Base points |
|---|---|---|---|
| 3 Pain | SG-08 | Provider or settlement frustration | 10 |
| 3 Pain | SG-07 | Public till complaints | 8 |
| 3 Pain | SG-04 | Finance or reconciliation hiring | 6 |
| 3 Pain | SG-10 | Payment channel change | 4 |
| 3 Pain | SG-09 | Several payment instructions | 4 |
| 4 Trigger | SG-01 | New outlet | 8 |
| 4 Trigger | SG-02 | New city or region | 6 |
| 4 Trigger | SG-03 | Multi-site group formation | 5 |
| 4 Trigger | SG-06 | New senior leader | 4 |
| 4 Trigger | SG-11 | Technology investment | 4 |
| 4 Trigger | SG-19 | First-party engagement | 4 |
| 4 Trigger | SG-14 | Funding or investment | 3 |
| 4 Trigger | SG-05 | Hiring wave (managers, cashiers) | 2 |
| 4 Trigger | SG-12 | Online channel expansion | 2 |
| 4 Trigger | SG-13 | New partnership | 2 |
| 4 Trigger | SG-15 | Renovation or relaunch | 2 |
| 4 Trigger | SG-20 | Seasonal or event peak | 2 |
| Fast lane | SG-16, SG-17, SG-18 | Explicit intent | Not scored |

### Recency multiplier

| Age of signal | Multiplier |
|---|---|
| 30 days or less | 1.0 |
| 31 to 90 days | 0.75 |
| 91 to 180 days | 0.5 |
| 181 to 365 days | 0.25 |
| Over 365 days | 0 |

The same signal seen more than once counts once, using the most recent date.

### Verification multiplier

| Level | Definition | Multiplier |
|---|---|---|
| Verified | Primary source (the business's own page or post) or two independent sources | 1.0 |
| Single source | One credible source, not confirmed elsewhere | 0.75 |
| Unconfirmed | Rumour, anonymous or hard-to-attribute source | 0.5 |

An unconfirmed signal never moves an account to outreach. It only prompts a check.

## Combining signals

**Categories.** Each signal belongs to one category:

| Category | Signals |
|---|---|
| Growth | SG-01, SG-02, SG-03, SG-15, SG-20 |
| People | SG-04, SG-05, SG-06 |
| Pain | SG-07, SG-08, SG-09 |
| Payments | SG-10 |
| Technology and partners | SG-11, SG-12, SG-13 |
| Capital | SG-14 |
| Hubtel-side | SG-19 |

**Stacking rule.** Within a category, the highest signal counts in full and the others count at 50%. Signals in different categories count in full. This rewards **different kinds of evidence** over repeated evidence of one kind. Several growth events usually describe one expansion, not several.

**Signal Score** = Stage 3 points (capped at 30) + Stage 4 points (capped at 20). Maximum 50. Round to one decimal.

### How combinations raise priority

| Pattern | Signals | What it suggests | Typical action |
|---|---|---|---|
| **Scaling and straining** | Growth (SG-01) + Pain (SG-07 or SG-08) | Expansion is exposing the problem. Strongest pattern | Research now |
| **Scaling the back office** | Growth + SG-04 | Growing and adding finance capacity. Possible tool need | Research now if gates pass |
| **Switching window** | SG-08 or SG-10 + SG-11 | Dissatisfaction with provider plus active change | Research now. Check the incumbent |
| **Reorganising** | SG-06 + SG-04 | New leader hiring finance staff | Research. Look for pain |
| **Growth without pain** | Growth only | Opportunity, but no evidence of the problem | Monitor. Look for pain evidence |
| **Pain without trigger** | SG-07 or SG-09 only | Problem exists, no timing | Monitor. Revisit in 90 days |
| **Context only** | Only weak signals | Not enough | Log |

**Minimum evidence rule.** To be Qualified under the qualification framework, an account needs at least one stage 3 signal (pain evidence). Growth alone can raise research priority but cannot qualify an account.

## Research decision

Based on the Signal Score, after gates and capability fit:

| Decision | Rule | Action |
|---|---|---|
| **Fast lane** | Any explicit intent signal (SG-16, SG-17, SG-18), gates pass | Human review within two working days. Skip the score. Confirm capability fit before reply |
| **Research now** | Signal Score 20 or more, with at least one stage 3 signal, gates pass | Full enrichment and qualification this week |
| **Monitor** | Signal Score 10 to 19.9, or 20 or more with no stage 3 signal | Light research. Re-check in 30 to 90 days |
| **Log only** | Signal Score below 10 | Record the signal. No research effort |
| **Excluded** | Fails any gate | Record reason. Do not contact |

**Capability check overrides.** If the account's strongest pain only maps to capabilities that Product has not confirmed (branch dashboards, per-staff tracking, automated reconciliation, audit logs), the account is moved to Monitor, whatever its score.

**Refresh.** Re-score every 90 days. Recency decay lowers old signals automatically.

## Decision flow: from event to action

| Step | Question | If no |
|---|---|---|
| 1 | Is the event in the matrix? | Log as "other". Consider adding it to the matrix after three similar sightings |
| 2 | Is it the same business, not a name collision? | Discard |
| 3 | Does it pass gates G1 to G8 and the suppression list? | Excluded |
| 4 | Is it explicit intent? | Fast lane |
| 5 | Is it verified (two sources or a primary source)? | Check before scoring. Score at 0.5 meanwhile |
| 6 | What is the Signal Score and category mix? | Apply the research decision table |
| 7 | Does the strongest pain match confirmed Hubtel capability? | Monitor |
| 8 | Who is the buyer (owner, GM, finance lead)? | Research the buyer, then use the full qualification framework |

## Signal log fields

Record each signal in the CRM or tracking sheet.

| Field | Description |
|---|---|
| account_id | Link to the account |
| signal_id | SG-01 to SG-20 |
| class | Explicit, strong, weak |
| category | Growth, people, pain, payments, technology, capital, Hubtel-side |
| observed_date | Date the event happened |
| detected_date | Date we found it |
| source_url | Where it was found |
| verification_level | Verified, single source, unconfirmed |
| evidence_note | One line: what exactly was seen |
| points | Calculated |
| false_positive_check | Done or not, with notes |
| next_action | One of the research decisions |
| reviewed_by | Name |

## Hypothetical examples

**These examples are hypothetical.** The businesses are invented for illustration and are not real Hubtel prospects or customers. The scores show how the method works. They are not benchmarks.

### Example A (hypothetical): growing restaurant group with visible pain

**Account:** "Harbour Grill Group", a four-site restaurant group in Accra (fictional).
**Signals found:**
- SG-07: two customer reviews about card payments failing, 20 days ago, from different people, both visible on the same review site. Verified. 8 × 1.0 × 1.0 = **8.0**.
- SG-04: job post for an accounts officer, "daily sales reconciliation across outlets", 15 days ago, on the group's own page. Verified. 6 × 1.0 × 1.0 = **6.0**.
- SG-01: fifth outlet announced 45 days ago on the group's page and local press. Verified. 8 × 0.75 × 1.0 = **6.0**.

**Categories:** Pain, People and Growth. All different, so each counts in full.
**Signal Score:** Stage 3 = 8.0 + 6.0 = 14.0. Stage 4 = 6.0. Total **20.0**.
**Gates:** pass. Not on the suppression list.
**Pattern:** Scaling and straining, plus scaling the back office.
**Decision:** **Research now.** Pain maps to POS and settlement (documented capabilities), so the capability check passes.
**Next action:** Find the owner and finance contact. Confirm the outlet count and payment methods. Qualify with the full framework. Possible angle: payments at the new outlet from day one and faster access to money (as Hubtel states, S48).

### Example B (hypothetical): attractive hotel with no actionable signal

**Account:** "Palm Court Hotel", a single-site hotel in Accra (fictional).
**Signals found:**
- Hotel wins a "best boutique hotel" award. Interesting, not actionable. **0**.
- SG-15: renovation announced, reopening date given, 100 days ago. Verified. 2 × 0.5 × 1.0 = **1.0**.

**Gates:** G4 fails (single site, no stated expansion plan).
**Signal Score:** 1.0, but the gate failure comes first.
**Decision:** **Excluded** (G4). Log the renovation signal.
**Next action:** Revisit if the hotel announces a second site. The lesson: a strong brand and a pleasant event do not make an account qualified.

### Example C (hypothetical): retail chain whose pain Hubtel cannot yet confirm it solves

**Account:** "Greenleaf Pharmacies", a six-branch pharmacy chain (fictional, secondary ICP).
**Signals found:**
- SG-01: seventh branch opened 60 days ago, shown on the chain's page and a map listing. Verified. 8 × 0.75 × 1.0 = **6.0**.
- SG-04: job post for a finance officer, 10 days ago. Single source (one job board). 6 × 1.0 × 0.75 = **4.5**.
- SG-06: new operations director on LinkedIn, 30 days ago. Single source. 4 × 1.0 × 0.75 = **3.0**.

**Categories:** Growth, People and People. Within People, the highest (SG-04, 4.5) counts in full and SG-06 at 50% (1.5).
**Signal Score:** Stage 3 = 4.5. Stage 4 = 6.0 + 1.5 = 7.5. Total **12.0**.
**Gates:** pass.
**Decision:** **Monitor.** Score is between 10 and 19.9. Also, the likely pain in a pharmacy chain is branch stock and cash reconciliation, and Product has not confirmed branch reporting or reconciliation.
**Next action:** Look for pain evidence (reviews, owner interviews). Ask Product about branch reporting. Re-check in 60 days. Do not contact yet.

### Example D (hypothetical): explicit intent

**Account:** "Serenity Spa & Salon", a three-branch spa group (fictional).
**Signal found:** SG-16, the business's official page asks followers: "Which POS works when the internet is down? Our payments keep failing." Posted two days ago.
**Gates:** pass. Not on the suppression list. Confirm the post is from the business, not a private person.
**Decision:** **Fast lane.** No score needed.
**Capability check:** no-internet payments through USSD are documented in Hubtel's own spa case study (S50), so the capability fit is a pass. Confirm the current set-up with Product.
**Next action:** Human review within two working days. Reply with an answer to the question asked and an offer of a short call, in line with the platform's rules. Record the signal and outcome.

### Example E (hypothetical): growth stacked in one category, with no pain

**Account:** "Coastline Hotels", a three-site hotel group (fictional).
**Signals found:**
- SG-01: fourth property opened this month. Verified. 8 × 1.0 × 1.0 = **8.0**.
- SG-02: the same property is in a new city, 10 days ago. Verified. 6 × 1.0 × 1.0 = **6.0**.
- SG-06: new general manager appointed 70 days ago. Single source. 4 × 0.75 × 0.75 = **2.25**.

**Categories:** Growth (SG-01 and SG-02) and People (SG-06). In Growth, SG-01 counts in full (8.0) and SG-02 at 50% (3.0), because both describe one expansion.
**Signal Score:** Stage 3 = 0. Stage 4 = 8.0 + 3.0 + 2.25 = 13.25, shown as 13.3. Total **13.3**.
**Gates:** pass. City is covered by Hubtel (confirm with Commercial).
**Decision:** **Monitor.** No stage 3 pain evidence, so the account cannot reach Research now or Qualified.
**Next action:** Look for pain evidence (reviews, provider mentions). Check payment methods at the new property. If SG-07 or SG-08 appears, re-score. The lesson: strong timing without evidence of the problem is a prompt to research, not to contact.

## How to use this day to day

1. **Collect:** run the detection routines in the matrix against the segment list (new listings, job boards, social pages, press).
2. **Log:** record every sighting in the signal log, with source and date.
3. **Verify:** confirm with a second source or a primary source. Check for false positives listed on the signal card.
4. **Score and decide:** apply the formula and the research decision table.
5. **Review weekly:** a human reviews Research now and Fast lane accounts. Monitor accounts are re-scored when new signals appear or after 90 days.
6. **Feed back:** record what happened to each account (replied, declined, no response, won). Use this to recalibrate.

## Calibration plan

| Question | How to answer it | When |
|---|---|---|
| Which signals preceded real wins? | Sales and Customer Success review of 10 recent small-business wins | Before first campaign |
| Can signals be found at all for target businesses? | Run detection on 20 accounts and count findings per source | Before first campaign |
| Are the thresholds right? | Compare scored status with human judgement on 20 accounts | After first batch |
| Do high-scoring accounts reply more? | Reply and meeting rates by status and pattern | After first campaign |
| Which signals produce false positives? | Log outcome of each false-positive check | Ongoing |

If few accounts reach Research now, review the segment and data sources before lowering thresholds.

## Confidence

- Structure (classes, formula, stacking, decision table): medium. Sound method, untested.
- Base points, multipliers and thresholds: low. Starting assumptions.
- Signal availability for small Ghanaian businesses: low. Untested.

## Knowledge gaps

- No win or loss data from Hubtel linked to signals.
- No tested data sources or coverage rates.
- First-party data availability and permitted use.
- Ghana data-protection rules.
- Product confirmation of branch, staff, reconciliation and audit capabilities.

## Next steps

1. Confirm the thresholds with Sales leadership and adjust to deal volume.
2. Run the 20-account detection test.
3. Add the signal log fields to the CRM or tracking sheet.
4. Move to P7, mapping the GTM revenue system, using the signals that survive testing.
