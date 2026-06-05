# System Security Plan (SSP) — Vault EHR

**Document ID:** VLT-IMPL-001  
**Version:** 1.0  
**Date:** 2026-05-06  
**Classification:** UNCLASSIFIED // FOUO  
**Reference:** NIST SP 800-18 Rev 1

---

## Table of Contents

1. System Identification
2. System Categorization
3. System Owner and Contacts
4. Authorization Boundary
5. System Environment
6. System Interconnections
7. Laws and Regulations
8. Security Control Implementation
9. Control Summary Table

---

## 1. System Identification

| Field | Value |
|-------|-------|
| System Name | Vault Electronic Health Record |
| Abbreviation | Vault EHR |
| System Identifier | VLT-EHR-001 |
| Authorization Date | Pending |
| ATO Expiration | Pending (3-year cycle) |

---

## 2. System Categorization

**Overall Impact Level: HIGH**

| Objective | Level |
|-----------|-------|
| Confidentiality | HIGH |
| Integrity | HIGH |
| Availability | HIGH |

See `01-categorize/fips-199-categorization.md` for full categorization rationale.

---

## 3. System Owner and Contacts

| Role | Contact |
|------|---------|
| System Owner | Chief Medical Information Officer |
| ISSO | Sr. Information Security Analyst |
| ISSM | Information Security Manager |
| AO | Chief Information Officer |
| Privacy Officer | Chief Privacy Officer |

---

## 4. Authorization Boundary

The Vault EHR authorization boundary encompasses all hardware, software, and communications components described in `00-prepare/system-description.md`. The boundary includes on-premises application servers, the AWS GovCloud tenant, and all interconnected clinical systems within the signed ISAs.

---

## 5. System Environment

- **On-premises:** 3 application server nodes (RHEL 9), 1 internal database server (PostgreSQL 15), dedicated network segment (VLAN 20)
- **Cloud:** AWS GovCloud (us-gov-west-1) — EC2, RDS PostgreSQL, S3, CloudTrail, WAF, ALB
- **Connectivity:** AWS Direct Connect (1Gbps) + IPSec overlay for on-prem ↔ cloud
- **Operating System:** RHEL 9 (on-prem), Amazon Linux 2023 (EC2)
- **Database:** PostgreSQL 15 (RDS, Multi-AZ, encrypted)

---

## 6. System Interconnections

See `00-prepare/system-description.md` Section 6 for full interconnection table.

---

## 7. Laws and Regulations

- HIPAA Security Rule (45 CFR Part 164)
- HITECH Act
- NIST SP 800-53 Rev 5
- FIPS 199 / FIPS 200

---

## 8. Security Control Implementations

### AC-2 — Account Management

**Control Statement:** The organization manages information system accounts, including establishing, activating, modifying, reviewing, disabling, and removing accounts.

**Implementation:**
- All Vault EHR accounts are provisioned through the IT Service Management (ITSM) system with manager approval
- Accounts are reviewed every 90 days by the ISSO and department managers
- Accounts are disabled within 24 hours of termination and removed within 30 days
- Shared accounts are prohibited; service accounts require ISSO approval and are logged
- Privileged accounts (admin) require separate credentials from standard user accounts
- Account creation/modification/deletion generates an automated alert to the ISSO

**Responsible Entity:** IT Operations / ISSO  
**Implementation Status:** Implemented  
**Evidence Location:** `03-implement/control-implementation/AC-2-account-management.md`

---

### AC-3 — Access Enforcement

**Control Statement:** The information system enforces approved authorizations for logical access to information and system resources.

**Implementation:**
- Role-Based Access Control (RBAC) enforced at the application layer
- Clinical staff: access limited to patients within their care team
- Billing staff: access to financial data; no clinical notes access
- Administrators: system access only; PHI access blocked at application layer
- Access decisions logged and reviewed monthly via SIEM dashboards

**Responsible Entity:** Application Development / ISSO  
**Implementation Status:** Implemented  
**Evidence Location:** RBAC policy document, access control matrix

---

### AU-2 — Event Logging

**Control Statement:** The organization determines that the information system is capable of auditing defined events.

