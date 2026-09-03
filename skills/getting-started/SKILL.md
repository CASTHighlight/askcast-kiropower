---
name: getting-started
description: Connect Kiro to the CAST Highlight MCP Server and verify the connection before doing any portfolio analysis
---

# Set up CAST Highlight

## Step 1: Get your connection details

CAST Highlight's MCP Server is a remote SaaS endpoint, not something you run locally. You need three values from your CAST Highlight tenant:

- **MCP URL** — the remote endpoint for your CAST Highlight instance's MCP server
- **Domain Id** — an integer identifying your CAST Highlight domain/tenant
- **User Token** — a UUID that authenticates you as a specific user

Ask your CAST Highlight administrator for these, or find them in the CAST Highlight application under your account/API settings.

## Step 2: Set environment variables

Export these before launching Kiro, or set them in your shell profile:

```bash
export CAST_HIGHLIGHT_MCP_URL="https://<your-instance>.casthighlight.com/mcp"
export CAST_HIGHLIGHT_DOMAIN_ID="12345"
export CAST_HIGHLIGHT_USER_TOKEN="00000000-0000-0000-0000-000000000000"
```

## Step 3: Approve the environment variables in Kiro

Kiro only expands environment variables you've explicitly approved:

1. Open Kiro Settings (`Cmd+,` / `Ctrl+,`)
2. Search for "Mcp Approved Env Vars"
3. Add `CAST_HIGHLIGHT_MCP_URL`, `CAST_HIGHLIGHT_DOMAIN_ID`, and `CAST_HIGHLIGHT_USER_TOKEN`

## Step 4: Verify the connection

Open the Kiro panel's MCP view and confirm `cast-highlight` shows a green (connected) status. If it doesn't connect:

- Double-check the Domain Id is the numeric ID, not the domain name
- Confirm the User Token hasn't expired or been revoked
- Check View → Output → "Kiro - MCP Logs" for the specific error

## Step 5: Review available tools before auto-approving

The first time you connect, look at what tools the server exposes and decide which are safe to auto-approve (read-only queries like listing applications or fetching scores) versus which should prompt every time (anything that could modify domain data, if such tools exist). Add the safe ones to `autoApprove` in `mcp.json`.
