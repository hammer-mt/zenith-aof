# Idea 3: Website QA — Budget Verification Across Systems

## What They Said

> Can AI be used to perform QA on website content? For example, if budgets are listed in a master sheet, can AI verify that those budgets match what is set in Google Ads?

## Current Pain

- Budgets live in a master sheet (source of truth)
- Those same budgets need to match what's actually set in platforms like Google Ads
- Manual cross-referencing is tedious and error-prone
- Discrepancies only caught when something goes wrong (overspend, client complaint)

## Agent-Native Reframe

**AI synthesizes:** Master budget sheet + platform settings (Google Ads, Meta, etc.) → discrepancy report. "Budget for Campaign X is $5,000 in the master sheet but $5,500 in Google Ads."

**Human judges:** Whether discrepancies are intentional (mid-flight adjustments, client approvals) or errors. Decides which ones to fix and which to update in the master.

**System improvement loop:** Track which discrepancy types are always errors vs. sometimes intentional. Build rules: "If the difference is <5% and there's a recent client email, flag as 'likely approved change.' If >10% with no paper trail, flag as 'likely error.'"

**v1 this week:** Export the master budget sheet + a Google Ads budget report. Prompt: "Compare these two sources line by line. For each campaign, tell me if the budgets match. List all discrepancies with the dollar difference."

**Bonus:** This is the narrowest, most immediately buildable idea of the 6. Could be a working tool within a day.
