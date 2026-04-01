# Task: Consolidate Blocking Charts into Maximizer-Ready Forecast

You are a forecasting assistant at a media agency. A Director needs to update the Maximizer system with current vendor spend forecasts for the upcoming monthly forecasting session.

## Instructions

1. Read the 3 blocking charts below — each has a different format, different vendors, and different date ranges
2. Read last month's Maximizer entries for this client (what's currently in the system)
3. Consolidate all blocking charts into a single monthly spend breakdown by vendor
4. Compare to last month's Maximizer entries and flag every change with the dollar delta
5. Identify anomalies that need investigation before entering into Maximizer

## Output

1. **Maximizer-Ready Table** — Monthly vendor spend for Apr–Jun 2026 (the forecast window)
2. **Change Log vs. Last Month's Forecast** — What moved, by how much, and which blocking chart it came from
3. **Anomaly Flags** — Anything that looks wrong, incomplete, or needs planner confirmation before entry
4. **Stale Data Warnings** — Any blocking chart that appears outdated based on dates or missing expected entries

---

## Blocking Chart A: VitalFit — Core Digital (Updated March 28, 2026)

**Prepared by:** Jordan (Planner)
**Format:** Monthly spend by vendor

| Vendor | Jan | Feb | Mar | Apr | May | Jun | Jul-Dec | Total |
|--------|-----|-----|-----|-----|-----|-----|---------|-------|
| Meta | $18,000 | $20,000 | $22,000 | $25,000 | $28,000 | $25,000 | Hold | $138,000 |
| Google Search | $12,000 | $14,000 | $15,000 | $16,000 | $18,000 | $16,000 | Hold | $91,000 |
| Google Shopping | $8,000 | $8,000 | $8,000 | $9,000 | $10,000 | $9,000 | Hold | $52,000 |
| Google PMAX | $10,000 | $12,000 | $13,000 | $14,000 | $14,000 | $12,000 | Hold | $75,000 |

Notes: "Apr-Jun reflects spring push. Jul-Dec TBD pending H2 planning."

---

## Blocking Chart B: VitalFit — TikTok & Social (Updated March 15, 2026)

**Prepared by:** Anika (Insights) — *Note: this chart is 2 weeks old*
**Format:** Flight-based with daily rates

| Campaign | Vendor | Flight Start | Flight End | Daily Rate | Est. Total |
|----------|--------|-------------|-----------|-----------|------------|
| VF Spring Creators | TikTok | Mar 1 | May 31 | $650 | $59,150 |
| VF Spring Spark Ads | TikTok | Mar 1 | Apr 30 | $420 | $25,620 |
| VF Influencer Seeding | Creator Network (Grin) | Apr 1 | Jun 30 | $200 | $18,200 |
| VF Pinterest Test | Pinterest | Apr 15 | Jun 30 | $150 | $11,550 |
| VF Reddit Community | Reddit | May 1 | Jun 30 | $100 | $6,100 |

Notes: "TikTok rates may increase in May per managed service renegotiation. Pinterest and Reddit are test-and-learn — may not proceed if Q1 performance review says no."

---

## Blocking Chart C: VitalFit — Connected TV & Programmatic (Updated March 25, 2026)

**Prepared by:** Marcus (Programmatic Lead)
**Format:** Quarterly totals with monthly split percentages

| Vendor | Q1 Total | Q2 Total | Q2 Monthly Split | Notes |
|--------|----------|----------|-----------------|-------|
| SparkPoint Media (CTV) | $30,000 | $50,000 | Apr 30% / May 35% / Jun 35% | "Increasing per strong Q1 brand lift results" |
| ReachMax Digital (Programmatic) | $25,000 | $30,000 | Apr 35% / May 35% / Jun 30% | "Shifting to native-heavy mix in Q2" |
| The Trade Desk (Self-Serve) | $0 | $15,000 | Apr 20% / May 40% / Jun 40% | "NEW — client wants to test self-serve programmatic" |
| Vistar Media (DOOH) | $0 | $12,000 | Apr 0% / May 50% / Jun 50% | "Pending final approval — gym network OOH" |

---

## Last Month's Maximizer Entries (Entered Feb 28, 2026)

These are the numbers currently in the system for VitalFit. The forecast window you're updating is April–June 2026.

| Vendor | Apr (Current) | May (Current) | Jun (Current) | Last Updated By |
|--------|--------------|--------------|--------------|----------------|
| Meta | $22,000 | $25,000 | $22,000 | Jordan |
| Google Search | $15,000 | $16,000 | $15,000 | Jordan |
| Google Shopping | $8,000 | $9,000 | $8,000 | Jordan |
| Google PMAX | $12,000 | $13,000 | $12,000 | Jordan |
| TikTok | $18,000 | $18,000 | $15,000 | Anika |
| SparkPoint Media (CTV) | $10,000 | $10,000 | $10,000 | Marcus |
| ReachMax Digital | $8,000 | $8,000 | $8,000 | Marcus |
| Creator Network (Grin) | $0 | $0 | $0 | — |
| Pinterest | $0 | $0 | $0 | — |
| Reddit | $0 | $0 | $0 | — |
| The Trade Desk | $0 | $0 | $0 | — |
| Vistar Media (DOOH) | $0 | $0 | $0 | — |
| **TOTAL** | **$93,000** | **$99,000** | **$90,000** | |

---

## What Makes This Tricky

- Blocking Chart B is 2 weeks old — TikTok spend may have already changed
- Chart B uses daily rates and flight dates — you need to calculate monthly breakdowns yourself
- Chart C uses quarterly totals with percentage splits — another conversion step
- New vendors (Pinterest, Reddit, The Trade Desk, Vistar/DOOH) appearing for first time — need to be added to Maximizer
- Vistar is "pending approval" — should it go in the forecast or not?
- The TikTok Spark Ads flight ends Apr 30 — does it renew or stop? Chart doesn't say.
- "Hold" in Chart A for Jul-Dec means no forecast data beyond June
- Some numbers in last month's Maximizer don't match current blocking charts even for past months — drift has occurred
