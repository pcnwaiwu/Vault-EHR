# Continuous Monitoring Strategy — Vault EHR

**Document ID:** VLT-MON-001  
**Version:** 1.0  
**Date:** 2026-05-06

---

## 1. Purpose

This document defines the continuous monitoring strategy for Vault EHR in accordance with NIST SP 800-137. It establishes the ongoing monitoring activities, frequencies, and responsibilities that allow the AO to maintain situational awareness of the system's security posture.

---

## 2. Monitoring Activities

### Security Control Monitoring

| Control Category | Monitoring Method | Frequency | Responsible |
|-----------------|------------------|-----------|-------------|
| Access controls | Automated account review scripts; SIEM dashboard | Monthly | ISSO |
| Audit logging | SIEM alert rules; log completeness check | Daily | ISSO |
| Vulnerability management | Tenable Nessus scans | Weekly (unauth), Monthly (auth) | IT Ops |
| Configuration management | AWS Config rules; CIS benchmark scan | Weekly | Cloud Ops |
| Incident response | IR metrics (MTTD, MTTR) tracked in Splunk | Monthly | ISSO |
| Patch compliance | Patch status report | Monthly | IT Ops |
| Backup and recovery | Backup success/failure alerts; quarterly restore test | Daily alerts, Quarterly test | Cloud Ops |

### Security Metrics Reported to ISSM/AO

| Metric | Target | Reporting Frequency |
|--------|--------|-------------------|
| Critical patch SLA compliance | ≥ 95% | Monthly |
| Open High/Critical POA&M items | 0 past due | Monthly |
| Mean time to detect incidents | ≤ 1 hour | Quarterly |
| Mean time to respond to incidents | ≤ 4 hours | Quarterly |
| MFA enrollment rate | 100% | Monthly |
| Failed login attempts (anomalous spike) | < 50/day average | Weekly |
| PHI access outside business hours | Alert on any | Real-time |

---

## 3. Significant Change Management

Any proposed change to Vault EHR that may affect the security posture must be reviewed by the ISSO before implementation. Significant changes include:

- New system interconnections or data flows
- Changes to authentication mechanisms
- New software components or third-party integrations
- Changes to encryption configurations
- Cloud region additions or major infrastructure changes
- Changes to backup or logging configurations

**Process:** ISSO reviews change request → determines if security impact analysis required → updates SSP if necessary → notifies ISSM if authorization boundary affected

---

## 4. Annual Assessment Requirements

- **Annual control testing:** Subset of controls re-tested annually; full assessment every 3 years (ATO renewal)
- **Annual penetration test:** External + internal scoped pen test
- **Annual risk assessment update:** Update threat landscape and risk ratings
- **Annual POA&M review:** Confirm all items on track; close completed items with evidence

---

## 5. Reporting Chain

| Report | Audience | Frequency | Format |
|--------|---------|-----------|--------|
| ConMon status dashboard | ISSO | Continuous | Splunk dashboard |
| Monthly security metrics | ISSM | Monthly | Email + PDF |
| Quarterly risk briefing | ISSM + AO | Quarterly | Briefing deck |
| Annual security posture report | AO + System Owner | Annually | Formal report |
| Incident reports | ISSM + AO + Privacy Officer | As needed | IR report form |
