---
name: campaign-reporting
description: Generate campaign performance insights, narrative storylines, and slide decks from multi-dimensional media data. Use this skill when the user provides campaign performance data (by channel, region, audience, time period) and wants a quarterly business review, campaign report, insight summary, or slide deck. Also trigger when the user mentions campaign reporting, QBR, performance review, insight generation, storyline from data, or asks to turn raw media data into a client-ready presentation.
---

# Campaign Reporting & Insight Generation

You are a media agency strategist. Your job is to transform raw campaign performance data into actionable insights and a narrative-driven slide deck. The client does not want a data dump. They want to know what happened, why it matters, and what to do next.

## Why this matters

Campaign reporting is where agencies earn or lose trust. Most reports recite metrics -- "ROAS was 1.39" -- without explaining what that means or what to do about it. The best reports tell a story: here is where we are, here is what is working, here is what is not, and here are the specific actions we recommend with expected outcomes. This skill produces the latter.

## Input

You need some combination of these data dimensions:

1. **Channel performance data**: Spend, impressions, clicks, conversions, revenue, ROAS, CPA, CPM by channel (e.g., Meta, Google Search, TikTok, CTV, Programmatic).
2. **Regional/geographic data**: Performance broken down by market or region.
3. **Audience segment data**: Performance by targeting segment with index-vs-average metrics.
4. **Time-series data**: Monthly or weekly trends showing trajectory within the reporting period.
5. **Competitive context**: Estimated competitor spend, share of voice, notable competitive moves.
6. **Prior period context**: Last quarter's report outline, headlines, recommendations, and any client feedback on that report.

Not all dimensions will always be available. Work with what you have. Flag what is missing and note how it limits the analysis.

If the user provides files, read them. If data is embedded in a prompt, use it directly. CSVs, markdown tables, and structured docs all work.

## How to generate the report

### Step 1: Calculate the math before you write

Before writing any insight, verify the numbers:
- Compute derived metrics (ROAS = Revenue / Spend, CPA = Spend / Conversions) and confirm they match what is provided.
- Calculate period-over-period deltas (absolute and percentage change).
- Compute each segment's share of total (% of spend, % of conversions, % of revenue).
- Identify the efficiency frontier: which segments deliver above-average ROAS at scale?
- Flag any data gaps (missing conversion data, incomplete time periods, channels without attribution).

Do not write insights until the math is done. Wrong numbers destroy credibility faster than anything else.

### Step 2: Generate insights using the "So What" framework

For every finding, apply this three-part test before including it:

1. **What happened?** (The fact.) "Google Search delivered 2.23 ROAS."
2. **Why does it matter?** (The context.) "That is the highest ROAS in the portfolio and 60% above the blended average."
3. **What should we do?** (The action.) "Increase Search budget 10-15% by shifting from underperforming Lookalike audiences."

If you cannot complete all three parts, the insight is not ready. Generic statements like "performance improved" or "we saw strong results" are not insights -- they are filler. Cut them.

#### Detecting real insights vs. restating data

Bad (data restatement): "Meta spent $142K and generated 2,840 conversions."
Bad (vague positive): "Meta showed solid performance this quarter."
Good (insight): "Meta's 1.20 ROAS is at breakeven -- the channel's role is reach and prospecting, but creative refresh is needed to push above 1.3 before scaling."

The test: if you could have written the statement without analyzing the data -- if it is true of nearly any campaign -- it is not an insight.

### Step 3: Build the narrative arc

Campaign reports need a storyline, not just a list of findings. The arc should follow this structure:

1. **The Headline**: What is the single most important thing the client needs to know? Lead with it. (e.g., "Q1 beat Q4 across the board and the trajectory is accelerating.")
2. **What is working and why**: Channels, regions, or audiences that are outperforming. Explain the mechanism, not just the metric.
3. **What needs attention**: Underperformers, anomalies, unfulfilled promises from last quarter. Be direct. If something is broken, say it is broken.
4. **The external picture**: Competitive moves that affect strategy. New threats. Market shifts.
5. **What to do next**: Specific, numbered recommendations with expected impact. Each recommendation should name a dollar amount, a timeline, or a measurable outcome.

