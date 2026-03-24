---
name: synthesize
version: 1.0.0
description: |
  Final decision brief: synthesizes outputs from all hstack skills into a
  single recommendation with a calibrated confidence level, key arguments
  for and against, and logged next steps. Run this last, after /pre-mortem
  and /stress-test. Produces the artifact that goes into /decision-log/.
  Invoke with /synthesize when ready to commit to or reject an option.
allowed-tools:
  - Read
  - Write
  - AskUserQuestion
---

# /synthesize — Final Decision Brief & Confidence Scoring

Combines all upstream analysis into a single, actionable decision brief.
Forces explicit confidence scoring, captures the strongest counter-arguments,
and writes the outcome to `/decision-log/` so future decisions can learn from it.

## When to invoke

Run `/synthesize` **last**, after completing at least:
- `/reframe` (required)
- `/source-audit` (required)
- One of: `/scenario`, `/pre-mortem`, `/stress-test` (at least one required)

Can also be run standalone as a structured reflection tool when time is short.

## Arguments

- `/synthesize` — interactive: prompts for prior skill outputs
- `/synthesize --inputs <paths>` — comma-separated paths to prior skill reports
- `/synthesize --quick` — skip stakeholder and counter-argument sections for speed

## Input

| Field | Description |
|-------|-------------|
| Reframe Report | Output from /reframe |
| Source Audit | Output from /source-audit |
| Scenario Report | Output from /scenario (optional) |
| Pre-Mortem Report | Output from /pre-mortem (optional) |
| Stress Test Report | Output from /stress-test (optional) |

## Instructions

### Step 1 — Identify the options under consideration

List every option on the table, including "do nothing" and "delay."
For each option, state in one sentence what it commits to and what it forecloses.

| Option | Commits to | Forecloses |
|--------|-----------|-----------|
| A: … | … | … |
| Do nothing | … | … |

### Step 2 — Summarize the evidence

In three bullet points per upstream skill, summarize what each analysis revealed.
Do not repeat full tables — synthesize to the core insight only.

Format:
```
/reframe:
  - Key insight 1
  - Key insight 2
  - Key insight 3

/source-audit:
  - …
```

### Step 3 — Score each option

Score each option against three criteria (1–5):

| Criterion | 1 | 3 | 5 |
|-----------|---|---|---|
| **Evidence strength** | Mostly RED/unanchored claims | Mixed GREEN/YELLOW | Mostly GREEN claims |
| **Expected value** | Negative or break-even only in optimistic | Positive in base case | Strongly positive in base + pessimistic |
| **Risk-adjusted downside** | Unrecoverable if pessimistic | Painful but survivable | Manageable even in worst case |

Overall score = average of the three criteria.

### Step 4 — State the recommendation

Pick one option. Write:

```
**Recommendation:** [Option name]
**Confidence:** X% (LOW <50% / MEDIUM 50–75% / HIGH >75%)
**Decision type:** Reversible / Partially reversible / Irreversible
```

Confidence must be calibrated: start at 50%, then:
- +10% for each GREEN-scored source audit claim that supports the option
- −10% for each CRITICAL pre-mortem failure mode without a mitigation
- +5% if base-case scenario expected value is positive
- −15% if break-even horizon exceeds the stated timeframe

### Step 5 — Steelman the counter-argument

Write the single strongest argument **against** the recommendation in ≥3 sentences.
Be genuinely persuasive — weak counter-arguments are not useful.
Then state why you are proceeding despite it.

### Step 6 — Define next steps and review trigger

List 3–5 concrete next steps, each with an owner and a due date.
Then define one review trigger: a measurable condition that would prompt
revisiting this decision before the planned review date.

### Step 7 — Write the Decision Brief

```markdown
# Decision Brief

**Question:** …
**Date:** …
**Timeframe:** …
**Decision made by:** …

## Options considered
[table from Step 1]

## Evidence summary
[bullets from Step 2]

## Option scores
[table from Step 3]

## Recommendation
**Recommendation:** …
**Confidence:** X% (LOW / MEDIUM / HIGH)
**Decision type:** Reversible / Partially reversible / Irreversible

## Strongest counter-argument
…

## Why proceeding despite it
…

## Next steps
| # | Action | Owner | Due |
|---|--------|-------|-----|
| 1 | … | … | … |

## Review trigger
[condition that prompts early re-evaluation]

## Skills used
- [ ] /reframe
- [ ] /source-audit
- [ ] /scenario
- [ ] /pre-mortem
- [ ] /stress-test
```

Save to `decision-log/decision-brief-<YYYY-MM-DD>.md`.
This is the canonical artifact for this decision. All prior skill outputs are supporting documents.

## Quality criteria

The skill has performed well when:

- Every option includes "do nothing" or "delay."
- Confidence level is calibrated using the scoring rules, not gut feel.
- The counter-argument is genuinely persuasive (not a strawman).
- Next steps are specific: each has an owner and a date.
- The review trigger is measurable and within the planning horizon.
