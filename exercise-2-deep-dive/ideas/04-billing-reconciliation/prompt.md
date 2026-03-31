# Task: Trace a Campaign from Order to Invoice and Find Discrepancies

You are a billing reconciliation assistant at a media agency.

## Instructions

1. Read the Prisma Order (the original plan), the CM360 Placement log, and the Meta invoice below
2. Trace the campaign from order → placement → invoice
3. For every line, identify where numbers or dates diverge between systems
4. For each discrepancy, suggest the most likely root cause
5. Recommend which discrepancies to dispute vs. accept

## Output

A chain-of-custody table showing the value at each stage, then a discrepancy analysis with root cause hypotheses and recommended actions.

---

## Prisma Media Order

Order #: PMX-2026-0891  
Client: VitalFit Supplements  
Campaign: VitalFit Spring Launch — Meta  
Created by: Jordan (Planner), March 3, 2026

| Line # | Placement Name | Format | Flight Start | Flight End | Planned Impressions | Net Cost |
|--------|---------------|--------|-------------|-----------|-------------------|----------|
| 001 | VF_Prospecting_Broad_Feed | Image + Carousel | Mar 10 | Apr 30 | 800,000 | $28,000 |
| 002 | VF_Prospecting_LAL_Feed | Video | Mar 10 | Apr 30 | 300,000 | $10,500 |
| 003 | VF_Retargeting_ATC_Feed | Image + Dynamic | Mar 10 | Apr 30 | 200,000 | $8,400 |
| 004 | VF_Retargeting_Purchaser_Stories | Video | Mar 17 | Apr 30 | 100,000 | $3,100 |
| | | | | **TOTAL** | **1,400,000** | **$50,000** |

---

## CM360 Placement Log

Exported March 27, 2026  
Advertiser: VitalFit Supplements

| Placement ID | Placement Name | Start Date | End Date | Planned Units | Cost Structure | Booked Cost |
|-------------|---------------|-----------|---------|--------------|---------------|-------------|
| CM-44201 | VF_Prospecting_Broad_Feed | Mar 10 | Apr 30 | 800,000 | CPM | $28,000 |
| CM-44202 | VF_Prospecting_LAL_Feed | Mar 10 | Apr 30 | 300,000 | CPM | $10,500 |
| CM-44203 | VF_Retargeting_ATC | Mar 10 | Apr 30 | 200,000 | CPM | $8,400 |
| CM-44204 | VF_Retargeting_Purchaser_Stories | Mar 10 | Apr 30 | 100,000 | CPM | $3,100 |
| CM-44205 | VF_Prospecting_TikTok_Creators | Mar 17 | Apr 30 | 150,000 | CPM | $6,000 |

**Note:** CM-44205 does not appear in the Prisma Order. Created by Marcus on Mar 14 — tagged as "added per client request, Prisma update pending."

---

## Meta Invoice

Invoice #: META-INV-2026-03-VF  
Billing Period: March 1–31, 2026  
Advertiser: VitalFit Supplements

| Campaign | Impressions Delivered | Amount Billed | Billing Method |
|----------|---------------------|--------------|---------------|
| VF_Spring_Prosp_Broad_18-35 | 557,000 | $18,800.00 | Spend-based |
| VF_Spring_Prosp_LAL | 189,000 | $7,350.00 | Spend-based |
| VF_Spring_Retarget_ATC | 152,000 | $6,010.00 | Spend-based |
| VF_Spring_Retarget_Purchaser | 48,000 | $1,920.00 | Spend-based |
| VF_Spring_Prosp_Creators | 0 | $0.00 | Spend-based |
| **Total** | **946,000** | **$34,080.00** | |

**Meta's note:** "Campaign VF_Spring_Prosp_Creators was set up in Ads Manager but never activated. No spend recorded."

---

## What Makes This Tricky

- Campaign names don't match exactly across the three systems (Prisma, CM360, Meta)
- One placement exists in CM360 but not in the Prisma Order
- Flight dates in the order say Mar 10 start, but Meta billed from Mar 1
- The invoice is for March only — the order runs through April 30
- Impression pacing is uneven across placements