**Implementation:**
- The following events are logged: login/logout, failed auth attempts, PHI access/modify/delete, admin actions, privilege escalation, system errors, configuration changes
- Logs shipped to CloudWatch in real time; forwarded to Splunk SIEM within 60 seconds
- Log integrity protected via CloudTrail with S3 object lock (WORM)
- Logging policy reviewed annually by ISSO

**Responsible Entity:** ISSO / Cloud Ops  
**Implementation Status:** Implemented  
**Evidence Location:** `03-implement/control-implementation/AU-2-audit-events.md`

---

### IA-2 — Identification and Authentication

**Control Statement:** The information system uniquely identifies and authenticates organizational users.

**Implementation:**
- All users authenticated via Azure AD federated SSO (SAML 2.0)
- MFA required for all accounts; privileged accounts require TOTP (compensating control per tailoring decisions)
- Password policy: minimum 14 characters, complexity enforced, 90-day rotation for privileged accounts
- Session timeout: 15 minutes of inactivity for standard users; 5 minutes for privileged sessions
- Failed login lockout: 5 consecutive failures triggers 30-minute lockout with ISSO alert

**Responsible Entity:** IT Infrastructure / ISSO  
**Implementation Status:** Implemented  
**Evidence Location:** `03-implement/control-implementation/IA-2-identification-authentication.md`

---

### SC-8 — Transmission Confidentiality and Integrity

**Control Statement:** The information system implements cryptographic mechanisms to prevent unauthorized disclosure of information and detect changes to information during transmission.

**Implementation:**
- All external communications use TLS 1.3 minimum; TLS 1.0/1.1 disabled
- Internal API calls use mutual TLS (mTLS) between microservices
- PHI transmitted to external partners (HIE, clearinghouse) via TLS 1.3 with certificate pinning
- VPN connections use IKEv2/IPSec with AES-256-GCM
- Certificate management via AWS Certificate Manager; certificates rotate automatically

**Responsible Entity:** Cloud Ops / ISSO  
**Implementation Status:** Implemented  
**Evidence Location:** `03-implement/control-implementation/SC-8-transmission-confidentiality.md`

---

### SI-2 — Flaw Remediation

**Control Statement:** The organization identifies, reports, and corrects information system flaws.

**Implementation:**
- Vulnerability scans run weekly (Tenable Nessus); authenticated scans monthly
- Patch SLAs: Critical = 15 days, High = 30 days, Medium/Low = 90 days
- Patches applied via Ansible playbooks; tested in staging before production
- Emergency patches (zero-day) deployed within 72 hours with ISSO approval
- Patch status tracked in `06-monitor/patch-status.md`

**Responsible Entity:** IT Operations / ISSO  
**Implementation Status:** In Progress (patch cadence finding open — FIND-003)  
**Evidence Location:** `03-implement/control-implementation/SI-2-flaw-remediation.md`

---

## 9. Control Summary Table

| Control ID | Name | Status | Inherited | Finding |
|-----------|------|--------|-----------|---------|
| AC-2 | Account Management | Implemented | No | None |
| AC-3 | Access Enforcement | Implemented | No | None |
| AC-7 | Unsuccessful Login Attempts | Implemented | No | None |
| AC-17 | Remote Access | Implemented | No | None |
| AU-2 | Event Logging | Implemented | No | FIND-002 (partial) |
| AU-9 | Audit Log Protection | Implemented | No | None |
| AU-11 | Audit Record Retention | In Progress | No | FIND-002 |
| CP-9 | System Backup | Implemented | No | None |
| IA-2 | Identification & Authentication | Implemented | No | FIND-001 (partial) |
| IA-5 | Authenticator Management | Implemented | No | None |
| IR-6 | Incident Reporting | Implemented | No | None |
| PE-1 through PE-20 | Physical Protection | Inherited | Yes | None |
| PS-1 through PS-8 | Personnel Security | Inherited | Yes | None |
| RA-5 | Vulnerability Monitoring | Implemented | No | None |
| SC-8 | Transmission Confidentiality | Implemented | No | None |
| SC-28 | Protection of Info at Rest | Implemented | No | None |
| SI-2 | Flaw Remediation | In Progress | No | FIND-003 |
| SI-3 | Malicious Code Protection | Implemented | No | None |
