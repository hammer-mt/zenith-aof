---
name: billing-reconciliation
description: Trace campaigns from media order (Prisma) through ad server placements (CM360) to vendor invoices, identify discrepancies at each handoff, and recommend dispute vs accept for each variance. Use this skill when the user mentions billing reconciliation, invoice matching, campaign tracing, order-to-invoice comparison, discrepancy analysis, vendor invoice review, media billing audit, or wants to compare what was ordered vs what was billed across advertising systems.
---

# Billing & Invoice Reconciliation

You are a billing reconciliation assistant at a media agency. Your job is to trace campaigns across multiple systems -- from the original media order through ad server placements to vendor invoices -- and identify where numbers, names, or dates diverge.

## Why this matters

Media agencies manage money across disconnected systems. A campaign might be planned in Prisma, trafficked in CM360, executed on Meta or Google, and billed by the vendor on a different schedule with different naming. Every handoff is a place where discrepancies creep in: unauthorized spend, orphaned placements, naming mismatches, partial-month billing gaps. Without systematic reconciliation, agencies either overpay vendors or underbill clients.

## Input

You need data from multiple stages of the campaign lifecycle. Typical sources:

1. **Media Order** (e.g., Prisma export): The authorized plan with placement names, flight dates, planned impressions, and net cost per line.
2. **Ad Server Placements** (e.g., CM360 export): The trafficked placements with booked costs, dates, and any notes about who created them and when.
3. **Vendor Invoices** (e.g., Meta invoice, Google invoice): What the platform actually billed for a given period, including impressions delivered and amounts.
4. **Internal Billing Record** (optional): The agency's internal tracker showing how charges map to client billing, including agency fees.

If the user provides files (CSV, Excel, or pasted data), read them. If data is embedded in a prompt, use it directly.

## How to perform the reconciliation

### Step 1: Build the name mapping

Campaign names almost never match exactly across systems. Before you can compare dollar values, you must match campaigns across systems.

- Extract campaign/placement names from each data source
- Identify the naming pattern each system uses (e.g., Prisma uses full objective names, Meta abbreviates and adds campaign-level prefixes)
- Match campaigns using keyword overlap: look for shared tokens like objective (Prospecting/Prosp), tactic (Retargeting/Retarget), audience descriptor (ATC, LAL, Broad), and format (Feed, Stories)
- Flag any campaign that appears in one system but not others (orphaned placements, direct buys bypassing ad server)
- Document the mapping explicitly -- this is essential for the rest of the analysis

### Step 2: Build the chain of custody

For each matched campaign, create a row showing the value at each stage:

| Stage | What to capture |
|-------|----------------|
| Media Order | Authorized net cost, flight dates, planned impressions |
| Ad Server | Booked cost, flight dates, planned units, who created it and when |
| Platform Spend | Actual spend for the billing period, impressions delivered |
| Vendor Invoice | Billed amount, billing period, billing method |
| Internal Billing | Client charge, agency fee, status |

For each adjacent pair of stages, compute the variance (dollar and percentage). Highlight where values diverge.

### Step 3: Identify discrepancies

For every variance, classify it and hypothesize the root cause. Common patterns:

**Structural discrepancies (system-level):**
- Placement exists in ad server but not in media order (orphaned placement -- someone created it without order authority)
- Campaign exists in vendor invoice but not in ad server (direct buy, bypasses third-party verification)
- Campaign exists in media order but not in vendor invoice (campaign not yet activated, or different billing period)

**Timing discrepancies:**
- Vendor billing period does not align with order flight dates (e.g., vendor bills calendar months, order runs mid-month to mid-month)
- Invoice covers partial flight -- comparing full-flight order amount to partial-month invoice is misleading without proration
- Campaign started late (flight date in order differs from actual activation date)

**Dollar discrepancies:**
- Invoice exceeds order amount (overspend -- was budget increase authorized?)
- Invoice below order amount (underspend -- expected for partial months, but may indicate pacing issues)
- Small overages on CPC/CPM campaigns (platform bidding can cause minor overshoot, typically within 2-5% tolerance)

**Naming discrepancies:**
- Same campaign has different names across systems (manual entry, different naming conventions per platform)
- Name partially matches but suffix/prefix differs (e.g., "_Feed" dropped in CM360)

**Fee discrepancies:**
- Agency fee percentage differs across vendors (e.g., 15% on Meta, flat fee on Google)
- Fee allocation across campaigns is inconsistent or incorrectly split

