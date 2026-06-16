# Risk Register — Vault EHR

**Document ID:** VLT-AUTH-004
**Version:** 1.0
**Date:** 2026-06-15
**Last Updated:** 2026-06-15
**Owner:** ISSO
**Review Frequency:** Monthly (ISSO), Quarterly (ISSM + AO)
**Classification:** UNCLASSIFIED // FOR OFFICIAL USE ONLY (FOUO)

---

## 1. Purpose

This Risk Register provides a centralized, living record of all identified security risks for the Vault Electronic Health Record (Vault EHR) system. It consolidates findings from the Security Assessment Report (SAR), tracks remediation via the Plan of Action and Milestones (POA&M), and documents residual risk acceptance decisions made by the Authorizing Official (AO). This document is maintained in alignment with NIST SP 800-37 Rev 2 and NIST SP 800-30 Rev 1.

---

## 2. System Information

| Field | Value |
|---|---|
| System Name | Vault Electronic Health Record (Vault EHR) |
| System Type | Hybrid Electronic Healthcare Management System |
| FIPS 199 Impact Level | HIGH |
| Data Types | PHI, PII, Clinical Records, Billing Data |
| RMF Status | Conditional ATO — Pending AO Signature |
| Overall Residual Risk | MODERATE |
| ISSO | [ISSO Name] |
| ISSM | [ISSM Name] |
| Authorizing Official | [AO Name / CIO] |

---

## 3. Risk Scoring Methodology

Risks are scored using a **Likelihood x Impact** matrix aligned to NIST SP 800-30 Rev 1.

| Likelihood / Impact | LOW | MODERATE | HIGH |
|---|---|---|---|
| **HIGH** | Moderate | High | Critical |
| **MODERATE** | Low | Moderate | High |
| **LOW** | Low | Low | Moderate |

### Risk Rating Definitions

| Rating | Action Required |
|---|---|
| Critical | Immediate remediation required; may block ATO |
| High | Remediate within 30 days; ISSM notification required |
| Moderate | Remediate within 90 days; tracked in POA&M |
| Low | Remediate within 180 days or accept risk |

---

## 4. Risk Register

### RISK-001 — MFA Not Enforced for All Privileged Accounts

| Field | Details |
|---|---|
| **Risk ID** | RISK-001 |
| **Finding Reference** | FIND-001 / POA-001 |
| **Date Identified** | 2026-07-21 |
| **NIST Control** | IA-2(1) — Identification and Authentication (Multi-Factor) |
| **Risk Title** | MFA not enforced for all privileged accounts |
| **Risk Description** | Three privileged administrator accounts are excluded from the Conditional Access MFA policy due to a legacy policy exemption. If compromised, an attacker could gain elevated access to PHI and system infrastructure without a second authentication factor. |
| **Threat Source** | External attacker; malicious insider |
| **Likelihood** | High |
| **Impact** | High |
| **Inherent Risk Rating** | **Critical** |
| **Risk Response** | Mitigate |
| **Compensating Controls** | Admin accounts restricted to dedicated jump host with IP allowlisting; session activity monitored via SIEM |
| **Residual Likelihood** | Moderate |
| **Residual Impact** | Moderate |
| **Residual Risk Rating** | **Moderate** |
| **Remediation Owner** | IT Operations / ISSO |
| **POA&M Item** | POA-001 |
| **Target Remediation Date** | 2026-08-21 |
| **Status** | Open |
| **AO Risk Acceptance** | Conditionally Accepted (pending remediation) |

**Remediation Milestones:**
- 2026-07-28 — Remove MFA exclusion from legacy Conditional Access policy
- 2026-08-01 — Force MFA enrollment for all admin accounts
- 2026-08-15 — Implement certificate-based authentication for service accounts
- 2026-08-21 — ISSO verification and evidence collection

---

### RISK-002 — Audit Log Retention Gap (Splunk 1yr vs HIPAA 7yr Requirement)

