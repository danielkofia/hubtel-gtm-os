# treg Setup

Status: **Prepared, not installed, not logged in.** Deferred because the account cannot be funded yet. No credits bought, no paid calls made, no balance or catalog result has been observed.

Evidence key: [Doc] stated in official treg material, [Src] read from the published package source (`tools-registry` 0.30.0 wheel, inspected without installing), [Untested] not run on this machine.

## What treg is

[Doc] A service that gives AI agents one account and one token for a catalog of third-party data and tool endpoints (the site cites 4,100+ endpoints from 127 providers, covering areas such as contact enrichment and buying signals). Calls are billed per call from a prepaid balance. The site states a free starting credit for new verified accounts and 0% markup. These are vendor claims and must be verified in the dashboard before relying on them.

Sources: https://treg.to, https://treg.to/llms.txt, https://treg.to/docs, https://github.com/superdesigndev/treg (accessed 2026-11-13).

## How the CLI works

[Doc] The `treg` CLI is a thin client: each command is one HTTP call to the registry at `https://treg.to`. The token is sent in the `X-Treg-Token` header. Provider credentials are injected server-side.

Never send your treg token through the `/call/` proxy path, because it is relayed to the provider [Doc].

## Installation on Windows 11

[Doc] The official one-liner is `curl -fsSL https://treg.to/install.sh | sh`. It is written for POSIX shells and does not address native Windows. Do not run it in PowerShell.

[Doc] The package is on PyPI as `tools-registry` (provides the `treg` command). PyPI metadata requires **Python >=3.12 and <3.14**.

This machine: default `python` is 3.14.6 (incompatible). Python 3.13 is present (`py -3.13`). `uv` and `pipx` are not installed. [Verified locally]

Suggested route [Untested], PowerShell:

```powershell
winget install --id astral-sh.uv -e
# open a NEW terminal so uv is on PATH
uv tool install --python 3.13 tools-registry
treg --help
```

Do not create a virtual environment inside this project folder: `.gitignore` does not cover it and it would be committed.

Note: the official installer script also sends anonymous telemetry. A PyPI install does not run that script. If you ever use the script, set `TREG_TELEMETRY=0` first.

## Authentication

[Doc] Login options (all [Untested]):

- `treg login` : browser sign-in with GitHub (default) or Google.
- `treg login --email` : emailed one-time code.
- `treg login --token <token>` : for agents and CI.
- `TREG_TOKEN` environment variable overrides the saved login for that process [Src].

[Doc] The site says first sign-in creates the account. Whether sign-in itself needs payment is not stated in the docs, so confirm in the browser. Adding funds is separate (`treg topup`).

Treat the token as a secret. Never paste it into chat, a committed file or `CLAUDE.md`.

## Configuration (TREG_CONFIG)

[Src] `TREG_CONFIG` is the path to an alternate **config file**. Default: `~/.treg/config.json`. It is not a directory. The official docs do not mention it, so this is based on the package source (`treg/cli.py`) and may change.

Project setup done in this repo:

- Folder `.treg/` created at the project root (gitignored).
- `.claude/settings.local.json` (gitignored) sets, under the supported `env` key:

```json
{
  "env": {
    "TREG_CONFIG": "C:\\Users\\USER\\OneDrive\\Documents\\hubtel-gtm-os\\.treg\\config.json"
  }
}
```

- `.treg/config.json` does not exist yet. It is created by `treg login` and will contain your token.

Limits:

- The variable applies to processes Claude Code starts, after a **session restart**. A normal PowerShell window will not have it. To use the project config there: `$env:TREG_CONFIG = "<path above>"` for that window.
- This folder is inside OneDrive, so the token file in `.treg/` will sync to OneDrive. Consider moving the project outside OneDrive or accepting that risk.
- If the project folder moves, update the absolute path.

## Balance checking

[Doc] `treg` with no arguments shows account, team and balance. `treg balance` shows credit, calls in flight and recent spend. The dashboard also shows balance. [Untested]

## Catalog searching and pricing verification

[Doc] These are intended to be read-only [Untested]:

```powershell
treg catalog search "find work email for a person at a company"
treg catalog get <id>      # parameters, price, reliability, example call
```

Before any paid call:

1. Run `catalog get` and record the stated price per call.
2. Check `treg balance`.
3. Cap spend per call with the `X-Treg-Route-Max-Cost` header if calling over HTTP [Doc].
4. Start with one test record, then scale.
5. Ask the human for approval first (project rule: ask before spending).

Verify whether `catalog search` itself is free on your account before running it in volume. The docs do not say.

## Future use cases for Hubtel GTM

Only after research and ICP exist (priorities P2 and P4):

- Enrich a small, approved account list with firmographics.
- Find buying-signal data sources for the signal matrix (P6).
- Compare providers by price and success rate for the outbound workflow (P8).

Record every price and result in `output/data/` (CSV is gitignored) and cite the provider.

## Resuming when funds are available

1. Install via the route above, confirm `treg --help` works.
2. Restart Claude Code in this folder so `TREG_CONFIG` loads.
3. `treg login`, then confirm `.treg/config.json` exists and `git status` does not list it.
4. `treg balance`, and screenshot or note the real figure in the work log.
5. Run `catalog search` and `catalog get`, record prices in the work log.
6. Update [tool-integration-register.md](tool-integration-register.md) and the Tools section of `CLAUDE.md`.
