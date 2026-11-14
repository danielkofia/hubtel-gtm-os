# Workflow Specification: New-Outlet Payments Setup

**Owner:** Go-to-Market Engineering | **Audience:** GTM, Sales and leadership | **Version:** 2026-W46 | **Status:** Draft design. Nothing is built, activated or sent.
Related: [workflow-architecture.md](workflow-architecture.md) | [data-schema.md](data-schema.md) | [qualification-rules.md](qualification-rules.md) | [GTM system map](../../knowledge-base/playbooks/gtm-system-map.md) | [signal matrix](../../context/docs/research/signal-matrix.md) | [ICP](../../context/icp/ideal-customer-profile.md) | [buying committee](../../context/icp/buying-committee.md)

## 1. Summary

**Workflow:** when an owner-led hospitality or food-service business in Greater Accra opens or announces a new outlet, find it, verify it, check it against the ICP, look for evidence of payment pain, identify the buyer, and give a human a ready-to-approve outreach recommendation.

**Why this one:** it combines our strongest signal (new outlet, SG-01), the best-fit segment, public data and a natural reason to get in touch (the new site needs a payments set-up). It is also the easiest to test by hand before any tool is paid for.

**Scope of this document:** design only. No live outreach automation is built or activated. Every step has a manual version that works with a spreadsheet.

## 2. Choosing the workflow

Three candidates were compared. Scores run from 1 (poor) to 5 (strong). For difficulty and cost, 5 means easiest and cheapest. Weights and scores are our judgement, to be revisited after the pilot.

| Criterion | Weight | A. New outlet (SG-01, SG-02, SG-03) | B. Payment pain (SG-07, SG-08) | C. Finance hiring (SG-04) |
|---|---|---|---|---|
| ICP relevance | 20 | 5 | 5 | 4 |
| Signal strength | 20 | 5 | 4 | 3 |
| Data availability | 15 | 3 | 2 | 4 |
| Business value | 15 | 4 | 4 | 3 |
| Implementation ease | 10 | 3 | 2 | 4 |
| Cost (5 = cheapest) | 10 | 4 | 4 | 4 |
| Scalability | 10 | 3 | 2 | 4 |
| **Weighted score (out of 100)** | | **81** | **70** | **73** |

Score = sum of (weight × score) divided by 5.

| Candidate | Why it scored as it did |
|---|---|
| **A. New outlet** | High intent (SG-01 is rated High) and time-bound. Observable on business pages, listings and local news. The angle is concrete: set up payments at the new site. Detection is semi-manual at first because sources are untested |
| **B. Payment pain** | Strongest evidence of need when found (SG-08 is High). Reviews and complaints are scattered, low in volume and sensitive to use. Quoting or acting on customer reviews carries brand risk. Hard to automate and scale |
| **C. Finance hiring** | Easiest to detect because job posts are dated and name the employer. Intent is only Medium. Many posts are replacements or tax and audit roles. Weak ground for a specific angle |

**Sensitivity check.** A leads in both the weighted view and the two criteria that matter most (ICP relevance and signal strength). C wins only on data availability, ease and scalability. If the pilot shows that new-outlet signals cannot be found for most accounts, C is the fallback and its job-post data can serve as a corroborating signal inside workflow A.

**Design consequence of the ICP rules.** A new outlet is a trigger, not proof of pain. Our qualification rules require at least one pain-evidence signal before an account is Qualified. Workflow A therefore does two things: it acts on accounts that already show pain, and it **re-checks new-outlet accounts 30 days after opening**, when customer reviews and payment complaints become visible.

## 3. Business problem

Hubtel sells payments and back-office tools to owner-led, multi-outlet businesses. Today there is no repeatable way to know which of these businesses are at a payment decision point. Generic outreach arrives at the wrong time, and the team cannot tell whether a message failed because of timing, angle or fit.

A new outlet is a moment when an owner chooses tills, payment channels and settlement for the site and loses daily visibility of takings across sites. That moment is public and datable.

## 4. Intended outcome

- A weekly list of ranked, verified accounts, each with the signal, the evidence, the buyer, a recommended angle and a draft sequence ready for approval.
- A learning record: for each account, what we saw, what we did and what happened.
- Answers to three questions after the pilot:
  1. Can new-outlet signals be found reliably for target businesses?
  2. Do accounts with a verified new-outlet signal and pain evidence reply and book meetings more than accounts selected on fit alone?
  3. Which angle and channel work best?

No revenue or volume target is set. We have no baseline data. Set targets after the first batch.

## 5. Trigger