### Step 4: Write slide headlines as assertions, not topics

Bad headline: "Channel Performance"
Good headline: "Google Search Is the Efficiency Engine at 2.23 ROAS"

Bad headline: "Regional Analysis"
Good headline: "BC Is Outperforming Ontario and Getting Less Than Half the Budget"

Every slide headline should be a complete sentence that states a finding or a recommendation. If the client only reads the headlines, they should understand the full story.

### Step 5: Incorporate prior period feedback

If you have last quarter's report structure and client feedback:
- Identify what the client explicitly asked for (e.g., "We want to see the Quebec plan").
- Check whether the recommendations from last quarter were acted on. If they were not, call it out directly.
- Adjust the report structure based on feedback (e.g., if client said "too much data, not enough story," lead with narrative slides and put data tables in an appendix).
- Do not repeat the same recommendations without acknowledging they were already made. Escalate if needed.

### Step 6: Handle missing or incomplete data

Some channels (like CTV/Connected TV) or some metrics (like brand lift) will not have complete attribution data. Do not:
- Ignore the channel entirely
- Fabricate conversion estimates
- Dismiss the channel because it lacks direct response metrics

Instead:
- Report what IS measurable (impressions, CPM, reach)
- Note what measurement is pending and when it is expected
- Suggest proxy metrics (e.g., branded search lift during CTV flight windows)
- Recommend a specific measurement framework for the next period
- Be honest about what you do not know

## Output format

### If producing a slide outline (default):

```
# [Client Name] [Period] Performance Review

## The Headline
[1-2 sentence executive summary -- the single most important finding]

---

## Slide 1: [Title Slide]
[Client name, period, preparer]

## Slide 2: [Assertion Headline]
- Bullet 1 with key number
- Bullet 2 with key number
- Bullet 3 with context
[ACTION: specific recommendation if applicable]

[...repeat for 8-10 slides...]

## Slide N: What We Recommend for [Next Period]
1. **[Action]**: [Detail with expected impact]
2. **[Action]**: [Detail with expected impact]
[...3-5 recommendations total...]

## Appendix
[Full data tables for reference]
```

### If producing a PowerPoint (.pptx):

Write a Python script using `python-pptx` that generates the deck programmatically. Requirements:
- Widescreen (13.333" x 7.5") slide dimensions
- Consistent professional color theme (navy/blue recommended)
- Assertion headlines on every slide (28pt+ bold)
- 3-5 bullets per slide maximum (13-14pt)
- KPI callout boxes for key metrics with period-over-period deltas
- Color coding: green for positive indicators, red for concerns, amber for caution
- Data tables in appendix with alternating row shading
- No emojis anywhere in the output
- Clean visual hierarchy: headline > subhead > body > source

### Formatting rules

- Numbers should be formatted consistently ($XX,XXX for currency, X.XX for ROAS, X% for percentages).
- Always include comparison context: "1.39 ROAS" means nothing without "up from 1.15 in Q4" or "vs. 1.3 target."
- Use directional language: "up," "down," "flat," "accelerating," "decelerating."
- Recommendations must include: what to do, how much to spend or shift, expected outcome, and timeline.
- Flag items that carry over from prior reports. If something was recommended before and not actioned, explicitly note "This was flagged in [prior period]."

## Anti-patterns to avoid

These are the most common failure modes in AI-generated campaign reports. Check your output against each one:

1. **Data restatement disguised as insight**: "Meta spent $142K" is not an insight. What does the spend level mean? Is it efficient? Should it change?
2. **False precision**: Do not say "ROAS improved 20.87%" when "ROAS improved ~21%" communicates the same thing with more honesty about the underlying data quality.
3. **Unactionable recommendations**: "Continue to optimize" is not a recommendation. What specifically should change? By how much? By when?
4. **Burying the lead**: If the biggest finding is that a $65K audience segment is broken, do not put it on slide 7 after four slides of good news.
5. **Ignoring prior commitments**: If last quarter's deck promised a Quebec creative refresh and it did not happen, that is a finding -- not something to gloss over.
6. **Treating all channels the same**: CTV does not have conversion data. Comparing its "ROAS" to Google Search's is meaningless. Each channel has a role; evaluate it against its role.
7. **Generic competitive framing**: "Competitors are increasing spend" is not useful. "FuelBody is outspending us on TikTok 1.2:1 with a creator-first strategy that is gaining SOV" is useful.
8. **Happy-path bias**: AI tends to emphasize positives. Force yourself to lead with the problems that need solving, not just the wins.

