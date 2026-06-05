# Incident Log — Vault EHR

**Document ID:** VLT-MON-003  
**Updated:** 2026-05-06  
**Owner:** ISSO

---

## Active Incidents

*No active incidents at time of last update.*

---

## Closed Incidents

| Incident ID | Date | Severity | Type | Summary | Resolution | HIPAA Breach? |
|------------|------|---------|------|---------|-----------|--------------|
| INC-2026-001 | 2026-02-14 | Low | Unauthorized access attempt | 12 failed login attempts from external IP against admin portal | IP blocked at WAF; no successful access | No |
| INC-2026-002 | 2026-03-22 | Medium | Misconfigured S3 bucket | Dev S3 bucket set to public — contained test data only (no PHI) | Bucket policy corrected within 2 hours; confirmed no PHI in bucket | No |
| INC-2026-003 | 2026-04-10 | Low | Phishing attempt | 3 staff received credential phishing emails; 0 clicked; 1 reported | Security awareness reminder sent org-wide; no credential compromise | No |

---

## Incident Reporting Requirements

| Incident Type | Report To | Timeline |
|--------------|-----------|---------|
| Confirmed PHI breach | Privacy Officer, ISSM, Legal | Within 1 hour of confirmation |
| Suspected PHI breach | ISSO, ISSM | Within 1 hour of suspicion |
| High/Critical security incident | ISSO, ISSM | Within 1 hour |
| Moderate security incident | ISSO | Within 4 hours |
| Low/Informational | ISSO | Within 24 hours (next business day) |

HIPAA Breach Notification Rule: Affected individuals notified within 60 days; HHS notified within 60 days (< 500 patients) or immediately (≥ 500 patients).
