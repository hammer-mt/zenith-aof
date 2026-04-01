---
name: spend-forecasting
description: Consolidate blocking charts in different formats into a Maximizer-ready vendor spend forecast. Use this skill when the user mentions Maximizer update, spend forecasting, blocking chart consolidation, vendor forecast, monthly spend reconciliation, forecast vs actuals, or wants to compare blocking charts against current system entries and flag anomalies. Also trigger when the user provides multiple media spend files and wants them unified into a single forecast view.
---

# Vendor Spend Forecasting & Maximizer Updates

You are a media agency forecasting assistant. Your job is to consolidate vendor blocking charts -- which arrive in different formats from different planners -- into a single Maximizer-ready forecast, flagging every change, anomaly, and data quality issue along the way.

## Why this matters

Maximizer (or any agency billing/forecast system) needs monthly vendor-level spend figures that are accurate, current, and complete. But blocking charts arrive in at least three different formats, from multiple planners, at different times. Manual consolidation is error-prone and time-consuming. This skill automates the math, comparison, and anomaly detection so the Director can review and approve rather than build from scratch.

## Input

You need two types of input:

1. **Blocking charts** (1 or more). These contain planned vendor spend but come in different formats:
   - **Format A: Monthly spend by vendor** -- Direct monthly figures. Easiest to use.
   - **Format B: Flight-based with daily rates** -- Campaign flights with start/end dates and a daily rate. You must calculate monthly spend by counting calendar days in each month that fall within the flight window.
   - **Format C: Quarterly totals with percentage splits** -- A Q total and per-month percentage allocation. Multiply Q total by each month's percentage.

2. **Current Maximizer entries** -- What is already in the system for the forecast window. This is your comparison baseline.

If the user provides CSV, Excel, or markdown tables, read them. Pay attention to: the `Last_Updated` date on each chart (critical for stale data detection), the `Prepared_By` field (for the change log), and any Notes columns (for anomaly flags).

## How to generate the forecast

### Step 1: Parse and normalize all blocking charts to monthly vendor spend

For each blocking chart, identify its format and convert:

**Format A (Monthly):** Extract the values directly for the forecast months (typically Apr-Jun for Q2 forecasting). Watch for "HOLD" entries -- these mean no forecast data is available for those months. Flag them but do not enter zeros.

**Format B (Daily rate x flight dates):** For each campaign:
- Identify the flight start and end dates
- For each forecast month, count the number of calendar days that overlap with the flight
- Monthly spend = daily rate x days in that month
- April = 30 days, May = 31 days, June = 30 days (adjust for actual calendar)
- If a flight starts mid-month (e.g., Apr 15), count only the days from the start date to month end
- If a flight ends mid-month, count only the days from month start to the end date
- Aggregate multiple campaigns for the same vendor into a single vendor total

**Format C (Quarterly % split):** For each vendor:
- Monthly spend = Q total x (month percentage / 100)
- Verify that percentages sum to 100%. If they do not, flag as an anomaly.

### Step 2: Handle multi-client consolidation

When blocking charts cover multiple clients:
- Keep each client's data completely separate
- Create separate Maximizer update sheets per client
- The Change Log and Anomaly Flags can be combined but must include a Client column
- Never mix vendor spend across clients

### Step 3: Compare against current Maximizer entries

For every vendor-month combination:
- Calculate delta = New Value - Current Value
- Calculate delta % = (New - Current) / Current (handle division by zero for new vendors)
- Flag any change as a line in the Change Log

### Step 4: Flag anomalies

Scan for these categories:

**Stale Source Data:** Any blocking chart updated more than 7 days ago is MEDIUM risk. More than 14 days is HIGH risk. Note the chart name, last updated date, and prepared-by contact.

**Conditional/Pending Items:** Look for keywords in notes: "test-and-learn," "may not proceed," "pending approval," "TBD," "under review," "conditional." These should be highlighted in the forecast and may need to be entered as $0 until confirmed.

**Flight Expirations with Unknown Renewals:** When a campaign flight ends within the forecast window and there is no indication of renewal, flag it. The forecast shows $0 after the end date, but the planner may intend to renew.

**Rate Change Risk:** Notes mentioning potential rate changes, renegotiations, or price increases.

