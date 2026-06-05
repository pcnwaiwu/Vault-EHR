# AU-2 — Audit Events

**Control ID:** AU-2  
**Implementation Status:** Implemented (partial finding — see FIND-002)  
**Last Reviewed:** 2026-05-06

---

## Audited Events

| Event Category | Events Logged | Log Destination |
|---------------|---------------|-----------------|
| Authentication | Login, logout, failed attempts, MFA events | CloudWatch → Splunk |
| PHI Access | View, create, modify, delete patient records | Application logs → Splunk |
| Admin actions | User provisioning, config changes, privilege use | CloudWatch → Splunk |
| System | Startup/shutdown, errors, security alerts | CloudWatch → Splunk |
| Network | Firewall allow/deny, VPN connections | Network logs → Splunk |

## Log Format

All logs use structured JSON with fields: `timestamp`, `user_id`, `action`, `resource`, `result`, `source_ip`, `session_id`.

## Retention

Logs retained for **7 years** per HIPAA and AU-11 requirement. Current implementation: 90-day hot (CloudWatch), remainder in S3 Glacier. **Gap: Splunk index only retains 1 year — see FIND-002.**

## Review Cadence

- Real-time: Splunk alerts on anomalous patterns
- Daily: ISSO reviews alert queue
- Weekly: Manual log sampling (10% of PHI access events)
- Monthly: Compliance report generated and reviewed by ISSM
