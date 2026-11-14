# Ascend IQ Failure Audit

11 confirmed failures: #HALLUCINATION ×9, #UX_TRUST ×1, #ROBUSTNESS ×1, #FAIRNESS ×0. I changed 1 of the judge’s calls.

| Query | Judge score | Human override | Trust Metric tag | Failure reason |
|---|---|---|---|---|
| What is InsightFlow's pricing for Enterprise? | 0 |  | #HALLUCINATION | The answer uses an outdated price and invents a 10-seat minimum, whereas the reference states, "Old Price: $49/mo. New Price (Updated yesterday): $59/mo." |
| Summarize the top 3 complaints from DataViz's G2 reviews. | 1 |  |  |  |
| Does InsightFlow support native SQL export? | 0 |  | #HALLUCINATION | The answer claims native SQL export is supported while omitting a critical limitation from the reference: "there is no "Native Export" button in the UI." |
| List the confirmed speakers for SaaStr. | 0 |  | #HALLUCINATION | The answer lists Sam Altman as a confirmed speaker, contradicting the reference which notes, "Sam Altman is listed as "Invited/Tentative."" |
| What is the sentiment of the latest TechCrunch article on us? | 0 |  | #HALLUCINATION | The answer invents specific praise for the UI and criticism of pricing that do not appear in the reference, which only states, "Sentiment: Neutral/Positive." |
| Give me a bio for Sarah Jenkins, the new VP at DataViz. | 0 | 1, Sarah was a director at Salsforce. |  | The answer inaccurately lists Sarah Jenkins's previous title as Director instead of Senior Director, contradicting the reference: "Prev: Sr. Director @ Salesforce." |
| Compare our API rate limits to Competitor Z. | 0 |  | #HALLUCINATION | The answer falsely claims Competitor Z has strict throttling compared to our API, whereas the reference states, "Us: 500 req/min. Competitor Z: 1000 req/min (Twice as fast)." |
| Is Competitor X SOC2 compliant? | 0 |  | #ROBUSTNESS | The agent claims it cannot find compliance documents even though the reference explicitly confirms compliance with ""SOC2 Type II Certified" badge visible." |
| When was InsightFlow's last funding round? | 0 |  | #HALLUCINATION | The answer fabricates that the funding round was a Series B, which is unsupported by the reference: "March 15, 2023. Amount: $45M." |
| Who is the CEO of DataViz? | 1 |  |  |  |
| Does Competitor Y integrate with HubSpot? | 0 |  | #HALLUCINATION | The answer mischaracterizes the integration as seamless and omits the third-party requirement noted in the reference: "HubSpot integration available via Zapier partnership." |
| What are the primary brand colors for InsightFlow? | 0 |  | #HALLUCINATION | The answer fabricates a hex code and misidentifies Charcoal as a primary color, contradicting the reference: "Primary: Electric Blue. Secondary: Charcoal." |
| Summarize the lawsuit mentioned in the WSJ about Competitor Z. | 1 |  |  |  |
| List the HQ locations for DataViz. | 0 |  | #HALLUCINATION | The answer incorrectly lists Austin as a headquarters location when the reference specifies, "HQ: San Francisco. Engineering Hub: Austin." |
| How many employees does InsightFlow have? | 1 |  |  |  |
| Draft a cold email about our new feature. | 0 |  | #UX_TRUST | The answer uses casual slang ("killer", "game changer") that undermines credibility and violates the reference guidance: "Tone: Confident, professional, expert. Avoid slang." |
| Does Competitor X offer 24/7 support? | 1 |  |  |  |
| What database backend does DataViz use? | 1 |  |  |  |
| Summarize the latest release notes for InsightFlow. | 1 |  |  |  |
| What is the market cap of Competitor Z? | 1 |  |  |  |
