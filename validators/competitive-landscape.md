# Validator: Competitive Landscape

**Purpose:** Confirm that no competitor, substitute, or incumbent makes the decision's core value proposition redundant, uncompetitive, or legally blocked.

**When to use:** Any decision that enters a market, launches a product, or expands into a segment where other actors already operate. Required when `/source-audit` flags competitive positioning claims as YELLOW or RED.

---

## Hypothesis to validate

> "[DECISION] is viable because no existing competitor or substitute satisfies [TARGET CUSTOMER]'s need for [VALUE PROPOSITION] at [PRICE POINT] at the required scale."

Fill in the brackets before running this validator.

---

## Validation method: Competitive Landscape Audit

### Step 1 — Enumerate competitors and substitutes

List every option a target customer currently uses to solve the same problem.
This includes:
- **Direct competitors:** Same product category
- **Indirect competitors:** Different category, same job-to-be-done
- **DIY / workarounds:** Spreadsheets, manual processes, doing nothing
- **Incumbents with lock-in:** Enterprise contracts, switching costs, network effects

Minimum: 5 options. If you find fewer than 5, you have not looked hard enough.

**Sources to check:**
- G2, Capterra, ProductHunt (for software)
- Google search: "[pain point] solution", "[pain point] alternative", "[pain point] software"
- LinkedIn: companies with relevant keywords in their description
- Crunchbase: companies in the same category with funding in the last 3 years
- Target customer interviews: "What do you use today to solve this?"

### Step 2 — Score each competitor on five dimensions

Rate each competitor 1–5 on:

| Dimension | 1 | 3 | 5 |
|-----------|---|---|---|
| **Fit for target segment** | Wrong customer entirely | Partial overlap | Direct overlap |
| **Price competitiveness** | Much cheaper than you | Similar | Much more expensive than you |
| **Switching cost imposed on customer** | None | Moderate | High (data lock-in, contracts) |
| **Execution quality** | Poor product/service | Adequate | Excellent, well-funded |
| **Rate of improvement** | Stagnant | Incremental | Rapidly improving |

Sum each competitor's score (max 25). Rank them.

### Step 3 — Identify your differentiation

State in one sentence why your option is better **for the specific target segment**
than the top-ranked competitor. The differentiation must be:
- Specific (not "better quality" or "lower price" without data)
- Defensible over 12 months (not easily copied)
- Valued by the target customer (confirmed via customer interviews, not assumed)

### Step 4 — Check for legal and regulatory blockers

For the top 3 competitors, check:
- Do they hold relevant patents? (Google Patents search)
- Do they operate under an exclusive contract or partnership in your target market?
- Are there regulatory requirements (licenses, certifications) you don't currently have?

---

## Threshold values

| Finding | Interpretation |
|---------|---------------|
| No competitor scores >15 AND differentiation is specific and defensible | Competitive position **VIABLE** — proceed |
| 1–2 competitors score 16–20; differentiation exists but narrow | Position **FRAGILE** — acceptable if execution risk is low; flag in `/pre-mortem` |
| Any competitor scores >20 OR differentiation is not specific/defensible | Position **NOT VIABLE** — do not proceed without a pivot to a narrower segment |
| Any legal/regulatory blocker found | **HARD BLOCK** — resolve before any other analysis |

---

## Minimum viable artifact

A markdown file with:
- Date and analyst name
- Competitor table with scores on 5 dimensions
- Differentiation statement (one sentence)
- Legal/regulatory status (clear / flagged items)
- Verdict: Viable / Fragile / Not Viable / Blocked

Template: `validators/artifacts/competitive-landscape-<YYYY-MM-DD>.md`

---

## Edge cases

- **Monopoly or oligopoly market:** Score the incumbent's switching costs carefully. If >20, treat as a hard barrier and re-run `/reframe` to find a segment the incumbent doesn't serve well.
- **Geographic expansion:** Run the audit separately for the new geography — competitive dynamics often differ.
- **Platform risk:** If a competitor is a platform you depend on (e.g., Amazon, App Store), rate their "rate of improvement" as 5 and flag the existential dependency in `/pre-mortem`.
