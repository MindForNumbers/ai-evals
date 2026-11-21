# Module 4 · Launch Strategy · Ascend IQ Copilot

## 4.0 Release Criteria

| Gate | Failure | Metric | Threshold | Dataset | Method | Runs at |
|---|---|---|---|---|---|---|
| Hard | Wrong Pricing (#HALLUCINATION) | Share of pricing answers where every quoted dollar amount or numeric figure appears verbatim in the retrieved reference text (or uses "custom pricing" / "contact sales" with zero $ signs when no reference price exists). | 100% pass rate (0 fabricated pricing figures allowed; 0 misses and 0 false alarms across the golden dataset) | Ascend IQ golden set | Code-based check | Pull Request |
| Soft | Row 5 · Hallucination: lists an unconfirmed speaker as confirmed | Share of event and speaker answers that list invited or tentative individuals as confirmed speakers against the reference agenda. | 95% pass rate (or <= 5% unconfirmed-speaker hallucinations across the golden dataset) | Ascend IQ golden set | LLM judge | Staging |
| Advisory | Row 17 · Tone: slang detected | Share of drafted customer-facing emails that contain casual slang or violate the confident, professional brand voice guidelines. | 90% pass rate (or <= 10% slang/tone violations across the golden dataset) | Ascend IQ golden set | Code-based check | Pull Request |

## CI Gate Request for Engineering

- **Hard gate · Wrong Pricing (#HALLUCINATION).** Check: the code-based check, run on the Ascend IQ golden set at Pull Request. Measures: Share of pricing answers where every quoted dollar amount or numeric figure appears verbatim in the retrieved reference text (or uses "custom pricing" / "contact sales" with zero $ signs when no reference price exists).. Passes when: 100% pass rate (0 fabricated pricing figures allowed; 0 misses and 0 false alarms across the golden dataset). On a fail: block the merge.
- **Soft gate · Row 5 · Hallucination: lists an unconfirmed speaker as confirmed.** Check: the LLM judge, run on the Ascend IQ golden set at Staging. Measures: Share of event and speaker answers that list invited or tentative individuals as confirmed speakers against the reference agenda.. Passes when: 95% pass rate (or <= 5% unconfirmed-speaker hallucinations across the golden dataset). On a fail: pause the release until the PM signs off on an override.
- **Advisory gate · Row 17 · Tone: slang detected.** Check: the code-based check, run on the Ascend IQ golden set at Pull Request. Measures: Share of drafted customer-facing emails that contain casual slang or violate the confident, professional brand voice guidelines.. Passes when: 90% pass rate (or <= 10% slang/tone violations across the golden dataset). On a fail: post a warning, and don't block.

## Mitigation Plan · Soft Gate

If our Soft gate fails (unconfirmed event speakers are listed as confirmed above our 5% failure threshold), I recommend a staged rollout (launching to 5% of users first) because it allows us to cap executive exposure to inaccurate conference agendas, monitor live LLM-judge scores in production, and immediately roll back if accuracy drops while we expand our golden dataset.
