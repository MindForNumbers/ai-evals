# Module 5 · Eval Budget · Ascend IQ

**Quarterly budget cap:** $200,000
**Online eval spend:** $180,000 (3 of at most 3 online evals)

## Budget

| Failure | Trust metric | Risk | Level | Cost |
| --- | --- | :---: | :---: | ---: |
| Data Fabrication | Hallucination Rate | P0 | Online eval | $85,000 |
| Context Specificity | Robustness | P1 | Online eval | $70,000 |
| Overconfident Tone | UX Trust | P1 | Periodic audit | $6,500 |
| Data Bias | Fairness | P2 | Periodic audit | $5,500 |
| Slow Answers | Latency | P3 | Online eval | $25,000 |

## Downgrades

### Periodic audit · Overconfident Tone (UX Trust · P1)
- **Cheaper check:** Weekly LLM-judge audit reviewing 150 live answers where source evidence is partial or indirect to verify the agent uses calibrated hedging language instead of stating guesses as facts.
- **Why it’s enough:** What it still catches: Catches systemic prompt or model drift where the agent presents unverified inferences as definitive facts across weekly sample reviews at 90% lower cost than continuous online scoring.
What it misses: Individual unhedged statements on unsampled queries between weekly audits.
Why we can live with that: Tone calibration shifts gradually across model/prompt updates rather than per query, and our Data Fabrication checks already catch outright false numbers—making a $6,500 weekly audit sufficient without spending $65,000 on live traffic scoring.

### Periodic audit · Data Bias (Fairness · P2)
- **Cheaper check:** Weekly stratified audit reviewing 100 multi-region summaries to compare US vs. APAC source citation counts and coverage balance.
- **Why it’s enough:** What it still catches: Catches systemic US-over-APAC weighting drift in weekly sample reviews at 90% lower cost than continuous online scoring.
What it misses: Real-time regional imbalances on individual unsampled queries between weekly audits.
Why we can live with that: Geographic dataset balance shifts slowly across index updates rather than per query, and most current Ascend IQ users focus primarily on US markets—so a $5,500 weekly audit protects regional quality without spending $55,000 on live traffic scoring.

