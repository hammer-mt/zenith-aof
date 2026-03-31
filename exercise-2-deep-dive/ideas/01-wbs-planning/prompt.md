# Task: Generate a WBS from Past Projects

You are a project planning assistant at a media agency.

## Instructions

1. Read the two completed project WBS documents and the new project brief below
2. Generate a Work Breakdown Structure for the new project that:
   - Follows the structure and task patterns from past projects
   - Assigns roles based on the team in the brief
   - Estimates timelines based on historical durations
   - Marks any tasks where the new project deviates from past patterns with ⚠️

## Output Format

Use a table per phase with columns: Task | Owner | Duration | Dependencies | Notes

End with:
- **⚠️ Uncertainty Flags** — where this project deviates from past patterns
- **Recommendations** — anything you'd flag to the PM based on what you see

---

## Past Project A: FreshBrew Coffee — Summer Push (Completed)

**Duration:** 8 weeks | **Budget:** $320K | **Channels:** Meta, Google Search, YouTube

| Phase | Task | Owner | Duration | Notes |
|-------|------|-------|----------|-------|
| 1. Setup | Client kickoff call | Account Lead | Week 1 | |
| 1. Setup | Receive brand assets & guidelines | Account Coord | Week 1 | Delayed 3 days — client slow to send |
| 1. Setup | Build media plan | Planner | Week 1-2 | |
| 1. Setup | Trafficking & tagging | Ad Ops | Week 2 | |
| 2. Launch | Campaign launch (Meta + Google) | Planner + Ad Ops | Week 3 | |
| 2. Launch | YouTube pre-roll go-live | Video Specialist | Week 3 | Delayed 2 days — creative not approved |
| 3. Optimize | Weekly performance reviews | Planner | Weeks 3-7 | |
| 3. Optimize | Mid-flight optimization report | Planner | Week 5 | Client requested extra cut by region |
| 3. Optimize | Creative refresh (Meta) | Creative + Planner | Week 5 | |
| 4. Wrap | Final performance report | Planner + Insights | Week 8 | |
| 4. Wrap | Vendor reconciliation | Finance | Week 8-9 | Took extra week due to Meta discrepancy |
| 4. Wrap | Client debrief presentation | Account Lead | Week 9 | |

---

## Past Project B: GlowUp Skincare — Holiday Campaign (Completed)

**Duration:** 10 weeks | **Budget:** $480K | **Channels:** Meta, TikTok, Google Search, Programmatic Display

| Phase | Task | Owner | Duration | Notes |
|-------|------|-------|----------|-------|
| 1. Setup | Client kickoff call | Account Lead | Week 1 | |
| 1. Setup | Receive brand assets & guidelines | Account Coord | Week 1 | |
| 1. Setup | Audience research & persona development | Insights | Week 1-2 | New for this client |
| 1. Setup | Build media plan | Planner | Week 1-3 | Extra week — 4 channels |
| 1. Setup | Trafficking & tagging (all platforms) | Ad Ops | Week 3 | |
| 1. Setup | Programmatic deal setup (PMPs) | Programmatic Lead | Week 2-3 | |
| 2. Launch | Phased launch: Meta + Google first | Planner | Week 4 | |
| 2. Launch | TikTok + Programmatic launch | Planner + Prog Lead | Week 5 | Staggered to manage QA |
| 3. Optimize | Weekly performance reviews | Planner | Weeks 4-9 | |
| 3. Optimize | Mid-flight report | Planner + Insights | Week 6 | |
| 3. Optimize | Creative refresh (Meta + TikTok) | Creative + Planner | Week 7 | |
| 3. Optimize | Audience rebalancing | Planner | Week 7 | Shifted budget from Display → TikTok |
| 4. Wrap | Final performance report | Planner + Insights | Week 10 | |
| 4. Wrap | Vendor reconciliation | Finance | Week 10-11 | |
| 4. Wrap | Client debrief + next steps | Account Lead + Planner | Week 11 | |

---

## New Project Brief: VitalFit Supplements — Spring Launch

**Client:** VitalFit (sports nutrition, DTC brand, first time working with this agency)  
**Budget:** $400K  
**Duration:** Target 10 weeks  
**Channels:** Meta, TikTok, Google Search, Connected TV (new channel — agency hasn't run CTV for a DTC client before)

**Team:**
- Account Lead: Sarah
- Planner: Jordan
- Ad Ops: Priya
- Programmatic Lead: Marcus (handling CTV buys)
- Insights: Anika
- Creative: External agency (client's existing partner)

**Key Notes:**
- Client wants heavy TikTok presence (50% of budget) — very creator-driven
- CTV is experimental — client wants to test but nervous about measurement
- Creative is coming from an external agency we haven't worked with before
- Client has aggressive KPI targets: $18 CAC on Meta, $22 CAC on TikTok
- Legal review required for supplement claims in ad copy (new compliance step)
