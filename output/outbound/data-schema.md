# Data Schema: New-Outlet Payments Setup Workflow

**Owner:** Go-to-Market Engineering | **Audience:** GTM engineers, Sales Ops | **Version:** 2026-W46 | **Status:** Design. No sheet, database or CRM field has been created.
Related: [workflow-spec.md](workflow-spec.md) | [workflow-architecture.md](workflow-architecture.md) | [qualification-rules.md](qualification-rules.md) | [qualification framework CRM fields](../../context/icp/icp-qualification-framework.md)

## 1. Summary

Eleven tables, linked by `account_id`. Phase 0 uses one spreadsheet tab per table. Later phases map the same fields to Clay tables and CRM objects. Principles:

1. **Every fact has a source URL and a date.** Unknown is stored as `unknown`, never blank and never guessed.
2. **Append, do not overwrite.** Signals, qualifications, approvals and outcomes are new rows. The latest row wins for display.
3. **IDs are stable.** An ID is never reused.
4. **Business-level data only.** Contacts are business roles. No private personal data beyond what outreach needs.
5. **Calculated fields are marked.** Humans edit inputs, not calculated results. Overrides carry a reason.

## 2. Tables

### 2.1 accounts

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| account_id | text | Yes | `ACC-0001` | Primary key. Never reused |
| business_name | text | Yes | | Trading name |
| name_variants | text list | No | | Alternate spellings, for matching |
| segment | enum | Yes | `hospitality`, `food_service`, `retail`, `other` | |
| sub_type | enum | No | `hotel`, `restaurant_group`, `cafe`, `spa_salon`, `venue`, `catering_bakery`, `other` | |
| city | enum | Yes | Approved city list | Greater Accra first |
| address_notes | text | No | | Public address only |
| outlet_count | integer | No | 1 or more, or `unknown` | |
| outlet_count_confidence | enum | Yes | `confirmed`, `estimated`, `unknown` | |
| ownership_type | enum | No | `owner_led`, `group_or_chain`, `franchise`, `unknown` | Large groups are excluded |
| payment_channels_observed | list | No | `cash`, `momo`, `card`, `qr`, `bank_transfer` | |
| staff_handling_money | enum | No | `evident`, `owner_only`, `unknown` | |
| owner_presence | enum | No | `not_at_every_outlet`, `always_on_site`, `unknown` | |
| operational_structure | enum | No | `documented`, `informal`, `unknown` | |
| current_provider | text | No | | If visible or stated |
| website_url | URL | No | | |
| social_urls | URL list | No | | |
| listing_url | URL | No | | |
| source_url | URL | Yes | | Where the account was found |
| source_date | date | Yes | `YYYY-MM-DD` | |
| suppression_flag | boolean | Yes | `true` if on suppression list | Checked every run |
| suppression_reason | enum | No | `customer`, `open_opportunity`, `opt_out`, `other` | |
| created_date | date | Yes | | |
| last_reviewed | date | No | | |
| reviewed_by | text | No | | |

### 2.2 signals

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| signal_row_id | text | Yes | `SIG-00001` | Primary key |
| account_id | text | Yes | FK to accounts | |
| signal_id | enum | Yes | `SG-01` to `SG-20` | From the signal matrix |
| class | enum | Yes | `explicit`, `strong`, `weak` | Derived from signal_id |
| category | enum | Yes | `growth`, `people`, `pain`, `payments`, `technology`, `capital`, `hubtel_side` | Derived |
| stage | enum | Yes | `pain` (stage 3), `trigger` (stage 4), `fast_lane` | Derived |
| observed_date | date | Yes | Date the event happened | Used for recency |
| detected_date | date | Yes | Date we found it | |
| source_url | URL | Yes | | |
| source_2_url | URL | No | | Second source if any |
| verification_level | enum | Yes | `verified`, `single_source`, `unconfirmed` | |
| evidence_note | text | Yes | One line: what was seen | No customer names or quotes from private individuals |
| base_points | number | Yes | From the scoring framework | Calculated |
| recency_multiplier | number | Yes | 1.0, 0.75, 0.5, 0.25, 0 | Calculated at score date |
| verification_multiplier | number | Yes | 1.0, 0.75, 0.5 | Calculated |
| points | number | Yes | base × recency × verification | Calculated |
| false_positive_checked | boolean | Yes | | |
| false_positive_note | text | No | | |
| entered_by | text | Yes | | |

