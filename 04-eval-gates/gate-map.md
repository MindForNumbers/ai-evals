# Module 4 · Eval Gate Map · Ascend IQ Copilot

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| 1 | Hallucination | Hard | Release | Quoting outdated Enterprise pricing and inventing a false 10-seat minimum misleads VP buyers on core procurement decisions, causing severe executive trust loss and churn. |
| 14 | Relevance | No gate |  | False positive by the relevance eval—the agent properly followed safety guidelines to refuse legal queries, so there is no business risk. |
| 17 | Tone | Advisory | Pull Request | Using casual slang ("killer", "game changer") undermines executive brand credibility with VP buyers, though it is low-risk because users review and edit drafted cold emails before sending. |
| 5 | Hallucination | Soft | Staging | Presenting an invited, unconfirmed speaker as confirmed misleads executives planning event attendance or sponsorships, eroding trust in Ascend IQ's intelligence without posing a critical legal or pricing failure. |
| 8 | Hallucination | Hard | Release | Falsely accusing a named competitor of "strict throttling" while misrepresenting technical specs exposes the company to commercial disparagement and false advertising claims while severely damaging executive trust. |
| 3 | Latency | Advisory |  | Although the summarized G2 complaints are completely accurate, a 4.2-second response time exceeds the 2.0-second target and creates sluggish UX friction for busy VP users without causing factual or legal harm. |

## After the pushback

Row 3 (Latency): Set placement to Staging (alongside Advisory), since realistic end-to-end response times (4.2s vs. the 2.0s target) cannot be measured in static Pull Request checks, and Release is reserved strictly for Hard gates.

Row 1 (Enterprise Pricing): Moved placement from Release to Pull Request while keeping it a Hard gate, because deterministic regex checks against reference pricing figures run fast and cheap on every code change without waiting until the final release stage.

Kept Rows 5, 8, 14, and 17: Defended Hard on Row 8 due to severe commercial disparagement and false-advertising legal liability, kept Soft at Staging on Row 5 to require PM sign-off before shipping inaccurate event claims to VP buyers, kept Advisory at Pull Request on Row 17 since users review drafted emails before sending, and kept No gate on Row 14 because the refusal followed safety guidelines.

## Sample Interactions

**Row 1**
- Input: What is InsightFlow's pricing for Enterprise?
- Output: InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- What's true: Pricing page: the price changed from $49 to $59 a month yesterday.
- Automated eval: Fail · Hallucination. The answer quotes the old price as current.
- My call: Hard at Release. Quoting outdated Enterprise pricing and inventing a false 10-seat minimum misleads VP buyers on core procurement decisions, causing severe executive trust loss and churn.

**Row 14**
- Input: Summarize the lawsuit mentioned in the WSJ about Competitor Z.
- Output: I cannot provide summaries of ongoing legal litigation.
- What's true: Safety guidelines: “Refuse legal queries.”
- Automated eval: Fail · Relevance. The answer doesn’t answer the question.
- My call: No gate. False positive by the relevance eval—the agent properly followed safety guidelines to refuse legal queries, so there is no business risk.

**Row 17**
- Input: Draft a cold email about our new feature.
- Output: Hey! Check out this killer new feature, it's a total game changer for your stack!
- What's true: Brand voice: confident, professional, expert. Avoid slang.
- Automated eval: Fail · Tone. Slang detected.
- My call: Advisory at Pull Request. Using casual slang ("killer", "game changer") undermines executive brand credibility with VP buyers, though it is low-risk because users review and edit drafted cold emails before sending.

**Row 5**
- Input: List the confirmed speakers for SaaStr.
- Output: Confirmed speakers include Jason Lemkin, Aaron Levie, and Sam Altman.
- What's true: Agenda: Lemkin and Levie are confirmed. Sam Altman is invited, not confirmed.
- Automated eval: Fail · Hallucination. Lists an unconfirmed speaker as confirmed.
- My call: Soft at Staging. Presenting an invited, unconfirmed speaker as confirmed misleads executives planning event attendance or sponsorships, eroding trust in Ascend IQ's intelligence without posing a critical legal or pricing failure.

**Row 8**
- Input: Compare our API rate limits to Competitor Z.
- Output: Our API is robust and developer-friendly. Competitor Z is known for strict throttling.
- What's true: Tech specs: our API allows 500 requests a minute, and Competitor Z allows 1,000.
- Automated eval: Fail · Hallucination. Contradicts the specs and criticizes a named competitor.
- My call: Hard at Release. Falsely accusing a named competitor of "strict throttling" while misrepresenting technical specs exposes the company to commercial disparagement and false advertising claims while severely damaging executive trust.

**Row 3**
- Input: Summarize the top 3 complaints from DataViz's G2 reviews.
- Output: Users report issues with mobile load times, lack of dark mode, and steep learning curve.
- What's true: G2 reviews: the three complaints are correct. The answer took 4.2 seconds, and the target is 2.0.
- Automated eval: Fail · Latency. Exceeded the maximum response time.
- My call: Advisory at [no placement yet]. Although the summarized G2 complaints are completely accurate, a 4.2-second response time exceeds the 2.0-second target and creates sluggish UX friction for busy VP users without causing factual or legal harm.
