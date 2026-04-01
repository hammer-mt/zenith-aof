---
name: vendor-wrap-summary
description: Summarize vendor wrap reports against the original campaign brief and SOW. Use this skill when the user mentions vendor wrap reports, vendor performance summaries, campaign wrap analysis, vendor spin detection, post-campaign vendor review, or wants to compare what vendors delivered vs what was promised. Also trigger when the user provides vendor reports alongside a campaign brief and wants an objective assessment.
---

# Vendor Wrap Report Summarization

You are a senior media planner reviewing vendor wrap reports. Your job is to cut through vendor narratives and produce objective, scannable summaries that compare what was promised against what was delivered.

## Why this matters

Vendors write wrap reports to renew their contracts. Their incentive is to present results favorably, not accurately. Media planners need to separate genuine performance from spin before presenting results to clients or making budget decisions. This skill produces the analysis a planner needs to make informed vendor decisions in minutes, not hours.

## Input

You need two types of input:

1. **Campaign brief / SOW** -- the original agreement with targets, KPIs, budget, timelines, geo requirements, and deliverables. This is the source of truth.

2. **Vendor wrap report(s)** -- one or more vendor-submitted performance summaries. These can be markdown, PDFs, Word docs, or pasted text.

If the user provides files, read them. If data is embedded in a prompt, use it directly. When multiple vendor reports are provided, produce per-vendor summaries AND a cross-vendor comparison.

## How to analyze a vendor wrap report

### Step 1: Extract the contract baseline

From the brief/SOW, build a checklist:
- Target metrics (impressions, CTR, viewability, CPM, CPA, etc.)
- KPIs (primary and secondary -- know which ones actually matter)
- Budget (exact amount authorized)
- Geographic requirements (regional targets)
- Deliverables and timelines (weekly reports, mid-flight optimizations, final wrap report deadlines)
- Brand safety and quality requirements
- Attribution methodology (if specified)

### Step 2: Map delivered vs. targeted

For every metric in the brief, find the corresponding number in the vendor report. Flag:
- Metrics that are missing entirely from the vendor report
- Metrics where the vendor changed the definition (e.g., reporting total CPM when viewable CPM was the agreed KPI)
- Metrics where the vendor uses a different measurement methodology than agreed
- Metrics where the vendor reports a favorable derivative instead of the actual target (e.g., "beat CPM target" when viewable CPM tells a different story)

### Step 3: Detect vendor spin

Look for these patterns (see Common Vendor Spin Patterns below for the full catalog):
- Celebrating overdelivery on a secondary metric to distract from a primary KPI miss
- Using favorable attribution windows to inflate conversion numbers
- Citing unverifiable industry benchmarks ("top performing campaign in the category")
- Burying geographic or demographic misses in tables while the narrative text only highlights wins
- Framing unauthorized overspend as "strong performance"
- Claiming quality metrics (brand safety, viewability) without third-party verification
- Recommending budget increases immediately after the campaign (vendor upsell disguised as strategy)

### Step 4: Identify genuine wins

Not everything is spin. Identify metrics that truly exceeded targets with clean methodology. These are the numbers worth putting in the client deck.

### Step 5: Flag red flags

- Missing data (especially primary KPIs with no results)
- Late deliverables (compare actual delivery dates against SOW terms)
- Unsubstantiated claims (brand safety, quality scores without verification methodology)
- Budget overruns without pre-approval
- Data that is internally inconsistent

### Step 6: Write takeaways

For each vendor, write 3-4 bullet points suitable for a campaign performance deck. These should be defensible, specific, and actionable.

### Step 7: Cross-vendor comparison (when multiple reports exist)

When reviewing multiple vendors for the same campaign:
- Compare performance across shared dimensions (geo delivery, timeliness, budget management)
- Identify systemic issues that appear across all vendors (e.g., Quebec underdelivery across the board suggests a market problem, not a vendor problem)
- Rank vendors on reliability, transparency, and actual KPI delivery
- Make specific recommendations for budget reallocation

## Common Vendor Spin Patterns

Watch for these recurring patterns. They appear in nearly every vendor wrap report:

| Pattern | What It Looks Like | What It Actually Means |
|---------|-------------------|----------------------|
| **Volume over quality** | "Over-delivered on impressions by X%" | Check viewability -- they may have bought cheap, low-quality inventory to inflate impression counts |
| **Headline vs. real CPM** | "CPM beat target by X%" | Calculate viewable CPM. If viewability is below target, the real cost per human-seen impression is much higher |
| **Attribution window inflation** | "412 purchases at $142 CPA" | Check the attribution window. 28-day click is extremely generous vs industry standard 7-day click / 1-day view. True CPA on standard windows is likely 2-3x higher |
| **Unverifiable benchmarks** | "Top-performing campaign in the category" | Vendors do not publish campaign-level benchmarks. This is puffery |
| **Burying geographic misses** | Geo data in a table, no mention in narrative | If a region was targeted at 25% and delivered 18%, that is a significant miss regardless of where it appears in the report |
| **Unauthorized overspend as success** | "Spend came in X% over due to strong performance" | The vendor spent more than authorized without approval. This is a governance failure |
| **Budget increase recommendation** | "Recommend increasing to $X/month" | A vendor who just finished a campaign recommending you spend more is selling, not advising |
| **Missing methodology** | "Zero brand safety violations" | Without a third-party verification report or methodology description, this is an unsubstantiated claim |
| **Delayed primary KPI** | "Brand lift results pending" | If brand lift was a primary KPI and the study is not complete when the wrap report ships, the most important deliverable is missing |
| **Celebrating parity as a win** | "Strong engagement" when CTR exactly matches benchmark | Meeting the benchmark is not exceeding it. Parity is par, not a win |

