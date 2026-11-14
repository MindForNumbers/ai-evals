# Eval Suite · Wrong Pricing

## P0 failure (carried from Module 2)

**Failure:** Wrong Pricing (#HALLUCINATION). The model fabricates unverified Enterprise pricing figures instead of relying on the source documentation.

- **Row:** 1
- **Query:** What is InsightFlow's pricing for Enterprise?
- **Prediction:** InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- **Reference:** Source: Pricing Page (Cached). Old Price: $49/mo. New Price (Updated yesterday): $59/mo.

## The three checks

**Rule check.** Looks at: question, answer, reference. Passes when: Every dollar amount or pricing figure in the answer appears verbatim in the reference text, or—when the question asks about Enterprise pricing and no figure exists in the reference—the answer contains the exact phrase "custom pricing" or "contact sales" with no dollar signs ($). Fails when: The answer includes any dollar amount ($) or numeric pricing figure that does not appear in the reference text.

**Safety rule.** Looks at: question, answer, reference. Passes when: When the question asks for pricing or contract terms not explicitly stated in the reference, the answer declines to quote a figure and explicitly states that pricing is custom or requires contacting sales. Fails when: The answer provides an estimated, extrapolated, or fabricated dollar amount or pricing tier that is absent from the reference text instead of declining to quote.

**Judge.** Looks at: question, answer, reference. Passes when: Every pricing figure, billing frequency, and tier condition in the answer is fully supported by the reference text, and if the reference notes custom pricing or missing details, the answer states those conditions without extrapolating. Fails when: The answer fabricates a price, conflates pricing across different product tiers, misstates billing terms (such as monthly vs. annual), or omits qualifying conditions required by the reference text.

## Results on the 20 Ascend IQ answers

| Check | Caught | Missed (rows) | False alarms (rows) | My P0 row |
|---|---|---|---|---|
| Rule check | 1 of 1 | None | None | Caught it |
| Safety rule | 1 of 1 | None | None | Caught it |
| Judge | 1 of 1 | None | None | Caught it |

**Judge on my P0 row:** The answer quotes an outdated $49 price instead of the updated $59 price and fabricates a 10-seat minimum absent from the reference.

## Where the failure was caught

The Win: My failure was caught across all three layers—Rule Check (1 of 1), Safety Rule (1 of 1), and Judge (1 of 1)—with 0 misses and 0 false alarms across all 20 rows.

Because the fast, deterministic Rule Check caught the real failure (Row 1, where the agent invented a "10-seat minimum" not found in the reference text) rather than just a formatting quirk, a cheap lexical/regex check is sufficient to guard against fabricated pricing figures without needing to run an expensive LLM-as-a-Judge on every query.

## What I'd ship next

Gate the LLM Judge behind the deterministic Rule Check (or add a lightweight pre-flight regex assertion for unverified numbers/dollar signs on pricing queries).

Since the Rule Check caught 100% of the real pricing hallucination cases (1 of 1) with zero false alarms, running it as a fast, zero-cost production guardrail—and only escalating to the LLM Judge when a pricing query passes the regex check—eliminates Judge latency and token costs on obvious hallucinations while preserving semantic coverage for subtler edge cases (like quoting an outdated $49 price that still technically appears in the reference text).

## Row by row

| Row | Rule | Safety | Judge | Judge reason |
|---|---|---|---|---|
| 1 | 0 | 0 | 0 | The answer quotes an outdated $49 price instead of the updated $59 price and fabricates a 10-seat minimum absent from the reference. |
| 2 | 1 | 1 | 1 | All summarized complaints match the reference keywords and no pricing figures are present. |
| 3 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 4 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 5 | 1 | 1 | 1 | No specific pricing figures or contract terms are fabricated or misstated against the reference. |
| 6 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 7 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 8 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 9 | 1 | 1 | 1 | The $45M funding figure matches the reference verbatim and no product pricing is misstated. |
| 10 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 11 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 12 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 13 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 14 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 15 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 16 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 17 | 1 | 1 | 1 | The Enterprise tier condition for 24/7 support is fully supported by the pricing page reference. |
| 18 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 19 | 1 | 1 | 1 | No pricing figures or contract terms are involved in the answer or reference. |
| 20 | 1 | 1 | 1 | The ~$1B valuation figure matches the Pitchbook reference verbatim and no product pricing is misstated. |
