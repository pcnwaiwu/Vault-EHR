# AUTHORITY TO OPERATE (ATO) PACKAGE
## Vault Electronic Health Record (Vault EHR)

**Document ID:** VLT-ATO-MASTER
**Version:** 1.0
**Date:** 15 June 2026
**Classification:** UNCLASSIFIED // FOR OFFICIAL USE ONLY (FOUO)
**Framework:** NIST SP 800-37 Rev 2 — Risk Management Framework

---

## PART 1 — ATO COVER SHEET

| Field | Value |
|---|---|
| **Document ID** | VLT-AUTH-002 |
| **System Name** | Vault Electronic Health Record (Vault EHR) |
| **System Identifier** | VLT-EHR-001 |
| **System Type** | Hybrid Electronic Healthcare Management System |
| **Classification** | UNCLASSIFIED // FOR OFFICIAL USE ONLY (FOUO) |
| **FIPS 199 Impact Level** | HIGH |
| **Authorization Boundary** | On-premises RHEL 9 nodes (VLAN 20) + AWS GovCloud (us-gov-west-1) + clinical systems within signed ISAs |
| **Authorization Type** | Conditional Authority to Operate (C-ATO) |
| **Recommended Decision** | CONDITIONAL ATO — GRANTED |
| **ATO Period** | 3 years from date of AO signature |
| **ATO Expiration** | [AO signature date + 3 years] |

### Package Index

| Document | File Reference | Version | Date |
|---|---|---|---|
| System Security Plan (SSP) | `03-implement/ssp.md` | 1.0 | 2026-05-06 |
| FIPS 199 Categorization | `01-categorize/fips-199-categorization.md` | 1.0 | 2026-05-06 |
| Control Baseline | `02-select/control-baseline.md` | 1.0 | 2026-05-06 |
| Security Assessment Plan (SAP) | `04-assess/sap.md` | 1.0 | 2026-05-06 |
| Security Assessment Report (SAR) | `04-assess/sar.md` | 1.0 | 2026-07-21 |
| Plan of Action and Milestones (POA&M) | `05-authorize/poam.md` | 1.0 | 2026-07-21 |
| Risk Register | `05-authorize/risk-register.md` | 1.0 | 2026-06-15 |
| Risk Acceptance Memo | `05-authorize/risk-acceptance-memo.md` | 1.0 | TBD |
| Continuous Monitoring Strategy | `06-monitor/conmon-strategy.md` | 1.0 | 2026-05-06 |

### Authorization Conditions

1. POA&M-001 (MFA gap) fully remediated within **60 days** of AO signature
2. POA&M-002 (log retention) funded and in active remediation within **30 days**
3. POA&M-003 (patch SLA) improved to meet SLA targets within **90 days**

### Authorizing Official Signature Block

| Role | Name | Signature | Date |
|---|---|---|---|
| Authorizing Official (CIO) | _________________ | _________________ | _________________ |
| ISSM | _________________ | _________________ | _________________ |
| System Owner (CMIO) | _________________ | _________________ | _________________ |

---

## PART 2 — SYSTEM SECURITY PLAN (SSP)

**Document ID:** VLT-IMPL-001 | **Reference:** NIST SP 800-18 Rev 1

### 2.1 System Identification

| Field | Value |
|---|---|
| **System Name** | Vault Electronic Health Record |
| **Abbreviation** | Vault EHR |
| **System Identifier** | VLT-EHR-001 |
| **System Owner** | Chief Medical Information Officer |
| **ISSO** | Sr. Information Security Analyst |
| **ISSM** | Information Security Manager |
| **Authorizing Official** | Chief Information Officer |
| **Privacy Officer** | Chief Privacy Officer |

### 2.2 System Description and Mission

Vault EHR is a hybrid Electronic Healthcare Management System that allows healthcare providers to manage patient records, appointments, billing, and clinical documentation within a secure, centralised platform. Its mission is to support patient registration, enable appointment scheduling, maintain EHRs, facilitate billing and insurance coordination, support clinical documentation, generate compliance reports, and maintain audit logs.

