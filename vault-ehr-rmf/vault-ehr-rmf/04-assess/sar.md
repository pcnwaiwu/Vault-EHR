# Security Assessment Report (SAR) — Vault EHR

**Document ID:** VLT-ASSESS-002  
**Version:** 1.0  
**Date:** 2026-07-21  
**Assessor:** [3PAO Organization Name]  
**Assessment Period:** 2026-06-01 through 2026-07-21

---

## 1. Executive Summary

The 3PAO conducted an independent security assessment of Vault EHR from June 1 through July 21, 2026. The assessment covered 45 controls from the NIST SP 800-53 Rev 5 HIGH baseline as documented in the System Security Plan.

### Overall Assessment Result

**CONDITIONAL — Recommend Conditional ATO with POA&M commitments**

| Finding Severity | Count |
|-----------------|-------|
| Critical | 0 |
| High | 1 |
| Moderate | 2 |
| Low | 3 |
| Informational | 4 |

No critical findings were identified. One high-severity finding (MFA gap for privileged accounts) and two moderate findings (audit log retention and patch SLA compliance) require POA&M remediation within agreed timelines before the AO should consider full ATO.

---

## 2. Assessment Coverage

| Control Family | Controls Assessed | Satisfied | Partially Satisfied | Not Satisfied |
|---------------|-----------------|-----------|--------------------|----|
| AC | 12 | 10 | 2 | 0 |
| AU | 8 | 6 | 1 | 1 |
| IA | 6 | 5 | 1 | 0 |
| SC | 7 | 7 | 0 | 0 |
| SI | 5 | 3 | 1 | 1 |
| IR | 4 | 4 | 0 | 0 |
| CP | 3 | 3 | 0 | 0 |

---

## 3. Findings Summary

| Finding ID | Severity | Control | Title | Status |
|-----------|---------|---------|-------|--------|
| FIND-001 | High | IA-2(1) | MFA not enforced for all privileged accounts | Open |
| FIND-002 | Moderate | AU-11 | Audit log retention gap (Splunk 1yr vs 7yr HIPAA) | Open |
| FIND-003 | Moderate | SI-2 | Patch SLA non-compliance for Critical vulnerabilities | Open |
| FIND-004 | Low | AC-2 | Orphaned accounts found in quarterly review | Remediated |
| FIND-005 | Low | SC-8 | Two legacy API endpoints still accept TLS 1.2 | Open |
| FIND-006 | Low | AU-2 | Bulk data export events not captured in audit log | Open |

---

## 4. Detailed Findings

See individual finding documents in `04-assess/findings/`.

---

## 5. Assessor Recommendation

The 3PAO recommends a **Conditional Authority to Operate** with the following conditions:

1. FIND-001 remediated or accepted with compensating controls within 60 days
2. FIND-002 remediation plan with funding approved within 30 days
3. FIND-003 patch cadence improved to meet SLA within 90 days

All findings must be tracked in an approved POA&M reviewed monthly by the ISSO and quarterly by the ISSM and AO.

---

## 6. Assessor Signature

| Role | Name | Date |
|------|------|------|
| Lead Assessor | [3PAO Lead Name] | 2026-07-21 |
| 3PAO Organization | [Organization] | 2026-07-21 |
