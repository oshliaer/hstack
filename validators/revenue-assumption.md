# Validator: Revenue & Growth Assumption

**Purpose:** Verify that projected revenue figures, growth rates, or conversion assumptions are grounded in comparable real-world evidence.

**When to use:** Any decision that depends on a specific revenue number, growth rate, or conversion rate. Required when `/source-audit` flags financial projections as RED/YELLOW or Unanchored.

---

## Hypothesis to validate

> "Revenue from [DECISION] will reach [TARGET] within [TIMEFRAME] given [ASSUMPTION]."

Fill in the brackets before running this validator.

---

## Validation method: Reference Class Benchmarking

### Step 1 — Find the reference class

A reference class is a group of businesses or decisions that are similar in:
- Business model (SaaS, retail, service, marketplace, etc.)
- Stage (early-stage, growth, established)
- Geography and market

**Minimum: 3 comparable examples.** Sources:

| Source | What to find |
|--------|-------------|
| Crunchbase / PitchBook | Revenue milestones for funded companies in your space |
| Industry reports (IBISWorld, Statista, McKinsey) | Average growth rates for the sector |
| Public company 10-Ks | Revenue ramp curves for similar businesses 5–10 years ago |
| Operator communities (Indie Hackers, SaaStr, YC forums) | Self-reported growth metrics from founders |

### Step 2 — Extract the comparable metric

For each comparable, extract:
- Time to reach the revenue milestone
- Starting conditions (team size, capital, market context)
- Any structural differences from your situation

### Step 3 — Compute the reference class range

Calculate: median, 25th percentile (pessimistic), and 75th percentile (optimistic)
of time-to-milestone or growth rate across your comparables.

---

## Threshold values

| Finding | Interpretation |
|---------|---------------|
| Your projection ≤ 75th percentile of reference class | Assumption **PLAUSIBLE** — proceed |
| Your projection between 75th and 90th percentile | Assumption **AGGRESSIVE** — flag in `/scenario` as optimistic-only |
| Your projection > 90th percentile of reference class | Assumption **FALSIFIED** — revise downward before proceeding |
| Fewer than 3 comparables found | Assumption **UNANCHORED** — treat as Unknown in `/source-audit`; validate with customer interviews instead |

---

## Minimum viable artifact

A markdown file with:
- Date and analyst name
- Table: 3+ comparables with metric, source, and structural notes
- Computed range: pessimistic / median / optimistic
- Verdict: Plausible / Aggressive / Falsified / Unanchored

Template: `validators/artifacts/revenue-assumption-<YYYY-MM-DD>.md`

---

## Edge cases

- **New market (no comparables):** Use the closest adjacent market as a ceiling, not a target. Treat the assumption as Unanchored and run `market-validation.md` first.
- **Internal projections from sales team:** These are systematically optimistic. Apply a 0.6× correction factor as a starting point, then seek external reference class.
- **Growth rate vs. absolute revenue:** If only growth rates (not absolute figures) are available, convert your projection to an implied growth rate and compare against the reference class distribution.
