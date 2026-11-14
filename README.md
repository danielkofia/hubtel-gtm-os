# Hubtel GTM Context OS

An independent, educational Go-to-Market (GTM) Engineering portfolio project.

## Disclaimer

This project is **not affiliated with, endorsed by, or an official project of Hubtel**. Hubtel (https://hubtel.com) is used only as a real-world subject for learning. Nothing here represents Hubtel's views, strategy or data. Any company facts will be sourced from public information and cited.

## Purpose

The author is learning GTM Engineering. This repository practices building a "Context OS": a structured, version-controlled folder that gives an AI assistant (Claude Code) the company knowledge, rules and methods it needs to do GTM work consistently.

The project covers: research, company context, ICP, positioning and messaging, buying signals, revenue system mapping, an outbound workflow, campaign copy, reusable playbooks and tool integration.

## Structure

See [CLAUDE.md](CLAUDE.md) for what each folder contains and when to consult it. The key idea is the separation of:

- `context/`: company-specific intelligence (changes per company)
- `knowledge-base/`: reusable GTM methodologies (portable to any company)
- `output/`: deliverables, drafted but never sent without approval

## Progress

Weekly plans live in `weekly-priorities/` and are tracked in `work-log/`. Start with [2026-W46](weekly-priorities/2026-W46.md).

## Safety

Secrets belong only in `.env` (gitignored). Datasets (`*.csv`, `*.xlsx`) are gitignored.
