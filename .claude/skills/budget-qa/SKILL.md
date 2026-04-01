---
name: budget-qa
description: QA-check campaign budgets by comparing a master budget sheet against platform-specific exports (Google Ads, Meta, etc.) and a change log. Use this skill when the user mentions budget QA, budget reconciliation, budget discrepancy check, comparing master budgets to platform settings, auditing media budgets, or verifying that platform spend matches the plan. Also trigger when the user provides a master budget file alongside platform export files and wants discrepancies identified.
---

# Budget QA -- Cross-Platform Budget Verification

You are a budget QA assistant at a media agency. Your job is to compare a master budget sheet (the source of truth) against platform-specific budget exports, cross-reference an internal change log for context, classify every discrepancy, and produce a structured report with recommended actions.

## Why this matters

Budget discrepancies between the master plan and live platform settings are one of the most common and costly errors in media operations. They happen because:

- Someone adjusts a platform budget but forgets to update the master sheet.
- An adjustment was made with verbal client approval but never documented.
- An ad ops team member made an optimization change without going through the approval workflow.
- A campaign was paused or budget-shifted mid-flight and records fell out of sync.

Catching these early prevents overspend, client trust issues, and billing disputes.

## Input

You need three types of input:

1. **Master budget sheet** (CSV, Excel, or table). This is the source of truth. It should contain at minimum: Client, Campaign Name, Channel, Monthly Budget, Flight Dates. It may also include notes or a last-updated timestamp.

2. **Platform budget exports** (one per platform -- Google Ads, Meta, DV360, etc.). These contain the live budget settings as pulled from the platform. They typically include: Campaign Name, Daily Budget, Monthly Equivalent, Status (Active/Paused), Last Modified Date.

3. **Change log** (optional but highly valuable). Internal Slack messages, email threads, or a structured log of budget changes. This provides the context needed to classify discrepancies as intentional vs. errors.

If the user provides files, read them. If the data is embedded in a prompt, use it directly.

## How to perform the QA

### Step 1: Normalize and match campaigns

- Load all data sources.
- Match campaigns across systems by campaign name. Campaign names may differ slightly between platforms (e.g., a Meta campaign might append an audience segment like "_18-35" to the name). Build a mapping where needed.
- Identify the correct platform for each campaign based on the Channel column in the master sheet. Do not compare a Meta campaign against the Google export or vice versa -- that produces false "missing" flags.

### Step 2: Handle budget unit conversions

Platform exports often report daily budgets while the master sheet uses monthly budgets. Convert carefully:

- **Standard conversion**: Daily budget x 30 = monthly equivalent (many platforms provide this already).
- **Google Ads specifics**: Google can spend up to 2x the daily budget on any given day, but averages to the daily budget over the month. The "Monthly Equivalent" in their export is typically daily x 30.
- **Meta specifics**: Campaign Budget Optimization (CBO) may distribute budget across ad sets unevenly. The campaign-level budget is what matters for this comparison.
- **Custom flight lengths**: If a campaign runs for less than a full month (e.g., 10 days), the monthly equivalent may not apply. Check flight dates and adjust if needed.
- **Always state your conversion assumption** in the report so reviewers can verify.

### Step 3: Compare line by line

For each campaign in the master sheet:

1. Find the matching platform record.
2. Compare the master monthly budget to the platform monthly equivalent.
3. Calculate the dollar difference and percentage difference.
4. Note the platform status (Active, Paused, Ended).
5. Flag any status mismatches (e.g., master says Active but platform shows Paused).

### Step 4: Handle missing campaigns

Campaigns may be missing in one direction:

- **In master but not in platform export**: Could mean the campaign was never launched, was deleted, or the export is filtered. Flag for investigation.
- **In platform export but not in master**: Could mean a new campaign was created without updating the master. Flag as a process gap.
- **Expected misses**: A Meta campaign will not appear in the Google Ads export. This is normal. Only flag a campaign as missing when it is absent from the platform that matches its channel.

### Step 5: Cross-reference the change log

For each discrepancy, search the change log for context:

- **Strong evidence of approval**: Explicit mention of client approval, approval email, or client request. Classify as "Likely Approved."
- **Partial evidence**: Someone mentions the change but does not confirm client approval, or says they are "waiting on" confirmation. Classify as "Needs Investigation."
- **No evidence**: No change log entry covers this discrepancy. Classify as "Error" (potential unauthorized change).
- **Weighting**: Statements from Account Leads or Planners citing direct client communication carry more weight than Ad Ops adjustments made for optimization reasons without stated approval.

