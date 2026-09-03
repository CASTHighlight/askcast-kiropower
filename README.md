# CAST Highlight — Kiro Power

Gives Kiro's agent instant, on-demand access to CAST Highlight's application
portfolio data — technical debt, open-source security risk, cloud readiness,
and agentic/AI readiness — via the CAST Highlight MCP Server, the domain
vocabulary to talk about results the way CAST Highlight does (Portfolio
Advisor quadrants, Verified/Inferred CVE detection, etc.), and the ability
to trigger a fresh scan of a repo via
[MichaelMULLER/highlight-scan-github-action](https://github.com/MichaelMULLER/highlight-scan-github-action).

## What's included

```
power-cast-highlight/
├── plugin.json                     # Manifest — name, description, activation keywords
├── mcp.json                        # Two remote MCP servers: cast-highlight + github
└── skills/
    ├── getting-started/SKILL.md    # Connect & verify the cast-highlight MCP server
    ├── portfolio-analysis/SKILL.md # Query and frame portfolio results
    ├── security-findings/SKILL.md  # Work through CVE/SCA findings
    └── run-code-scan/SKILL.md      # Trigger the GitHub Action scan and read results back
```

`mcp.json` now wires up two servers:

- **`cast-highlight`** — your existing remote server (unchanged), reads
  portfolio/scorecard/CVE data
- **`github`** — GitHub's official remote MCP server
  (`https://api.githubcopilot.com/mcp/`), scoped to the `actions` and
  `repos` toolsets, used only to check/trigger the scan workflow and read
  run status — not to browse or modify code beyond that

## Install locally (for testing)

1. Open Kiro → Powers panel → **Add Custom Power**
2. Choose **Import power from a folder**
3. Select this `power-cast-highlight/` directory
4. Follow the `getting-started` skill to set your three CAST Highlight
   environment variables (`CAST_HIGHLIGHT_MCP_URL`,
   `CAST_HIGHLIGHT_DOMAIN_ID`, `CAST_HIGHLIGHT_USER_TOKEN`) and approve
   them in Kiro settings
5. The `github` server uses OAuth — Kiro will open a browser sign-in the
   first time the agent tries to use a `github` tool. No token to manage
   yourself for this one.
6. In the target repository, make sure the three prerequisites from
   `run-code-scan/SKILL.md` are in place (workflow file with
   `workflow_dispatch`, `hl.env`, and the `CAST_HIGHLIGHT_API_TOKEN`
   secret) — the skill will check and tell you what's missing, but it
   won't set the secret for you (that stays a manual step, deliberately)

## Before sharing this more broadly

- **Fill in `autoApprove`** in `mcp.json` once you've seen the actual tool
  names the CAST Highlight MCP Server exposes — it's left empty here since
  the exact tool list wasn't available while drafting this.
- **Confirm the `url` shape** — this assumes a single MCP endpoint per
  tenant with the three custom headers already documented for your other
  clients (Claude Desktop, Cursor, Windsurf, VS Code, etc.); adjust if
  Kiro needs anything different.
- **Add a `homepage`/`repository`** pointing at wherever you'll host this
  (e.g. an internal GitHub repo) so the power can be installed via
  **Import power from GitHub** instead of a local folder.
- **Consider an org-wide default** — if most CAST Highlight customers only
  ever use one Domain Id, you could bake a setup script into
  `skills/getting-started/scripts/` that looks it up automatically instead
  of asking the user to find it manually.
- **Double-check the `github` server's blast radius** — `X-MCP-Toolsets:
  actions,repos` still grants more than just "trigger this one workflow."
  If you want to constrain it further, GitHub's remote server also
  supports `X-MCP-Tools` to allow-list individual tools (e.g. just
  `list_workflows`, `run_workflow`, `get_workflow_run`,
  `get_job_logs`) instead of the whole `actions` toolset — worth doing
  before handing this power to anyone outside your own testing.
- **Leave `CAST_HIGHLIGHT_API_TOKEN` out of scope entirely** — the power
  is written so the agent never touches that secret's value, only checks
  whether it exists. Keep it that way in any future revision.

## Sharing

```bash
cd power-cast-highlight
git init
git add plugin.json mcp.json skills/ README.md
git commit -m "Initial release: CAST Highlight Kiro power"
git push origin main
```

Others install it via **Add Custom Power** → **Import power from GitHub**.


## Privacy & Support
- **Privacy Policy:** https://www.castsoftware.com/privacy
- **Support:** https://help.castsoftware.com