### 2.3 qualifications

One row per scoring run per account.

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| qualification_id | text | Yes | `QUA-00001` | |
| account_id | text | Yes | FK | |
| run_date | date | Yes | | |
| rules_version | text | Yes | e.g. `qr-0.1` | Version of the rules file used |
| gates_failed | list | No | `G1` to `G8` | Empty if none |
| entry_condition_met | boolean | Yes | Verified SG-01, SG-02 or SG-03 in the last 180 days | |
| fit_score | number | Yes | 0 to 40 | Calculated |
| pain_score | number | Yes | 0 to 30 | Calculated |
| trigger_score | number | Yes | 0 to 20 | Calculated |
| signal_score | number | Yes | pain_score + trigger_score | Calculated |
| contact_score | number | Yes | 0 to 10 | Calculated |
| total_score | number | Yes | 0 to 100 | Calculated |
| capability_fit | enum | Yes | `pass`, `hold`, `not_checked` | From Product's confirmed list |
| capability_note | text | No | | |
| workflow_status | enum | Yes | See section 3 | |
| recheck_date | date | No | | |
| override_flag | boolean | Yes | | |
| override_reason | text | No | Required if override_flag is true | |
| reviewed_by | text | No | | |

### 2.4 contacts

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| contact_id | text | Yes | `CON-0001` | |
| account_id | text | Yes | FK | |
| full_name | text | Yes | | Business role holder |
| role_title | text | Yes | | As stated publicly |
| role_type | enum | Yes | `owner_md`, `gm`, `finance_ops`, `outlet_manager`, `other` | |
| buying_role | enum | Yes | `economic`, `functional`, `technical`, `influencer`, `unknown` | From the buying committee |
| channel_type | enum | Yes | `email`, `whatsapp_business`, `phone`, `linkedin`, `form` | |
| channel_value | text | Yes | | Business contact detail |
| channel_verified | boolean | Yes | | |
| source_url | URL | Yes | | |
| source_date | date | Yes | | |
| lawful_basis_note | text | Yes | | Filled after Legal guidance |
| status | enum | Yes | `active`, `invalid`, `opted_out` | |

### 2.5 enrichment_log

One row per field filled by a tool or by hand.

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| enrichment_id | text | Yes | `ENR-00001` | |
| account_id | text | Yes | FK | |
| contact_id | text | No | FK | |
| field_name | text | Yes | Name of the field filled | |
| value | text | Yes | | |
| provider | text | Yes | `manual`, `clay`, `treg:<provider>` | |
| source_url | URL | No | | |
| confidence | enum | Yes | `verified`, `likely`, `unknown` | |
| cost | number | Yes | 0 for manual | In the billing currency, recorded as given |
| cost_currency | text | No | | |
| run_id | text | Yes | FK to run_log | |
| date | date | Yes | | |

### 2.6 recommendations

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| recommendation_id | text | Yes | `REC-0001` | |
| account_id | text | Yes | FK | |
| contact_id | text | Yes | FK | Primary contact |
| lead_signal_row_id | text | Yes | FK to signals | The signal that justifies contact now |
| angle | enum | Yes | `faster_access_to_money`, `payments_at_counter`, `one_place_to_approve`, `new_site_setup`, `hold` | From the angle table in the spec |
| allowed_proof | list | Yes | Source IDs such as `S48`, `S50`, `S46`, `S47` | Attributed to Hubtel |
| forbidden_claims | list | Yes | Defaults to the standing list in the spec | |
| channel | enum | Yes | `email`, `whatsapp_business`, `phone`, `linkedin` | |
| rationale | text | Yes | Two to three lines | |
| created_date | date | Yes | | |

### 2.7 sequences and touches

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| touch_id | text | Yes | `TCH-00001` | |
| recommendation_id | text | Yes | FK | |
| touch_number | integer | Yes | 1 to 3 | |
| planned_date | date | Yes | | |
| channel | enum | Yes | As in recommendations | |
| draft_text | text | Yes | | Draft only until approved |
| facts_file_version | text | Yes | | Version of the approved facts file |
| copy_check | enum | Yes | `passed`, `failed`, `not_run` | Copy rules and banned phrases |
| status | enum | Yes | `draft`, `approved`, `sent`, `cancelled` | |
| sent_date | date | No | | Filled only after sending |

