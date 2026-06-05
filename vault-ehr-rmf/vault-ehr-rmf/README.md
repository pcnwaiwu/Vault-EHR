# Vault EHR — NIST RMF Security Authorization Package

**System Name:** Vault Electronic Health Record (Vault EHR)  
**System Type:** Hybrid Electronic Healthcare Management System  
**Classification:** UNCLASSIFIED // FOR OFFICIAL USE ONLY (FOUO)  
**FIPS 199 Impact Level:** HIGH  
**RMF Status:** In Progress  
**Last Updated:** 2026-05-06

---

## System Overview

Vault EHR is a hybrid Electronic Healthcare Management System built to streamline daily healthcare operations. It allows healthcare providers to manage patient records, appointments, billing, and clinical documentation within a secure, centralized platform. The system processes, stores, and transmits sensitive data including Protected Health Information (PHI) and Personally Identifiable Information (PII).

---

## Repository Structure

```
vault-ehr-rmf/
├── 00-prepare/                        # RMF Step 1 — Prepare
│   ├── system-description.md
│   ├── roles-and-responsibilities.md
│   └── risk-management-strategy.md
├── 01-categorize/                     # RMF Step 2 — Categorize
│   ├── fips-199-categorization.md
│   ├── data-inventory.md
│   └── system-categorization-report.md
├── 02-select/                         # RMF Step 3 — Select
│   ├── control-baseline.md
│   └── tailoring-decisions.md
├── 03-implement/                      # RMF Step 4 — Implement
│   ├── ssp.md
│   ├── control-implementation/
│   │   ├── AC-2-account-management.md
│   │   ├── AU-2-audit-events.md
│   │   ├── SC-8-transmission-confidentiality.md
│   │   ├── IA-2-identification-authentication.md
│   │   └── SI-2-flaw-remediation.md
│   └── architecture-diagrams/
│       └── system-boundary-diagram.md
├── 04-assess/                         # RMF Step 5 — Assess
│   ├── sap.md
│   ├── sar.md
│   └── findings/
│       ├── FIND-001-mfa-gap.md
│       ├── FIND-002-audit-log-retention.md
│       └── FIND-003-patch-cadence.md
├── 05-authorize/                      # RMF Step 6 — Authorize
│   ├── poam.md
│   ├── risk-acceptance-memo.md
│   └── ato-package/
│       └── ato-cover-sheet.md
├── 06-monitor/                        # RMF Step 7 — Monitor
│   ├── conmon-strategy.md
│   ├── patch-status.md
│   └── incident-log.md
└── .github/
    └── ISSUE_TEMPLATE/
        ├── finding.md
        └── poam-item.md
```

---

## RMF Phase Status

| Phase | Step | Status | Owner |
|-------|------|--------|-------|
| Prepare | 0 | ✅ Complete | ISSO |
| Categorize | 1 | ✅ Complete | ISSO |
| Select | 2 | ✅ Complete | ISSO / ISSM |
| Implement | 3 | 🔄 In Progress | System Owner |
| Assess | 4 | 🔄 In Progress | Assessor |
| Authorize | 5 | ⏳ Pending | AO |
| Monitor | 6 | ⏳ Pending | ISSO |

---

## Key Contacts

| Role | Responsibility |
|------|----------------|
| System Owner | Accountable for overall system and mission |
| ISSO | Day-to-day security oversight and documentation |
| ISSM | Security management and policy compliance |
| Authorizing Official (AO) | Grants Authority to Operate |
| Assessor (3PAO) | Independent security control assessment |

---

## Regulatory Frameworks

- NIST SP 800-37 Rev 2 — Risk Management Framework
- NIST SP 800-53 Rev 5 — Security and Privacy Controls
- NIST SP 800-60 — Information Types / Impact Categorization
- FIPS 199 — Standards for Security Categorization
- FIPS 200 — Minimum Security Requirements
- HIPAA Security Rule (45 CFR Part 164)

---

## Branch & Contribution Policy

All changes to security documentation require a Pull Request with at least one reviewer approval. Direct pushes to `main` are disabled. See branch protection rules in Settings.

**Branch naming:** `rmf/{phase}/{short-description}`  
**Example:** `rmf/03-implement/AC-2-account-management`

---

> ⚠️ This repository contains security-sensitive documentation. Do not commit real PHI, PII, private keys, passwords, or signed authorization letters.
