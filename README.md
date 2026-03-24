# hstack

**Strategic decision support for founders, leaders, and operators — powered by Claude Code.**

hstack is a set of analytical skills modeled after [garrytan/gstack](https://github.com/garrytan/gstack),
re-oriented from *shipping code* to *making better decisions*. Where gstack gives you a virtual
engineering team, hstack gives you a virtual analyst team: a reframer, an evidence auditor,
a scenario planner, a risk analyst, a financial stress-tester, and a synthesis writer.

It works on any decision: financial, product, hiring, market entry, or personal.

---

## Quick start

```
1. Clone hstack into your Claude Code skills directory:
   git clone https://github.com/oshliaer/hstack ~/.claude/skills/hstack

2. Run /reframe — describe your decision, context, and timeframe.
3. Run /source-audit — give it the claims your decision depends on.
4. Run /scenario or /stress-test (or both) based on your decision type.
5. Run /pre-mortem — assume it failed; find the causes.
6. Run /synthesize — get the final recommendation with confidence level.
7. Log everything in /decision-log/.
```

---

## Skill sequence by decision type

### Financial decision (e.g., taking a loan, large capital allocation)

```
/reframe → /source-audit → /stress-test → /scenario → /pre-mortem → /synthesize
```

Use validators: `market-validation.md`, `revenue-assumption.md`, `risk-tolerance.md`

### Product decision (e.g., build vs. buy, enter new segment)

```
/reframe → /source-audit → /scenario → /pre-mortem → /synthesize
```

Use validators: `market-validation.md`, `competitive-landscape.md`

### Hiring or org decision (e.g., key hire, team restructure)

```
/reframe → /scenario → /pre-mortem → /synthesize
```

Use validators: `risk-tolerance.md`

### Personal or career decision (e.g., leave company, geographic move)

```
/reframe → /scenario → /pre-mortem → /synthesize
```

Use validators: `risk-tolerance.md`

---

## Repository structure

```
hstack/
├── skills/
│   ├── reframe/SKILL.md        # Problem reframing & hidden-assumption detection
│   ├── source-audit/SKILL.md   # Evidence & source reliability audit
│   ├── scenario/SKILL.md       # Scenario planning (optimistic/base/pessimistic)
│   ├── pre-mortem/SKILL.md     # Failure mode & risk matrix
│   ├── stress-test/SKILL.md    # Quantitative / financial stress testing
│   └── synthesize/SKILL.md     # Final decision brief & confidence scoring
├── validators/
│   ├── market-validation.md     # Confirm market existence via 5 customer interviews
│   ├── revenue-assumption.md    # Benchmark revenue projections against reference class
│   ├── risk-tolerance.md        # Pre-commitment stress interview for downside acceptance
│   └── competitive-landscape.md # Competitor scoring & differentiation audit
├── decision-log/
│   ├── TEMPLATE.md              # Blank decision log template
│   └── example-2026-03-24.md   # Worked example: $500K loan expansion decision
└── README.md                    # This file
```

---

## Skills

### `/reframe` — Problem Reframing & Assumption Audit

**Run this first.** Challenges how the decision is framed before any analysis begins.

- **Input:** Decision question, context, timeframe
- **Output:** Reframe Report with hidden assumptions table, 5 alternative framings, 5 Whys chain, recommended question
- **Methods:** Assumption mapping, 5 Whys, alternative framing generation
- **File:** `skills/reframe/SKILL.md`

---

### `/source-audit` — Evidence & Source Reliability Audit

**Run second.** Scores every claim and data source that the decision depends on.

- **Input:** Decision claims, sources, reframe output
- **Output:** Source Audit Report with claim scores (GREEN/YELLOW/RED), unanchored claims, validator recommendations
- **Methods:** Source reliability scoring (reliability × recency × relevance), base rate checking
- **File:** `skills/source-audit/SKILL.md`

---

### `/scenario` — Scenario Planning & Outcome Mapping

**Run for decisions with meaningful uncertainty.** Builds three distinct futures with probability weights.

- **Input:** Reframe + source-audit output, key metrics, timeframe
- **Output:** Scenario Report with 3 futures, probability weights, expected values, decision triggers
- **Methods:** Reference class forecasting, outcome tree, expected value calculation
- **File:** `skills/scenario/SKILL.md`

---

### `/pre-mortem` — Failure Mode & Risk Matrix

**Run before finalizing any irreversible decision.** Assumes the plan failed and works backward.

- **Input:** Leading option description, context, scenario output
- **Output:** Pre-Mortem Report with risk matrix (likelihood × impact), mitigations, non-negotiable conditions
- **Methods:** Pre-mortem, red-team questioning, FMEA-lite
- **File:** `skills/pre-mortem/SKILL.md`

---

### `/stress-test` — Financial & Quantitative Stress Testing

**Run for any decision with significant financial stakes.** Models break-even, downside exposure, and sensitivity.

- **Input:** Capital at stake, revenue projections, cost structure, cash position
- **Output:** Stress Test Report with cash model, sensitivity matrix, max-loss scenario, go/no-go thresholds
- **Methods:** Break-even analysis, sensitivity analysis, cash runway modeling
- **File:** `skills/stress-test/SKILL.md`

---

### `/synthesize` — Final Decision Brief & Confidence Scoring

**Run last.** Combines all upstream analysis into a single recommendation with calibrated confidence.

- **Input:** Outputs from all prior skills
- **Output:** Decision Brief with recommendation, confidence %, counter-argument, next steps, review trigger
- **Methods:** Multi-criteria scoring, confidence calibration, steelmanning
- **File:** `skills/synthesize/SKILL.md`

---

## Validators

Validators are real-world verification methods tied to specific hypotheses.
Run them when `/source-audit` flags a claim as RED or Unanchored.

| Validator | Use when | Falsification threshold |
|-----------|----------|------------------------|
| `market-validation.md` | Assuming customers exist and will pay | <3 of 5 interviews confirm pain → hypothesis falsified |
| `revenue-assumption.md` | Projecting revenue or growth rates | Projection >90th percentile of reference class → revise downward |
| `risk-tolerance.md` | Any irreversible or large capital commitment | <3 of 5 stress-interview answers are specific → do not proceed |
| `competitive-landscape.md` | Entering or competing in an existing market | Any competitor scores >20/25 without defensible differentiation → not viable |

---

## Decision log

Every decision processed through hstack should produce a log entry in `/decision-log/`.

### How to log

1. Run `/synthesize` — it saves a Decision Brief automatically.
2. Or copy `decision-log/TEMPLATE.md` and fill it in manually.
3. Name the file: `decision-log/decision-brief-<YYYY-MM-DD>.md`.
4. Supporting skill outputs (reframe, source-audit, etc.) go in the same folder with their own date-stamped names.

### Why log

- Future decisions reference past assumptions and outcomes.
- You track your calibration over time (were your confidence scores accurate?).
- Teams can share context without re-litigating history.
- At the review date, fill in the Outcome Log section to close the loop.

See `decision-log/example-2026-03-24.md` for a complete worked example.

---

## How to adapt hstack to your context

**Change the timeframe defaults:** Each skill accepts `--horizon <months>`. Set it to match your planning cycle.

**Add domain-specific validators:** Copy any file from `/validators/` as a template. Replace the hypothesis, methods, and thresholds for your industry.

**Extend the skill sequence:** For complex decisions, run `/scenario` and `/stress-test` in parallel — they are independent after `/source-audit`.

**Skip skills for speed:** At minimum, run `/reframe` + `/synthesize`. This takes 10–15 minutes and is better than no structure. Add the other skills when stakes are high.

---

## License

MIT. Fork it. Adapt it. Make better decisions.
