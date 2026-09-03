---
name: run-code-scan
description: Trigger a CAST Highlight scan of a repository using the highlight-scan-github-action, then check the run and pull the refreshed results
---

# Run a CAST Highlight scan via GitHub Actions

This uses MichaelMULLER/highlight-scan-github-action, which runs in the
target repository's own GitHub Actions and uploads results to CAST
Highlight. It needs three things to already exist in that repo:

1. A workflow file (e.g. `.github/workflows/cast-highlight-scan.yml`) with
   a step that uses `MichaelMULLER/highlight-scan-github-action`
2. An `hl.env` file at the repo root containing the CAST Highlight company
   ID and application ID the results should upload to
3. A repository secret named `CAST_HIGHLIGHT_API_TOKEN` holding a CAST
   Highlight API/CLI user token

## Step 1: Confirm the target

Ask which repository (and which CAST Highlight application it maps to) if
it isn't already clear — one CAST Highlight domain can hold many
applications, and `hl.env` is what ties a specific repo to a specific one.

## Step 2: Check prerequisites before touching anything

Use the `github` MCP tools to check, in order:

- Does `.github/workflows/` contain a workflow that uses
  `MichaelMULLER/highlight-scan-github-action`, and does that workflow
  declare a `workflow_dispatch:` trigger? (Without `workflow_dispatch`,
  the action can only run on its existing triggers — e.g. push or
  schedule — not on demand.)
- Does `hl.env` exist at the repo root, and does it look populated with
  a company ID and application ID?
- Does a repository secret named `CAST_HIGHLIGHT_API_TOKEN` exist? (The
  API can confirm a secret's *name* exists, never its value.)

Report what's missing before doing anything else.

## Step 3: Fill gaps — with the person's sign-off, one thing at a time

- **Missing workflow file or missing `workflow_dispatch` trigger** — draft
  the workflow YAML (add `workflow_dispatch:` alongside whatever trigger
  already exists) and show it before committing anything.
- **Missing or incomplete `hl.env`** — ask for the CAST Highlight company
  ID and application ID rather than guessing them; a wrong ID silently
  uploads results to the wrong application.
- **Missing `CAST_HIGHLIGHT_API_TOKEN` secret** — do not attempt to create
  or set this yourself. Point the person to add it themselves in
  **Settings → Secrets and variables → Actions** on the repo (they'll
  need a CAST Highlight API/CLI token from
  https://doc.casthighlight.com/feature-focus-api-cli-user-token-management/).
  Entering a token on someone's behalf, even via API, is a credential —
  treat it the same as any other secret and leave it to the person.

Any change to workflow files or repo settings is a real, visible change
to someone else's repository — confirm the specific file/diff with the
person before pushing, even if they asked you to "just set it up."

## Step 4: Trigger the scan

Once prerequisites are in place, use the `github` MCP tools to dispatch
the workflow (`workflow_dispatch`) on the branch the person wants scanned.
Confirm the repo, workflow, and branch out loud before firing it — this
kicks off a real CI run and, on completion, publishes results into CAST
Highlight, overwriting/updating whatever was there for that application.

## Step 5: Watch the run

Poll the workflow run via the `github` MCP tools until it finishes.
If it fails, pull the job logs and summarize the failure — the most
common causes are a missing/expired `CAST_HIGHLIGHT_API_TOKEN`, a
mismatched company/application ID in `hl.env`, or the runner not having
network access to the CAST Highlight endpoint.

## Step 6: Hand off to portfolio analysis

Once the run succeeds, the new scan results are in CAST Highlight but may
take a few minutes to finish processing on the CAST Highlight side. Use
the `portfolio-analysis` or `security-findings` skills in this power to
pull the refreshed scorecard or CVE list for that application once it's
ready, rather than assuming the scan finishing on GitHub means the data
is already queryable.
