# Task: Standardize Vendor Data to MDI Template

You are a data operations assistant at a media agency.

## Instructions

1. Read the MDI template schema and the vendor mapping reference below
2. Read the two raw vendor exports (Meta and Google)
3. Transform each vendor's data into the MDI standard format
4. Flag any fields you cannot map with confidence as ⚠️ NEEDS REVIEW

## Output

One unified table in MDI format covering both vendors, then a section listing every mapping decision you made and any ambiguities.

---

## MDI Template Schema

| Field | Description | Format |
|-------|-------------|--------|
| Campaign_Name | Standardized campaign name | [Client]_[Channel]_[Objective]_[Audience]_[Quarter] |
| Platform | Source platform | Meta / Google / TikTok / DV360 |
| Ad_Product | Ad format type | Standard_Display / Video / Native / Search / Shopping |
| Date_Range | Reporting period | YYYY-MM-DD to YYYY-MM-DD |
| Impressions | Total impressions served | Integer |
| Clicks | Total clicks | Integer |
| Spend_Media | Actual media cost (net) | CAD, 2 decimals |
| Spend_Fees | Agency/platform fees | CAD, 2 decimals |
| Spend_Total | Media + Fees | CAD, 2 decimals |
| Conversions | Primary conversion event | Integer |
| Conv_Type | Conversion definition | Purchase / Lead / SignUp / AddToCart |
| CPM | Cost per 1000 impressions | CAD, 2 decimals (calculated from Spend_Media) |
| CPC | Cost per click | CAD, 2 decimals |
| CPA | Cost per acquisition | CAD, 2 decimals |
| CTR | Click-through rate | Percentage, 2 decimals |

---

## Vendor Mapping Reference (Known Translations)

| Vendor Term | MDI Standard | Notes |
|-------------|-------------|-------|
| Meta: "Amount Spent" | Spend_Media | Does NOT include fees |
| Meta: "Results" | Conversions | Check Result_Type to determine Conv_Type |
| Meta: "Link Clicks" | Clicks | Not "All Clicks" — that includes likes, comments |
| Meta: "Reach" | — | No MDI equivalent, log but don't map |
| Google: "Cost" | Spend_Total | INCLUDES fees — must subtract to get Spend_Media |
| Google: "Conversions" | Conversions | |
| Google: "Conv. value" | — | No MDI equivalent |
| Google: "Impr." | Impressions | Abbreviated |

---

## Raw Vendor Export: Meta

Campaign: VitalFit_Spring_Prospecting
Reporting Period: March 1-15, 2026

| Campaign name | Ad Set | Format | Impressions | Reach | Link Clicks | All Clicks | Amount Spent | Results | Result Type | Frequency |
|--------------|--------|--------|-------------|-------|-------------|------------|-------------|---------|-------------|-----------|
| VF_Spring_Prosp_Broad_18-35 | Fitness Enthusiasts | Single Image | 245,000 | 198,000 | 3,420 | 5,100 | $8,240.00 | 142 | Purchase | 1.24 |
| VF_Spring_Prosp_Broad_18-35 | Health Conscious | Carousel | 312,000 | 251,000 | 4,680 | 7,200 | $10,560.00 | 198 | Purchase | 1.24 |
| VF_Spring_Prosp_LAL | LAL - Past Purchasers | Video | 189,000 | 162,000 | 2,100 | 3,800 | $7,350.00 | 167 | Purchase | 1.17 |
| VF_Spring_Retarget_ATC | Site Visitors - ATC | Single Image | 85,000 | 42,000 | 1,890 | 2,400 | $3,200.00 | 89 | Add to Cart | 2.02 |
| VF_Spring_Retarget_ATC | Site Visitors - ATC | Dynamic Product | 67,000 | 38,000 | 1,540 | 2,100 | $2,810.00 | 112 | Add to Cart | 1.76 |

Agency fee rate: 15% of media spend (not included in Amount Spent above)

---

## Raw Vendor Export: Google Ads

Campaign: VitalFit Spring Launch
Reporting Period: March 1-15, 2026

| Campaign | Ad group | Ad type | Impr. | Clicks | Cost | Conversions | Conv. value | Conv. type |
|----------|----------|---------|-------|--------|------|-------------|-------------|------------|
| VF_Spring_Brand | Brand - Exact | Responsive Search | 42,000 | 8,200 | $4,100.00 | 312 | $18,720.00 | Purchase |
| VF_Spring_Brand | Brand - Broad | Responsive Search | 68,000 | 5,400 | $3,780.00 | 189 | $11,340.00 | Purchase |
| VF_Spring_NB_Protein | Non-Brand - Protein | Responsive Search | 156,000 | 4,200 | $8,820.00 | 94 | $5,640.00 | Purchase |
| VF_Spring_NB_Supplements | Non-Brand - Supplements | Responsive Search | 198,000 | 3,800 | $9,120.00 | 78 | $4,680.00 | Purchase |
| VF_Spring_Shopping | All Products | Shopping | 284,000 | 6,100 | $7,930.00 | 156 | $9,360.00 | Purchase |
| VF_Spring_PMAX | Performance Max | PMAX | 520,000 | 4,800 | $12,400.00 | 201 | $12,060.00 | Purchase |

Google Ads "Cost" column includes platform fees. Agency fee: flat $2,500/month.
