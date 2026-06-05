# Risk Management Strategy — Vault EHR

**Document ID:** VLT-PREP-003  
**Version:** 1.0  
**Date:** 2026-05-06

---

## 1. Purpose

This document establishes the risk management strategy for Vault EHR. It defines how risk is identified, assessed, communicated, and accepted across the RMF lifecycle.

---

## 2. Risk Tolerance

The organization has a **LOW risk tolerance** for:
- Unauthorized disclosure of PHI or PII
- Loss of integrity of clinical records (patient safety risk)
- Prolonged unavailability of the system (> 4 hours RTO)

The organization has a **MODERATE risk tolerance** for:
- Non-production environment outages
- Low-severity configuration findings with compensating controls

---

## 3. Risk Assessment Approach

Risks are assessed using a likelihood × impact matrix aligned to NIST SP 800-30 Rev 1.

| Likelihood \ Impact | LOW | MODERATE | HIGH |
|--------------------|-----|----------|------|
| HIGH | Moderate | High | Critical |
| MODERATE | Low | Moderate | High |
| LOW | Low | Low | Moderate |

### Risk Rating Definitions

| Rating | Action Required |
|--------|----------------|
| Critical | Immediate remediation required; may block ATO |
| High | Remediate within 30 days; ISSM notification required |
| Moderate | Remediate within 90 days; tracked in POA&M |
| Low | Remediate within 180 days or accept risk |

---

## 4. Risk Response Options

| Response | Description | When Used |
|----------|-------------|-----------|
| Mitigate | Implement controls to reduce likelihood or impact | Default response for High/Critical |
| Accept | AO formally accepts residual risk | Low/Moderate with compensating controls |
| Transfer | Contractually transfer risk (e.g., cyber insurance) | Third-party data processing risks |
| Avoid | Discontinue the risky activity | When risk exceeds mission benefit |

---

## 5. Risk Communication

- **Monthly:** ISSO reports control status to ISSM
- **Quarterly:** ISSM briefs AO on risk posture and POA&M status
- **Immediately:** Critical findings reported to ISSM and AO within 1 business day
- **Annually:** Full risk re-assessment prior to ATO renewal

---

## 6. Continuous Monitoring Strategy

See `06-monitor/conmon-strategy.md` for full continuous monitoring plan. Summary:

- Vulnerability scans: Weekly (automated), Monthly (authenticated)
- Log review: Daily (SIEM alerts), Weekly (manual sampling)
- Control testing: Annually (full), Ongoing (automated checks)
- POA&M review: Monthly
