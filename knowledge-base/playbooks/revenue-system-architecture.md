# Revenue System Architecture

**Owner:** Go-to-Market Engineering | **Audience:** GTM, Sales, Sales Ops and leadership | **Version:** 2026-W46
Companion: [gtm-system-map.md](gtm-system-map.md) (the 15 stages and handoffs). Related: [signal scoring framework](../../context/docs/research/signal-scoring-framework.md), [qualification framework](../../context/icp/icp-qualification-framework.md).

## Summary

This document describes how the 15-stage system is built: the data it holds, the tools it needs, where humans decide, the controls that protect data and brand, the metrics, and a phased build plan. It is deliberately simple. **Start with a spreadsheet and a human reviewer, prove the signals work, then add a CRM and automation.**

Design principles:
1. **One account record, many linked tables.** Every stage reads and writes the same account ID.
2. **Every field has a source and a date.** Unknown stays unknown.
3. **Humans decide at four points:** list approval, qualification review, message approval, and handoff to Sales.
4. **Automate only what has been proven by hand.**
5. **Outcomes flow back.** Stage 14 results change stages 4, 5 and 9.

## Architecture in layers

| Layer | Purpose | Contents |
|---|---|---|
| **Knowledge** | What we know and how sure we are | Research files, source register, ICP, buying committee, signal matrix, messaging facts |
| **Data** | Accounts, signals, contacts, activity, outcomes | Tables below, in a sheet first, then in the CRM |
| **Logic** | Rules that turn data into decisions | Gates, scoring formula, status rules, suppression, capability check |
| **Workflow** | Steps and handoffs | The 15 stages, review gates, task queues |
| **Channel** | How we reach people | Email, WhatsApp business, phone, LinkedIn, in-person (all to be tested) |
| **Control** | Safety and quality | Suppression, data protection, copy rules, approvals, audit trail |
| **Measurement** | Learning | Funnel metrics, score-band performance, review cadence |

## Data model

Seven core tables. Field names align with the CRM fields in the [qualification framework](../../context/icp/icp-qualification-framework.md) and the signal log fields in the scoring framework.

| Table | Key fields | Created at stage | Written by |
|---|---|---|---|
| **Account** | account_id, name, segment, city, outlet_count, outlet_count_confidence, payment_channels_observed, staff_handling_money, current_provider, source_url, source_date, suppression_flag | 3 | GTM Engineering |
| **Signal** | signal_id (SG-xx), account_id, class, category, observed_date, detected_date, source_url, verification_level, evidence_note, points | 4 | GTM Engineering |
| **Qualification** | account_id, gates_failed, fit_score, pain_score, trigger_score, contact_score, total_score, capability_fit, status, reviewed_by, review_date | 5 | GTM Engineering, human reviewer |
| **Contact** | contact_id, account_id, name, role, channel, channel_verified, source_url, source_date, consent_notes | 6, 7 | GTM Engineering |
| **Outreach** | outreach_id, account_id, contact_id, channel, angle, lead_signal_id, message_version, sent_date, approved_by, reply_status | 9, 10 | GTM Engineering, Sales |
| **Meeting and opportunity** | opportunity_id, account_id, meeting_date, attendees, stated_pain, stage, owner, value (if known), outcome, outcome_reason | 11 to 13 | Sales |
| **Feedback** | account_id, outcome, reason, objections, capability_gaps, reference_permission, notes_date | 14 | Sales, Customer Success |

**Keys and rules:**
- `account_id` is the single key across all tables. Deduplicate on normalised name plus city plus a social or listing URL.
- Signals are never overwritten. A new observation creates a new row.
- Status is calculated. Humans may override it, but the reason is recorded.
- A suppressed account (existing Hubtel customer) is flagged at creation and cannot be moved to stage 9.

## Account lifecycle

