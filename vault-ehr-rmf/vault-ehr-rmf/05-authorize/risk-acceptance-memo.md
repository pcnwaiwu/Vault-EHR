# Risk Acceptance Memo — Vault EHR

**Document ID:** VLT-AUTH-003  
**Date:** [PENDING]  
**To:** Authorizing Official (CIO)  
**From:** ISSM  
**Subject:** Residual Risk Acceptance — Vault EHR Conditional ATO

---

## Purpose

This memo summarizes the residual risk associated with granting a Conditional Authority to Operate (C-ATO) for Vault EHR and recommends AO acceptance of that risk.

---

## Residual Risk Summary

| Finding | Severity | Compensating Control | Residual Risk |
|---------|---------|---------------------|---------------|
| FIND-001: MFA gap (3 admin accounts) | High | IP-restricted jump host; session monitoring | Moderate |
| FIND-002: Splunk log retention (1yr vs 7yr) | Moderate | S3 Glacier raw log retention; manual retrieval | Low |
| FIND-003: Patch SLA delay (3 CVEs) | Moderate | WAF virtual patching; network ACL compensating | Low |

**Overall Residual Risk: MODERATE**

---

## ISSM Recommendation

The ISSM recommends the AO grant a Conditional ATO with POA&M remediation requirements. The system provides critical healthcare services; denial of operation would significantly impair patient care. The identified findings do not represent imminent threat of PHI breach given the compensating controls in place, and all have clear, funded remediation paths.

---

## AO Acknowledgment

The Authorizing Official accepts the residual risk described above and authorizes Vault EHR to operate under the terms stated in the ATO cover sheet.

| | |
|--|--|
| **AO Signature:** | _________________________________ |
| **Date:** | _________________________________ |
