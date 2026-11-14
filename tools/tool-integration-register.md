# Tool Integration Register

Last updated: 2026-11-13 (week 2026-W46). Update after every change.

| Tool | Installed | Authenticated | Working | Notes |
|---|---|---|---|---|
| Git 2.55.0 | Yes | n/a | Yes | Repo initialised, one local commit |
| GitHub CLI 2.96.0 | Yes | Yes (account `danielkofia`) | Yes | Repo not yet published |
| Miro MCP (plugin `miro@miro-ai` 2.0.0) | Yes, project scope | Yes | Connected (health check 2026-11-13; no board read yet) | See [miro-setup.md](miro-setup.md) |
| Notion MCP | Yes, in `.mcp.json` | Yes (approved) | Connected (health check 2026-11-13; no page read yet) | See [notion-setup.md](notion-setup.md) |
| treg CLI | **No** | **No** | No | Deferred, see below |
| rex (Clay SDK, imported) | Files only | No | No | Needs Clay account and session cookie. Unofficial. Not set up |
| crawl4ai (imported guide) | **No** | n/a | No | Guide in `tools/crawl4ai/README.md`, Windows uses `.venv\Scripts\` |
| agent-browser (imported guide) | **No** | n/a | No | Guide in `tools/agent-browser/README.md`, needs Node 18+ |

## Installed
- Git, GitHub CLI, Miro plugin (project scope), Notion MCP server entry.

## Authenticated
- GitHub CLI, Miro MCP, Notion MCP (per `claude mcp list`, which reported Connected).

## Available but not authenticated
- None.

## Not yet exercised
- Miro and Notion have not been used to read or write anything. Their tools load in a new session. First use should be a harmless read, and any write needs approval.

## Deferred
- **treg:** account cannot be funded (payment card issue). Also not installed: the default Python (3.14.6) is outside the supported range (>=3.12, <3.14); Python 3.13 exists and `uv` is not installed. Local config path prepared (`.treg/`, `TREG_CONFIG` in `.claude/settings.local.json`). No balance, catalog result or enrichment has been obtained. Resume steps in [treg-setup.md](treg-setup.md).

## Facts not verified
- treg's free starting credit and pricing are vendor claims.
- `TREG_CONFIG` behaviour comes from package source, not official docs.
- treg CLI commands were not run.

## Security notes
- Gitignored: `.env`, `.treg/`, `.claude/settings.local.json`.
- Committed config contains no credentials: `.mcp.json`, `.claude/settings.json`.
- Project is inside OneDrive: gitignored files, including a future treg token, still sync to the cloud.