### 2.8 approvals

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| approval_id | text | Yes | `APP-00001` | |
| gate | enum | Yes | `HA1`, `HA2`, `HA3`, `HA4` | |
| object_type | enum | Yes | `source`, `account`, `override`, `sequence`, `spend` | |
| object_id | text | Yes | | ID of the item approved |
| decision | enum | Yes | `approved`, `edited`, `rejected` | |
| reason | text | Conditional | | Required for edits, rejections and overrides |
| approver | text | Yes | | |
| date | date | Yes | | |

### 2.9 outcomes

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| outcome_id | text | Yes | `OUT-00001` | |
| account_id | text | Yes | FK | |
| recommendation_id | text | Yes | FK | |
| outcome_code | enum | Yes | `replied_interested`, `replied_not_now`, `declined`, `opt_out`, `meeting_booked`, `no_response`, `bounced`, `wrong_person`, `referred` | |
| outcome_date | date | Yes | | |
| decline_reason | enum | Conditional | `has_provider`, `no_need`, `price`, `trust`, `timing`, `capability_gap`, `other` | Required if declined |
| stated_pain | text | No | | In their words, business only |
| capability_gap_noted | text | No | | Passed to Product |
| recheck_date | date | No | | |
| crm_record_id | text | No | | After handoff |
| notes | text | No | | |

### 2.10 suppression

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| suppression_id | text | Yes | `SUP-0001` | |
| business_name | text | Yes | | |
| match_keys | text list | Yes | Name variants, phone, domain, social URL | For matching |
| reason | enum | Yes | `customer`, `open_opportunity`, `opt_out`, `do_not_contact` | |
| source | text | Yes | Commercial export, CRM, reply | |
| added_date | date | Yes | | |

### 2.11 run_log

| Field | Type | Req | Allowed values or format | Notes |
|---|---|---|---|---|
| run_id | text | Yes | `RUN-0001` | |
| workflow | text | Yes | `W1` to `W7`, or `manual` | |
| start_time | datetime | Yes | | |
| end_time | datetime | No | | |
| accounts_in | integer | Yes | | |
| accounts_excluded | integer | Yes | | |
| accounts_advanced | integer | Yes | | |
| errors | integer | Yes | | |
| error_summary | text | No | | |
| spend_total | number | Yes | 0 for manual | |
| operator | text | Yes | | |

## 3. Enumerations

**workflow_status**

| Value | Meaning | Allowed action |
|---|---|---|
| `EXCLUDED` | Failed a gate or suppressed | None. Never contact |
| `LOG_ONLY` | Signal score below 10 | Record only |
| `MONITOR` | Signal score 10 to 19.9, or no pain evidence, or capability hold | Re-check on `recheck_date` |
| `RESEARCH_NOW` | Signal score 20 or more with a pain signal. Not yet scored as qualified | Enrich and re-score |
| `PILOT_REVIEW` | Total 55 to 69 with pain 10 or more and capability pass | HA2 may override to proceed |
| `QUALIFIED` | Total 70 or more with pain 10 or more and capability pass | Recommend, then HA3 |
| `FAST_LANE` | Verified explicit intent and gates pass | Human review within two working days |

**verification_level to multiplier:** `verified` 1.0, `single_source` 0.75, `unconfirmed` 0.5.

**recency multiplier by age:** 30 days or less 1.0; 31 to 90 0.75; 91 to 180 0.5; 181 to 365 0.25; over 365 0.

## 4. Relationships

```
accounts 1 --- n signals
accounts 1 --- n qualifications
accounts 1 --- n contacts
accounts 1 --- n enrichment_log
accounts 1 --- n recommendations --- n touches
accounts 1 --- n outcomes
approvals refer to any object by object_type and object_id
suppression is matched against accounts and contacts on every run
run_log is referenced by enrichment_log and every automated change
```

## 5. Validation rules

