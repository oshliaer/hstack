---
name: reframe
version: 1.0.0
description: |
  Problem reframing and hidden-assumption detection for strategic decisions.
  Breaks the decision open by challenging how the question is framed, surfacing
  unstated assumptions, and generating alternative framings. Use this skill first —
  before any analysis — to make sure you are solving the right problem.
  Invoke with /reframe when given a decision question and context.
allowed-tools:
  - Read
  - Write
  - AskUserQuestion
---

# /reframe — Problem Reframing & Assumption Audit

Challenges the framing of a strategic decision before any analysis begins.
Prevents wasted effort on well-executed answers to the wrong question.

## When to invoke

Run `/reframe` as the **first skill** in every decision workflow.
Also run it whenever a decision feels stuck or conclusions conflict.

## Arguments

- `/reframe` — interactive: prompts for question, context, and timeframe
- `/reframe "<question>"` — skips the question prompt
- `/reframe --silent` — no clarifying questions; work from what is given

## Input

Provide all three:

| Field | Description | Example |
|-------|-------------|---------|
| `DECISION_QUESTION` | The decision as currently stated | "Should I take a $500K loan to expand the business?" |
| `CONTEXT` | Business model, key metrics, constraints, stakeholders | Revenue, burn rate, market position, team size |
| `TIMEFRAME` | short (≤6 months) / medium (6–24 months) / long (>2 years) | medium |

## Instructions

### Step 1 — Parse the question

Read the decision question literally. Identify:

- **The actor** — who is deciding?
- **The action** — what is the proposed course of action?
- **The assumption** — what must be true for this to be the right question?
- **The alternative** — what is NOT being asked but probably should be?

Write these four elements as a brief table.

### Step 2 — Surface hidden assumptions

List every assumption buried in the question and context. For each:

1. State the assumption explicitly.
2. Rate its certainty: **Known** / **Believed** / **Guessed** / **Unknown**.
3. Mark whether the decision outcome flips if the assumption is wrong.

Use this table format:

| # | Assumption | Certainty | Decision-flipping? |
|---|------------|-----------|-------------------|
| 1 | … | Known / Believed / Guessed / Unknown | Yes / No |

Minimum 5 assumptions. Stop at 10 unless more are clearly relevant.

### Step 3 — Generate alternative framings

Produce 3–5 alternative ways to frame the same underlying problem.
Each reframing must:

- Shift who the actor is, what is being optimized for, OR what the real constraint is.
- Open at least one option that the original framing forecloses.

Format:

```
Reframe A: [one-sentence question]
Why this matters: [what it unlocks]

Reframe B: …
```

### Step 4 — Apply the 5 Whys

Take the original question. Ask "Why does this matter?" five times.
Stop early if you reach a root motivation that changes the decision space.

Format:

```
Why 1: [answer]
Why 2: [answer]
…
Root motivation: [one sentence]
```

### Step 5 — Output the Reframe Report

Produce a single markdown document:

```markdown
# Reframe Report

**Original question:** …
**Date:** …
**Timeframe:** short / medium / long

## Actor, Action, Assumption, Alternative
[table from Step 1]

## Hidden Assumptions
[table from Step 2]

## Alternative Framings
[list from Step 3]

## 5 Whys
[chain from Step 4]

## Recommended question to proceed with
[pick the most decision-useful framing; explain why in ≤3 sentences]
```

Save this report to `decision-log/reframe-<YYYY-MM-DD>.md`.

## Quality criteria

The skill has performed well when:

- At least one hidden assumption is marked **Guessed** or **Unknown** AND **decision-flipping**.
- At least one alternative framing would lead to a materially different set of options.
- The recommended question to proceed with differs meaningfully from the original.
- The report is usable as the input context for `/source-audit` and `/scenario`.
