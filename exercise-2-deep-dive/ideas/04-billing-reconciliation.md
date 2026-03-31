# Idea 4: Billing & Invoice Reconciliation (End-to-End)

## What They Said

> **The task or workflow:** All things billing and invoice reconciliation related
>
> **The people/roles involved:** Planning team, Finance team, varying degree of PMX teams
>
> **The step-by-step process today:** Planning team creates Prisma Order, creates Placements (varying levels of consistency re: PMX teams creating placements), pushed to Campaign Manager 360 to create Placements, tags sent manually to Programmatic teams, campaign runs. Monthly Draft Billing approval emails which take time for teams to review and approve manually before invoices issued to clients. Later, invoices come from vendors like Meta and Google.
>
> **Where it breaks or slows down:** When invoices come through from vendor, discrepancies are called out which can lead to manual investigation.
>
> **How AI could handle some or all of it:** End to end streamlining, including placement creation and more rapidly identifying culprit of discrepancies.

## Current Pain

- Multi-step process across 3+ teams (Planning, Finance, PMX)
- Placement creation is inconsistent across teams
- Manual tag sending to Programmatic teams
- Monthly billing approval is slow (email-based review cycles)
- Vendor invoices (Meta, Google) don't match internal records → manual investigation
- Root cause of discrepancies is hard to trace back through the chain

## Agent-Native Reframe

**AI synthesizes:** Prisma Order → Placements → CM360 Placements → Vendor invoices → Internal billing records. Cross-references the entire chain to find where numbers diverge. "The Meta invoice says $42,000 but the Prisma Order was $38,000. The discrepancy originated at the placement level — PMX created a placement with a different flight date."

**Human judges:** Whether to dispute the invoice, adjust the internal record, or escalate. Decides on process fixes when the same type of discrepancy keeps recurring.

**System improvement loop:** Track discrepancy root causes over time. "80% of Meta discrepancies come from flight date mismatches at placement creation." → Surface this pattern to the team creating placements BEFORE the campaign runs, not after.

**v1 this week:** Take one month's billing cycle — the Prisma Order, the CM360 placements, and the vendor invoice. Prompt: "Trace this campaign from order through placement through invoice. Identify every point where numbers or dates diverge. For each discrepancy, suggest the most likely root cause."

**Connection to Exercise 1:** This is essentially the Vendor Monitoring demo from Exercise 1, but zoomed into the billing chain specifically. Call that out.