| Field | Details |
|---|---|
| **Risk ID** | RISK-002 |
| **Finding Reference** | FIND-002 / POA-002 |
| **Date Identified** | 2026-07-21 |
| **NIST Control** | AU-11 — Audit Record Retention |
| **Risk Title** | Audit log retention gap — Splunk retains 1 year vs HIPAA 7-year requirement |
| **Risk Description** | The current Splunk SIEM retains audit logs for only 1 year. HIPAA requires retention for a minimum of 6 years (45 CFR 164.312(b)), and organizational policy requires 7 years. This gap could impair investigation of historical incidents or demonstration of compliance during a HIPAA audit. |
| **Threat Source** | Compliance / Regulatory; Internal audit failure |
| **Likelihood** | Moderate |
| **Impact** | Moderate |
| **Inherent Risk Rating** | **Moderate** |
| **Risk Response** | Mitigate |
| **Compensating Controls** | Raw logs retained 7 years in AWS S3 Glacier; manual retrieval process documented and tested |
| **Residual Likelihood** | Low |
| **Residual Impact** | Low |
| **Residual Risk Rating** | **Low** |
| **Remediation Owner** | Cloud Ops / ISSO |
| **POA&M Item** | POA-002 |
| **Target Remediation Date** | 2026-10-21 |
| **Status** | In Remediation |
| **AO Risk Acceptance** | Conditionally Accepted (compensating control in place) |

**Remediation Milestones:**
- 2026-07-28 — Budget request submitted for Splunk SmartStore
- 2026-08-15 — Vendor quote received and approved
- 2026-10-01 — Splunk SmartStore implemented and tested
- 2026-10-21 — 7-year retention verified with test queries

**Estimated Cost:** $4,000/year (SmartStore S3 backend) + 40 hours Cloud Ops labor

---

### RISK-003 — Patch SLA Non-Compliance for Critical Vulnerabilities

| Field | Details |
|---|---|
| **Risk ID** | RISK-003 |
| **Finding Reference** | FIND-003 / POA-003 |
| **Date Identified** | 2026-07-21 |
| **NIST Control** | SI-2 — Flaw Remediation |
| **Risk Title** | Patch SLA non-compliance for Critical vulnerabilities |
| **Risk Description** | Three Critical CVEs exceeded the organization's 30-day patch SLA due to the absence of a staging environment mirroring production. Delayed patching increases the window of exposure to exploitation of known vulnerabilities, potentially leading to unauthorized access or data compromise. |
| **Threat Source** | External attacker exploiting known CVEs |
| **Likelihood** | Moderate |
| **Impact** | High |
| **Inherent Risk Rating** | **High** |
| **Risk Response** | Mitigate |
| **Compensating Controls** | WAF virtual patching applied immediately upon CVE identification; network ACLs restrict exposure; affected services isolated where feasible |
| **Residual Likelihood** | Low |
| **Residual Impact** | Moderate |
| **Residual Risk Rating** | **Low** |
| **Remediation Owner** | IT Operations |
| **POA&M Item** | POA-003 |
| **Target Remediation Date** | 2026-09-01 |
| **Status** | Open |
| **AO Risk Acceptance** | Conditionally Accepted (compensating control in place) |

**Remediation Milestones:**
- 2026-08-01 — Formal patch exception process documented
- 2026-08-15 — Staging environment updated to mirror production
- 2026-09-01 — Patch SLA compliance tracked in monthly metrics

---

### RISK-004 — Orphaned Accounts Found in Quarterly Review

| Field | Details |
|---|---|
| **Risk ID** | RISK-004 |
| **Finding Reference** | FIND-004 |
| **Date Identified** | 2026-07-21 |
| **NIST Control** | AC-2 — Account Management |
| **Risk Title** | Orphaned user accounts found during quarterly access review |
| **Risk Description** | Orphaned accounts belonging to former employees or contractors were identified during the quarterly access review. These accounts could be exploited to gain unauthorized access to the system and its data. |
| **Threat Source** | Malicious insider; unauthorized access |
| **Likelihood** | Low |
| **Impact** | Moderate |
| **Inherent Risk Rating** | **Low** |
| **Risk Response** | Mitigate |
| **Compensating Controls** | N/A — Finding remediated |
| **Residual Likelihood** | Low |
| **Residual Impact** | Low |
| **Residual Risk Rating** | **Low** |
| **Remediation Owner** | IT Operations / ISSO |
| **POA&M Item** | N/A |
| **Target Remediation Date** | N/A |
| **Status** | Remediated |
| **AO Risk Acceptance** | N/A — Closed |

---

### RISK-005 — Legacy API Endpoints Accept TLS 1.2