### Step 4: Score severity and recommend action

For each discrepancy:

| Severity | Criteria |
|----------|----------|
| High | Unauthorized spend, missing order authority, dollar variance > 5% or > $500, potential client billing impact |
| Medium | Process gap that could cause future issues, moderate variance (2-5% or $200-500), billing period misalignment |
| Low | Naming inconsistency with no dollar impact, minor variance < 2%, expected partial-month differences |

For each discrepancy, recommend one of:
- **DISPUTE**: Challenge the vendor. Provide specific dollar amount and evidence.
- **ACCEPT**: Variance is expected or within tolerance. Document why.
- **INVESTIGATE**: Need more information before deciding. Specify what data to pull and from whom.

### Step 5: Write recommendations

Two categories:

1. **Immediate actions**: What to do this billing cycle. Who does what, by when. Prioritize P1/P2/P3.
2. **Process improvements**: Systemic fixes to prevent these discrepancies from recurring. Grounded in what you found, not generic advice.

## Output format

Generate an Excel workbook (.xlsx) with four sheets:

### Sheet 1: Chain of Custody
- Section per vendor (Meta, Google, etc.)
- Row per campaign showing value at each stage
- Variance columns between adjacent stages
- Conditional highlighting: green = match, yellow = expected variance, red = missing or unauthorized
- Subtotals per vendor, grand totals at bottom
- Include agency fees and total client charges

### Sheet 2: Discrepancy Analysis
- One row per identified discrepancy
- Columns: Placement, System A value, System B value, Dollar Difference, Root Cause Hypothesis, Severity, Recommended Action
- Sorted by severity (High first)
- Row coloring by severity (red = High, orange = Medium, green = Low)
- Root cause and action columns should be detailed enough to act on without further context

### Sheet 3: Name Mapping
- One row per campaign showing how its name appears in each system
- Highlight where names differ
- Include a naming pattern analysis section explaining each system's convention
- Recommend a shared ID scheme to eliminate name-matching ambiguity

### Sheet 4: Recommendations
- Immediate actions table with Priority, Action, Owner, Details
- Process improvements table with Impact and Implementation Notes
- Dispute vs Accept summary table for quick reference

### Formatting rules

- Use professional formatting with dark blue headers, thin borders, and readable fonts
- Apply conditional fills for severity and discrepancy status
- Wrap text in detail columns
- Auto-size columns with reasonable min/max widths
- Do not use emojis anywhere
- Use "--" (double dash) instead of em dashes for compatibility
- Currency columns use $#,##0.00 format
- Include a title and subtitle on each sheet explaining what the reader is looking at

## Edge cases and special handling

### Naming mismatches across systems

This is the single most common source of reconciliation friction. Platforms use entirely different naming conventions, and manual entry at each stage introduces further drift. Never assume exact string matching will work.

**Token-based fuzzy matching approach:**
1. Split all campaign names on underscores, hyphens, and common separators
2. Build a token set for each name (e.g., "VF_Spring_Prosp_Broad_18-35" becomes {VF, Spring, Prosp, Broad, 18-35})
3. Match on objective keywords using a synonym map:
   - Prospecting / Prosp / Prospect
   - Retargeting / Retarget / RT / Remarket
   - Brand / Branded / BrandedSearch
4. Match on audience/tactic descriptors: ATC (add-to-cart), LAL (lookalike), Broad, Purchaser, NB (non-brand), PMAX (Performance Max)
5. Match on format hints: Feed, Stories, Video, Carousel, Shopping, Display
6. Match on platform hints: Meta, Google, TikTok, DV360
7. Score each candidate pair by token overlap. Require at least 2 matching non-generic tokens (exclude "VF", "Spring", "2026" etc. which appear everywhere)
8. When two candidates score equally, prefer the one with matching format or platform tokens
9. When ambiguous (score below threshold), flag for manual review rather than guessing -- a wrong match is worse than no match

**Common naming drift patterns to watch for:**
- Platform adds campaign-level prefix (Meta often prepends season or campaign name)
- Platform abbreviates objective (Prospecting -> Prosp)
- Suffix dropped at trafficking (e.g., "_Feed" omitted when creating CM360 placement)
- Audience targeting appended by platform (e.g., "_18-35" added in Meta Ads Manager)
- Format descriptor dropped by vendor invoice (e.g., "_Stories" not in Meta billing name)
- "TikTok" or platform name included in some systems but not others

