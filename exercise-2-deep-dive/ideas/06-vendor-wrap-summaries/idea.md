# Idea 6: Vendor Wrap Report Summarization

## What They Said

> **The task or workflow:** Summarizing large vendor campaign wrap reports and including key takeaways and outcomes
>
> **The people/roles involved:** Planners
>
> **The step-by-step process today:** Skimming through each individual page searching for highlights and relevant campaign highlights
>
> **Where it breaks or slows down:** Having multiple reports to read through for a single campaign in a limited time frame
>
> **How AI could handle some or all of it:** AI could do this all in seconds whereas it may take up to an hour or more for a person to read through the whole deck and grab key insights and takeaways to include on the overall campaign performance deck

## Current Pain

- Vendors send lengthy wrap reports (often 30-50 pages)
- Multiple vendor reports per campaign
- Planners skim looking for highlights — inconsistent, easy to miss things
- Time pressure means reports get surface-level reads
- Key insights need to be extracted and added to the overall campaign performance deck

## Agent-Native Reframe

**AI synthesizes:** Full vendor wrap report + original campaign brief/SOW → structured summary: key results vs. objectives, standout metrics, underperformance flags, and recommended takeaways for the client deck.

**Human judges:** Whether the vendor's "key results" are actually impressive in context. Vendors always frame their numbers positively — the human spots when "10M impressions" sounds great but was against a 15M target.

**System improvement loop:** Build a "vendor report card" over time. Track which vendors consistently over-promise, which metrics they inflate, and where their reports diverge from platform data. Feed this context into future summarizations.

**v1 this week:** Take one vendor wrap report + the original brief. Prompt: "Summarize this vendor report. For each metric they highlight, compare to the original brief targets. Flag where they're celebrating something that actually underperformed."

**Connection to Exercise 1:** This is literally Demo 5 (Vendor Monitoring) from Exercise 1 — point this out. You already showed it working live. The difference here is scaling it across multiple vendors per campaign.