| State | Entered when | Next states |
|---|---|---|
| Identified | Account added at stage 3 | Excluded, Monitoring |
| Monitoring | Passed gates, below research threshold | Research now, Not now |
| Research now | Signal Score 20 or more with a pain signal | Qualified, Not now |
| Qualified | Total score 70 or more, capability pass, human reviewed | Contacted |
| Fast lane | Explicit intent and gates pass | Engaged |
| Contacted | First message sent | Engaged, No response |
| Engaged | Reply received | Meeting booked, Declined |
| Meeting booked | Meeting scheduled | Opportunity, Declined |
| Opportunity | Handed to Sales in the CRM | Won, Lost, Stalled |
| Customer | Won | Out of acquisition scope (account management) |
| Excluded or Declined | Gate failed, or declined | Recheck date set |

Recheck dates stop declined or stalled accounts from being forgotten or over-contacted.

## Components and tools

Only listed tools exist today. Everything else is a need, not a purchase.

| Need | Today | Phase 1 option | Later |
|---|---|---|---|
| Knowledge and documents | Git repo, Notion MCP (connected, unused for content), Miro (connected, unused) | Same | Same |
| Account and signal tables | None | Spreadsheet with locked headers and validation lists | CRM |
| CRM | Unknown. Hubtel Sales may already have one | Use Hubtel's CRM if it exists. Confirm with Sales Ops | Add custom fields from this model |
| Data sources | Public pages, search | Manual collection from the tested sources | Automated enrichment |
| Contact data | Manual | Manual from LinkedIn and business pages | Paid enrichment (treg is deferred, no budget approved) |
| Outreach channel tools | None | Manual send from approved accounts | Sequencing tool after approval |
| Workflow automation | None | Task checklist and a weekly review | Scripts or the imported kit's tools, only after approval |
| Reporting | None | Pivot tables on the sheet | CRM dashboards |

**Imported tools not in use.** `tools/rex` (Clay), `tools/crawl4ai` and `tools/agent-browser` are imported but not installed. The Clay-based skills need accounts we do not have. Do not install or run any without approval.

**Decisions needed:** which CRM, which outbound channel, who owns the data, and who approves spend.

## Where humans decide

| Gate | Decision | Who | Rule |
|---|---|---|---|
| H1 List approval | Which source and which accounts enter the list | GTM Engineering lead | Test first on 20 accounts |
| H2 Qualification review | Confirm Qualified or Research now status | GTM Engineering plus Sales | Review the first 20, then a weekly sample |
| H3 Message approval | Approve copy and each batch | Sales lead | Claims limited to documented capabilities. No unverified numbers. No customer names without permission |
| H4 Handoff | Accept the opportunity | Sales owner | Needs stated pain and meeting notes |

Explicit-intent fast-lane leads skip H1 and H2 but still pass the gates, the suppression check and H3.

## Controls

| Area | Control |
|---|---|
| **Suppression** | Existing Hubtel customers, current opportunities and opt-outs are removed before every batch |
| **Data protection** | Collect business-level data and business-role contacts only. Review Ghana data-protection obligations with Legal before building lists or sending outreach |
| **Claims** | Messaging uses only documented capabilities and attributes figures to Hubtel. Branch dashboards, per-staff tracking, automated reconciliation, audit logs and pricing are off limits until confirmed |
| **Copy rules** | No em dashes in marketing copy. Follow the playbook rules in `knowledge-base/playbooks/copy-iron-laws.md` and `copy-bans.yaml` |
| **Contact limits** | A maximum number of touches per account, and a pause after a decline. Set the limits before the first batch |
| **Audit trail** | Every signal, status change and message has a date, a source and a person |
| **Spend** | No paid lookups or tools without approval |
| **Publishing** | Nothing is published or sent without approval |

## Metrics

No benchmarks are assumed. Measure first, then set targets.

