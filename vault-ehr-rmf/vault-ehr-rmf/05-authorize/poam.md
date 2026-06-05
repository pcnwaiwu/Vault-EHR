# Plan of Action and Milestones (POA&M) — Vault EHR

**Document ID:** VLT-AUTH-001  
**Version:** 1.0  
**Date:** 2026-07-21  
**Last Updated:** 2026-07-21  
**Review Frequency:** Monthly (ISSO), Quarterly (ISSM + AO)

---

## Summary

| Total Items | Open | In Remediation | Completed | Risk Accepted |
|-------------|------|----------------|-----------|---------------|
| 6 | 5 | 1 | 0 | 0 |

---

## POA&M Items

### POA&M-001

| Field | Value |
|-------|-------|
| **ID** | POA-001 |
| **Finding Reference** | FIND-001 |
| **Control** | IA-2(1) |
| **Title** | MFA not enforced for all privileged accounts |
| **Severity** | High |
| **Status** | Open |
| **Responsible Party** | IT Operations / ISSO |
| **Original Due Date** | 2026-08-21 |
| **Scheduled Completion** | 2026-08-21 |
| **Milestone 1** | Remove MFA exclusion from legacy Conditional Access policy — 2026-07-28 |
| **Milestone 2** | Force MFA enrollment for all admin accounts — 2026-08-01 |
| **Milestone 3** | Implement certificate auth for service accounts — 2026-08-15 |
| **Milestone 4** | ISSO verification and evidence collection — 2026-08-21 |
| **Resources Required** | 8 hours IT Operations labor; no additional cost |
| **Compensating Controls** | Admin accounts restricted to dedicated jump host with additional IP restrictions |

---

### POA&M-002

| Field | Value |
|-------|-------|
| **ID** | POA-002 |
| **Finding Reference** | FIND-002 |
| **Control** | AU-11 |
| **Title** | Audit log retention gap — Splunk 1yr vs 7yr HIPAA requirement |
| **Severity** | Moderate |
| **Status** | In Remediation |
| **Responsible Party** | Cloud Ops / ISSO |
| **Original Due Date** | 2026-10-21 |
| **Scheduled Completion** | 2026-10-21 |
| **Milestone 1** | Budget request submitted for Splunk SmartStore — 2026-07-28 |
| **Milestone 2** | Vendor quote received and approved — 2026-08-15 |
| **Milestone 3** | Splunk SmartStore implemented and tested — 2026-10-01 |
| **Milestone 4** | 7-year retention verified with test queries — 2026-10-21 |
| **Resources Required** | $4K/year (SmartStore S3 backend); 40 hours Cloud Ops labor |
| **Compensating Controls** | Raw logs retained 7 years in S3 Glacier; manual retrieval process documented |

---

### POA&M-003

| Field | Value |
|-------|-------|
| **ID** | POA-003 |
| **Finding Reference** | FIND-003 |
| **Control** | SI-2 |
| **Title** | Patch SLA non-compliance for Critical vulnerabilities |
| **Severity** | Moderate |
| **Status** | Open |
| **Responsible Party** | IT Operations |
| **Original Due Date** | 2026-09-01 |
| **Scheduled Completion** | 2026-09-01 |
| **Milestone 1** | Formal patch exception process documented — 2026-08-01 |
| **Milestone 2** | Staging environment updated to mirror production — 2026-08-15 |
| **Milestone 3** | Patch SLA compliance tracked in monthly metrics — 2026-09-01 |
| **Resources Required** | 20 hours IT Operations labor |
| **Compensating Controls** | WAF virtual patching and network ACLs applied immediately upon vulnerability identification |

---

## Monthly Update Log

| Date | Updated By | Summary |
|------|-----------|---------|
| 2026-07-21 | ISSO | Initial POA&M created from SAR findings |
