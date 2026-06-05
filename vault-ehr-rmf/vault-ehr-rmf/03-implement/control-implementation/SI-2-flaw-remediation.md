# SI-2 — Flaw Remediation

**Control ID:** SI-2  
**Implementation Status:** In Progress — open finding FIND-003  
**Last Reviewed:** 2026-05-06

---

## Patch Management Process

1. **Identification:** Tenable Nessus scans weekly (unauthenticated) and monthly (authenticated)
2. **Triage:** ISSO reviews scan results within 5 business days; assigns CVSS-based severity
3. **Testing:** Patches applied to staging environment first; 48-hour soak period
4. **Production deployment:** Ansible playbooks deploy patches during maintenance windows (Sundays 02:00–06:00 EST)
5. **Verification:** Post-patch scan confirms remediation
6. **Documentation:** Patch status updated in `06-monitor/patch-status.md`

## SLA Targets

| Severity | CVSS Score | Patch Deadline | Current Compliance |
|----------|------------|----------------|-------------------|
| Critical | 9.0–10.0 | 15 days | 85% (gap — FIND-003) |
| High | 7.0–8.9 | 30 days | 92% |
| Medium | 4.0–6.9 | 90 days | 98% |
| Low | 0.1–3.9 | 180 days | 100% |

## Open Finding

**FIND-003:** Three Critical/High patches from the 2026-04-01 scan cycle exceeded the 15-day SLA due to dependency conflicts with the EHR application. Remediation target: 2026-06-01. See `04-assess/findings/FIND-003-patch-cadence.md`.
