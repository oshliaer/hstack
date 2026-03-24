# Validator: Market Existence

**Purpose:** Confirm that a meaningful market exists for the product, service, or expansion the decision depends on.

**When to use:** Any decision that assumes customers exist and are willing to pay. Required when `/source-audit` flags market size or demand claims as RED or YELLOW.

---

## Hypothesis to validate

> "There is a sufficient number of customers who have [PAIN POINT] and are willing to pay [PRICE POINT] for [SOLUTION]."

Fill in the brackets before running this validator.

---

## Validation method: Customer Discovery Sprint

### Minimum artifact required

**5 customer interviews** (real conversations, not surveys) that meet all of the following:
- Participant matches the target customer profile (define it explicitly before interviewing).
- Interview follows the Mom Test protocol: ask about past behavior, not hypothetical future behavior.
- Interview explores whether the pain point is actively felt, not just acknowledged.

### Interview script (Mom Test–compatible)

1. Tell me about the last time you experienced [PAIN POINT].
2. What did you do about it? What did you try first?
3. How much time/money did you spend dealing with it last [month/quarter]?
4. What would have to be true for you to stop using [current workaround]?
5. If a solution cost [PRICE POINT], would that be expensive, fair, or cheap compared to what you spend now?

Do not describe your solution until question 5. Do not ask "would you use this?"

### How to find 5 participants

- Your existing customer list (fastest)
- LinkedIn outreach to people with the relevant job title/role (2–3 day turnaround)
- r/[relevant subreddit] — look for complaints matching the pain point
- Industry Slack/Discord communities

Offer a 20-minute call. No compensation required if the pain is real.

---

## Threshold values

| Outcome | Interpretation |
|---------|---------------|
| ≥4 of 5 confirm pain is active and costly | Hypothesis **CONFIRMED** — proceed |
| 3 of 5 confirm pain | Hypothesis **WEAK** — narrow the customer segment and retest |
| <3 of 5 confirm pain | Hypothesis **FALSIFIED** — market-existence assumption is unproven; reassess the decision |

"Confirm" means: they described the pain unprompted OR reported spending time/money on it.

---

## Minimum viable artifact

A markdown file with:
- Date and interviewer name
- 5 rows: participant role, pain confirmed (Y/N), verbatim quote, willingness-to-pay signal
- Summary: confirmed / weak / falsified + one-sentence recommendation

Template: `validators/artifacts/market-validation-<YYYY-MM-DD>.md`

---

## Edge cases

- **B2B with long sales cycles:** 5 interviews with economic buyers (not end users) who have budget authority.
- **Regulated markets:** Substitute "would pay" with "would budget for" or "would recommend to procurement."
- **Existing customers:** If you already have paying customers, 3 of 5 existing customers describing the expanded pain is sufficient for CONFIRMED.
