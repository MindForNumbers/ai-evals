# AI Evaluation Strategy Canvas

> Repo file `ai-evals/01-evaluation-strategy/strategy-canvas.md` (the repo is your submission).

## 1. Product Strategy, The Context

**Who it's for:** VP-level strategists and product leaders at Fortune 500 companies who pay upward of $50,000 a year for verified market intelligence.

**What they use it for:** Asking plain-language questions, like “Compare the pricing models of Stripe and Adyen,” and getting answers in seconds instead of digging through the platform.

**What's at stake:** Engagement is dropping, Q4 retention is at risk, and the CPO wants Ascend IQ live for the top 50 enterprise accounts next month. One poor answer to the wrong client can do lasting damage to the relationship.

## 2. Measurements, The Execution

**User promise.** For Fortune 500 strategy leaders, Ascend IQ promises answers typically under 10 seconds where every factual claim is traceable to a cited Ascend source, and an explicit “no verified data” response instead of a guess, so that they can put its answers straight into roadmap decisions and keep renewing.

**Top 3 trust metrics:**
- **Latency**, Response speed (P95 / P99). Slow kills engagement.
- **Hallucination Rate**, % of outputs that are confidently false or fabricated.
- **Robustness**, Coherence on messy, adversarial, out-of-scope inputs.

**Why these three:** Hallucination Rate
Why: One confidently fabricated number about a competitor’s pricing, given to a VP paying $50K+ for verified data, breaks the core promise and can cost the account. Target ≤1% (at an estimated ~X queries/week across 50 accounts, anything higher means multiple clients see a fabricated figure every week).

Robustness
Why: Executives will ask vague, multi-part, or out-of-scope questions, and Ascend IQ has to stay coherent and say “I don’t have data on that” instead of guessing. Target ≥95% of out-of-scope, ambiguous, or adversarial queries (e.g., attempts to extract other clients’ data or override instructions) correctly declined or clarified.

Latency
Why: Ascend IQ exists because finding answers in the dense platform takes too long; if the agent itself feels slow, VPs won’t build the habit, and the engagement problem it was built to fix persists. P95 under 10s, P99 under 20s (Soft gate). Consequence: VPs abandon a tool that feels broken and fall back to analysts or competitors, which kills adoption in the 50-account pilot. **Guardrail · Over-refusal:** ≤10% of in-scope questions (where Ascend has the data) get a refusal or "no verified data" response. Consequence: if Ascend IQ declines questions it should answer, VPs conclude it's useless and stop asking. This guardrail keeps our hallucination-first strategy from quietly turning into a timid agent.

## 3. Strategic Trade-Offs, The Cost

### Trade-off 1 · Hallucination Rate ↔ Latency
We prioritize low hallucination rate over latency because a VP will wait an extra few seconds for an answer they can trust, but one fabricated competitor figure in a roadmap deck can cost us a $50K+ account. Speed only matters if the answer is right.

### Trade-off 2 · Hallucination Rate ↔ Robustness
We prioritize low hallucination over answer coverage because for a VP, “Ascend doesn’t have verified data on that” is an inconvenience, while a confident fabrication is a breach of what they pay for. We accept the cost: some questions will go unanswered or get a partial answer, and Sales must position Ascend IQ as “verified answers,” not “answers to anything.” We cap this cost with the over-refusal guardrail (≤10% of in-scope questions declined).

---
_Generated from the AI Evaluation Strategy Canvas, M1 lab tool, AI Evals Certification._