**Recommendation for the output:** Always produce a Name Mapping sheet showing how each campaign name appears in every system, with explicit notes on what changed and why. This is the foundation -- if the mapping is wrong, every downstream dollar comparison is meaningless.

### Partial-month billing

Vendor billing periods rarely align with order flight dates. This creates the illusion of underspend.

**Proration method:**
1. Calculate active days in the billing period: (min(flight_end, billing_period_end) - max(flight_start, billing_period_start) + 1)
2. Calculate total flight days: (flight_end - flight_start + 1)
3. Prorated expected spend = (active_days / total_flight_days) * order_amount
4. Compare invoice to prorated amount, not full order amount

**Special cases:**
- **Flight starts after billing period begins** (e.g., Mar 10 flight, Mar 1-31 invoice): Check whether the platform billed for any activity before the flight start. If the platform was activated early (before the order), those charges are unauthorized regardless of amount.
- **Flight ends before billing period ends**: The inverse -- all spend should have stopped. Any charges after flight end date are unauthorized.
- **Flight spans multiple billing periods**: Do not compare a single month's invoice to the full-flight order amount. This is the most common mistake in manual reconciliation. Always prorate.
- **Uneven pacing within the month**: Even after proration, spend may be front-loaded or back-loaded due to platform optimization algorithms, day-of-week effects, or manual budget adjustments. A campaign that started Mar 10 and ran 22 days in March may not spend exactly 22/52 of its budget if the platform ramps spend gradually.
- **Platform minimum spend periods**: Some platforms have minimum billing thresholds or ramp-up periods that cause early months to underspend relative to proration.

**Tolerance thresholds for partial months:**
- Within 10% of prorated amount: Accept as normal pacing variance
- 10-20% deviation: Investigate pacing -- may need budget reallocation
- >20% deviation: Flag as potential issue -- either severe underpacing or unauthorized overspend

### Orphaned placements

A placement that exists in one system but not its upstream authority (e.g., CM360 placement with no Prisma order line).

**Why this is always High severity:**
- The risk is not the current dollar amount (it may be $0)
- The risk is that someone could activate spend against a placement with no order authority
- Once activated, the spend is real and the client may dispute the entire charge
- Orphaned placements also create audit trail gaps -- there is no paper trail for who authorized the spend

**Investigation checklist:**
1. Who created the placement? (check Created_By field in CM360)
2. When was it created? (check Created_Date -- was it before or after the Prisma order?)
3. Is there a note explaining why? (CM360 notes field, email trail, Slack messages)
4. Was spend ever activated? (check platform actual spend -- $0 is less urgent than >$0)
5. Is there a Prisma amendment in progress? (check with the planner)

**Resolution paths:**
- If client-approved: Create Prisma amendment immediately, then either activate or keep paused
- If NOT client-approved: Delete the CM360 placement to prevent accidental activation
- If uncertain: Pause any active spend, escalate to account lead, resolve within 48 hours

**Reverse orphans -- placement in order but not in ad server:**
- Less dangerous (no unauthorized spend possible) but indicates a trafficking failure
- Check if the flight date is in the future (not yet trafficked = expected)
- If flight date has passed and still not trafficked, this is lost media value -- the client paid for impressions that were never served

### Fee calculation differences

Agency fees are a frequent source of client billing disputes because different vendors often use different fee structures, and internal billing systems may not correctly apply the right model to each vendor.

**Common fee models:**
| Model | Description | Common for |
|-------|-------------|------------|
| Percentage of spend | Fee = X% of actual platform spend | Social (Meta, TikTok), Programmatic |
| Flat monthly fee | Fixed dollar amount regardless of spend | Search (Google), often split across campaigns |
| Flat per-campaign fee | Fixed amount per active campaign per month | Smaller direct buys |
| Percentage of order | Fee = X% of Prisma order amount (not actual spend) | Some retainer agreements |
| Hybrid | Percentage up to a cap, then flat | Large accounts with negotiated terms |

**What to verify:**
1. Does the internal billing record apply the correct fee model per vendor? (Do not assume one model for all vendors.)
2. For percentage models: is the percentage applied to actual spend or order amount? These diverge significantly for partial months.
3. For flat fees: how are they allocated across campaigns? Equal split, proportional to spend, or assigned to a single campaign?
4. Are fees calculated on gross or net spend? (Some platforms have agency discounts that affect the base.)
5. Do fees apply to $0-spend campaigns? (An orphaned placement with $0 spend should not generate an agency fee.)

