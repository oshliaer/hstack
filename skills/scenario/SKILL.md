---
name: scenario
version: 1.0.0
description: |
  Scenario planning for strategic decisions. Constructs three futures —
  optimistic, base-case, and pessimistic — with probability weights, key
  drivers, and outcome metrics. Use after /source-audit to map the decision
  space before committing to a course of action.
  Invoke with /scenario when you have a reframed question and audited evidence.
allowed-tools:
  - Read
  - Write
  - AskUserQuestion
---

# /scenario — Scenario Planning & Outcome Mapping

Builds three distinct futures for a decision, assigns probability weights,
identifies the 2–3 drivers that separate them, and maps the outcome range
before any commitment is made.

## When to invoke

Run `/scenario` **after `/source-audit`**.
Best when the decision has meaningful uncertainty over a 6–24 month horizon.
Also useful when stakeholders disagree — scenarios make disagreements explicit.

## Arguments

- `/scenario` — interactive: prompts for context and preferred output format
- `/scenario --horizon <months>` — set explicit time horizon (default: from TIMEFRAME)
- `/scenario --drivers "<driver1>; <driver2>"` — pre-specify key uncertainty drivers

## Input

| Field | Description | Example |
|-------|-------------|---------|
| Decision question | From /reframe output | Reframe Report path or inline |
| Evidence base | From /source-audit output | Source Audit Report path or inline |
| Key metrics | What does success/failure look like numerically? | Revenue, headcount, cash runway |
| Timeframe | short / medium / long | medium (12 months) |

## Instructions

### Step 1 — Identify key uncertainty drivers

List the 2–4 variables that will most determine the outcome.
Drivers must be:
- **Uncertain** — not already known with high confidence
- **Impactful** — their value materially changes the outcome
- **Independent** — not just re-labelings of the same variable

For each driver, define its range: low value → high value.

### Step 2 — Construct three scenarios

Using the drivers, define three distinct futures:

| Scenario | Driver 1 value | Driver 2 value | Narrative (2–3 sentences) |
|----------|----------------|----------------|--------------------------|
| Optimistic (O) | high | high | … |
| Base case (B) | mid | mid | … |
| Pessimistic (P) | low | low | … |

The scenarios must be **narratively coherent** — each should tell a plausible story,
not just a list of numbers.

### Step 3 — Assign probabilities

Assign a probability to each scenario. Probabilities must sum to 100%.
Use the evidence from `/source-audit` to anchor estimates.
If no base rate exists, use 25/50/25 as a prior and note the uncertainty.

| Scenario | Probability |
|----------|------------|
| Optimistic | X% |
| Base case | Y% |
| Pessimistic | Z% |

### Step 4 — Map outcome metrics

For each scenario, project the key metrics at the chosen time horizon.

| Metric | Optimistic | Base case | Pessimistic |
|--------|-----------|-----------|-------------|
| Metric 1 | … | … | … |
| Metric 2 | … | … | … |

Calculate expected value for each metric:
`EV = (O × P_O) + (B × P_B) + (P × P_P)`

### Step 5 — Identify decision triggers

For each scenario transition (e.g., "base → pessimistic"), name the observable
signal that would tell you the scenario is unfolding:

| Transition | Observable signal | Lead time |
|------------|------------------|-----------|
| Base → Optimistic | … | … |
| Base → Pessimistic | … | … |

### Step 6 — Output the Scenario Report

```markdown
# Scenario Report

**Decision question:** …
**Date:** …
**Time horizon:** …

## Key uncertainty drivers
1. [Driver]: [low value] → [high value]
2. …

## Scenarios
[table from Step 2]

## Probabilities
[table from Step 3]

## Outcome metrics
[table from Step 4]

## Expected values
- Metric 1 EV: …
- Metric 2 EV: …

## Decision triggers
[table from Step 5]

## Implication for the decision
[2–3 sentences: given the expected value and downside, what does this suggest?]
```

Save to `decision-log/scenario-<YYYY-MM-DD>.md`.

## Quality criteria

The skill has performed well when:

- The three scenarios are narratively distinguishable, not just ±10% variants.
- Probabilities are anchored to at least one base rate or evidence source.
- At least one decision trigger is observable within the planning horizon.
- Expected value is computed for the primary success metric.
- The implication section gives a directional recommendation, not a hedge.