| Trigger | Description | Phase 0 (manual) |
|---|---|---|
| **T1 Weekly scan** | A scheduled scan of approved sources for new-outlet signals among target accounts | A person runs the scan once a week, in a fixed 90 minute slot |
| **T2 Re-check** | 30 days after a verified opening, re-check the account for pain evidence (reviews, provider mentions) | The sheet lists due re-checks every Monday |
| **T3 Inbound or referral** | An explicit-intent signal (SG-16 to SG-18). Uses the fast lane described in the signal framework | Handled by Sales. Logged in the same sheet |

## 6. Required inputs

| Input | Source | Status |
|---|---|---|
| ICP rules, gates, scoring | `context/icp/` | Documented |
| Signal definitions | `signal-matrix.md` | Documented, untested |
| Account universe | Stage 3 of the system map | Not built. Start with 20 to 50 accounts collected by hand |
| Suppression list (existing Hubtel customers, opt-outs, open opportunities) | Commercial and Sales | **Not requested yet. Blocks any outreach** |
| Confirmed capability list | Product | **Not requested yet. Blocks any claim beyond the documented ones** |
| Approved messaging and facts file | P5 | **Not started. Blocks drafts** |
| City coverage | Commercial | Hubtel says 8+ cities (S1). Confirm real coverage |
| Data-protection guidance | Legal | **Not requested yet** |

## 7. Data sources

All sources are candidates. Coverage and accuracy for small Ghanaian businesses are untested. Use only public, business-level data and respect each platform's terms. No login scraping.

| Purpose | Source | Method | Notes |
|---|---|---|---|
| New-outlet signal | Facebook and Instagram business pages, business websites | Manual weekly review, saved searches | Posts are often informal. Dates matter |
| New-outlet signal | Google Maps listings | Manual search by area and category | Shows new listings and photos |
| New-outlet signal | Local press, event and directory posts | Alerts and manual reading | |
| Corroboration | Job boards, LinkedIn jobs | Manual or alert | SG-04 corroborates growth |
| Pain evidence | Public reviews and posts | Manual | Use for insight only. Never quote customers in outreach |
| Buyer identification | LinkedIn, business pages | Manual | Business roles only |
| Provider clues | Photos of counters, decals, notices | Manual | Identifies incumbent where visible |
| First-party | Hubtel website, sign-ups, inbound | Internal export | Use only after Legal and Data confirm |
| Paid enrichment | Clay and treg providers | Later phases, one-record test first | Coverage for Ghana unknown |

## 8. Processing logic

The 12 steps follow the requested architecture. Each is written so that a person can do it in a spreadsheet today.

| # | Step | Action | Output | Decision rule |
|---|---|---|---|---|
| 1 | Detect | Scan sources for an opening, announcement or new listing | Candidate row: business name, location, URL, observed date | Keep only hospitality and food-service candidates. Otherwise discard |
| 2 | Identify | Match to an existing account or create one. Deduplicate on name, city and social or listing URL | Account ID | If it cannot be matched to a real business, discard |
| 3 | Verify | Confirm the new outlet with two sources or the business's own post. Record date and verification level | Signal row (SG-01, SG-02 or SG-03) | One source only: Single source. Fewer than that: Unconfirmed, no scoring until checked |
| 4 | ICP fit | Run gates G1 to G8 and the suppression check. Score fit | Gate results and fit score | Any gate failure: Excluded. Log the reason |
| 5 | Decision-makers | Identify owner or MD, GM, finance or operations lead | Contact rows with role and source | No business-role contact: hold at Research |
| 6 | Enrich | Fill required fields (section 11) | Enriched account record | Missing required fields stay "unknown" and score at neutral |
| 7 | Score and prioritise | Add pain evidence, triggers and contactability. Apply the capability check | Score, status, rank | Apply [qualification-rules.md](qualification-rules.md) |
| 8 | Recommend | Choose angle, lead signal, allowed proof and forbidden claims | Outreach recommendation card | Only documented capabilities. No unverified numbers |
| 9 | Prepare sequence | Draft a short sequence for the chosen channel, as drafts only | Sequence draft (not sent) | Needs the facts file and approved messaging |
| 10 | Human approval | Reviewer approves, edits or rejects | Approval record | No approval, no send |
| 11 | Record outcome | Log sent date, reply, meeting, decline, no response | Outcome row | Every account gets an outcome or a recheck date |
| 12 | Learn | Weekly review compares outcomes with scores, signals and angles | Change log | Adjust only with evidence, and record the change |

### Sequence preparation (step 9)

Design parameters, to be agreed with Sales:
- Up to three touches over about two weeks, then stop.
- Touch 1 refers to the verified new outlet and the set-up question. Later touches add one new useful point each. No repeat of the first message.
- Channels are tested one at a time: email, WhatsApp Business, phone, LinkedIn. Which is allowed and effective in this segment is **unknown**.
- Pause for 90 days after any decline. Stop at once after an opt-out.
- No copy is written in this phase. Copy depends on the facts file and approved messaging.