### 2.3 System Users

| Role | Access Description |
|---|---|
| Patients | Personal health records and appointment visibility |
| Doctors | View and update patient records and treatment notes |
| Nurses | Access and update patient care information |
| Administrative Staff | Scheduling and patient registration |
| Billing Staff | Financial data only; no clinical notes access |
| System Administrators | System configuration; PHI blocked at application layer |
| Security Team | Security monitoring and incident response |

### 2.4 System Environment

- **On-premises:** 3 RHEL 9 application server nodes; 1 PostgreSQL 15 database server; VLAN 20
- **Cloud:** AWS GovCloud (us-gov-west-1) — EC2, RDS PostgreSQL (Multi-AZ, encrypted), S3, CloudTrail, WAF, ALB
- **Connectivity:** AWS Direct Connect (1Gbps) with IPSec overlay
- **OS:** RHEL 9 (on-premises), Amazon Linux 2023 (EC2)

### 2.5 Data Handled

| Data Type | Sensitivity | Regulatory Driver |
|---|---|---|
| Protected Health Information (PHI) | HIGH | HIPAA Security Rule |
| Personally Identifiable Information (PII) | HIGH | HIPAA / Privacy Act |
| Billing and Insurance Data | HIGH | HIPAA / False Claims Act |
| Treatment Notes / Clinical Documentation | HIGH | HIPAA |
| Appointment / Scheduling Data | MODERATE | HIPAA |
| System Audit Logs | MODERATE | HIPAA / NIST |
| Authentication Data | HIGH | NIST SP 800-53 |

### 2.6 Authorization Boundary

The boundary encompasses all hardware, software, and communications within the on-premises VLAN 20 segment, the full AWS GovCloud tenant, and all interconnected clinical systems covered by signed ISAs. Physical and personnel controls for the data centre are inherited from the organisation's common control provider.

### 2.7 Applicable Laws and Regulations

- HIPAA Security Rule (45 CFR Part 164)
- HITECH Act
- NIST SP 800-53 Rev 5
- FIPS 199 / FIPS 200
- NIST SP 800-37 Rev 2
- NIST SP 800-30 Rev 1
- GDPR (where applicable to EU data subjects)

### 2.8 Key Security Control Implementations

#### AC-2 — Account Management (Implemented)

All accounts provisioned through ITSM with manager approval. Reviewed every 90 days; disabled within 24 hours of termination; removed within 30 days. Shared accounts prohibited. Privileged accounts require separate credentials. All lifecycle events generate automated ISSO alerts.

#### AC-3 — Access Enforcement (Implemented)

RBAC enforced at the application layer. Clinical staff limited to patients in their care team; billing staff access financial data only; administrators have no PHI access at the application layer. Access decisions logged and reviewed monthly via SIEM.

#### AU-2 — Event Logging (Implemented)

Events logged: login/logout, failed authentication, PHI access/modification/deletion, admin actions, privilege escalation, system errors, configuration changes. Logs shipped to CloudWatch in real time; forwarded to Splunk within 60 seconds. Integrity protected via CloudTrail with S3 object lock (WORM).

#### IA-2 — Identification and Authentication (Implemented — finding open)

All users authenticate via Azure AD federated SSO (SAML 2.0). MFA required for all accounts; privileged accounts use TOTP. Password policy: minimum 14 characters, 90-day rotation for privileged accounts. Session timeout: 15 minutes (standard), 5 minutes (privileged). Five consecutive failures trigger 30-minute lockout with ISSO alert. **Note:** Three legacy admin accounts carry an MFA policy exclusion — see FIND-001.

#### SC-8 — Transmission Confidentiality and Integrity (Implemented)

All external communications use TLS 1.3 minimum; TLS 1.0/1.1 disabled. Internal API calls use mutual TLS (mTLS). PHI to external partners uses TLS 1.3 with certificate pinning. VPN uses IKEv2/IPSec with AES-256-GCM. Certificates managed via AWS Certificate Manager with automatic rotation. **Note:** Two legacy internal endpoints still accept TLS 1.2 — see FIND-005.

