# Patch Status Report — Vault EHR

**Document ID:** VLT-MON-002  
**Reporting Period:** May 2026  
**Updated:** 2026-05-06  
**Owner:** IT Operations / ISSO

---

## Patch Compliance Summary

| Severity | Total Open | Within SLA | Past SLA | Compliance Rate |
|---------|-----------|-----------|---------|----------------|
| Critical | 0 | — | — | N/A |
| High | 2 | 2 | 0 | 100% |
| Medium | 8 | 8 | 0 | 100% |
| Low | 14 | 14 | 0 | 100% |

---

## Open Vulnerabilities

| CVE | CVSS | Component | Discovered | SLA Due | Status | Compensating Control |
|-----|------|-----------|-----------|---------|--------|---------------------|
| CVE-2026-3311 | 7.8 | RHEL kernel | 2026-04-28 | 2026-05-28 | Patch scheduled 2026-05-18 | Network segmentation |
| CVE-2026-4422 | 7.5 | nginx 1.24 | 2026-05-01 | 2026-05-31 | Testing in staging | WAF rule deployed |

---

## Recently Patched (Last 30 Days)

| CVE | CVSS | Component | Patched Date | Verified By |
|-----|------|-----------|-------------|-------------|
| CVE-2026-1234 | 9.8 | OpenSSL 3.0 | 2026-05-02 | Tenable rescan |
| CVE-2026-5678 | 9.1 | Linux kernel | 2026-04-28 | Tenable rescan |
| CVE-2026-9012 | 9.3 | PostgreSQL 15 | 2026-05-18 | Tenable rescan |

*Note: CVE-2026-1234, -5678, -9012 were past SLA — documented in FIND-003 / POA&M-003.*
