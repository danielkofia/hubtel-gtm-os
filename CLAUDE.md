# Hubtel GTM Context OS

## 1. Company

Hubtel is the subject of this independent educational GTM Engineering portfolio project. This is not an official Hubtel project and the author is not affiliated with the company.
Hubtel's business description, products, customers and market position are NOT yet established. They must be verified through research and cited in `context/docs/research/` before use anywhere else.

## 2. How This Folder Works

- `.claude/skills/`: custom Claude skills. Consult when a task repeats and should be codified.
- `context/icp/`: ideal customer profiles and buying-signal matrix. Consult before targeting or prioritizing accounts.
- `context/positioning/`: positioning statements and differentiation. Consult before writing any message.
- `context/messaging/`: messaging framework, value props, proof points. Consult before drafting copy.
- `context/brand-kit/`: voice, tone, style rules. Consult before producing any customer-facing text.
- `context/docs/`: company context documents. `research/` holds raw cited research. Consult first for any company fact.
- `knowledge-base/playbooks/`: reusable GTM methodologies, company-agnostic. Consult when designing a workflow.
- `knowledge-base/learnings/`: lessons from experiments and mistakes. Consult before repeating a tactic.
- `meetings/`: notes and decisions from mentor or stakeholder sessions.
- `output/campaigns/`, `outbound/`, `social/`: finished drafts by channel. Nothing here is sent until approved.
- `output/data/`: working datasets (CSV/XLSX are gitignored).
- `tools/`: scripts and integration notes. Consult before adding or running automation.
- `weekly-priorities/`: the plan for each ISO week (`YYYY-Www.md`).
- `work-log/`: running record of what was done each week, linked to priorities.

## 3. Rules

- Cite sources (URL and access date) for every company fact.
- Never invent statistics. If a number is unknown, say so.
- Label every claim as Fact, Assumption or Recommendation.
- No em dashes in marketing copy.
- Ask before publishing, sending or spending.
- Keep the work log updated at the end of every work session.
- Keep company-specific intelligence (`context/`) separate from reusable methodologies (`knowledge-base/`).
- Never expose credentials or secrets. Keys live only in `.env`, which is gitignored.

## 4. Tools

- Git (branch `main`) tracks the project. Commit after each meaningful unit of work. Run `git status` and review the diff before every commit. Never commit secrets.
- GitHub CLI (`gh`) is used for the public repo. Pushing is outward-facing: ask first.
- Miro plugin (project scope) is authenticated and connected. Ask before creating or editing boards.
- Notion MCP (`.mcp.json`) is approved, authenticated and connected. Publish only approved, finished docs; GitHub stays the source of truth.
- treg is NOT installed or logged in (deferred, payment). Never run paid lookups. See `tools/tool-integration-register.md`.
- Imported but NOT installed: `tools/rex` (Clay), `tools/crawl4ai`, `tools/agent-browser`. Do not install or run without approval.
When tools are added, document each one here with its purpose, how to run it on Windows 11 (PowerShell), and which env vars it needs (names only, never values).

## 5. Skills (from the GTM Starter Kit, MIT, see `THIRD-PARTY.md`)

Core chain, run in order, each stops for approval: `/campaign-strategy` (ideas) -> `/signal-matrix` (segments and signals) -> `/build-workflow-spec` (structure, no copy) -> `/campaign-copy` (needs an approved spec and `context/messaging/facts.md`).
Also: `/miro-gtm-flowchart` (draws on Miro). Clay skills (`build-clay`, `prompt-builder`, `campaign-contract`, `design-clay-table-json`, `import-clay-table`, `save-clay-schema`, `calculate-costs`, `workspace-cost-audit`, `export-tables`, `campaign-qa`), `crawl4ai`, `agent-browser` and `inbox-placement-test` need tools or accounts we do not have. Do not use them yet.
Skills read `context/` first. Run them only after research and ICP exist. Playbooks they read are in `knowledge-base/playbooks/`.