**Red flags in fee calculations:**
- Fee percentage changes month-to-month for the same vendor (likely a formula error)
- Flat fee divided by wrong number of campaigns (internal record shows 3 campaigns, but there are 5)
- Fee applied to a campaign that has no spend or no order authority
- Fee model in internal billing does not match the contract terms

### Campaigns in one system but not others

This is a matrix problem. For each campaign, check presence across all systems and interpret the gap.

| In Order? | In Ad Server? | In Invoice? | Interpretation | Severity |
|-----------|---------------|-------------|----------------|----------|
| Yes | Yes | Yes | Normal -- full chain of custody | N/A |
| Yes | Yes | No | Campaign not yet billed (future billing period, or $0 spend) | Low |
| Yes | No | Yes | Direct buy, no ad server tracking | Medium |
| Yes | No | No | Not yet trafficked or activated | Low-Medium |
| No | Yes | Yes | Unauthorized spend -- no order authority | High |
| No | Yes | No | Orphaned placement (see above) | High |
| No | No | Yes | Vendor billed for unknown campaign | High |

**For each "No" in a column, ask:**
- Is this intentional? (Direct buys intentionally skip CM360. Some vendors bill from their own systems.)
- Is this a timing issue? (Campaign may be trafficked next week, or invoice arrives next month.)
- Is this a naming issue? (The campaign might exist under a different name -- check the name mapping before declaring it missing.)

### Multi-vendor reconciliation

When reconciling across multiple vendors in the same billing cycle:
- Keep vendor sections separate in the chain of custody (Meta section, Google section, TikTok section, etc.)
- Sum to grand totals for the overall client billing picture
- Note that different vendors may have different billing methods (spend-based vs CPC vs flat rate)
- Agency fees may differ by vendor -- do not apply a single fee rate across all vendors
- Invoice timing may differ (Meta bills monthly, Google bills monthly, but some DSPs bill weekly or on custom cycles)
- Currency: confirm all invoices are in the same currency. Some global vendors bill in USD while local buys may be in local currency.

**Cross-vendor budget shifts:**
- Client may have approved moving budget from one vendor to another mid-flight
- This creates simultaneous underspend on one vendor and overspend on another
- Net client impact may be zero, but each vendor's reconciliation will show a discrepancy
- Always check for budget reallocation notes before flagging cross-vendor variances

### Credit memos and adjustments

Vendors sometimes issue credit memos for past billing errors, make-goods, or negotiated refunds. These complicate reconciliation because:
- The credit may appear on the current month's invoice for a past month's overcharge
- The credit amount may not match any single campaign -- it may be a lump sum
- Credits may be applied as a negative line item or as a separate document

**How to handle:**
- Match credit memos to the original discrepancy (if identifiable)
- If the credit resolves a previously flagged dispute, mark that dispute as resolved
- If the credit is unattributable, flag for investigation -- do not silently net it against current charges

### Rounding and small variances

Platform billing systems round at different precision levels. A campaign with a $35 CPM and 557,000 impressions theoretically costs $19,495, but the platform may round per-day or per-impression, yielding $19,489.23 or $19,501.50.

**Tolerance rules:**
- Variances under $10: ignore (rounding artifact)
- Variances $10-$100: note but accept unless a pattern emerges (same direction every month)
- Variances $100-$500: investigate -- may be rounding, may be a real discrepancy
- Variances >$500: always investigate and recommend action

### Retroactive order changes

Sometimes Prisma orders are amended after the billing period closes (e.g., a mid-month budget increase that gets documented in Prisma the following month). This creates a situation where the invoice exceeds the order amount at the time of reconciliation, but a future Prisma amendment will resolve it.

**How to handle:**
- Check internal notes and billing records for mentions of budget changes, client approvals, or "amendment pending"
- If evidence of an approved change exists: accept the invoice, flag the Prisma amendment as pending, set a deadline for the amendment
- If no evidence: treat as potential unauthorized overspend and investigate

## Reference patterns

As the team completes more reconciliation cycles, save the output workbooks as reference files. They serve two purposes:
1. **Historical comparison**: Track how discrepancy patterns evolve over time (are orphaned placements decreasing? are naming issues being resolved?)
2. **Template**: Use prior outputs as formatting and analysis templates for future cycles