#### SC-28 — Protection of Information at Rest (Implemented)

All PHI encrypted at rest with AES-256 on RDS PostgreSQL (Multi-AZ). S3 buckets use server-side encryption. On-premises storage uses encrypted RHEL 9 volumes.

#### SI-2 — Flaw Remediation (In Progress — finding open)

Weekly unauthenticated and monthly authenticated Tenable Nessus scans. Patch SLAs: Critical = 15 days, High = 30 days, Medium/Low = 90 days. Patches applied via Ansible; tested in staging before production. Emergency patches within 72 hours with ISSO approval. **Note:** Three Critical CVEs exceeded SLA due to absence of production-mirroring staging — see FIND-003.

#### CP-9 — System Backup (Implemented)

Automated daily backups of RDS and application data to S3. Daily backup success/failure alerts. Quarterly restore tests documented.

### 2.9 Control Summary Table

| Control | Name | Status | Open Finding |
|---|---|---|---|
| AC-2 | Account Management | Implemented | None |
| AC-3 | Access Enforcement | Implemented | None |
| AC-7 | Unsuccessful Login Attempts | Implemented | None |
| AC-17 | Remote Access | Implemented | None |
| AU-2 | Event Logging | Implemented | FIND-006 (partial) |
| AU-9 | Audit Log Protection | Implemented | None |
| AU-11 | Audit Record Retention | In Progress | FIND-002 |
| CP-9 | System Backup | Implemented | None |
| IA-2 | Identification and Authentication | Implemented | FIND-001 (partial) |
| IA-5 | Authenticator Management | Implemented | None |
| IR-6 | Incident Reporting | Implemented | None |
| PE-1 to PE-20 | Physical Protection | Inherited | None |
| PS-1 to PS-8 | Personnel Security | Inherited | None |
| RA-5 | Vulnerability Monitoring | Implemented | None |
| SC-8 | Transmission Confidentiality | Implemented | FIND-005 (partial) |
| SC-28 | Protection of Info at Rest | Implemented | None |
| SI-2 | Flaw Remediation | In Progress | FIND-003 |
| SI-3 | Malicious Code Protection | Implemented | None |

---

## PART 3 — FIPS 199 SECURITY CATEGORIZATION

**Document ID:** VLT-CAT-001 | **Reference:** FIPS 199; NIST SP 800-60 Vol. 2

| Information Type | Confidentiality | Integrity | Availability |
|---|---|---|---|
| Health Records (C.3.1.1) | HIGH | HIGH | MODERATE |
| Billing and Insurance (C.3.1.2) | HIGH | HIGH | MODERATE |
| Appointment and Scheduling (C.3.1.3) | MODERATE | HIGH | HIGH |
| System Audit Logs (C.3.1.4) | MODERATE | HIGH | LOW |

**System Security Category (high-water mark):**

> **SC Vault EHR = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}**
>
> **Overall System Impact Level: HIGH**

This mandates the **NIST SP 800-53 Rev 5 HIGH baseline** for control selection.

---

## PART 4 — CONTROL BASELINE SUMMARY

**Document ID:** VLT-SEL-001 | **Baseline:** NIST SP 800-53 Rev 5 HIGH Impact

### Priority Controls (Healthcare / PHI Focus)

| Control | Name | Priority Rationale |
|---|---|---|
| AC-2 | Account Management | PHI access must be strictly controlled |
| AC-3 | Access Enforcement | Role-based access to patient data |
| AC-17 | Remote Access | Clinician remote access is common |
| AU-2 | Event Logging | HIPAA audit trail requirement |
| AU-9 | Protection of Audit Information | Prevent log tampering |
| IA-2 | Identification and Authentication | MFA for all privileged users |
| IA-5 | Authenticator Management | Password and token lifecycle |
| SC-8 | Transmission Confidentiality | PHI in transit protection |
| SC-28 | Protection of Info at Rest | PHI at rest encryption |
| SI-2 | Flaw Remediation | Patch management for healthcare |
| IR-6 | Incident Reporting | HIPAA breach notification |
| CP-9 | System Backup | Data recovery for patient records |
| RA-5 | Vulnerability Monitoring | Regular scanning |

