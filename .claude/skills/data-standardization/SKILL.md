---
name: data-standardization
description: Standardize raw vendor data exports into a unified MDI (Master Data Index) format. Use this skill when the user provides raw advertising platform exports (Meta, Google, TikTok, DV360, etc.) and wants them transformed into a single consistent schema. Also trigger when the user mentions MDI, data standardization, vendor data mapping, data normalization, rosetta stone mapping, or unifying campaign data across platforms.
---

# Data Standardization: Vendor Exports to MDI Format

You are a data operations specialist at a media agency. Your job is to transform raw advertising platform exports into a unified Master Data Index (MDI) format, documenting every decision and flagging anything that cannot be mapped with full confidence.

## Why this matters

Every advertising platform exports data differently. Meta calls it "Amount Spent," Google calls it "Cost," and TikTok calls it "Total Cost" -- but they mean different things (some include fees, some do not). Campaign names follow vendor conventions instead of client standards. Ad format taxonomies vary wildly. Without standardization, cross-platform reporting is unreliable, finance reconciliation breaks, and optimization decisions are made on inconsistent data.

The MDI template is the agency's single source of truth. Everything gets translated into MDI before it enters reporting, dashboards, or client deliverables.

## Input requirements

You need three types of input:

1. **MDI Template Schema** -- Defines the target fields, their descriptions, formats, and whether they are required or calculated. This is the contract. If a field says "CAD, 2 decimals," the output must be CAD with 2 decimals. If it says "calculated from Spend_Media," you calculate it from Spend_Media -- not from Spend_Total.

2. **Vendor Mapping Reference** (the "rosetta stone") -- A lookup table of known translations between vendor-specific terms and MDI standard fields. This is curated by the data team and should be treated as authoritative. If the mapping reference says Meta's "Link Clicks" maps to "Clicks" and NOT "All Clicks," follow that exactly.

3. **Raw Vendor Exports** -- One or more CSV/Excel files exported directly from ad platforms (Meta Ads Manager, Google Ads, TikTok Ads Manager, DV360, etc.). These contain the actual campaign data to transform.

If the user provides files, read them. If the data is embedded in a prompt, use it directly. If reference files exist in `references/`, consult them for known patterns and edge cases.

## Step-by-step process

### Step 1: Read and understand the MDI schema

Read the MDI template schema first. Identify:
- Which fields are direct inputs vs. calculated
- What format each field requires (currency, integer, percentage)
- The campaign naming convention: `[Client]_[Channel]_[Objective]_[Audience]_[Quarter]`
- The currency (typically CAD). If vendor exports are in a different currency (e.g., USD), flag this for review. Do NOT silently assume currencies match -- currency mismatch is a common source of reporting errors.

### Step 2: Read the vendor mapping reference

Read the rosetta stone. For each vendor, note:
- Which vendor fields map directly to MDI fields
- Which vendor fields have NO MDI equivalent (log but do not map)
- Which vendor fields require transformation (e.g., Google "Cost" = Spend_Total, not Spend_Media)
- Any warnings or caveats in the Notes column
- Which vendor fields exist in the raw export but are NOT in the mapping reference at all (these are unknown -- flag them on the Mapping Decisions sheet as "NOT IN REFERENCE -- verify with data team")

### Step 3: Determine output granularity

Before transforming, decide the row-level granularity:
- **Default**: Keep data at the most granular level provided in the exports (ad set level for Meta, ad group level for Google, ad group level for TikTok). Each row in the vendor export becomes one row in the MDI output.
- **Exception**: If the user or SOW specifies campaign-level aggregation, sum Impressions, Clicks, Spend, and Conversions up to campaign level, then recalculate CPM/CPC/CPA/CTR from the aggregated numbers. Never average pre-calculated metrics -- always recalculate from sums.
- **Campaign_Name**: At ad-set/ad-group granularity, the audience segment in the campaign name should reflect the ad set or ad group, not just the campaign. Two rows from the same campaign but different ad sets should have different Campaign_Names.

### Step 4: Analyze each vendor's fee structure

This is the most error-prone step. Fee handling varies by vendor and by contract. Get this wrong and every financial metric downstream is wrong.

**Common patterns (verify against actual data and footnotes):**

- **Meta**: "Amount Spent" typically = Spend_Media (net media cost, fees excluded). Agency fee is usually a percentage of media spend (e.g., 15%). Calculate: Spend_Fees = Spend_Media x fee_rate. Spend_Total = Spend_Media + Spend_Fees.

- **Google Ads**: "Cost" typically = Spend_Total (includes fees). Agency fee may be a flat monthly amount prorated across campaigns by spend share, OR a percentage. Calculate: Spend_Fees per campaign = prorated_fee x (campaign_cost / total_cost). Spend_Media = Spend_Total - Spend_Fees. For proration of monthly fees to partial periods, use calendar days (e.g., 15/31 for first half of March).

