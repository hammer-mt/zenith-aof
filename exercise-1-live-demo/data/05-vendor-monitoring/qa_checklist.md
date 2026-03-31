# Vendor QA Checklist
## PixelPerfect Media — Q1 2026 Campaign Audit

**Audit Conducted By:** Lisa Park  
**Date:** March 21, 2026  
**Status:** IN PROGRESS

---

## 1. Budget & Financial Review

| Check | SOW | Reported | Match? | Notes |
|-------|-----|----------|--------|-------|
| Total Campaign Budget | $62,000 | $68,400 | ❌ NO | +$6,400 overage (10.3%) |
| Written approval for overage? | Required | Not found | ❌ NO | They claim "verbal approval Feb 12" |
| Media Spend (net) | $52,500 | $58,200 | ❌ NO | $5,700 over |
| Platform Fee (15%) | $7,875 | $8,730 | ⚠️ CHECK | Fee is 15% but of higher base |
| Verification Fees | $1,625 | $1,470 | ✅ YES | Actually under |

**Financial Discrepancy Total:** $6,400 over contracted amount

**Action Required:** 
- [ ] Locate written approval for overage (check email, Slack)
- [ ] If no written approval, escalate to Sarah

---

## 2. Deliverable Guarantees

| Metric | Guaranteed | Delivered | Met? |
|--------|------------|-----------|------|
| Total Impressions | 16,000,000 | 18,450,000 | ✅ YES |
| Viewability Rate | 70% | 68% | ❌ NO |
| Brand Safety Score | 98% | 99.2% | ✅ YES |
| Invalid Traffic (IVT) | <3% | 2.1% | ✅ YES |

**Deliverable Issues:**
- Viewability 2 points below guarantee (68% vs 70%)
- Impressions exceeded (but spent more to achieve)

---

## 3. Targeting Compliance

| Requirement | SOW | Wrap Report | Compliant? |
|-------------|-----|-------------|------------|
| Geography: US Only | Yes | Yes | ✅ YES |
| Priority: Retargeting first | Yes | Yes (13% + 6.5%) | ✅ YES |
| No political adjacency | Yes | Not mentioned | ⚠️ VERIFY |
| No MFA inventory | Yes | Not mentioned | ⚠️ VERIFY |
| No competitor conquesting | Yes | Not mentioned | ⚠️ VERIFY |

**Action Required:**
- [ ] Request brand safety detail report
- [ ] Verify no MFA sites in placement list

---

## 4. Device & Format Mix

| Spec | SOW | Delivered | Compliant? |
|------|-----|-----------|------------|
| Mobile | 55-65% | 60% | ✅ YES |
| Desktop | 30-40% | 30% | ✅ YES |
| Tablet | 5-10% | 10% | ✅ YES |
| Video | 0% | 0% | ✅ YES |

---

## 5. Reporting SLA Compliance

| Requirement | Met? | Notes |
|-------------|------|-------|
| Weekly reports Tuesdays by 12pm | ⚠️ PARTIAL | Week 4 delivered Wednesday |
| Monthly summaries | ✅ YES | |
| Wrap report within 7 days | ✅ YES | Due March 22, delivered March 20 |
| Issue response <4 hours | ✅ YES | No issues logged |

---

## 6. Invoice Line Item Verification

| Invoice Line | Amount | Expected | Match? |
|--------------|--------|----------|--------|
| Media Spend (net) | $58,200 | $52,500 | ❌ NO |
| Platform Fee (15%) | $8,730 | $7,875 | ❌ NO |
| Verification Fees | $1,470 | $1,625 | ✅ YES (under) |
| **Total** | **$68,400** | **$62,000** | ❌ NO |

---

## 7. Performance Cross-Check

### Impression Verification
| Source | Impressions |
|--------|-------------|
| Wrap Report | 18,450,000 |
| DoubleVerify (if available) | TBD |
| DSP Raw Data (if available) | TBD |

### Conversion Verification
| Source | Conversions |
|--------|-------------|
| Wrap Report | 892 |
| Lumina GA4 | 847 |
| **Discrepancy** | **45 (5.3%)** |

**Note:** 45 conversion discrepancy — wrap report shows more conversions than our GA4 tracking. May be attribution methodology difference but should clarify.

---

## 8. Red Flags Identified

### Critical
1. **$6,400 budget overage without written approval** — SOW explicitly requires written approval, they cite verbal call
2. **Viewability below guarantee** — 68% vs 70% guaranteed

### Moderate
3. **Conversion discrepancy** — 45 more conversions in their report vs our GA4
4. **Missing compliance documentation** — No detail on brand safety/MFA exclusions

### Minor
5. **Late report in week 4** — One day late, not pattern

---

## 9. Questions for PixelPerfect

1. Please provide written documentation of budget overage approval
2. Why did viewability fall below the 70% guarantee? What remediation?
3. Please provide site-level brand safety report
4. Please confirm no MFA inventory was included
5. Explain conversion tracking methodology and 45-unit discrepancy vs our GA4

---

## 10. Recommendation

**Based on this audit:**

- [ ] APPROVE invoice as-is
- [ ] APPROVE invoice with conditions
- [x] DISPUTE invoice — request remediation

**Proposed Resolution:**
1. Credit for viewability underperformance (~$1,200 estimated)
2. Written justification for overage or credit back to contracted amount
3. Satisfactory answers to brand safety questions before Q2 renewal

---

*Checklist template v2.1*
*Audit in progress — do not finalize until all items verified*