| Field | Details |
|---|---|
| **Risk ID** | RISK-005 |
| **Finding Reference** | FIND-005 |
| **Date Identified** | 2026-07-21 |
| **NIST Control** | SC-8 — Transmission Confidentiality and Integrity |
| **Risk Title** | Two legacy API endpoints still accept TLS 1.2 connections |
| **Risk Description** | Two internal API endpoints have not yet been upgraded to enforce TLS 1.3 exclusively. TLS 1.2 contains known weaknesses that could be exploited in a targeted network attack to intercept data in transit, including PHI. |
| **Threat Source** | Network-based attacker; man-in-the-middle |
| **Likelihood** | Low |
| **Impact** | Moderate |
| **Inherent Risk Rating** | **Low** |
| **Risk Response** | Mitigate |
| **Compensating Controls** | Traffic limited to internal network segments; TLS inspection enabled on perimeter |
| **Residual Likelihood** | Low |
| **Residual Impact** | Low |
| **Residual Risk Rating** | **Low** |
| **Remediation Owner** | IT Operations |
| **POA&M Item** | N/A (Low — tracked informally) |
| **Target Remediation Date** | 2026-12-31 |
| **Status** | Open |
| **AO Risk Acceptance** | Accepted — Low residual risk with compensating controls |

---

### RISK-006 — Bulk Data Export Events Not Captured in Audit Log

| Field | Details |
|---|---|
| **Risk ID** | RISK-006 |
| **Finding Reference** | FIND-006 |
| **Date Identified** | 2026-07-21 |
| **NIST Control** | AU-2 — Event Logging |
| **Risk Title** | Bulk data export events not captured in audit log |
| **Risk Description** | The audit logging configuration does not capture bulk data export events such as mass downloads of patient records. This visibility gap means unauthorized or anomalous data exfiltration activity involving PHI may go undetected, impacting both security monitoring and HIPAA audit trail requirements. |
| **Threat Source** | Malicious insider; data exfiltration |
| **Likelihood** | Low |
| **Impact** | High |
| **Inherent Risk Rating** | **Moderate** |
| **Risk Response** | Mitigate |
| **Compensating Controls** | DLP alerts configured for large file transfers at the network perimeter; SIEM anomaly detection rules partially cover bulk access patterns |
| **Residual Likelihood** | Low |
| **Residual Impact** | Moderate |
| **Residual Risk Rating** | **Low** |
| **Remediation Owner** | ISSO / Cloud Ops |
| **POA&M Item** | N/A (Low — tracked informally) |
| **Target Remediation Date** | 2026-12-31 |
| **Status** | Open |
| **AO Risk Acceptance** | Accepted — Low residual risk with compensating controls |

---

## 5. Risk Summary Dashboard

| Risk ID | Title | Inherent Risk | Residual Risk | Status |
|---|---|---|---|---|
| RISK-001 | MFA gap — privileged accounts | Critical | Moderate | Open |
| RISK-002 | Audit log retention gap | Moderate | Low | In Remediation |
| RISK-003 | Patch SLA non-compliance | High | Low | Open |
| RISK-004 | Orphaned accounts | Low | Low | Remediated |
| RISK-005 | Legacy API endpoints — TLS 1.2 | Low | Low | Open |
| RISK-006 | Bulk export not audited | Moderate | Low | Open |

**Overall System Residual Risk: MODERATE** (driven by RISK-001)

---

## 6. Risk Response Summary

| Response Type | Count | Risk IDs |
|---|---|---|
| Mitigate | 6 | RISK-001 through RISK-006 |
| Accept | 0 | N/A |
| Transfer | 0 | N/A |
| Avoid | 0 | N/A |

---

## 7. Update Log

| Date | Updated By | Summary |
|---|---|---|
| 2026-06-15 | ISSO | Initial risk register created, consolidating SAR findings (VLT-ASSESS-002) and POA&M (VLT-AUTH-001) |

---

## 8. Related Documents

| Document | ID | Location |
|---|---|---|
| Risk Management Strategy | VLT-PREP-003 | 00-prepare/risk-management-strategy.md |
| Security Assessment Report (SAR) | VLT-ASSESS-002 | 04-assess/sar.md |
| Plan of Action and Milestones (POA&M) | VLT-AUTH-001 | 05-authorize/poam.md |
| Risk Acceptance Memo | VLT-AUTH-003 | 05-authorize/risk-acceptance-memo.md |
| ATO Cover Sheet | VLT-AUTH-002 | 05-authorize/ato-package/ato-cover-sheet.md |

---

*This document is classified UNCLASSIFIED // FOR OFFICIAL USE ONLY (FOUO). Do not distribute outside authorized personnel. Do not commit real PHI, PII, private keys, or signed authorization letters to this repository.*