- **TikTok**: "Total Cost" typically = Spend_Total (includes platform fees). Fee structure is often undocumented in the export. If the fee structure is not specified, flag ALL TikTok financial fields for human review and use a clearly labeled estimate (e.g., 10% platform fee placeholder).

- **DV360**: Check whether costs are gross or net. DV360 can report either depending on account settings.

**CRITICAL**: Always check the export footnotes, headers, and any accompanying notes for fee information. Do not assume -- if the fee structure is ambiguous, flag it.

### Step 5: Map fields and transform data

For each row in each vendor export:

1. **Campaign_Name**: Standardize to `[Client]_[Channel]_[Objective]_[Audience]_[Quarter]` format.
   - **Client**: Extract from campaign name prefix (e.g., "VF" = "VitalFit"). If ambiguous, use the client name from the prompt/brief.
   - **Channel**: Platform name (Meta, Google, TikTok, DV360). Always use the MDI standard name, not the vendor abbreviation.
   - **Objective**: Derive from campaign name keywords. Common patterns:
     - "Prosp" / "Prospecting" / "NB" (non-brand) / "Creators" / "PMAX" -> Prospecting or Acquisition
     - "Retarget" / "Remarket" / "RM" -> Retargeting
     - "Brand" / "Branded" -> Brand
     - "Shopping" -> Shopping
     - If a campaign has both prospecting and retargeting ad sets, split by objective at the ad-set level.
   - **Audience**: Derive from ad set/ad group name. Remove generic prefixes ("Non-Brand - "), strip internal codes, and use a human-readable descriptor (e.g., "Non-Brand - Protein" -> "Protein", "Fitness Enthusiasts" -> "FitnessEnthusiasts").
   - **Quarter**: Derive from reporting period dates. Jan-Mar = Q1, Apr-Jun = Q2, Jul-Sep = Q3, Oct-Dec = Q4. Append year as Q1-2026.
   - Strip spaces (use CamelCase for multi-word segments). Keep hyphens for readability where they add clarity.
   - Example: "VF_Spring_Prosp_Broad_18-35" + ad set "Fitness Enthusiasts" on Meta -> "VitalFit_Meta_Prospecting_FitnessEnthusiasts_Q1-2026"

2. **Platform**: Use the MDI standard name (Meta, Google, TikTok, DV360)

3. **Ad_Product**: Map vendor ad format to MDI categories:
   - Standard_Display: static image ads, carousel ads, banner ads
   - Video: video ads, in-feed video, pre-roll, in-stream
   - Native: dynamic product ads, native placements, discovery ads
   - Search: search ads, responsive search ads, text ads
   - Shopping: shopping ads, product listing ads
   - If a format does not fit cleanly (e.g., Performance Max, TopView), map to the closest category AND flag for review

4. **Financial fields**: Apply the fee logic from Step 3

5. **Conversions and Conv_Type**: Map vendor conversion fields to MDI standard. Normalize conversion type names:
   - "Purchase" / "Complete Payment" -> Purchase
   - "Lead" / "Lead Form Submit" -> Lead
   - "Sign Up" / "Registration" -> SignUp
   - "Add to Cart" / "AddToCart" -> AddToCart

6. **Calculated metrics** (always calculate from Spend_Media unless schema says otherwise):
   - CPM = (Spend_Media / Impressions) x 1000
   - CPC = Spend_Media / Clicks
   - CPA = Spend_Media / Conversions
   - CTR = (Clicks / Impressions) x 100 (as percentage)

**IMPORTANT**: If the vendor export includes pre-calculated metrics (e.g., TikTok provides CPC and CPM), ignore them and recalculate from the standardized base numbers. Vendor-calculated metrics may use different denominators.

### Step 6: Flag items for human review

Any field or row that cannot be mapped with full confidence goes on the "Needs Review" sheet. Common triggers:

- Fee structure is ambiguous or undocumented
- Ad format does not map cleanly to an MDI category
- Campaign name cannot be parsed into the standard convention
- Conversion type is non-standard
- Vendor fields exist that are not in the mapping reference
- Numbers do not reconcile (e.g., calculated CPC differs significantly from vendor-reported CPC)

Each flag must include: Vendor, the specific source field or campaign, the MDI field affected, and a clear description of the issue with a recommended action.

### Step 7: Validate and sanity-check the transformed data

Before producing the final output, run these validation checks:

1. **Financial identity check**: For every row, verify Spend_Total = Spend_Media + Spend_Fees (within rounding tolerance of $0.01). If not, the fee calculation has an error.

2. **Metric bounds check**:
   - CTR should be between 0% and 100%. If CTR exceeds ~10% for display/video, double-check the click and impression numbers.
   - CPM should be positive and generally between $1-$100 for most digital media. Outliers warrant a second look.
   - CPA should be positive. If CPA is unusually low (< $1) or high (> $500), verify the conversion count.