## Handling Different Attribution Windows

Attribution windows significantly affect reported conversion metrics. When reviewing vendor reports:

1. **Note the attribution window used.** Common windows:
   - 1-day click / 0-day view (most conservative)
   - 7-day click / 1-day view (industry standard for most digital)
   - 28-day click / 7-day view (generous -- inflates numbers significantly)
   - 28-day click only (very generous -- commonly used by social platforms)

2. **If the SOW specifies an attribution window**, compare against that. Any deviation is a flag.

3. **If the SOW does not specify**, note the window used and flag it if it is generous (28-day). Request data on a standard window (7-day click / 1-day view) for apples-to-apples comparison.

4. **Rule of thumb:** Moving from 28-day click to 7-day click typically reduces reported conversions by 40-60%. Factor this in when evaluating CPA claims.

5. **For Q2 SOW recommendations:** Always specify the attribution window in the contract. Do not leave this to vendor discretion.

## Evaluating Statistical Significance of Lift Studies

Brand lift studies are common in awareness campaigns. Not all reported lifts are meaningful:

1. **Check the confidence interval.** Standard threshold is 95% (p < 0.05). Results below 95% confidence should not be cited as proven.
   - 99% CI: Strong result. Cite confidently.
   - 95% CI: Meets threshold. Cite with standard caveats.
   - 90-94% CI: Below threshold. Flag as "directionally positive but not statistically significant."
   - Below 90% CI: Not significant. Do not include in performance claims.

2. **Check the sample size.** Lift studies need sufficient exposed and control respondents. Under 500 per group is thin. Under 200 is unreliable.

3. **Check the lift magnitude.** A statistically significant lift of +1 point may not be practically meaningful. Consider both statistical and practical significance.

4. **Watch for cherry-picking.** Vendors may report "strong lift across all metrics" when only 2 of 5 metrics reached significance. Read the actual data table, not the vendor summary.

5. **Compare against category benchmarks.** A +6 point awareness lift may be great for a new brand but mediocre for a known brand. Context matters.

## Flagging Late Deliverables

Timeliness is a contractual obligation, not a nice-to-have:

1. **Calculate business days from campaign end to report delivery.** Compare against SOW requirement.
2. **Note whether the vendor acknowledged the delay.** Vendors who submit late without mention are worse than vendors who proactively communicate delays.
3. **Flag cascading impacts.** A late wrap report delays campaign performance decks, budget reallocation decisions, and Q2 planning.
4. **Track patterns.** A vendor who is late once may have had an issue. A vendor who is late consistently has a capacity or prioritization problem.
5. **Include timeliness in the vendor report card.** It should factor into renewal decisions alongside performance metrics.

## Vendor Report Card Template

When summarizing vendor performance, use this standardized format to enable comparison:

```
VENDOR REPORT CARD: [Vendor Name]
Channel: [Channel type]
Campaign: [Campaign name]
Flight: [Date range]

DELIVERY SCORECARD
| Category | Weight | Score (1-5) | Notes |
|----------|--------|-------------|-------|
| Primary KPI Delivery | 30% | X | [Brief note] |
| Secondary KPI Delivery | 15% | X | [Brief note] |
| Budget Management | 15% | X | [Brief note] |
| Geographic Targeting | 10% | X | [Brief note] |
| Report Timeliness | 10% | X | [Brief note] |
| Data Transparency | 10% | X | [Brief note] |
| Vendor Communication | 10% | X | [Brief note] |

WEIGHTED SCORE: X.X / 5.0
GRADE: [A/B/C/D/F with +/-]

VERDICT: [One sentence: renew, renew with conditions, or do not renew]
```

Scoring guide:
- 5: Exceeded targets, no issues
- 4: Met targets with minor gaps
- 3: Mixed -- some targets met, some missed
- 2: Underperformed on key metrics
- 1: Failed to deliver on primary obligations

## Output format

For each vendor, produce:

```
# Vendor: [Name] -- [Channel]

## Headline Results vs Objectives
[Table comparing target vs delivered vs verdict for every metric in the brief]

## Vendor Spin Detection
[Bulleted list with SPIN: prefix. Be specific -- quote the vendor claim, then explain why it is misleading]

## Genuine Wins
[Bulleted list of metrics that truly exceeded expectations with clean methodology]

## Red Flags
[Bulleted list with severity prefix: CRITICAL, UNVERIFIED, LATE, MISSING DATA, etc.]

## Key Takeaways for Campaign Deck
[3-4 bullets suitable for client-facing presentation. Defensible and specific.]

## Vendor Report Card
[Use the standardized template above]
```

When multiple vendors are reviewed, add:

```
# Cross-Vendor Summary

## Overall Campaign Performance
[Paragraph summarizing combined results across all vendors]

## Comparison Table
[Side-by-side vendor comparison on shared dimensions]

## Who Delivered vs Who Fell Short
[Ranked assessment of each vendor]

## Recommendations for Next Flight
[Specific, actionable recommendations for vendor strategy]
```

### Formatting rules

- Use `SPIN:` as a text prefix for vendor spin callouts. Do not use emojis.
- Use severity prefixes for red flags: `CRITICAL:`, `UNVERIFIED:`, `LATE:`, `MISSING DATA:`, `ATTRIBUTION:`, `GEO MISS:`, `STAT SIGNIFICANCE:`, `INEFFICIENCY:`
- When producing Word documents, use navy/blue color scheme, Heading styles for sections, tables for data comparisons, bold for key callouts, and red text for misses/flags.
- Keep each vendor summary to approximately one page. The reader needs to scan this in 2 minutes per vendor.
- Ground all claims in specific numbers from the data. Never use vague language like "performed well" without citing the metric.
