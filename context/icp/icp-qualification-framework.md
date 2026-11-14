# ICP Qualification Framework

**Owner:** Go-to-Market Engineering | **Audience:** GTM, Sales and leadership | **Version:** 2026-W46
Companion to [ideal-customer-profile.md](ideal-customer-profile.md) and [buying-committee.md](buying-committee.md). S# = source ID in the [source register](../docs/research/source-register.md).

## Summary

This framework turns the ICP into a repeatable way to decide which businesses to target, which to avoid and why. Industry never qualifies an account on its own. An account moves through seven stages: (0) scope, (1) hard gates, (2) structural fit, (3) evidence of pain, (4) triggers and timing, (5) capability-fit check, and (6) contactability. Only accounts that pass the gates and score well on **both** fit and pain evidence are targeted.

**Calibration.** Weights, thresholds and parameters are our starting assumptions, not derived from Hubtel or market data. We will adjust them after a human reviews the first 20 to 30 accounts and after the first campaign results.

**Capability rule.** We do not score an account on a pain that Hubtel cannot address today. Branch dashboards, per-staff tracking, automated reconciliation and audit logs are not documented in the material reviewed. Product must confirm them (stage 5) before we promise them.

## Principles

1. **Industry is a filter, never a qualifier.** A hotel is not qualified because it is a hotel.
2. **Structure plus evidence.** Qualify on structural fit (outlets, channels, staff handling money) and on **observable evidence** of the pain or a trigger.
3. **Every field has a source and an evidence label.** No field without a data source.
4. **Unknown is not zero and not a pass.** Unknown scores neutral and is flagged for research.
5. **Humans validate before outreach.** Automated scoring proposes. A person approves the target list.
6. **Do not use unverified numbers** (for example 15,000 merchants or 1 million daily transactions) as criteria. They were dropped in Pass 2 (C4, C5).

## Stage 0: Scope and sourcing

Define the universe before scoring.

| Item | Rule |
|---|---|
| Segment | Primary: multi-outlet hospitality and food service. Secondary: multi-branch retail |
| Geography | Greater Accra first. Add a city only after confirming Hubtel operates there (homepage says 8+ cities, S1; more after a Nov 2025 rollout, search summary) |
| Candidate sources (all unverified as data sources, to be tested) | Business registries (Registrar General), tourism and hospitality licensing and trade body lists, Google Maps and map listings, Facebook and Instagram business pages, LinkedIn company pages, news and local directories, job boards |
| Excluded sources | Anything requiring login scraping against terms; any personal data not needed |
| Suppression list | Hubtel's existing customers, supplied by Commercial, removed before scoring |
| Collection rule | Collect only business-level data and business-role contact details needed for outreach. Check data-protection obligations in Ghana before building any list (**not researched**) |

## Stage 1: Hard gates (pass or fail)

Any fail excludes the account. Record the failing gate and date.

| Gate | Pass condition | Evidence label | How to check |
|---|---|---|---|
| G1 Real and operating | Business appears active (recent posts, reviews, listing) | H | Public listings |
| G2 In scope geography | Located in an approved city | H | Address |
| G3 Not simple collection only | Has staff-handled counters or several channels | V that Hubtel excludes simple collection (S1) | Website, listings |
| G4 More than one outlet or site, or a credible expansion plan | 2 or more outlets, or a public plan | H | Website, listings, news |
| G5 Accepts or wants digital payments | Shows mobile money, card or QR acceptance, or complains about it | H (adoption concentrated in Accra and regional capitals, S24, snippet-level) | Photos, posts, reviews |
| G6 Not an existing Hubtel customer | Not on Hubtel's customer list | V once checked | Match against Hubtel's customer records (request from Commercial). Public signs such as decals are a backup check |
| G7 Not a different motion | Not a Hubtel Food partner whose only link is the marketplace; not a large group with central procurement; not a regulated financial institution; not betting or gaming | H, scope decision | Listings, group structure |
| G8 Contactable | A business role (not a private individual) can be reached through a public business channel | H | Page, listing |

## Stage 2: Structural fit score (0 to 40)

Scores are starting assumptions. Unknown scores the mid value and sets a research flag.

| Criterion | Evidence for criterion | Scoring (H) | Max |
|---|---|---|---|
| Outlet count | Pain depends on several sites (S2, S3, V that Hubtel says so) | 1 outlet: gate fail. 2 to 3: 8. 4 to 15: 12. More than 15: 6 (different buyer). Unknown: 6 | 12 |
| Payment channel mix | Several channels create the verification pain (S2) | One channel: 0. Two: 5. Three or more: 8. Unknown: 4 | 8 |
| Staff handle money | Control page addresses this (S3) | Evident cashiers or waiting staff taking money: 8. Owner takes all: 2. Unknown: 4 | 8 |
| Owner distance from daily operations | Owner cannot see money without asking staff (S3) | Owner not at every outlet: 6. Owner on site always: 2. Unknown: 3 | 6 |
| Operational maturity | "Scale-ready" is Hubtel's undefined term (S1) | Documented structure (managers, finance role): 6. Informal: 2. Unknown: 3 | 6 |

