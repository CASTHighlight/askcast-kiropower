# CAST Highlight — Kiro Power

Gives Kiro's agent instant, on-demand access to CAST Highlight's application
portfolio data — technical debt, open-source security risk, cloud readiness,
and agentic/AI readiness — via the CAST Highlight MCP Server, plus the
domain vocabulary to talk about results the way CAST Highlight does
(Portfolio Advisor quadrants, Verified/Inferred CVE detection, etc.).

## What's included

```
power-cast-highlight/
├── plugin.json                     # Manifest — name, description, activation keywords
├── mcp.json                        # Remote MCP server config (CAST Highlight MCP Server)
└── skills/
    ├── getting-started/SKILL.md    # Connect & verify the MCP server
    ├── portfolio-analysis/SKILL.md # Query and frame portfolio results
    └── security-findings/SKILL.md  # Work through CVE/SCA findings
```

## Install locally (for testing)

1. Open Kiro → Powers panel → **Add Custom Power**
2. Choose **Import power from a folder**
3. Select this `power-cast-highlight/` directory
4. Follow the `getting-started` skill to set your three environment
   variables (`CAST_HIGHLIGHT_MCP_URL`, `CAST_HIGHLIGHT_DOMAIN_ID`,
   `CAST_HIGHLIGHT_USER_TOKEN`) and approve them in Kiro settings

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