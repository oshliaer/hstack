---
name: stress-test
version: 1.0.0
description: |
  Quantitative and financial stress testing for strategic decisions.
  Models the break-even point, cash runway, and downside exposure of a plan
  under pessimistic assumptions. Produces sensitivity tables and go/no-go
  thresholds. Use for any decision with significant financial stakes.
  Invoke with /stress-test when you have financial data or projections.
allowed-tools:
  - Read
  - Write
  - AskUserQuestion
---

# /stress-test — Financial & Quantitative Stress Testing

Stress-tests the numbers behind a strategic decision. Finds the break-even point,
quantifies downside exposure, and identifies which variable has the most leverage
over the outcome. Works with rough estimates when precise data is unavailable.

## When to invoke

Run `/stress-test` **in parallel with or after `/scenario`**.
Required when the decision involves: capital allocation, hiring, pricing changes,
or any commitment with a quantifiable cost and expected return.
Also useful as a standalone sanity check before investor or board presentations.

## Arguments

- `/stress-test` — interactive: prompts for financial inputs
- `/stress-test --capital <amount>` — set the capital at stake (e.g., `500000`)
- `/stress-test --horizon <months>` — set the analysis horizon (default: 24)

## Input

Provide the best available numbers. Estimates are acceptable — label them as such.

| Field | Description | Example |
|-------|-------------|---------|
| Capital at stake | Total amount being committed or borrowed | $500,000 |
| Expected monthly revenue uplift | Revenue increase attributable to this decision | $40,000/month |
| Monthly cost of the decision | New costs incurred (interest, staff, rent, etc.) | $25,000/month |
| Time to first revenue | Months until the decision generates any return | 3 months |
| Current cash position | Cash on hand before the decision | $200,000 |
| Current monthly burn | Existing operating costs | $80,000/month |

## Instructions

### Step 1 — Build the base-case cash model

Using the inputs, model month-by-month cash position for the analysis horizon.

Key formulas:
```
Monthly net flow (post-decision) = Revenue uplift − Decision cost
Cumulative cash = Starting cash − (Burn × months) + max(0, Monthly net flow × max(0, months − Time to first revenue))
Break-even month = first month where cumulative incremental revenue ≥ capital at stake
```

Present the first 24 months (or to break-even, whichever is longer) as a table:

| Month | Incremental Revenue | Incremental Cost | Net Flow | Cumulative Return |
|-------|--------------------|--------------------|----------|------------------|
| 1 | … | … | … | … |

### Step 2 — Run sensitivity analysis

Vary the two most uncertain inputs (typically Revenue Uplift and Time to Revenue)
across three levels: −40%, base, +40%.

Present as a 3×3 matrix of break-even months:

| | Revenue −40% | Revenue base | Revenue +40% |
|---|---|---|---|
| **Time to rev −40%** | … | … | … |
| **Time to rev base** | … | … | … |
| **Time to rev +40%** | … | … | … |

Highlight the worst-case cell in red (conceptually — mark it **WORST CASE**).

### Step 3 — Compute downside exposure

Define the **maximum loss scenario**: revenue uplift = 0 (decision generates nothing).

```
Max loss = Capital at stake + (Decision cost × Analysis horizon in months)
Survival runway = Current cash ÷ (Current burn + Decision cost)
```

State: "Under zero-return assumptions, this decision costs $X over Y months
and reduces cash runway from Z months to W months."

### Step 4 — Identify the leverage variable

Which single input, if improved by 20%, has the largest positive effect on break-even?
Name it. This is where to focus execution effort.

### Step 5 — Set go/no-go thresholds

Define three numerical thresholds that, if missed, should trigger a stop/pause:

| Threshold | Value | What to do if missed |
|-----------|-------|----------------------|
| Minimum monthly revenue uplift to break even within horizon | $X/month | Pause and reassess |
| Maximum acceptable cash runway drop | Y months remaining | Do not proceed |
| Maximum break-even horizon acceptable | Z months | Seek cheaper alternative |

### Step 6 — Output the Stress Test Report

```markdown
# Stress Test Report

**Decision:** …
**Capital at stake:** …
**Date:** …
**Analysis horizon:** X months

## Base-case cash model
[table from Step 1 — first 12 months minimum]

**Break-even month (base case):** Month N

## Sensitivity analysis
[matrix from Step 2]

**Worst case break-even:** Month N (revenue −40%, ramp delayed +40%)

## Downside exposure
- Max loss under zero-return: $…
- Cash runway with decision: … months
- Cash runway without decision: … months

## Leverage variable
[name of input + quantified impact of 20% improvement]

## Go/no-go thresholds
[table from Step 5]

## Verdict
[1–2 sentences: does the base-case return justify the downside exposure?]
```

Save to `decision-log/stress-test-<YYYY-MM-DD>.md`.

## Quality criteria

The skill has performed well when:

- Break-even is computed under base, optimistic, and pessimistic assumptions.
- The maximum loss scenario is explicitly stated in dollars and months of runway.
- The leverage variable is identified and actionable.
- Go/no-go thresholds are numerical (not qualitative).
- The verdict is a directional statement, not a hedge.