## Stage 3: Evidence of pain (0 to 30)

Pain must be **observed**, not inferred from industry. Detailed signal definitions and point values are in the [signal matrix](../docs/research/signal-matrix.md) and [signal scoring framework](../docs/research/signal-scoring-framework.md), which keep the stage 3 cap of 30 and the stage 4 cap of 20. At least **one** piece of evidence is required for an account to be Qualified.

| Evidence type | Example source | Points (H) |
|---|---|---|
| Public complaints about payment failure or slow service at the till | Reviews, social comments | 0 to 10 |
| Publicly stated frustration with a current payment provider or terminal | Posts, interviews | 0 to 10 |
| Signals of manual cash handling and consolidation (for example job posts for accounts or reconciliation roles) | Job boards | 0 to 6 |
| Multiple different payment instructions to customers (several MoMo numbers, bank accounts) | Menus, receipts, social images. **V** that Hubtel names this problem (S2) | 0 to 4 |

Cap: 30. No evidence found scores 0 and the account cannot be Qualified.

## Stage 4: Triggers and timing (0 to 20)

| Trigger | Points (H) | Recency rule |
|---|---|---|
| New outlet announced or opened | 0 to 8 | Within last 6 months |
| Leadership or finance hire | 0 to 4 | Within last 6 months |
| Fast growth signals (new venue, franchise, funding news) | 0 to 4 | Within last 12 months |
| Seasonal or event preparation that stresses payments (hospitality) | 0 to 2 | Upcoming 3 months |
| Hubtel product event relevant to the account (for example BackOffice take-payment features, planned in S49, launch not verified) | 0 to 2 | Only after launch is confirmed |

Triggers decay. Re-score every 90 days. A strong trigger with no pain evidence is a prompt to research, not to contact.

## Stage 5: Capability-fit check (human, pass or hold)

Before an account is told Hubtel can solve a problem, confirm that Hubtel's documented product addresses it.

| Account need | Documented in sources read? | Action |
|---|---|---|
| Faster settlement and sweeps | Yes (S48, Hubtel claim) | May reference as "Hubtel states" |
| Approval workflow for payments out, payroll | Yes (S46, S47) | May reference |
| Accept cash, card, mobile money at POS | Yes (S51, vendor case) | May reference. Check which terminals and acquirers |
| Payments without internet (USSD) | Yes (S50, vendor case) | May reference |
| Branch-level reporting across outlets | **No** | **Hold. Verify before promising** |
| Per-staff sales attribution on POS | **No** (only in the custom insurance portal, S33) | **Hold** |
| Automated reconciliation | **No** (a planned feature, S49) | **Hold** |
| Audit log | **No** (not described in S47) | **Hold** |
| Pricing and fee comparison | **No** (S52, S53) | Do not quote |

If an account's strongest pain maps only to "Hold" capabilities, the account goes to **Research** until Product confirms the capability, however strong its pain.

## Stage 6: Contactability and buyer clarity (0 to 10)

| Item | Points (H) |
|---|---|
| Owner or senior decision-maker identifiable from public sources | 0 to 4 |
| Finance or operations lead identifiable | 0 to 3 |
| Public business channel responsive (email, WhatsApp business, LinkedIn) | 0 to 3 |

## Total score and status

Total = Stage 2 (40) + Stage 3 (30) + Stage 4 (20) + Stage 6 (10) = **100**. Thresholds are starting assumptions.

| Status | Rule | Action |
|---|---|---|
| **Qualified** | Passes all gates; total 70 or more; Stage 3 at least 10; Stage 5 passes for the strongest pain | Human review, then outreach |
| **Research** | Passes gates; total 40 to 69, or Stage 3 below 10, or Stage 5 on hold | Research more; monitor triggers; revisit in 90 days |
| **Not now** | Passes gates; total below 40 | No active outreach |
| **Excluded** | Fails any gate | Record reason; do not contact |

### Worked example (hypothetical accounts for illustration)

| | Account 1 | Account 2 |
|---|---|---|
| Description | Four-site restaurant group in Accra, complaints about slow card payments, opened a fourth outlet this quarter | Hotel group with 12 sites, no public pain evidence, strong industry fit |
| Gates | All pass | All pass |
| Stage 2 | 12 + 8 + 8 + 6 + 6 = 40 | 12 + 5 + 8 + 4 + 3 = 32 |
| Stage 3 | 14 | 0 |
| Stage 4 | 8 | 0 |
| Stage 6 | 8 | 3 |
| Total | 70 | 35 |
| Stage 5 | Pain maps to POS and settlement (documented): pass | n/a |
| Status | **Qualified** | **Research** (right industry, no evidence of pain, total 35) |

