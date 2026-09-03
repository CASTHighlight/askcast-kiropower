---
name: portfolio-analysis
description: Analyze an application portfolio with CAST Highlight data — technical debt, cloud readiness, agentic readiness, and Portfolio Advisor positioning
---

# Analyze a CAST Highlight portfolio

## Step 1: Confirm scope

Before querying, confirm with the user which slice of the portfolio they mean: a single application, a business unit/domain, or the whole tenant. CAST Highlight organizes applications under a Domain (identified by the Domain Id used to authenticate), so most tools will already be scoped to that domain.

## Step 2: Discover available tools

Call the CAST Highlight MCP tools available in this session to see what's exposed (application lists, scorecards, technical debt, cloud/agentic readiness, Portfolio Advisor data, etc.) — tool names may vary by CAST Highlight release, so inspect what's actually offered rather than assuming a fixed set.

## Step 3: Frame results the way CAST Highlight does

When presenting scores or comparisons, use the platform's own vocabulary so results are legible to someone who already works in Highlight:

- **Portfolio Advisor quadrants** — applications are typically grouped into *Strategic Priorities*, *Quick Wins*, *Deferred*, and *Deprioritized*. When summarizing portfolio positioning, use these four labels rather than inventing new categories.
- **Agentic readiness** — treat this as its own dimension alongside cloud readiness and technical debt, not folded into a generic "code quality" score.
- **Score normalization** — Highlight scores are typically produced via Min-Max Normalization against the portfolio (or a benchmark), so a score is relative, not absolute. Say so when a user might otherwise read a raw number as a universal grade.
- **Deterministic code patterns** — when explaining *why* a technical debt or risk score looks the way it does, distinguish findings driven by deterministic code pattern detection from more heuristic or statistical signals, if the tool output makes that distinction available.

## Step 4: Lead with customer value, not the metric

Don't open with "your CloudReady score is 62." Open with what that means for the application or the portfolio — migration risk, effort to modernize, or where it sits in prioritization — then bring in the specific metric as support.

## Step 5: Flag data gaps honestly

If a tool call returns partial data (e.g., an application hasn't been re-scanned recently, or a dimension wasn't assessed), say so explicitly rather than presenting the portfolio view as complete.
