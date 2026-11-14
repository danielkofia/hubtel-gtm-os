# Notion MCP Setup

Status: **Added to project config. Not yet approved, not authenticated.**

Source: https://developers.notion.com/docs/get-started-with-mcp (accessed 2026-11-13). Official form: `claude mcp add --transport http notion https://mcp.notion.com/mcp`.

## What was done

The instructor's command still works:

```powershell
claude mcp add --transport http --scope project notion https://mcp.notion.com/mcp
```

It created `.mcp.json` at the project root (HTTP transport, URL only, no credentials). `claude mcp list` shows `notion` as **Pending approval**: Claude Code requires you to approve project-scoped servers the first time.

## Approve and authenticate (you must do this)

1. Start a new session: `cd "C:\Users\USER\OneDrive\Documents\hubtel-gtm-os"` then `claude`.
2. Approve the `notion` server when prompted.
3. Type `/mcp`, select `notion`, choose Authenticate.
4. Complete the OAuth flow in the browser and pick the workspace.
5. `/mcp` should show Notion as connected. Until then it is not working.

OAuth tokens are held by Claude Code, not in `.mcp.json`. Never put tokens in that file.

## Role in this project

- GitHub is the source of truth. Notion is a publishing and sharing layer for finished documents.
- Write to Notion only finished, approved content, and only after the human approves (project rule: ask before publishing).
- Never put secrets or raw research dumps into Notion.
- Public GitHub content must not be assumed private in Notion, and vice versa. Check Notion page sharing before publishing.
