# Fee Structures by Vendor

This reference documents known fee structures for each advertising platform. Verify against current contracts -- these can change per client or per IO.

## Meta (Facebook/Instagram)

| Fee Model | Description | Calculation |
|-----------|-------------|-------------|
| Percentage of media | Agency charges X% on top of net media spend | Spend_Fees = Spend_Media x rate |
| Amount Spent field | Net media cost only -- does NOT include agency fees | Confirmed in vendor mapping reference |

**Typical agency fee**: 10-20% of media spend (15% is common).
**Key rule**: Meta's "Amount Spent" = Spend_Media. Fees are additive: Spend_Total = Spend_Media + Spend_Fees.

## Google Ads

| Fee Model | Description | Calculation |
|-----------|-------------|-------------|
| Flat monthly fee | Fixed dollar amount per month regardless of spend | Prorate for partial periods, distribute by spend share |
| Cost field | Total billed amount -- INCLUDES fees | Confirmed in vendor mapping reference |

**Typical structures**: Flat $2,000-$5,000/month, or percentage (10-15%).
**Key rule**: Google's "Cost" = Spend_Total. Fees are subtractive: Spend_Media = Spend_Total - Spend_Fees.

### Proration formula for flat fees

```
prorated_fee = monthly_fee x (period_days / days_in_month)
campaign_fee = prorated_fee x (campaign_cost / total_cost_all_campaigns)
```

Example: $2,500/month, March 1-15 (15 of 31 days):
- Prorated fee = $2,500 x (15/31) = $1,209.68
- Campaign with $4,100 of $46,150 total cost: fee = $1,209.68 x (4100/46150) = $107.47

## TikTok

| Fee Model | Description | Calculation |
|-----------|-------------|-------------|
| Platform fee (embedded) | TikTok takes a cut but does not break it out in exports | Estimate only -- verify against contract |
| Total Cost field | Total amount inclusive of platform fees | Confirmed in vendor mapping reference |

**Key rule**: TikTok fee structure is frequently opaque in exports. The split between media cost and platform fees is NOT provided. Always flag for human review and use a placeholder estimate (commonly 10%) until verified.

## DV360

| Fee Model | Description | Calculation |
|-----------|-------------|-------------|
| Gross vs. Net | DV360 can report either depending on account-level settings | Check account settings or ask the trading desk |
| Partner costs | May include data fees, verification fees, ad serving fees separately | Map each to Spend_Fees if they are non-media costs |

**Key rule**: Always confirm whether DV360 is reporting gross (includes markup) or net (media cost only). This fundamentally changes how Spend_Media and Spend_Fees are calculated.
