# Module 5 · Coverage Matrix · Competitor Signal Tracker

## Coverage Row

| Product | Hallucination Rate | Fairness | Latency | UX Trust | Robustness |
|---|---|---|---|---|---|
| Competitor Signal Tracker | ❌ Gap | ❌ Gap | ✅ Covered | ✅ Covered | ❌ Gap |

## What Runs Today

- A timer alerts if the nightly scoring run takes more than 2 hours.
- A style check flags summaries written in a casual or alarmist tone before they reach the sales team.

## Accepted Gap

**Fairness.** We accept this gap because Competitor Signal Tracker is an internal tool used only by Ascend sales and strategy teams to score public competitor news and social posts, so demographic or group fairness carries very low business risk today and building a multi-segment fairness audit would cost more than it saves.

We’ll look again: We'll look again if Competitor Signal Tracker outputs are surfaced directly to external clients or if international/SMB market coverage expands beyond 20% of tracked accounts, and we will review it during the Q2 portfolio eval budget check.

## Critical Gap

We’ve flagged Hallucination Rate as the most critical gap for Competitor Signal Tracker because We've flagged Hallucination Rate as the most critical gap for Competitor Signal Tracker because if it fabricates competitor news or pricing claims tomorrow, internal sales reps and downstream Ascend models will notice first when pitching prospects or feeding corrupted signals into client-facing intelligence—costing us lost enterprise deals, damaged executive credibility, and potential commercial disparagement exposure. To close it, we'll add a new eval gate in the nightly pipeline combining deterministic numeric/pricing verification with an LLM-as-a-judge grounding check against the source articles before any digest is published.

## After the Pressure Test

Corrected initial coverage marks (Step 01): Changed Hallucination Rate, Fairness, and Robustness from Covered/Partial to Not covered (❌) after reviewing what actually runs today on Competitor Signal Tracker (only a 2-hour nightly batch timer and a tone/style check). Kept UX Trust as Covered (✅) and Latency as Partial (⚠️).   Prioritized Hallucination Rate over Fairness (Steps 02–03): Accepted Fairness for now with clear re-evaluation triggers (external client exposure or >20% international/SMB coverage), and prioritized closing Hallucination Rate first via a nightly numeric + LLM-judge grounding gate because corrupted signals directly impact internal sales reps and downstream Ascend models