### Outreach angle options (directions, not copy)

| Condition | Angle direction | Allowed proof |
|---|---|---|
| New outlet verified, no pain evidence | Not eligible for outreach. Re-check at day 30 | n/a |
| New outlet and provider or settlement frustration | Faster access to money across sites | "Hubtel states" hourly crediting and sweeps (S48) |
| New outlet and till complaints or connectivity problems | Payments that keep working at the counter | "Hubtel states" USSD works without internet (S50) |
| New outlet and finance hire or several payment instructions | One place to see and approve money | "Hubtel states" approvals and payroll (S46, S47) |
| Pain maps only to unconfirmed capabilities | Hold | None. Ask Product |

## 9. Qualification criteria

Summary. Full rules are in [qualification-rules.md](qualification-rules.md).
- Passes gates G1 to G8. Is not on the suppression list.
- A verified new-outlet signal in the last 180 days.
- At least one pain-evidence signal (stage 3), or an explicit-intent signal.
- Capability fit passes for the strongest pain.
- A reachable business-role contact.
- Total score meets the Qualified threshold, or a documented reviewer override during the pilot.

## 10. Scoring logic

Uses the [signal scoring framework](../../context/docs/research/signal-scoring-framework.md): signal points = base × recency × verification. Different categories add in full, same-category signals add at 50% after the highest. Stage 3 is capped at 30 and stage 4 at 20. Total = fit (40) + pain (30) + triggers (20) + contactability (10).

**Calibration warning.** A total of 70 needs near-maximum fit plus real pain evidence plus a fresh trigger. Because unknown fields score at a neutral value, few early accounts may reach 70. The pilot setting in the qualification rules allows documented reviewer overrides for accounts with a total from 55 to 69. This is a pilot setting, not a change to the ICP framework. Confirm it with Sales.

## 11. Enrichment requirements

| Level | Fields |
|---|---|
| **Required** to qualify | Business name, city, outlet count and confidence, new-outlet evidence URL and date, at least one business-role contact with channel, suppression check |
| **Needed** to score | Payment channels observed, staff handling money, owner presence, operational structure, pain evidence URLs |
| **Useful** | Current provider, social and listing URLs, company website, seasonality, outlet addresses |
| **Not collected** | Private personal details, personal phone numbers not used for business, anything not needed for outreach |

Every field carries a source URL and date. See [data-schema.md](data-schema.md).

## 12. Output

| Output | Format | Consumer |
|---|---|---|
| Weekly ranked list | Sheet view, later CRM view | Sales lead |
| Outreach recommendation card per account | One row or record, fields in the schema | Reviewer |
| Sequence draft per approved account | Draft text, not sent | Reviewer |
| Approval log | Sheet rows | Audit |
| Outcome log | Sheet rows | GTM optimisation |
| Weekly learning note | Markdown in the work log | Team |
| CRM-ready record for accounts that book a meeting | Fields mapped in the schema | Sales |

## 13. Failure handling

| Failure | Detection | Response |
|---|---|---|
| Signal cannot be verified | Fewer than one credible source | Keep at Unconfirmed. Do not score above 0.5 multiplier. Re-check in 14 days |
| Name collision or wrong business | Mismatch on city, URL or photos | Discard and note |
| Duplicate account | Same name, city and URL | Merge and keep the earliest record |
| Existing Hubtel customer or open opportunity | Suppression match | Exclude. Never contact |
| Data source unavailable or blocked | Empty scan or error | Skip for the week, log, use another source. Do not work around platform rules |
| Contact not found | No business-role contact | Hold at Research. Set a recheck date |
| Contact channel invalid | Bounce, wrong number | Mark invalid. Try another channel only if allowed |
| Capability unconfirmed | Pain maps to an unconfirmed capability | Hold. Ask Product. Do not draft claims |
| Paid lookup fails or returns no data | Empty or error response | Do not retry in a loop. Log cost and result. Fall back to manual |
| Spend limit reached | Counter exceeds the approved cap | Stop paid calls. Alert owner |
| Reviewer unavailable | Batch not reviewed in 5 working days | Batch expires. Re-score before use |
| Scoring script error (later phases) | Error log | Stop the run. Do not default to Qualified |

Principle: **fail closed.** If a check cannot run, the account is not sent to outreach.

## 14. Human approval