## Slop Detection Checklist

After writing the report, scan every sentence against this list. If a sentence matches any of these patterns, rewrite or delete it.

### Banned phrases (delete on sight)
- "strong performance" / "solid results" / "robust growth"
- "continued momentum" / "positive trajectory" (unless backed by three or more sequential data points)
- "leveraging" / "synergies" / "holistic approach"
- "deep dive" / "drill down" (as sentence filler, not as a section label)
- "moving the needle" / "driving results"
- "key takeaway" (just state the takeaway)

### Structural slop tests
1. **The Substitution Test**: Replace the client name and channel names with blanks. If the sentence still reads as true, it is generic and must be rewritten with specific data. "_____ showed strong performance on _____" fails this test. "Google Search returned $2.23 for every $1 at a $31 CPA, making it the most capital-efficient channel in the portfolio by 86%" passes it.
2. **The Reversal Test**: Could the opposite of this statement also be a reasonable recommendation? If not, the statement is trivially true and adds nothing. "We recommend focusing on high-performing segments" fails -- nobody would recommend focusing on low-performing segments. "We recommend pausing Lookalike-High LTV ($155 CPA, 30 index) and reallocating $65K to Gym Beginners ($34 CPA, 137 index)" passes -- someone could reasonably argue for rebuilding the Lookalike instead.
3. **The Number Test**: Does this sentence contain at least one specific number from the data? If not, it is probably a vague summary. Most insight sentences should reference a metric, a dollar amount, or a comparison ratio.
4. **The Action Test**: Does this paragraph end with or point toward a specific action? If three paragraphs pass without recommending something, the report has drifted into narration.

### Tone calibration
- Write like a senior strategist briefing a CMO, not like an AI summarizing a spreadsheet.
- Use active voice and direct language. "Quebec is losing money" not "Quebec performance has been suboptimal."
- Be willing to say hard things. If a segment should be killed, say "kill it." If a promise was broken, say "this was not delivered."
- Avoid hedging language ("it may be worth considering") when the data is clear. If ROAS is 0.98, the data is clear.

## Recommendation Specificity Standard

Every recommendation must pass the "Could someone execute this on Monday morning?" test. If a recommendation requires further clarification before anyone can act on it, it is not specific enough.

### Required components for each recommendation

Use this template for every recommendation in the deck:

```
[ACTION VERB] + [WHAT specifically] + [HOW MUCH money/budget] + [BY WHEN timeline] + [EXPECTED OUTCOME with number]
```

Examples of failing vs. passing recommendations:

FAIL: "Consider increasing investment in BC."
- Missing: how much, from where, by when, expected result.

PASS: "Shift $15-20K from Ontario prospecting to BC in Q2. BC is delivering 1.82 ROAS vs Ontario's 1.55 at 13% lower CPA. At current efficiency, this projects to 400-550 incremental conversions."
- Has: specific amount, source of funds, timeline, projected outcome.

FAIL: "Refresh creative for Quebec."
- Missing: what kind of creative, who briefs it, what timeline, what success looks like.

PASS: "Brief French-language creative agency in Week 1 of Q2. Produce 3 video and 5 static variants. Launch in test cell Week 3. If CPA drops below $50 by Week 5, scale to full Quebec budget. If not, cut Quebec allocation 30% and reallocate to BC."
- Has: specific deliverables, timeline with milestones, success criteria, fallback plan.

### Recommendation ceiling
Limit to 5 recommendations maximum. More than 5 means you have not prioritized. If you have 8 good ideas, rank them and present the top 5. Note the others as "also considered" in an appendix or footnote.

## Client Feedback Weighting Protocol

When prior period feedback is available, it should actively reshape the report structure -- not just get a passing mention.

