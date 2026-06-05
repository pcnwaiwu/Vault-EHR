# FIND-002 — Audit Log Retention Gap

**Finding ID:** FIND-002  
**Severity:** Moderate  
**Control:** AU-11 — Audit Record Retention  
**Status:** Open  
**Identified:** 2026-06-20  
**POA&M Item:** POA&M-002

---

## Description

HIPAA requires audit logs to be retained for a minimum of 6 years. The organization's tailoring decision set a 7-year retention requirement. However, the current Splunk SIEM implementation only retains indexed log data for 1 year before purging. Logs are archived to S3 Glacier after 90 days in CloudWatch, which satisfies the raw log retention requirement, but Splunk — the primary tool used for incident investigation and compliance reporting — cannot query logs older than 1 year.

This does not result in loss of log data, but it significantly impairs the usability of historical logs for forensic and compliance purposes.

---

## Impact

**Likelihood:** Low (data is not lost; it is archived)  
**Impact:** Moderate (delayed or impaired incident response for historical events; compliance gap if auditors require searchable logs)  
**Risk Rating:** Moderate

---

## Recommended Remediation

Option A (Preferred): Expand Splunk index retention to 7 years (requires additional storage licensing ~$12K/year)  
Option B: Implement Splunk SmartStore with S3 backend for warm storage of logs 90 days–7 years (estimated $4K/year)

---

## Remediation Target Date

**2026-10-21** (90 days — funding approval cycle required)