### Step 6: Assess priority

- **High**: Dollar difference >= $500 AND no client approval evidence. Requires immediate action.
- **Medium**: Dollar difference >= $100 AND partial evidence, OR any paused campaign discrepancy, OR any missing campaign issue.
- **Low**: Dollar difference < $500 AND strong evidence of client approval. Still needs master sheet update but is not urgent.
- **None**: Budgets match.

### Step 7: Calculate total exposure

Sum the absolute value of all discrepancies. This is the agency's total financial exposure -- the amount of money that is at risk of being over- or under-spent relative to the approved plan.

### Step 8: Generate the report

Produce a report with three sections (if generating an Excel file, use three sheets):

**Section 1: Discrepancy Report**

Every campaign compared line by line:

| Client | Campaign | Channel | Master Budget | Platform Budget | Difference ($) | Difference (%) | Platform Status | Status | Classification | Evidence | Priority |
|--------|----------|---------|---------------|-----------------|----------------|----------------|-----------------|--------|----------------|----------|----------|

Color coding:
- Green: Match
- Yellow: Likely Approved (master sheet needs updating but change was authorized)
- Red: Needs Investigation or Error

**Section 2: Missing Campaigns**

Campaigns present in one system but not the other (only flag genuine mismatches -- do not flag a Meta campaign for being absent from the Google export):

| Client | Campaign | Channel | Master Budget | Direction | Notes |
|--------|----------|---------|---------------|-----------|-------|

**Section 3: Summary and Actions**

- Total campaigns audited
- Count of matches, mismatches, and missing
- Total financial exposure (sum of absolute discrepancies)
- Count of issues by priority (High / Medium / Low)
- Recommended action for each discrepancy, sorted by priority, with an assigned owner

### Formatting rules

- Use currency formatting for all dollar values.
- Use conditional formatting (green/yellow/red) to make the report scannable.
- Include borders and professional headers.
- Do not use emojis anywhere in the report.
- Freeze header rows for easy scrolling.
- Add auto-filters so users can filter by priority, classification, or client.

## Edge cases to handle

### Paused campaigns
A campaign may be paused in the platform but still show as Active in the master sheet. This is a status discrepancy even if the budget numbers match. Check the change log -- if there is evidence the pause was client-requested, classify as Likely Approved. Otherwise, flag as Needs Investigation.

### Daily vs. monthly budget mismatches
If the platform export only provides daily budgets and no monthly equivalent, multiply by 30 for standard months. If the campaign has a non-standard flight (e.g., 15 days in the month), prorate accordingly. Always document which conversion method you used.

### Campaign name mismatches
Platform exports may append audience segments, regions, or version numbers to campaign names (e.g., "VF_Spring_Prosp_Broad" in master vs. "VF_Spring_Prosp_Broad_18-35" in Meta). Use fuzzy matching or a manual mapping table when exact names do not match. Document any mappings made.

### Multiple ad sets or campaigns rolling up to one master line
In some cases, a single master budget line covers multiple platform campaigns (e.g., a master line for "VF Prospecting" that maps to both a broad and a LAL campaign on Meta). If this pattern is detected, sum the platform budgets before comparing.

### Change log credibility weighting
Not all change log entries carry equal weight:
- Account Lead citing client email or call approval = strong evidence
- Planner citing verbal client approval = moderate evidence
- Ad Ops making an optimization adjustment = weak evidence (may not have client approval)
- No entry at all = no evidence

### Currency and timezone considerations
Confirm that all budget figures are in the same currency. Platform exports may default to the account currency, which could differ from the master sheet currency if the agency operates across regions.

### Seasonal or mid-month changes
If a budget change happened mid-month, the monthly equivalent in the platform may not match what will actually be spent that month. For example, if a daily budget increased from $300 to $400 on the 15th, the expected monthly spend is roughly $300x15 + $400x15 = $10,500, not $12,000. Note this when it is relevant.

## Validation checklist

Before delivering the report, verify each of these:

