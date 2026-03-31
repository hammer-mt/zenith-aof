# Task: QA Budgets Across Master Sheet and Platform Settings

You are a QA assistant at a media agency.

## Instructions

1. Read the master budget sheet (source of truth) and the Google Ads budget export below
2. Compare every campaign line by line
3. For each: report whether budgets match or flag the discrepancy with the dollar difference
4. Classify each discrepancy as likely an error or a possible intentional adjustment (using the change log for clues)

## Output

A discrepancy report table, then a summary of total exposure and recommended actions.

---

## Master Budget Sheet (Source of Truth)

Last updated: March 25, 2026

| Client | Campaign | Channel | Monthly Budget | Flight Dates | Notes |
|--------|----------|---------|---------------|-------------|-------|
| VitalFit | VF_Spring_Brand | Google Search | $8,000 | Mar 1 - May 31 | |
| VitalFit | VF_Spring_NB_Protein | Google Search | $9,000 | Mar 1 - May 31 | |
| VitalFit | VF_Spring_NB_Supplements | Google Search | $9,000 | Mar 1 - May 31 | |
| VitalFit | VF_Spring_Shopping | Google Shopping | $8,000 | Mar 1 - May 31 | |
| VitalFit | VF_Spring_PMAX | Google PMAX | $12,000 | Mar 1 - May 31 | |
| VitalFit | VF_Spring_Prosp_Broad | Meta | $20,000 | Mar 1 - May 31 | |
| VitalFit | VF_Spring_Prosp_LAL | Meta | $7,500 | Mar 1 - May 31 | |
| VitalFit | VF_Spring_Retarget_ATC | Meta | $6,500 | Mar 1 - May 31 | |
| LuminaSkin | LS_Q1_Awareness | Meta | $15,000 | Jan 1 - Mar 31 | |
| LuminaSkin | LS_Q1_Retarget | Meta | $8,000 | Jan 1 - Mar 31 | |
| LuminaSkin | LS_Q1_Search_Brand | Google Search | $5,000 | Jan 1 - Mar 31 | |
| LuminaSkin | LS_Q1_Search_NB | Google Search | $12,000 | Jan 1 - Mar 31 | |

---

## Google Ads Budget Export (Pulled March 26, 2026)

| Campaign | Daily Budget | Monthly Equivalent | Status | Last Modified |
|----------|-------------|-------------------|--------|---------------|
| VF_Spring_Brand | $266.67 | $8,000.00 | Active | Mar 1 |
| VF_Spring_NB_Protein | $330.00 | $9,900.00 | Active | Mar 12 |
| VF_Spring_NB_Supplements | $300.00 | $9,000.00 | Active | Mar 1 |
| VF_Spring_Shopping | $300.00 | $9,000.00 | Active | Mar 18 |
| VF_Spring_PMAX | $433.33 | $13,000.00 | Active | Mar 15 |
| LS_Q1_Search_Brand | $166.67 | $5,000.00 | Active | Jan 5 |
| LS_Q1_Search_NB | $400.00 | $12,000.00 | Paused | Mar 20 |

---

## Change Log (Internal Slack Messages)

**Mar 12 — Jordan (Planner):** "Bumping VF Protein non-brand by $30/day, client approved on our call today. Will update master sheet tomorrow." 

**Mar 15 — Jordan (Planner):** "VF PMAX is crushing it, asked client if we can push budget. They said go for it, increasing to $433/day."

**Mar 18 — Priya (Ad Ops):** "Noticed Shopping was underspending, adjusted daily cap up to $300 to help it spend through."

**Mar 20 — Sarah (Account Lead):** "Client wants to pause LS non-brand search for the last 10 days of Q1, shifting budget to Meta awareness."