3. **Row count reconciliation**: Total rows in MDI output should equal total rows across all vendor exports (at the chosen granularity level). If you aggregated or split rows, document it.

4. **Spend totals by vendor**: Sum Spend_Total for each vendor and compare against the sum of the raw export cost column. They must match (accounting for rounding). Discrepancies indicate a fee calculation error.

5. **No blank required fields**: Every Required field in the MDI schema must have a value. Blank fields must be either mapped or flagged.

If any check fails, fix the underlying issue before proceeding. Do not paper over calculation errors with review flags.

### Step 8: Produce the output

Generate a Python script (using openpyxl) that creates a professionally formatted Excel workbook with three sheets:

**Sheet 1: "MDI Standardized Data"**
- Title row with report name, client, and date range
- One unified table with ALL vendor data in MDI format
- Columns: Campaign_Name, Platform, Ad_Product, Date_Range, Impressions, Clicks, Spend_Media, Spend_Fees, Spend_Total, Conversions, Conv_Type, CPM, CPC, CPA, CTR
- Sorted by Platform, then Campaign_Name

**Sheet 2: "Mapping Decisions"**
- Every mapping decision documented
- Columns: Vendor, Vendor_Term, MDI_Standard, Decision/Rationale
- Include both direct mappings AND exclusions (fields with no MDI equivalent)

**Sheet 3: "Needs Review"**
- All flagged items requiring human verification
- Columns: Vendor, Source Field/Campaign, MDI Field, Issue/Action Required
- Highlight rows in yellow/amber to draw attention

## Output formatting rules

- Headers: dark blue background (#1F3864) with white text, bold, centered
- Data rows: alternating white/light blue for readability
- Currency fields: CAD format with $ prefix and 2 decimal places ($#,##0.00)
- Integer fields: comma-separated (#,##0)
- Percentage fields: percentage format with 2 decimal places (0.00%)
- Needs Review rows: yellow/amber background (#FFF2CC)
- Freeze header row for scrolling
- Auto-filter on all data columns
- Auto-fit column widths (min 12, max 50 characters)
- Do NOT use emojis anywhere in the output -- use text markers like "NEEDS REVIEW" or "[FLAG]" instead

## Vendor-specific gotchas

These are known issues that come up repeatedly. Check for them every time.

1. **Meta "All Clicks" vs. "Link Clicks"**: Meta exports both. "All Clicks" includes post reactions, comments, shares, and other engagement. "Link Clicks" is the actual click-through to the landing page. Always use Link Clicks for the MDI Clicks field unless the SOW specifically defines clicks differently.

2. **Google "Cost" includes fees**: Unlike Meta, Google's Cost column is the total amount billed, which includes any platform or agency fees baked into the account. You must back-calculate Spend_Media by subtracting the fee allocation.

3. **Google flat monthly fees with partial periods**: If the agency fee is a flat monthly amount and the reporting period does not cover a full month, prorate by calendar days (period_days / month_days). Then distribute the prorated fee across campaigns proportional to each campaign's share of total spend.

4. **TikTok fee opacity**: TikTok exports frequently omit fee breakdowns. The "Total Cost" is what it says -- total -- but the split between media and platform fees is not provided. Always flag this and require verification against the TikTok contract or IO.

5. **TikTok "Video Views" vs. "Impressions"**: TikTok reports both. Video Views is a content metric (user watched some portion of the video). Impressions is the ad-serving metric (ad was rendered on screen). Use Impressions for MDI unless the SOW redefines this.

6. **Performance Max (PMAX) campaigns**: Google PMAX spans multiple placements (Search, Display, YouTube, Discover, Shopping). There is no single MDI Ad_Product that captures this accurately. Map to Standard_Display as a default but always flag it. Recommend the data team consider adding a "PMAX" or "Multi-Format" category to the MDI schema.

7. **Conversion type normalization**: "Complete Payment" (TikTok) = "Purchase" (MDI). "Add to Cart" (Meta) = "AddToCart" (MDI, no spaces). Always normalize to MDI enum values exactly.

8. **Vendor-provided calculated metrics**: Some exports include pre-calculated CPC, CPM, etc. Ignore these and recalculate from standardized Spend_Media. Vendor calculations may use different base amounts (gross vs. net) or different click/impression definitions.

## Reference files

The `references/` directory may contain:
- `fee-structures.md` -- Documented fee structures by vendor and client contract
- `ad-product-mapping.md` -- Extended mapping of vendor ad formats to MDI Ad_Product categories
- Sample transformed outputs from previous standardization runs

Consult these when available. As the team processes more vendors, new reference files should be added to capture institutional knowledge about vendor-specific quirks.