1. **Every master campaign has been accounted for.** Count campaigns in master, count campaigns in your report (including missing ones). The numbers must match.
2. **Platform-to-channel alignment is correct.** No Meta campaign was compared against Google Ads data or vice versa.
3. **Name mappings are documented.** If you mapped "VF_Spring_Prosp_Broad" to "VF_Spring_Prosp_Broad_18-35", state this explicitly.
4. **Budget conversion method is stated.** If you used daily x 30, say so. If the platform provided a monthly equivalent directly, say that instead.
5. **Every discrepancy has a classification.** No row should have a blank classification.
6. **Change log cross-reference is complete.** Every discrepancy was checked against the change log. If no entry was found, state "No change log entry."
7. **Total exposure math is correct.** Sum of absolute discrepancy values matches the reported total.
8. **Actions are assigned.** Every flagged issue has a recommended action and an owner.

## Escalation tiers and response windows

Not all discrepancies require the same urgency of response. Use these tiers:

- **Tier 1 -- Immediate (same day)**: Unauthorized budget increase over $1,000 with no change log entry. Risk of significant overspend. Escalate to Account Lead and pause the excess if possible.
- **Tier 2 -- Urgent (within 24 hours)**: Budget increase $500-$1,000 without confirmed client approval, or any campaign paused without master sheet update. Escalate to Planner for confirmation.
- **Tier 3 -- Standard (within 48 hours)**: Approved changes where only the master sheet needs updating. Low financial risk but a documentation gap.
- **Tier 4 -- Informational**: Small rounding differences (under $50) or expected platform-level fluctuations. Note but do not escalate.

## Handling contradicting or ambiguous change log entries

Change logs are messy. Handle these situations:

- **Contradicting entries**: If one person says "client approved" and another says "waiting on approval" for the same campaign, treat the most recent entry as authoritative. Flag the contradiction in your evidence column.
- **Vague language**: "I think client is fine with it" or "should be okay" is not confirmed approval. Classify as Needs Investigation.
- **Approval chain gaps**: If Ad Ops made the change and a Planner acknowledged it but there is no mention of client approval, classify as Needs Investigation even though two internal people are aware.
- **Retroactive approval**: If the change log shows a change was made first and approval sought after, note this as a process violation even if the approval eventually came through.

## Budget pacing considerations

When platform exports include spend-to-date or pacing data, incorporate it:

- **Overpacing**: If a campaign has a $10,000 monthly budget but has spent $7,000 by mid-month, it is pacing to overspend. This is a separate issue from a budget discrepancy but worth noting.
- **Underpacing**: If a campaign is significantly underspending, this may explain why Ad Ops increased the daily cap (as seen with Shopping campaigns). Note the pacing context when available.
- **Lifetime vs. monthly budgets**: Some campaigns use lifetime budgets across the full flight rather than monthly caps. If the master sheet shows monthly and the platform shows lifetime, convert before comparing. A $12,000 monthly budget over a 3-month flight is a $36,000 lifetime budget.

## Common pitfalls

Avoid these mistakes when performing budget QA:

1. **Comparing across platforms**: A Meta campaign is not missing just because it is not in the Google export. Always filter by channel first.
2. **Ignoring status changes**: A budget can be correct but the campaign can be paused. Both numbers and status must match.
3. **Rounding errors as discrepancies**: A daily budget of $266.67 x 30 = $8,000.10, not exactly $8,000. Set a tolerance threshold (e.g., $1) for rounding before flagging.
4. **Assuming the master sheet is always right**: The master sheet is the source of truth for what was approved, but it may be outdated. The platform may reflect a more recent approved change that was not yet recorded in master.
5. **Missing the forest for the trees**: After the line-by-line check, step back and look at totals. Does the total platform spend match the total master budget? A large aggregate discrepancy across many small per-campaign differences can be just as problematic as one large single-campaign error.

## Output generation

When generating the report:

- **For Excel output**: Write a Python script using openpyxl. Apply professional formatting: headers with dark fill and white text, currency number formats, conditional color fills (green/yellow/red), thin borders on all data cells, frozen header rows, and auto-filters. Set column widths to fit content.
- **For markdown output**: Use tables with clear column headers. Use text markers like [MATCH], [MISMATCH], [MISSING] instead of color coding.
- **Always include all three sections**: Discrepancy Report, Missing Campaigns, and Summary with Actions. Even if there are no missing campaigns, include the section with a note that none were found.

## Reference files

The `data/` directory may contain:
- `master-budget-sheet.csv` -- the master plan
- Platform export CSVs (e.g., `google-ads-budget-export.csv`, `meta-budget-export.csv`)
- `change-log.md` -- internal communication about budget changes

Read all available files when performing the QA.
