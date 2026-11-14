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
No other tools are integrated yet. Integration is a later priority (see `weekly-priorities/`).
When tools are added, document each one here with its purpose, how to run it on Windows 11 (PowerShell), and which env vars it needs (names only, never values).
