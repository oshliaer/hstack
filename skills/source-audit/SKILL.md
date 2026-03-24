---
name: source-audit
version: 1.0.0
description: |
  Data and evidence reliability audit for strategic decisions.
  Scores every claim, data point, and source underpinning the decision for
  reliability, recency, and relevance. Flags weak evidence chains before
  they corrupt downstream analysis. Use after /reframe and before /scenario.
  Invoke with /source-audit when given claims, data points, or research links.
allowed-tools:
  - Read
  - Write
  - AskUserQuestion
---

# /source-audit — Evidence & Source Reliability Audit

Stress-tests the factual foundation of a decision. Scores sources and claims
so that conclusions downstream are grounded in evidence, not assumption.

## When to invoke

Run `/source-audit` **after `/reframe`** and before quantitative or scenario analysis.
Also run it when a decision rests on market-size estimates, customer interviews,
competitor data, or financial projections.

## Arguments

- `/source-audit` — interactive: prompts for claims and sources
- `/source-audit --claims "<claim1>; <claim2>"` — comma/semicolon-separated claim list
- `/source-audit --file <path>` — read claims from a text or markdown file

## Input

| Field | Description | Example |
|-------|-------------|---------|
| Claims | List of factual statements the decision depends on | "The market grows 20% YoY" |
| Sources | URL, document name, interview notes, or "internal estimate" | Link, filename, or description |
| Context | Decision question and timeframe from /reframe output | Reframe Report path or inline |

## Instructions

### Step 1 — Extract all load-bearing claims

Read the decision context. A **load-bearing claim** is any factual statement that,
if wrong, would change the decision or its expected outcome.

List every load-bearing claim. Number them.

### Step 2 — Identify the source for each claim

For each claim:

- Name the source (publication, dataset, interview, internal model, intuition).
- Classify the source type:
  - **Primary** — first-hand data (your own customers, your own financials)
  - **Secondary** — published research, analyst reports, news
  - **Tertiary** — summaries, Wikipedia, LLM-generated estimates
  - **None** — no source identified

### Step 3 — Score each claim

Use this rubric (score 1–5 on each dimension, then sum for a total out of 15):

| Dimension | 1 | 3 | 5 |
|-----------|---|---|---|
| **Reliability** | No source / anecdote | Reputable secondary | Peer-reviewed / your own primary data |
| **Recency** | >5 years old | 2–5 years old | <2 years old |
| **Relevance** | Different market/geography | Adjacent | Directly applicable to your situation |

Flag any claim scoring ≤6 as **RED** (unreliable), 7–10 as **YELLOW** (verify),
11–15 as **GREEN** (proceed).

### Step 4 — Check base rates

For each RED or YELLOW claim, look for an applicable base rate:

- Industry default failure/success rates
- Reference class for similar decisions (e.g., "loan-funded SMB expansions")
- Historical analogues

If no base rate is findable, mark the claim as **Unanchored** and flag it for
validation (see `/validators/`).

### Step 5 — Output the Source Audit Report

```markdown
# Source Audit Report

**Decision question:** …
**Date:** …

## Claims & Scores

| # | Claim | Source | Type | Reliability | Recency | Relevance | Total | Status |
|---|-------|--------|------|-------------|---------|-----------|-------|--------|
| 1 | … | … | … | /5 | /5 | /5 | /15 | 🟢/🟡/🔴 |

## Unanchored claims (no base rate found)
1. …

## Recommended validators
For each RED or Unanchored claim, suggest the matching validator from /validators/:
- Claim #N → validators/<template>.md
```

Save to `decision-log/source-audit-<YYYY-MM-DD>.md`.

## Quality criteria

The skill has performed well when:

- Every load-bearing claim has a source type assigned.
- At least one RED or YELLOW claim has been identified (if none exist, the audit was too shallow).
- Each unanchored claim maps to a concrete validator template.
- The report is usable as direct input to `/scenario` and `/pre-mortem`.