Account 2 fits the industry but is not qualified.

## CRM field design

Fields to create in the CRM or tracking sheet. The CRM has not yet been chosen.

| Field | Type | Values | Source | Evidence label |
|---|---|---|---|---|
| account_name | text | | registry or listing | V |
| segment | pick-list | hospitality, retail, other | classification | H |
| city | pick-list | approved cities | listing | V |
| outlet_count | number | | website, listings | H (needs a check each time) |
| outlet_count_confidence | pick-list | confirmed, estimated, unknown | analyst | n/a |
| payment_channels_observed | multi-select | cash, MoMo, card, QR, bank transfer, other | photos, posts | H |
| staff_handling_money | pick-list | evident, owner only, unknown | observation | H |
| pain_evidence_type | multi-select | complaint, provider frustration, manual-process signal, multiple payment instructions | observation | H |
| pain_evidence_url | URL list | | source | V |
| trigger_type | multi-select | new outlet, finance hire, growth, event, other | news, jobs | H |
| trigger_date | date | | source | V |
| gates_failed | multi-select | G1 to G8 | analyst | n/a |
| fit_score, pain_score, trigger_score, contact_score, total_score | number | | calculated | n/a |
| capability_fit | pick-list | pass, hold, fail | stage 5 | n/a |
| status | pick-list | Qualified, Research, Not now, Excluded | calculated | n/a |
| buyer_role_identified | pick-list | owner, GM, finance, other, none | LinkedIn, page | H |
| last_reviewed | date | | analyst | n/a |
| reviewed_by | text | | analyst | n/a |
| data_source_notes | text | | analyst | n/a |

## Translating the ICP into account selection: step by step

For the GTM engineer.

1. **Fix the scope.** Confirm the segment, city list and exclusions (ICP section 4). Marketplace sellers, gaming and large enterprise accounts are excluded from the initial campaign; utilities, betting and regulated finance are deferred; existing Hubtel customers are excluded.
2. **Pick sources and test them on 20 accounts.** Check coverage, accuracy and data-protection fit before scaling.
3. **Build the universe.** Collect accounts in the approved city and segment, with business-level fields only.
4. **Apply gates.** Remove failing accounts and log reasons. This is where "right industry, wrong fit" accounts drop out.
5. **Enrich.** Add outlet counts, channel mix, staff signals, pain evidence links, triggers and buyer roles. Keep the source URL and access date for every field.
6. **Score.** Calculate fit, pain, trigger and contact scores. Mark unknowns.
7. **Run the capability check** for the account's strongest pain.
8. **Assign status.** Hand Qualified accounts to a human reviewer.
9. **Review 20 accounts manually.** Compare scored status with human judgement. Adjust weights where they disagree.
10. **Start with a small pilot batch.** Learn from replies. Record why accounts replied, declined or ignored.
11. **Recalibrate.** After the pilot, update weights, gates and the ICP itself. Record what changed in the work log and `knowledge-base/learnings/`.
12. **Refresh.** Re-score every 90 days; remove accounts that become Hubtel customers.

### Link to the GTM skills

The imported skills read `context/icp/icp.md` and `personas.md`, while our ICP files use different names. Before running `/signal-matrix`, create those two files as short pointers to the ICP and buying committee, or adapt the skills' paths. No skill has been run yet.

## How to decide who to target, who to avoid and why

| Decision | Rule |
|---|---|
| Target | Passes gates, shows observed pain, has a trigger, and the pain maps to documented Hubtel capability |
| Avoid, now | Right industry but no pain evidence; pain that only maps to "Hold" capabilities; single outlets; existing Hubtel customers |
| Avoid, for this campaign | Large enterprise accounts, gaming, marketplace sellers and partners, existing customers. Deferred: utilities, betting, regulated financial institutions |
| Research first | Strong trigger but weak pain; many outlets but unknown buyer; good fit but unknown channel mix |

## Open items

- Weights and thresholds need testing against real accounts.
- Coverage of Ghanaian business data sources is untested.
- Pain evidence relies on public data, which may be thin for small businesses.
- Ghana data-protection rules for contact data need review with Legal before any list is built.
- Pricing, sales motion and product depth: confirm with Commercial and Product.

## Confidence

- Framework structure and principles: medium.
- Weights and thresholds: low (starting assumptions).
- Candidate data sources: low (not tested).

## Next steps

1. Build a small, human-reviewed list of accounts scored with this framework, and hold discovery conversations alongside it.
2. First learning goal: can the stage 3 pain evidence be found at all for small Ghanaian businesses?
3. If few accounts qualify, revisit the segment. Do not loosen the gates.

Evidence base: S1 to S5, S16, S24, S33, S46 to S53.