### Inherited Controls

| Control Family | Inherited From |
|---|---|
| PE-1 through PE-20 (Physical Protection) | Facilities / Data Centre |
| PS-1 through PS-8 (Personnel Security) | HR / Personnel Security |
| IA-8 (Federated Identity via Azure AD) | Microsoft / IT Infrastructure |
| AT-1 through AT-3 (Security Awareness) | IT Security Training Programme |

---

## PART 5 — SECURITY ASSESSMENT REPORT (SAR) SUMMARY

**Document ID:** VLT-ASSESS-002
**Assessment Period:** 1 June – 21 July 2026
**Assessor:** Independent 3PAO
**Overall Result:** CONDITIONAL — Recommend Conditional ATO with POA&M commitments

45 controls assessed across the NIST SP 800-53 Rev 5 HIGH baseline.

| Severity | Count |
|---|---|
| Critical | 0 |
| High | 1 |
| Moderate | 2 |
| Low | 3 |
| Informational | 4 |

### Findings Summary

| Finding ID | Severity | Control | Title | Status |
|---|---|---|---|---|
| FIND-001 | **High** | IA-2(1) | MFA not enforced for all privileged accounts | Open |
| FIND-002 | **Moderate** | AU-11 | Audit log retention gap (Splunk 1yr vs 7yr HIPAA) | Open |
| FIND-003 | **Moderate** | SI-2 | Patch SLA non-compliance for Critical vulnerabilities | Open |
| FIND-004 | Low | AC-2 | Orphaned accounts found in quarterly review | **Remediated** |
| FIND-005 | Low | SC-8 | Two legacy API endpoints still accept TLS 1.2 | Open |
| FIND-006 | Low | AU-2 | Bulk data export events not captured in audit log | Open |

### Assessment Coverage

| Family | Assessed | Satisfied | Partially Satisfied | Not Satisfied |
|---|---|---|---|---|
| AC | 12 | 10 | 2 | 0 |
| AU | 8 | 6 | 1 | 1 |
| IA | 6 | 5 | 1 | 0 |
| SC | 7 | 7 | 0 | 0 |
| SI | 5 | 3 | 1 | 1 |
| IR | 4 | 4 | 0 | 0 |
| CP | 3 | 3 | 0 | 0 |

**3PAO Recommendation:** Conditional ATO with FIND-001 remediated within 60 days; FIND-002 funding approved within 30 days; FIND-003 patch cadence improved within 90 days.

---

## PART 6 — RISK REGISTER

**Document ID:** VLT-AUTH-004
**Owner:** ISSO | **Review:** Monthly (ISSO), Quarterly (ISSM + AO)

### Risk Scoring Matrix (NIST SP 800-30 Rev 1)

| Likelihood / Impact | LOW | MODERATE | HIGH |
|---|---|---|---|
| HIGH | Moderate | High | Critical |
| MODERATE | Low | Moderate | High |
| LOW | Low | Low | Moderate |

### Risk Register

| Risk ID | Title | Inherent Risk | Compensating Controls | Residual Risk | Status |
|---|---|---|---|---|---|
| RISK-001 | MFA gap — 3 privileged admin accounts | **Critical** | IP-restricted jump host; SIEM session monitoring | **Moderate** | Open |
| RISK-002 | Audit log retention gap (1yr vs 7yr HIPAA) | Moderate | S3 Glacier raw logs (7yr); manual retrieval documented | Low | In Remediation |
| RISK-003 | Patch SLA non-compliance for Critical CVEs | High | WAF virtual patching; network ACLs; service isolation | Low | Open |
| RISK-004 | Orphaned accounts found in access review | Low | N/A — Finding closed | Low | **Remediated** |
| RISK-005 | Two legacy API endpoints accept TLS 1.2 | Low | Traffic limited to internal segments; TLS inspection at perimeter | Low | Open |
| RISK-006 | Bulk export events not captured in audit log | Moderate | DLP alerts at perimeter; SIEM anomaly detection | Low | Open |

