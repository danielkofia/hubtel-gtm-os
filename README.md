# Hubtel GTM Context OS

The go-to-market engineering workspace for Hubtel's business payments and back-office offer. It is written from the perspective of an in-house Go-to-Market Engineer at Hubtel, responsible for the company's GTM strategy and systems.

It is a "Context OS": a structured, version-controlled folder that gives an AI assistant (Claude Code) the company knowledge, rules and methods it needs to do GTM work consistently.

## Selected segment

**Primary:** owner-led hospitality and food-service businesses with 2 to 15 outlets, starting with Greater Accra.
**Secondary:** owner-led multi-branch retail, once product capabilities are confirmed.

Details are in [the ICP](context/icp/ideal-customer-profile.md).

## What is in this repository

| Area | Files | Status |
|---|---|---|
| Company, market, competitive and customer research | [context/docs/research/](context/docs/research/) (five research files and a source register) | Done. Two passes, with conflicting figures flagged |
| ICP and buying committee | [context/icp/](context/icp/) | Done. A working ICP, to be refined with Sales input |
| Buying-signal matrix and scoring | [signal-matrix.md](context/docs/research/signal-matrix.md), [signal-scoring-framework.md](context/docs/research/signal-scoring-framework.md) | Drafted, untested |
| GTM revenue system | [gtm-system-map.md](knowledge-base/playbooks/gtm-system-map.md), [revenue-system-architecture.md](knowledge-base/playbooks/revenue-system-architecture.md) | Drafted, untested |
| Outbound workflow design | [output/outbound/](output/outbound/) (spec, architecture, data schema, qualification rules) | Design only. Nothing built or sent |
| Company context documents | `context/docs/` | Not started |
| Positioning, messaging and brand kit | `context/positioning/`, `context/messaging/`, `context/brand-kit/` | Not started |
| Campaign copy | `output/campaigns/` | Not started |
| Tool integrations | [tools/](tools/) (Miro and Notion connected, treg prepared but not installed) | Partly done |
| Final quality assurance | | Not started |

Progress and decisions are tracked in [weekly-priorities/2026-W46.md](weekly-priorities/2026-W46.md) and [work-log/2026-W46.md](work-log/2026-W46.md).

## Structure

See [CLAUDE.md](CLAUDE.md) for what each folder contains and when to consult it. The key separation:

- `context/`: company-specific intelligence (changes per company)
- `knowledge-base/`: reusable GTM methodologies (portable to any company)
- `output/`: deliverables, drafted but never sent without approval

## Evidence and limits

- The research uses public sources. Several figures (merchants served, daily transactions, revenue, funding, fees) conflict or are unverified. Check the [source register](context/docs/research/source-register.md) and the confidence notes before using any number.
- Branch dashboards, per-staff sales tracking, automated reconciliation and audit logs are not documented in the material reviewed. Product must confirm them before any message promises them.
- Pricing, the existing customer list, the CRM in use and the data-protection position need confirmation from the relevant Hubtel teams.
- No outreach has been sent, no paid data lookup made and no automation activated.

## Third-party content

Skills and playbooks adapted from the GTM Starter Kit and related open-source projects keep their original licences. See [THIRD-PARTY.md](THIRD-PARTY.md).

## Safety

Secrets belong only in `.env` (gitignored). Datasets (`*.csv`, `*.xlsx`) are gitignored. Nothing is sent, published or spent without approval.