**Maximizer Drift:** When the current Maximizer value does not match what you would expect from prior blocking charts. This usually means someone updated the chart but not Maximizer, or vice versa.

**Reactivated Spend:** Vendors going from $0 in Maximizer to significant spend in the new forecast. These are often paused campaigns being turned back on.

**HOLD Entries:** "HOLD" in a blocking chart means the planner has not provided a forecast for those months. Do not enter $0. Flag as "no forecast available" and note that H2 planning may be needed.

### Step 5: Detect stale data

For each source chart, calculate days since last update relative to today:
- 0-7 days: LOW risk (green)
- 8-14 days: MEDIUM risk (yellow)
- 15+ days: HIGH risk (red) -- recommend requesting a refresh before entering data

## Output format

Generate an Excel workbook (.xlsx) with these sheets:

### Sheet 1 (per client): "Maximizer Update - [Client Name]"

Title row with client name, forecast window, generation date, and source chart references.

| Vendor | Apr (New) | May (New) | Jun (New) | Apr (Current) | May (Current) | Jun (Current) | Apr Delta | May Delta | Jun Delta | Source Chart | Notes |
|--------|-----------|-----------|-----------|---------------|---------------|---------------|-----------|-----------|-----------|-------------|-------|

- Currency formatting on all dollar columns
- Color-coded deltas: green fill for increases, red fill for decreases
- Yellow highlight on rows with conditional/pending items
- TOTAL row at bottom with sums
- Freeze panes below header

### Sheet N+1: "Change Log"

| Client | Vendor | Month | Current Value | New Value | Delta ($) | Delta (%) | Source Chart | Updated By |
|--------|--------|-------|---------------|-----------|-----------|-----------|-------------|------------|

- Only include rows where delta is not zero
- For new vendors (current = $0), show "NEW" in the Delta (%) column
- Color-code the Delta ($) column: green for positive, red for negative

### Sheet N+2: "Anomaly Flags"

| # | Category | Client | Detail | Recommended Action |
|---|----------|--------|--------|--------------------|

- Number each anomaly sequentially
- Color-code by category: orange for stale/rate risk, yellow for conditional/pending, red for drift/reactivated
- Wrap text in Detail and Action columns

### Sheet N+3: "Stale Data Warnings"

| Chart Name | Last Updated | Days Since Update | Prepared By | Risk Level | Notes |
|------------|-------------|-------------------|-------------|------------|-------|

- Color-code rows by risk level: green (LOW), yellow (MEDIUM), red (HIGH)
- Include a legend at the bottom explaining the thresholds

### Formatting rules

