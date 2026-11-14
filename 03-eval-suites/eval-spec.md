# Eval Spec · Ascend IQ

| Part | Spec |
|---|---|
| Target risk | Wrong Pricing (#HALLUCINATION), an output risk |
| Evaluator | The rule check from Lab 1 |
| Threshold | 100% pass rate (0 fabricated pricing figures allowed; 0 misses and 0 false alarms across the golden dataset) — supported by Lab 1 results where the rule check caught 1 of 1, the safety rule caught 1 of 1, and the judge caught 1 of 1 |
| Business stakes | VP-level B2B buyers rely on Ascend IQ for competitive intelligence and procurement benchmarking. Quoting fabricated or outdated Enterprise pricing erodes executive trust, derails client negotiations, damages brand credibility, and risks customer churn or legal disputes over inaccurate commercial representations. |
| Owner | AI Product Manager (defines the pricing threshold and golden dataset) and Platform/ML Engineering Lead (enforces the deterministic rule check as a CI/CD release gate and production guardrail, with Product Marketing/RevOps verifying pricing source updates). |

## Messages

**Engineering · acceptance criteria:** Block any response as a fail (`0`) if it contains a dollar amount (`$`) or numeric pricing figure not present verbatim in the retrieved reference text, or if an Enterprise pricing query lacks a reference figure and omits the exact phrase `"custom pricing"` or `"contact sales"`. Pass (`1`) only when every quoted pricing figure matches the reference verbatim or the fallback phrase is present with zero dollar signs.

**Design · what the user sees:** When the check blocks an unverified pricing response, replace the model output with a clear, transparent fallback state stating that verified Enterprise pricing is not available in the source documentation and directing the user to contact the vendor's sales team for custom pricing. Avoid displaying broken error states or speculative price ranges so VP buyers retain trust in the platform's data integrity.

**Leadership · risk and return:** Enforcing a 100% pass rate with zero fabricated pricing figures eliminates the risk of VP-level buyers making high-stakes procurement decisions on hallucinated numbers, protecting Ascend IQ against executive churn, brand damage, and legal exposure. Because this deterministic rule check caught 1 of 1 real failures with 0 false alarms in testing, it delivers complete protection at near-zero compute cost and latency.
