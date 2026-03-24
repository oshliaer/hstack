---
name: pre-mortem
version: 1.0.0
description: |
  Pre-mortem analysis and failure mode risk matrix for strategic decisions.
  Imagines that the decision was executed and failed, then works backward
  to find the most likely causes. Produces a risk matrix scored by likelihood
  and impact, with mitigations. Run before finalizing a decision.
  Invoke with /pre-mortem when you have a plan or strong leading option.
allowed-tools:
  - Read
  - Write
  - AskUserQuestion
---

# /pre-mortem — Failure Mode & Risk Matrix

Runs a structured pre-mortem to surface the most dangerous failure modes before
a decision is locked in. Turns hindsight bias into foresight by assuming failure
has already happened and asking why.

## When to invoke

Run `/pre-mortem` **after `/scenario`** and before `/synthesize`.
Essential when: the decision is irreversible, involves significant capital,
or stakeholders are highly aligned (alignment suppresses dissent).

## Arguments

- `/pre-mortem` — interactive: prompts for plan and context
- `/pre-mortem --plan "<description>"` — describe the leading option inline
- `/pre-mortem --scenarios <path>` — load scenario output to use as context

## Input

| Field | Description | Example |
|-------|-------------|---------|
| Leading option | The plan that is most likely to be chosen | "Take $500K loan, hire 5 staff, open new location" |
| Context | Business state, constraints, stakeholders | Revenue, team, market position |
| Scenario report | Output from /scenario (optional but recommended) | Path or inline |

## Instructions

### Step 1 — Set the failure frame

Write one sentence: "It is 18 months from now. We executed the plan and it failed badly."
Then write one sentence: "The most obvious thing people say in hindsight is: _______."

This primes the analysis. Fill in the blank before proceeding.

### Step 2 — Generate failure modes via Red Team

Generate 8–12 distinct failure modes. Use these trigger questions to ensure coverage:

- **Execution failures:** What could we do wrong even if the plan was correct?
- **Assumption failures:** Which assumption from `/source-audit` was wrong?
- **Market failures:** How did the external environment not cooperate?
- **Resource failures:** What ran out — cash, time, people, or attention?
- **Stakeholder failures:** Who didn't do what we needed them to do?
- **Second-order failures:** What did we fix that broke something else?
- **Unknown unknowns:** What didn't we know we didn't know?

Each failure mode must be specific enough to be actionable (not "bad luck").

### Step 3 — Score each failure mode

Score every failure mode on two dimensions (1–5):

| Dimension | 1 | 3 | 5 |
|-----------|---|---|---|
| **Likelihood** | Very unlikely (<10%) | Possible (30–50%) | Very likely (>70%) |
| **Impact** | Minor setback | Significant cost/delay | Existential / unrecoverable |

Risk score = Likelihood × Impact (max 25).

Flag: **CRITICAL** ≥ 16, **HIGH** 9–15, **MEDIUM** 4–8, **LOW** ≤ 3.

### Step 4 — Assign mitigations

For each CRITICAL and HIGH failure mode, assign:

- **Prevention:** What action before or during execution reduces likelihood?
- **Detection:** What early-warning signal tells you this is happening?
- **Recovery:** If it happens anyway, what limits the damage?

### Step 5 — Identify non-negotiable conditions

From the CRITICAL failures, extract the 2–3 conditions that must be true
for the plan to have an acceptable risk profile. These become go/no-go criteria.

Format:
```
Non-negotiable #1: [condition that must hold]
  — If false, reconsider the decision entirely.
```

### Step 6 — Output the Pre-Mortem Report

```markdown
# Pre-Mortem Report

**Decision / Plan:** …
**Date:** …
**Failure frame:** [sentence from Step 1]

## Failure Modes & Risk Matrix

| # | Failure Mode | Likelihood /5 | Impact /5 | Risk Score | Level |
|---|-------------|--------------|-----------|------------|-------|
| 1 | … | | | | CRITICAL/HIGH/MEDIUM/LOW |

## Mitigations (CRITICAL & HIGH only)

### Failure Mode #N — [name]
- **Prevention:** …
- **Detection:** …
- **Recovery:** …

## Non-negotiable conditions
1. …
2. …

## Overall risk assessment
[2–3 sentences: is the risk profile acceptable given the expected upside from /scenario?]
```

Save to `decision-log/pre-mortem-<YYYY-MM-DD>.md`.

## Quality criteria

The skill has performed well when:

- At least one CRITICAL failure mode is identified.
- Every CRITICAL failure mode has all three mitigations (prevention, detection, recovery).
- At least one non-negotiable condition would cause the decision to be reconsidered.
- The overall risk assessment connects explicitly to the upside from `/scenario`.
- No failure mode is vague (e.g., "things go wrong" is not acceptable).