| Rule | Check |
|---|---|
| Source required | Every account, signal, contact and enrichment row has a `source_url` (except manual entries marked `manual`) |
| Dates | `observed_date` is not in the future and not before 2020-01-01. `detected_date` is on or after `observed_date` |
| No duplicate accounts | Same normalised name and city, or same URL, creates a flag and blocks insert |
| Signal ID valid | In `SG-01` to `SG-20` |
| Gate before score | No qualification row with a score if a gate failed. `workflow_status` is `EXCLUDED` |
| Override reason | `override_flag` requires `override_reason` and an HA2 approval row |
| Draft before send | A touch cannot be `sent` without an `approved` HA3 row |
| Suppression block | A suppressed account cannot have a recommendation or a touch |
| Opt-out permanence | An opt-out sets the contact `opted_out` and adds a suppression row |
| Cost recorded | Any paid enrichment row has a cost and an HA4 approval |
| Claims | `allowed_proof` values must exist in the facts file. `forbidden_claims` cannot be empty |
| Unknown allowed | `unknown` is valid wherever shown. Blank is not |

## 6. Spreadsheet layout (phase 0)

One workbook with tabs named after the tables: `accounts`, `signals`, `qualifications`, `contacts`, `enrichment_log`, `recommendations`, `touches`, `approvals`, `outcomes`, `suppression`, `run_log`, plus a `lists` tab with every enumeration for data-validation drop-downs, and a `rules` tab with the point tables.

- Lock header rows. Use drop-downs for enumerations.
- Keep calculated columns on a protected colour.
- Store the workbook outside any public repo. CSV and XLSX files are gitignored under `output/data/`.
- Save a dated copy after each weekly review.

## 7. Mapping to Clay and the CRM

| Schema | Clay | CRM |
|---|---|---|
| accounts | Accounts table | Company or Account object, plus custom fields |
| contacts | Contacts table | Contact object |
| signals | Account-linked rows or JSON column | Custom object or notes. Summary fields on the account |
| qualifications | Latest values as columns | Status and score fields on the account |
| recommendations, touches | Not stored. Held in n8n and the sheet until sending exists | Activities or tasks, once approved |
| approvals, run_log | Not stored | Audit note or a separate log |
| outcomes | Not stored | Activity outcomes, deal stage and loss reasons |
| suppression | Lookup table | Do-not-contact flags and a lookup list |

The CRM structure is unknown. Confirm object and field options with Sales Ops before building.

## 8. Data classification and retention

| Class | Examples | Handling |
|---|---|---|
| Business | Business name, address, outlets, signals | Internal. May be shared inside Hubtel |
| Business contact | Names, role titles, business email, business phone | Restricted. Business purpose only. Retention set with Legal |
| Secrets | API tokens, credentials | Never stored in sheets, docs or Git. Environment or credential store only |
| Financial | Tool spend | Internal |

Delete or anonymise contacts that opt out or decline when requested. Retention periods need Legal's input.

## 9. Example rows (hypothetical)

**These rows are hypothetical.** They are invented for illustration and do not describe a real business.

accounts

| account_id | business_name | segment | city | outlet_count | outlet_count_confidence | suppression_flag | source_url | source_date |
|---|---|---|---|---|---|---|---|---|
| ACC-0001 | Harbour Grill Group (hypothetical) | food_service | Accra | 4 | confirmed | false | https://example.com/harbour-grill-page | 2026-11-02 |

signals

| signal_row_id | account_id | signal_id | observed_date | verification_level | points | evidence_note |
|---|---|---|---|---|---|---|
| SIG-00001 | ACC-0001 | SG-01 | 2026-09-29 | verified | 6.0 | Fifth outlet announced on the group's page and in local press |
| SIG-00002 | ACC-0001 | SG-07 | 2026-10-24 | verified | 8.0 | Two reviews about failed card payments |
| SIG-00003 | ACC-0001 | SG-04 | 2026-10-29 | verified | 6.0 | Accounts officer post mentions daily sales reconciliation |

qualifications

| qualification_id | account_id | rules_version | fit_score | pain_score | trigger_score | contact_score | total_score | capability_fit | workflow_status |
|---|---|---|---|---|---|---|---|---|---|
| QUA-00001 | ACC-0001 | qr-0.1 | 40 | 14 | 6 | 5 | 65 | pass | PILOT_REVIEW |

The URLs above are placeholders.