**Overall System Residual Risk: MODERATE** (driven by RISK-001)

---

## PART 7 — PLAN OF ACTION AND MILESTONES (POA&M)

**Document ID:** VLT-AUTH-001 | **Review:** Monthly (ISSO), Quarterly (ISSM + AO)

| ID | Finding | Control | Severity | Responsible | Due Date | Status |
|---|---|---|---|---|---|---|
| POA-001 | MFA not enforced for all privileged accounts | IA-2(1) | **High** | IT Operations / ISSO | 2026-08-21 | Open |
| POA-002 | Audit log retention gap | AU-11 | Moderate | Cloud Ops / ISSO | 2026-10-21 | In Remediation |
| POA-003 | Patch SLA non-compliance for Critical CVEs | SI-2 | Moderate | IT Operations | 2026-09-01 | Open |

### POA-001 Milestones — MFA Gap

| Milestone | Target Date |
|---|---|
| Remove MFA exclusion from legacy Conditional Access policy | 2026-07-28 |
| Force MFA enrollment for all admin accounts | 2026-08-01 |
| Implement certificate-based authentication for service accounts | 2026-08-15 |
| ISSO verification and evidence collection | 2026-08-21 |

**Resources:** 8 hours IT Operations labour; no additional cost.
**Compensating Control:** Admin accounts restricted to dedicated jump host with IP allowlisting.

### POA-002 Milestones — Log Retention

| Milestone | Target Date |
|---|---|
| Budget request submitted for Splunk SmartStore | 2026-07-28 |
| Vendor quote received and approved | 2026-08-15 |
| Splunk SmartStore implemented and tested | 2026-10-01 |
| 7-year retention verified with test queries | 2026-10-21 |

**Resources:** $4,000/year (SmartStore S3 backend) + 40 hours Cloud Ops labour.
**Compensating Control:** Raw logs retained 7 years in S3 Glacier; manual retrieval process documented.

### POA-003 Milestones — Patch SLA

| Milestone | Target Date |
|---|---|
| Formal patch exception process documented | 2026-08-01 |
| Staging environment updated to mirror production | 2026-08-15 |
| Patch SLA compliance tracked in monthly metrics | 2026-09-01 |

**Resources:** 20 hours IT Operations labour.
**Compensating Control:** WAF virtual patching applied immediately upon CVE identification; network ACLs restrict exposure.

---

## PART 8 — RISK ACCEPTANCE MEMO

**Document ID:** VLT-AUTH-003
**From:** ISSM | **To:** Authorizing Official (CIO)
**Subject:** Residual Risk Acceptance — Vault EHR Conditional ATO

The ISSM recommends the AO grant a Conditional ATO with the POA&M remediation requirements stated above. Vault EHR provides critical healthcare services; denial of operation would significantly impair patient care. The identified findings do not represent an imminent threat of PHI breach given the compensating controls in place, and all have clear, funded remediation paths.

### Residual Risk Summary

| Finding | Severity | Compensating Control | Residual Risk |
|---|---|---|---|
| FIND-001: MFA gap (3 admin accounts) | High | IP-restricted jump host; session monitoring | Moderate |
| FIND-002: Splunk log retention (1yr vs 7yr) | Moderate | S3 Glacier raw logs; manual retrieval | Low |
| FIND-003: Patch SLA delay (3 CVEs) | Moderate | WAF virtual patching; network ACLs | Low |

**Overall Residual Risk: MODERATE**

### Signatures

| Role | Name | Signature | Date |
|---|---|---|---|
| ISSM | _________________ | _________________ | _________________ |
| ISSO | _________________ | _________________ | _________________ |
| AO (CIO) | _________________ | _________________ | _________________ |

---

## PART 9 — CONTINUOUS MONITORING STRATEGY

**Document ID:** VLT-MON-001 | **Reference:** NIST SP 800-137

