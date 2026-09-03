---
name: security-findings
description: Investigate open-source security findings (CVEs) surfaced by CAST Highlight's software composition analysis
---

# Work with CAST Highlight security findings

## Step 1: Pull the findings

Use the CAST Highlight MCP tools available in this session to retrieve open-source component and CVE data for the application(s) in scope.

## Step 2: Distinguish detection method before prioritizing

CAST Highlight tags each CVE match with how it was detected:

- **Verified** — a direct advisory match (the component/version is explicitly named in the vulnerability advisory)
- **Inferred** — an approximate match via NVD CPE matching, which can carry more false positives

Always surface this distinction when listing findings. Don't collapse Verified and Inferred into a single count — a portfolio with 40 Verified CVEs and a portfolio with 40 Inferred CVEs are different conversations, and treating them the same overstates or understates real exposure.

## Step 3: Prioritize with both severity and detection method

When helping a user triage, weigh:

1. Severity (critical/high/medium/low)
2. Detection method (Verified findings deserve action first; Inferred findings deserve a quick manual check before action)
3. Whether the affected component is reachable/exploitable in the application's actual usage, if that data is available

## Step 4: Report findings in plain terms

Translate CVE IDs and component names into what it means for the application — "this open-source library has a known remote code execution flaw and is used in your payment service" reads better than a bare CVE list. Keep the CVE identifiers alongside the plain-language summary so the user can cross-reference.
