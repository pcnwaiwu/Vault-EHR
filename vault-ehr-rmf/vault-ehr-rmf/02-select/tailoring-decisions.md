# Tailoring Decisions — Vault EHR

**Document ID:** VLT-SEL-002  
**Version:** 1.0  
**Date:** 2026-05-06

---

## Purpose

This document records all tailoring decisions made to the NIST SP 800-53 Rev 5 HIGH baseline for Vault EHR, including scoping guidance, compensating controls, and additions.

---

## Controls Added (Beyond HIGH Baseline)

| Control ID | Rationale |
|-----------|-----------|
| AC-2(13) | Disable accounts of individuals posing risk — added due to PHI sensitivity |
| AU-3(2) | Centralized management of audit records — HIPAA audit trail requirement |
| SC-8(1) | Cryptographic protection of PHI in transit — HIPAA Technical Safeguard |
| SI-3(2) | Automatic malicious code updates — critical for ransomware prevention in healthcare |
| IR-6(1) | Automated incident reporting — required for HIPAA breach notification timeliness |

---

## Controls Tailored Out (Not Applicable)

| Control ID | Control Name | Justification |
|-----------|-------------|---------------|
| AC-20 | Use of External Systems | No external system connections outside of documented ISAs |
| MA-4(6) | Cryptographic Protection of Maintenance Sessions | Maintenance only performed on-site or via dedicated jump host |
| PE-20 | Asset Monitoring and Tracking | Physical assets tracked by separate CMDB; not in EHR boundary |

---

## Controls with Compensating Implementations

| Control ID | Control Name | Standard Requirement | Compensating Measure | Approved By |
|-----------|-------------|---------------------|----------------------|-------------|
| IA-2(1) | MFA for Privileged Accounts | Hardware tokens | Software TOTP (Authenticator app) due to remote clinical staff | ISSM, 2026-04-01 |
| SC-7(10) | Prevent Exfiltration | Data loss prevention (DLP) tools | Enhanced audit logging + behavioral analytics until DLP deployed | ISSM, 2026-04-01 |

---

## Parameter Selections (Organization-Defined Values)

| Control | Parameter | Selected Value |
|---------|-----------|----------------|
| AC-2 | Account review frequency | 90 days |
| AC-7 | Consecutive invalid login attempts | 5 attempts |
| AC-7 | Lockout duration | 30 minutes |
| AU-11 | Audit log retention | 7 years (HIPAA) |
| CP-2 | Recovery Time Objective (RTO) | 4 hours |
| CP-2 | Recovery Point Objective (RPO) | 1 hour |
| IA-5(1) | Minimum password length | 14 characters |
| RA-5 | Vulnerability scan frequency | Weekly |
| SI-2 | Patch timeframe — Critical | 15 days |
| SI-2 | Patch timeframe — High | 30 days |
| SI-2 | Patch timeframe — Medium/Low | 90 days |