### Monitoring Activities

| Control Area | Method | Frequency | Owner |
|---|---|---|---|
| Access controls | Automated account review scripts; SIEM dashboards | Monthly | ISSO |
| Audit logging | SIEM alert rules; log completeness checks | Daily | ISSO |
| Vulnerability management | Tenable Nessus (unauthenticated weekly; authenticated monthly) | Weekly / Monthly | IT Ops |
| Configuration management | AWS Config rules; CIS benchmark scans | Weekly | Cloud Ops |
| Patch compliance | Monthly patch status reports | Monthly | IT Ops |
| Backup and recovery | Backup alerts (daily); restore tests (quarterly) | Daily / Quarterly | Cloud Ops |
| PHI access outside business hours | Real-time SIEM alerting | Real-time | ISSO |

### Security Metrics Reported to ISSM / AO

| Metric | Target | Frequency |
|---|---|---|
| Critical patch SLA compliance | >= 95% | Monthly |
| Open High/Critical POA&M items past due | 0 | Monthly |
| MFA enrollment rate | 100% | Monthly |
| Mean time to detect incidents | <= 1 hour | Quarterly |
| Mean time to respond to incidents | <= 4 hours | Quarterly |
| Failed login anomalous spikes | < 50/day average | Weekly |

### Annual Requirements

- Annual penetration test (external and internal scoped)
- Annual risk assessment update (threat landscape and risk ratings)
- Annual POA&M review (close completed items with evidence)
- Full control re-assessment every 3 years at ATO renewal

### Significant Change Triggers

Any of the following require ISSO review before implementation and may trigger an updated SSP or AO notification:

- New system interconnections or data flows
- Changes to authentication mechanisms
- New third-party software integrations
- Changes to encryption configurations
- Cloud region additions or major infrastructure changes
- Changes to backup or logging configurations

---

## PART 10 — AUTHORIZATION DECISION

**System:** Vault Electronic Health Record (VLT-EHR-001)

> ### DECISION: CONDITIONAL AUTHORITY TO OPERATE (C-ATO) — RECOMMENDED FOR GRANT

| Field | Value |
|---|---|
| **Basis** | SAR VLT-ASSESS-002; Risk Register VLT-AUTH-004; POA&M VLT-AUTH-001; Risk Acceptance Memo VLT-AUTH-003; SSP VLT-IMPL-001 |
| **ATO Duration** | 3 years from AO signature date |
| **Residual Risk Accepted** | MODERATE — driven by RISK-001 MFA gap, mitigated by compensating controls |

### Conditions of Authorization

1. POA&M-001 (MFA gap) fully remediated and evidence submitted to ISSO within **60 days** of AO signature
2. POA&M-002 (log retention) funding approved and implementation begun within **30 days**
3. POA&M-003 (patch SLA) process improvements in place within **90 days**
4. Monthly POA&M reviews by ISSO; quarterly reviews by ISSM and AO throughout the ATO period
5. Any significant change to the system boundary or security posture reported to the AO within 5 business days
6. Annual penetration test and risk assessment update completed and reported to the AO

> If any condition is unmet on schedule, the ISSM must notify the AO within 5 business days and present a revised remediation timeline. The AO reserves the right to revoke the C-ATO if residual risk materially increases.

### AO Signature

| Role | Name | Signature | Date |
|---|---|---|---|
| Authorizing Official (CIO) | _________________ | _________________ | _________________ |

---

## DOCUMENT CONTROL

| Field | Value |
|---|---|
| **Author** | Vault EHR Security Team |
| **Created** | 2026-06-15 |
| **Last Updated** | 2026-06-15 |
| **Next Review** | 2026-09-15 (quarterly) |
| **Version** | 1.0 |

---

> **DISCLAIMER:** Vault EHR is a fictional system created solely for educational and portfolio demonstration purposes. All data, scenarios, and documentation are simulated and do not represent any real organisation, system, or individual. Classification marking UNCLASSIFIED // FOUO is applied for realism only.