| Stage group | Metrics |
|---|---|
| Identification and signals (3, 4) | Accounts found per source; signals per account; false-positive rate |
| Qualification (5) | Share Qualified; human agreement rate |
| Contact and enrichment (6, 7) | Share with verified decision-maker; field completeness; bounce or wrong-number rate |
| Outreach (9, 10) | Reply rate by angle, signal and channel; time to first response |
| Meetings (11) | Meetings per 100 contacted; show rate |
| Pipeline (12, 13) | Handoff completeness; stage conversion; cycle time; objection frequency |
| Outcomes (14) | Win rate by score band and signal pattern; time to first value; capability gaps cited |
| System (15) | Improvement per monthly review; time from signal to first touch |

**Key diagnostic:** compare outcomes by score band. If higher bands do not convert better, the scoring is wrong.

## Roles

| Role | Responsibility | Stages |
|---|---|---|
| GTM Engineering | Build and run the data, scoring and workflow. Draft messages. Run reviews | 1 to 9, 12, 15 |
| Sales | Approve and send outreach, run conversations, own opportunities | 9 to 13 |
| Sales Ops | CRM set-up, data quality, reporting | 12, 13 |
| Product | Confirm capabilities, receive capability-gap feedback | 5, 10, 14 |
| Commercial | Provide the customer list, pricing, sales motion | 3, 10, 13 |
| Customer Success | Onboarding feedback, references | 14 |
| Legal and Data | Data-protection guidance | 3, 6, 7, 9 |
| Leadership | Approve scope and spend | All |

Roles are proposed. Confirm the real team structure.

## Build plan

| Phase | Goal | Build | Exit test |
|---|---|---|---|
| **0: Foundations** | Ready to test | Dependencies requested (customer list, capabilities, pricing, CRM, Legal). Spreadsheet with the data model. Signal log template | Dependencies answered or scoped |
| **1: Manual pilot** | Prove signals exist and predict interest | Run stages 3 to 8 by hand on 20 accounts. Review them with Sales | Human agreement on status. Signals found for most accounts |
| **2: Outbound test** | Learn what gets replies | Draft messaging (P5), workflow (P8) and copy (P9). Send a small approved batch from stage 9 | Reply and meeting data by angle |
| **3: CRM and handoff** | Connect to the pipeline | Set up CRM fields and handoff (stage 12). Track opportunities | Complete records for every handoff |
| **4: Optimise** | Improve with data | Monthly reviews, recalibration, structured feedback (stages 14, 15) | Documented changes linked to data |
| **5: Automate** | Reduce manual effort | Automate only stable, proven steps, after approval and budget | Same accuracy at lower effort |

Do not skip phase 1. Without it, automation would scale untested assumptions.

## Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Signals are hard to find for small businesses | The pipeline is thin | Phase 1 test; widen sources; revisit the segment before loosening gates |
| Product cannot support the main pain | Qualified accounts cannot be served | Capability check; Product input |
| Hubtel's existing customers receive outreach | Brand harm | Suppression list before every batch |
| Data-protection breach | Legal and reputational harm | Legal review; business-level data only |
| Overclaiming | Trust and compliance harm | Facts file; human message approval |
| Over-engineering early | Time wasted | Phased plan; manual first |
| Weak feedback loop | The system does not improve | Required outcome reasons at stages 13 and 14 |
| Pricing and sales motion unknown | Stage 10 and 13 cannot be designed | Request from Commercial |

## Open decisions

1. Which CRM, and who owns it.
2. Primary outbound channel (email, WhatsApp business, phone, LinkedIn). Test with Sales.
3. First batch size, based on Sales capacity.
4. Contact frequency limits.
5. Whether secondary ICP (retail) is tested in the first batch or held until capability confirmation.
6. Whether first-party Hubtel data (website, sign-ups, inbound) can be used in signal detection (SG-19).

## Confidence

- Architecture and data model: medium. Standard practice, adapted to our documents.
- Tooling and roles: low. We do not know Hubtel's actual stack or team.
- Metrics and targets: not set. No data yet.
- Phase timings: not set. They depend on Sales capacity and approvals.

## Next steps

1. Create the spreadsheet with the data model and the signal log.
2. Send the dependency requests listed in the system map.
3. Run phase 1 on 20 accounts.
4. Start P5 (positioning and messaging), which blocks stage 9.