| Point | Decision | Approver | Rule |
|---|---|---|---|
| HA1 List and sources | Which sources and which accounts enter the workflow | GTM Engineering lead | Test sources on 20 accounts first |
| HA2 Qualification | Confirm the status and any pilot override | GTM Engineering and Sales | Record the reason for every override |
| HA3 Messages | Approve each message and each batch | Sales lead | Claims only from the facts file. Attributed to Hubtel. No unverified numbers. No customer names without permission. No em dashes in copy |
| HA4 Spend | Approve any paid lookup or tool | Budget owner | Cap per run set in advance |

**Nothing is sent without HA3.** In this project phase, nothing is sent at all.

## 15. Compliance considerations

These are design requirements, not legal advice. Legal must review before any list is built or message is sent.

| Area | Requirement |
|---|---|
| **Data protection** | Ghana's data-protection rules for collecting and using contact data have not been researched. Confirm with Legal. Collect business-level data and business-role contacts only. Record the source and the basis for each contact |
| **Platform terms** | No scraping of sites that forbid it. No login scraping. Use manual review or permitted tools |
| **Messaging channel rules** | Check the rules for each channel, including WhatsApp Business and LinkedIn, before use |
| **Opt-out** | Every message gives a clear way to opt out. Opt-outs are logged and honoured permanently |
| **Public reviews** | Use reviews as private insight. Do not quote, tag or reference named customers |
| **Claims** | Only documented capabilities, attributed to Hubtel. Branch dashboards, per-staff tracking, automated reconciliation, audit logs and pricing stay off limits until confirmed |
| **Existing customers** | Excluded from acquisition outreach |
| **Spend** | No paid lookups without approval |
| **Data retention** | Set a retention period with Legal. Delete declined or opt-out contact data on request |
| **Secrets** | Keys in `.env` only. Names only in documents. `.env` is gitignored |

## 16. Measurement framework

| Stage | Metric | Why |
|---|---|---|
| Detection | New-outlet signals found per week; share verified | Does detection work? |
| Fit | Share passing gates; share per status | Is the list clean? |
| Pain check | Share of new-outlet accounts with pain evidence at day 0 and at day 30 | Does the day-30 re-check add value? |
| Review | Human agreement rate with scored status | Is the scoring trusted? |
| Outreach | Messages approved; sent; reply rate by angle and channel | What works? |
| Meetings | Meetings per 100 contacted; show rate | Are replies useful? |
| Pipeline | Handoff completeness; opportunity rate | Does it reach Sales? |
| Cost | Time per account; paid-data cost per verified account | Is it affordable? |
| Quality | False-positive rate; opt-out rate; complaints | Is it safe? |

**Test design.** Hold back a small comparison group chosen on fit alone, with no signal. Compare reply and meeting rates between the two groups. Without a comparison group, we will not know whether signals help. Group sizes need Sales input.

**Targets.** None are set. Set them after the first batch and record them in the work log.

**Review cadence.** Weekly 30-minute review of the batch and outcomes. Monthly recalibration of weights and thresholds.

## 17. Implementation requirements

| Requirement | Detail | Status |
|---|---|---|
| People | A GTM engineer to run it, a reviewer from Sales, and a budget owner | To assign |
| Time (phase 0) | About 90 minutes for the scan, plus 3 to 5 hours of research and review per weekly batch of about 10 accounts. These are estimates and need testing | Estimate |
| Tools (phase 0) | Spreadsheet with the schema, browser, Claude Code for drafting and scoring formulas | Available |
| Access | Suppression list, capability list, CRM access, Legal guidance | Not requested |
| Content | Facts file and approved messaging (P5), message copy (P9) | Not started |
| Budget | None needed for phase 0. Later tools carry costs that are not yet known | None approved |
| Later phases | Clay, n8n, treg and CRM per [workflow-architecture.md](workflow-architecture.md) | Not built |

**Definition of done for phase 0:** 20 accounts processed end to end by hand, a reviewer has checked them, and the pilot report answers the three questions in section 4.

## 18. Out of scope for this workflow

- Sending or scheduling any live outreach.
- Any paid data lookup.
- Retail accounts (secondary ICP) until Product confirms branch and reconciliation capabilities.
- Marketplace sellers, gaming, large enterprise accounts and existing Hubtel customers.
- Pricing offers.

## 19. Confidence

- Workflow choice: medium. Reasoned from our own documents, with no deal data.
- Step design: medium. Standard practice, untested here.
- Scores, thresholds, cadence and time estimates: low. Starting assumptions.
- Data availability for Ghanaian target businesses: low. Untested.

## 20. Open questions

1. Can the suppression list be provided, and in what format?
2. Which channels does Sales use and which are allowed?
3. How many accounts can Sales act on each week?
4. Is the pilot override range (55 to 69) acceptable?
5. Does Hubtel already have a CRM and a data-enrichment tool?