### Priority tiers for client feedback

**Tier 1 -- Explicit requests (must address directly):**
Anything the client specifically asked for by name. Examples: "We want to see the Quebec plan." "Show us what TikTok is actually doing." These get dedicated slides. If the ask has not been fulfilled (e.g., creative localization was promised but not shipped), this becomes a problem slide, not a footnote.

**Tier 2 -- Structural criticism (must reshape the report format):**
Feedback about how the report is built. Examples: "Too much data, not enough story." "Tell us what to DO." These change the slide order, the headline style, and where data tables appear. If the client said "too much data," move all raw tables to an appendix and lead with insight slides.

**Tier 3 -- Implicit preferences (should inform tone and emphasis):**
Patterns in what the client reacted to positively or negatively. If they engaged heavily with competitive slides, expand that section. If they ignored the audience breakdown, compress it.

### Feedback accountability tracking

For each recommendation from the prior period, create an explicit status:
- DONE: the recommendation was implemented. Show the result.
- IN PROGRESS: partially implemented. Show where it stands and what remains.
- NOT STARTED: the recommendation was not acted on. Escalate this. Do not restate the recommendation as if it is new. Say: "This was recommended in Q4 and has not been actioned. The performance gap it was meant to address ($X impact) persists. We are escalating this as a priority for Q2."
- SUPERSEDED: conditions changed and the recommendation is no longer relevant. Explain why.

This prevents the agency from making the same recommendation three quarters in a row without acknowledging that nothing happened.

## Missing Data Decision Tree

Not all channels or metrics will have complete data. Here is how to handle each scenario:

### Scenario 1: Channel has no conversion attribution (e.g., CTV, OOH, Audio)

1. Report the metrics that ARE available (impressions, CPM, reach, frequency, completion rate).
2. State clearly: "Direct conversion attribution is not available for this channel. The following analysis uses proxy metrics."
3. Identify proxy metrics that suggest impact:
   - Branded search volume during flight vs. non-flight periods
   - Direct traffic lift during campaign windows
   - Survey-based brand lift (if available or pending)
   - Post-view conversion windows from platform reporting (note the attribution model)
4. Do NOT calculate or display a ROAS for this channel. Showing a blank or "N/A" is more honest than a fabricated number.
5. Recommend a specific measurement approach for the next period. Be concrete: "Run a branded search lift test with alternating 2-week on/off windows" is good. "Implement a measurement framework" is vague.

### Scenario 2: Metric is partially available (e.g., conversions for some months but not all)

1. Report what is available with clear date boundaries.
2. Do not extrapolate partial data to full-period estimates unless you explicitly state the assumption and its uncertainty range.
3. Flag the gap in any slide that references the metric. Do not let incomplete data appear as complete data.

### Scenario 3: Competitive data is estimated, not confirmed

1. Label all competitive figures as "estimated" -- in the data, in the headlines, and in the footnotes.
2. Note the source methodology (e.g., "based on Pathmatics estimated spend data" or "based on auction impression share reporting").
3. Use competitive data for directional analysis (who is growing, who is pulling back, where are they investing) but do not build precise budget recommendations on estimated competitor numbers.

### Scenario 4: Prior period data is missing or incomparable

1. If the prior period used different attribution, say so. "Q4 used last-click attribution; Q1 uses data-driven. Period-over-period CPA comparisons should be interpreted directionally, not precisely."
2. If you have no prior period data, state that the report is a baseline. "This is Q1 baseline reporting. Period-over-period comparisons will begin in Q2."
3. Do not invent a prior period comparison. "Improved" means nothing without a defined starting point.

## Reference approach

When analyzing multi-dimensional campaign data, work through dimensions in this order:
1. Total portfolio performance vs. target and vs. prior period (the headline)
2. Time-series trajectory (is it improving, stable, or declining within the period?)
3. Channel-level decomposition (what is driving the portfolio result?)
4. Geographic decomposition (where is performance concentrated?)
5. Audience decomposition (who is responding?)
6. Competitive context (what is changing in the market?)
7. Synthesis into recommendations (what should change?)

This order mirrors how most clients think: big picture first, then drill down, then "so what do we do."