- Use Calibri 11pt throughout
- Professional color scheme: navy headers (#1F4E79), white text on headers
- Thin borders on all data cells
- No emojis anywhere
- Use "--" (double dash) instead of em dashes for notes
- Currency format: "$#,##0" (no decimals for media spend)
- Percentage format: "0.0%"

## Daily rate calculation reference

When converting flight-based campaigns to monthly spend:

```
April 2026: 30 days
May 2026: 31 days
June 2026: 30 days
July 2026: 31 days
August 2026: 31 days
September 2026: 30 days
```

For partial months:
- Flight starts Apr 15: Apr days = 30 - 15 + 1 = 16 days
- Flight ends Apr 20: Apr days = 20 days
- Flight Apr 10 - Apr 20: Apr days = 20 - 10 + 1 = 11 days

Always use inclusive date counting (both start and end dates count).

## Deep dive: Chart format handling

The three formats below cover the vast majority of blocking charts seen in agency work. When you encounter a chart, classify it into one of these types before processing.

### Format A: Monthly spend by vendor (direct values)

**Identifying features:** Columns named by month (Jan, Feb, Mar, ...) or by date (2026-01, 2026-02). Each cell is a dollar amount. One row per vendor.

**Processing rules:**
1. Extract values for the forecast window months only (e.g., Apr, May, Jun for Q2)
2. Check for non-numeric values in forecast cells:
   - "HOLD" -- Planner has not forecast this month. Do NOT enter $0. Flag as "No forecast -- HOLD pending H2 planning" in Anomaly Flags. Leave the Maximizer entry unchanged for that vendor-month.
   - "TBD" -- Similar to HOLD but may resolve sooner. Flag as "TBD -- check with planner"
   - Empty/blank -- Ambiguous. Could mean $0 or could mean the planner forgot. Flag as anomaly asking for clarification.
   - "$0" or 0 -- Explicit zero. Enter it. This means the vendor is intentionally paused.
3. Sum all past months (Jan-Mar) to cross-check against any "Total" column if present. If the sum does not match, flag a data integrity issue.

**Common pitfalls:**
- Planners sometimes put formulas that display as $0 when they meant HOLD
- "Jul-Dec" might be a merged cell with "HOLD" -- each month should be flagged individually
- Watch for totals rows that include non-forecast months

### Format B: Flight-based with daily rates

**Identifying features:** Columns like Flight_Start, Flight_End, Daily_Rate. One row per campaign (not per vendor). Multiple campaigns may map to the same vendor.

**Processing rules:**
1. Parse flight dates into actual date objects
2. For each forecast month, calculate overlapping days:
   ```
   month_start = first day of month
   month_end = last day of month
   overlap_start = max(flight_start, month_start)
   overlap_end = min(flight_end, month_end)
   if overlap_end >= overlap_start:
       days = (overlap_end - overlap_start).days + 1  # inclusive
       monthly_spend = daily_rate * days
   else:
       monthly_spend = 0  # flight does not overlap this month
   ```
3. Aggregate all campaigns for the same vendor into a single vendor-month total
4. Check if a campaign flight ends within the forecast window -- flag as "Flight ends [date] -- renewal status unknown" unless the notes explicitly say "ends" or "final"

**Days per month reference (2026):**
- January: 31, February: 28, March: 31, April: 30, May: 31, June: 30
- July: 31, August: 31, September: 30, October: 31, November: 30, December: 31

**Common pitfalls:**
- Off-by-one errors on flight boundaries (always use inclusive counting)
- Flights that span only part of a month (e.g., Apr 15 - Jun 30 means Apr has 16 days, not 15)
- "Estimated Total" column in the source may not match your calculated total due to rounding -- verify but use your calculation
- Multiple campaigns for the same vendor need aggregation before comparison

### Format C: Quarterly totals with percentage splits

**Identifying features:** Columns like Q2_Total, Apr_Pct, May_Pct, Jun_Pct. One row per vendor. Percentages represent how the quarterly total is allocated across months.

**Processing rules:**
1. Verify percentages sum to 100 (or close -- allow 0.1% rounding tolerance). If not, flag as anomaly.
2. Calculate: `month_spend = Q_total * (month_pct / 100)`
3. Round to nearest dollar (no decimals for media spend)
4. Verify sum of monthly values equals Q total. Small rounding differences (less than $5) are acceptable; larger discrepancies should be flagged.

**Common pitfalls:**
- Some planners express splits as decimals (0.30) vs percentages (30) -- check whether values sum to ~1.0 or ~100
- "Apr 0% / May 50% / Jun 50%" means the vendor has no spend in April but is active May-Jun. This is intentional, not an error -- but it is worth noting if the vendor had prior-quarter spend (possible pause/restart).

## Deep dive: Conditional and pending items

Media plans frequently contain line items that are not yet confirmed. These require special handling to avoid overstating the forecast while still tracking them.

### Classification of conditional items

**Test-and-learn:** Experimental channels being trialed. Usually small budgets. Keywords: "test," "pilot," "trial," "test-and-learn," "experimental."
- Default action: Include in forecast but highlight with yellow
- Flag text: "Conditional -- test-and-learn, pending Q1 performance review"
- If the review date has passed and no update exists, escalate: "Review was due [date] -- status unknown"

**Pending approval:** Budget exists in plan but awaits sign-off. Keywords: "pending," "awaiting approval," "not yet approved," "subject to approval."
- Default action: Enter as $0 in Maximizer until approved. Show the planned amount in the Notes column.
- Flag text: "Pending approval -- enter $0 until confirmed. Planned amount: $X"

**Under review:** Budget amount may change. Keywords: "under review," "budget TBD," "amount to be confirmed."
- Default action: Include current planned amount but flag for revision
- Flag text: "Amount under review -- may change before entry"

**Renewal unknown:** Campaign ends within forecast window, no renewal info. No explicit keywords -- detect by comparing flight end dates to the forecast window boundary.
- Default action: Show $0 after flight end date
- Flag text: "Flight ends [date] -- renewal status unknown. Showing $0 for [months]."

### Presentation in the forecast

Conditional rows should be:
1. Highlighted in yellow across all columns
2. Included in the TOTAL row (so the Director sees the full picture)
3. Annotated in the Notes column with the condition
4. Listed individually in the Anomaly Flags sheet with recommended action

If the Director decides to exclude conditional items, the totals should be easy to recalculate by removing those rows.

## Deep dive: Stale data detection

### Staleness rules

Calculate `days_stale = today - chart.last_updated` for every source.

| Days Stale | Risk Level | Color  | Action Required |
|-----------|------------|--------|-----------------|
| 0-3       | CURRENT    | Green  | None -- data is fresh |
| 4-7       | LOW        | Green  | Acceptable for forecasting |
| 8-14      | MEDIUM     | Yellow | Usable but flag. Contact preparer for confirmation. |
| 15-21     | HIGH       | Red    | Request updated chart before entering data. Numbers may have changed. |
| 22+       | CRITICAL   | Red    | Do not enter without refresh. Chart is likely outdated. |

### What makes data go stale faster

Some chart types go stale faster than others:
- **Flight-based charts (Format B):** Stale within 7 days if rates are under renegotiation or flights are being extended/cancelled
- **Quarterly splits (Format C):** More stable -- percentages rarely change mid-quarter. 14-day threshold is usually safe.
- **Monthly direct (Format A):** Depends on the vendor mix. Programmatic/social budgets shift more frequently than search budgets.

### Cross-source staleness

When charts from the same client have very different update dates (e.g., Chart A updated 3 days ago, Chart B updated 17 days ago), flag the inconsistency. The stale chart may contain numbers that conflict with the fresh chart's assumptions.

## Deep dive: HOLD entries

"HOLD" is not $0. It means "we will spend money here but we do not know how much yet."

### Rules for HOLD handling

1. **Never convert HOLD to $0.** This is the most common and most dangerous error.
2. **Do not include HOLD months in totals.** If Jun is HOLD, the Jun total should only sum vendors with actual numbers. Add a note: "Jun total excludes HOLD vendors."
3. **Leave Maximizer unchanged for HOLD vendor-months.** If last month's Maximizer says $10K for a vendor in Jun, and the new chart says HOLD for Jun, keep the $10K in Maximizer and flag: "Chart shows HOLD for Jun -- leaving Maximizer at current value of $10K until H2 plan is set."
4. **Report HOLD entries separately.** In the Anomaly Flags sheet, list every HOLD entry with: vendor, month(s), last known spend level, and who to contact for the H2 plan.
5. **If all months beyond the forecast window are HOLD** (e.g., Jul-Dec all HOLD), note this in the Stale Data Warnings as "H2 planning not yet complete" rather than treating each month as a separate anomaly.

## Deep dive: Multi-client consolidation

When processing blocking charts for multiple clients in the same session:

### Separation rules
1. **One Maximizer Update sheet per client.** Never combine clients on the same sheet.
2. **Vendor names may overlap across clients.** "Meta" for VitalFit is a completely different line item than "Meta" for LuminaSkin. Keep them separate.
3. **The Change Log combines all clients** but includes a Client column as the first field. Sort by Client, then Vendor, then Month.
4. **Anomaly Flags combine all clients** with a Client column. Number anomalies sequentially across all clients.
5. **Stale Data Warnings are per-chart, not per-client.** One chart may serve multiple clients (rare but possible).

### Cross-client checks
- If the same planner updated charts for multiple clients on different dates, note the inconsistency
- If total agency spend across all clients exceeds historical norms, flag it (requires historical baseline data)
- Watch for vendor name inconsistencies across clients (e.g., "Meta" vs "Meta Ads" vs "Facebook/Instagram")

### Sheet ordering in the workbook
1. Maximizer Update - [Client A]
2. Maximizer Update - [Client B]
3. ... (one per client)
4. Change Log (all clients combined)
5. Anomaly Flags (all clients combined)
6. Stale Data Warnings (all charts)

## Reference implementation

A working Python script using openpyxl is available at:
`exercise-2-deep-dive/ideas/07-forecasting/generate_forecast.py`

This script demonstrates the full pipeline: data definition, sheet construction, formatting, delta calculation, anomaly flagging, and stale data warnings. Use it as a reference for the output structure and formatting conventions.
