# Miro MCP Setup

Status: **Installed (project scope). Not authenticated.**

Sources: https://github.com/miroapp/miro-ai and its Claude Code docs (accessed 2026-11-13).

## What was done

Both commands from the instructor worked on this machine:

```powershell
claude plugin marketplace add miroapp/miro-ai
claude plugin install miro@miro-ai --scope project
```

Results:

- Marketplace `miro-ai` was added. Claude Code reported it was declared in **user** settings (machine-wide marketplace list).
- Plugin `miro@miro-ai` was installed at project scope and recorded in `.claude/settings.json` as `enabledPlugins`. That file is committed so the plugin is part of the project.
- `claude mcp list` shows `plugin:miro:miro` at `https://mcp.miro.com/` with status **Needs authentication**. This is expected.

The vendor docs show the in-session form (`/plugin install miro@miro-ai`) and do not mention scope. The `--scope project` flag worked in Claude Code 2.1.220.

Do not also add a manual Miro MCP entry. The vendor warns that this causes conflicts.

## Authenticate (you must do this)

1. Close the current Claude Code session.
2. In PowerShell: `cd "C:\Users\USER\OneDrive\Documents\hubtel-gtm-os"` then `claude`.
3. Type `/mcp`.
4. Select `plugin:miro:miro`, then choose Authenticate.
5. A browser opens. Sign in to Miro, approve access, and **choose your team** that holds the boards.
6. Return to Claude Code. `/mcp` should show Miro as connected.

Enterprise Miro accounts need an admin to enable MCP access first.

Do not claim Miro works until `/mcp` shows it connected.

## Use in this project

- GTM architecture: diagram the Context OS, from research through ICP to outbound.
- Customer journeys: map stages from awareness to purchase and the buying signals at each stage.
- Workflow mapping: draw the outbound workflow (trigger, enrich, qualify, message, follow-up) before building it.

Rules: boards hold visuals only. Facts on boards must cite the same sources as `context/`. GitHub stays the source of truth, so export or describe key diagrams in `knowledge-base/` or `context/docs/`. Ask before creating or editing boards you do not own.
