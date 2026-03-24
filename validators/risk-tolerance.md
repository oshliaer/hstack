# Validator: Risk Tolerance & Downside Acceptability

**Purpose:** Confirm that the decision-maker can genuinely absorb the worst-case outcome — financially, operationally, and psychologically.

**When to use:** Any decision that is partially or fully irreversible, involves a commitment of >10% of available capital, or has outcomes that are asymmetric (bounded upside, unbounded downside). Required when `/stress-test` identifies a worst-case loss that is ≥20% of current cash position.

---

## Hypothesis to validate

> "If this decision produces its worst-case outcome, we can recover within [TIMEFRAME] without existential harm to the business or key stakeholders."

Fill in the brackets before running this validator.

---

## Validation method: Pre-commitment Stress Interview

This validator requires a **structured conversation**, not a spreadsheet.
It must be done by the primary decision-maker(s), ideally with a trusted advisor
who has no stake in the outcome.

### Questions for the decision-maker

Work through all five questions. Record answers in writing.

**1. The walk-away question**
"If this goes to zero and you lose the full capital at stake — what exactly happens next? Walk me through the first 90 days."

A calm, specific answer is a green signal. Vagueness or avoidance is a red signal.

**2. The sleep test**
"On the night after committing to this decision, could you sleep? On the night after the worst case materializes — same question."

Both answers should be yes. If either is no, the risk is not actually acceptable.

**3. The stakeholder impact question**
"Who else is materially affected if this goes wrong? Have you had an explicit conversation with them about the downside?"

If key stakeholders have not been explicitly briefed on the downside, the tolerance has not been validated.

**4. The reversal question**
"At what point — and based on what signal — would you reverse course? What would make you cut losses?"

A specific answer (dollar amount, timeline, metric) is required. "We'd figure it out" is not an answer.

**5. The regret minimization question**
"Five years from now, which is more likely to cause regret: making this decision, or not making it?"

This question catches decisions where the real risk is opportunity cost, not downside.

---

## Threshold values

| Condition | Interpretation |
|-----------|---------------|
| All 5 answers are specific, calm, and consistent | Risk tolerance **CONFIRMED** — proceed |
| 3–4 specific answers; 1–2 vague or avoided | Risk tolerance **CONDITIONAL** — address the gaps before proceeding |
| <3 specific answers OR stakeholders not briefed | Risk tolerance **NOT CONFIRMED** — do not proceed until gaps are closed |
| Answer to Q4 (reversal) is absent | **HARD BLOCK** — no decision should be made irreversibly without a defined stop-loss |

---

## Minimum viable artifact

A markdown file with:
- Date and participants (decision-maker + advisor/facilitator)
- Five answers, verbatim or paraphrased faithfully
- Verdict: Confirmed / Conditional (with gap list) / Not Confirmed

Template: `validators/artifacts/risk-tolerance-<YYYY-MM-DD>.md`

---

## Edge cases

- **Solo founder:** Find a trusted advisor, mentor, or board member to run this with. Self-administered stress interviews are unreliable due to confirmation bias.
- **Partnership or board decision:** Every decision-maker with veto power must complete the exercise independently. Aggregate results — if any member is Not Confirmed, treat the group as Not Confirmed.
- **Personal decisions (not business):** Replace "business" with "personal finances/relationships" and adjust stakeholder question accordingly.
