# Control Baseline — Vault EHR

**Document ID:** VLT-SEL-001  
**Version:** 1.0  
**Date:** 2026-05-06  
**Baseline:** NIST SP 800-53 Rev 5 — HIGH Impact

---

## Selected Control Families

The following control families are applicable to Vault EHR. Controls are selected from the HIGH baseline and tailored per `tailoring-decisions.md`.

| Family | ID | Description | Implementation Status |
|--------|----|-------------|----------------------|
| Access Control | AC | Manages who can access the system and under what conditions | In Progress |
| Audit and Accountability | AU | Logs and monitors system activity | Implemented |
| Configuration Management | CM | Manages system configurations and changes | In Progress |
| Contingency Planning | CP | Plans for system disruption and recovery | Implemented |
| Identification & Authentication | IA | Verifies user identity before granting access | Implemented |
| Incident Response | IR | Detects, reports, and responds to incidents | Implemented |
| Maintenance | MA | Controls system maintenance activities | Implemented |
| Media Protection | MP | Protects system media containing PHI | In Progress |
| Physical Protection | PE | Controls physical access to system components | Inherited |
| Planning | PL | Documents security plans | Implemented |
| Program Management | PM | Manages the information security program | In Progress |
| Personnel Security | PS | Controls related to personnel | Inherited |
| Risk Assessment | RA | Assesses risk to the system | In Progress |
| System & Services Acquisition | SA | Manages system development and acquisition | In Progress |
| System & Comm. Protection | SC | Protects system communications | Implemented |
| System & Info. Integrity | SI | Protects against malware and flaws | In Progress |
| Supply Chain Risk Mgmt | SR | Manages supply chain risks | In Progress |

---

## Priority Controls for Vault EHR (PHI/Healthcare Focus)

| Control ID | Control Name | Priority | Rationale |
|-----------|-------------|----------|-----------|
| AC-2 | Account Management | P1 | PHI access must be strictly controlled |
| AC-3 | Access Enforcement | P1 | Role-based access to patient data |
| AC-17 | Remote Access | P1 | Clinician remote access is common |
| AU-2 | Event Logging | P1 | HIPAA audit trail requirement |
| AU-9 | Protection of Audit Information | P1 | Prevent log tampering |
| IA-2 | Identification and Authentication | P1 | MFA for all privileged users |
| IA-5 | Authenticator Management | P1 | Password/token lifecycle |
| SC-8 | Transmission Confidentiality | P1 | PHI in transit protection |
| SC-28 | Protection of Info at Rest | P1 | PHI at rest encryption |
| SI-2 | Flaw Remediation | P1 | Patch management for healthcare |
| IR-6 | Incident Reporting | P1 | HIPAA breach notification |
| CP-9 | System Backup | P1 | Data recovery for patient records |
| RA-5 | Vulnerability Monitoring | P1 | Regular scanning |

---

## Control Inheritance

The following controls are **inherited** from organizational common control providers and are not re-implemented by Vault EHR:

| Control | Provided By | Notes |
|---------|------------|-------|
| PE-1 through PE-20 | Facilities / Data Center | Physical security |
| PS-1 through PS-8 | HR / Personnel Security | Background checks, onboarding |
| IA-8 (Azure AD) | Microsoft / IT Infra | Federated identity |
| AT-1 through AT-3 | IT Security Training | Org-wide security awareness |
