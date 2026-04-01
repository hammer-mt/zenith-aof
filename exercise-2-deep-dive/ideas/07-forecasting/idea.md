# Idea 7: Vendor Spend Forecasting & Maximizer Updates

## What They Said

> Forecasting — typically handled at a Director level but requires background information usually handled by more junior levels (Planners or Assistants). The task involves compiling current planned/forecasted spends (mainly by vendor for the monthly forecasting session) and establishing a monthly breakdown of potential spends to properly update the system.
>
> Steps: Before the forecasting window opens, the most updated blocking charts are gathered for each client. I have a document for each client to compile all spends which requires manual inputs monthly. Once complete, I create a pivot table for formal inputs into the Maximizer system. From there, updates in Maximizer can commence.
>
> Where it breaks: Each blocking chart can be different (different vendors, different time periods, not standardized). Charts might not be fully updated or planning changes can be in progress. The overall process is tedious — sourcing charts, ensuring you have all of them (some clients have multiple brands/campaigns), manual inputs, finding anomalies, and going back to planning teams for answers. It's also on top of regular day-to-day work.
>
> How AI could help: Submitting all blocking charts for a client into AI to consolidate vendor-level spends and compile into reliable monthly breakouts, eliminating the manual nature of updates to build the pivot table for Maximizer.

## Current Pain

- Blocking charts are non-standardized: different vendors, time periods, formulas, layouts per client
- Multiple blocking charts per client (brands, campaigns) that all need to be compiled
- Manual monthly data entry into a consolidation doc, then pivot table, then Maximizer
- Blocking charts may be outdated or mid-revision when forecasting window opens
- Anomalies between current blocking charts and previous Maximizer entries require investigation
- Investigation means going back to planners for context — adds rounds of back-and-forth
- Director-level task that depends on junior-level data gathering — handoff friction
- Happens on top of day-to-day client work, not protected time

## Agent-Native Reframe

**AI synthesizes:** Multiple blocking charts (different formats, vendors, date ranges) + previous Maximizer entries + vendor mapping → unified monthly spend breakdown by vendor ready for Maximizer input. Flags anomalies: "Campaign X shows $0 in April but had $15K last month — is this a pause or a missing update?"

**Human judges:** Whether anomalies are real changes (planned pauses, budget shifts) or data gaps (outdated blocking chart, planner hasn't updated yet). Decides what to flag back to planning teams vs. accept as-is.

**System improvement loop:** Track which clients/blocking charts consistently cause issues. "Client Y's blocking chart is always 2 weeks behind." Build a pre-forecasting checklist that surfaces which charts are stale before the window opens. Over time, learn each client's blocking chart layout so parsing improves automatically.

**v1 this week:** Take 2-3 blocking charts for one client (different formats) + last month's Maximizer entries. Prompt: "Parse these blocking charts, consolidate vendor-level spend by month, flag anything that changed vs. last month's forecast, and output a Maximizer-ready table."

**Connection to other ideas:** This shares DNA with Idea 2 (data standardization) — both are about taking non-standard inputs and normalizing them. The difference is that Idea 2 is about platform reporting data going into MDI templates, while this is about planning/budget data going into a forecasting system. The "rosetta stone" pattern applies here too.
