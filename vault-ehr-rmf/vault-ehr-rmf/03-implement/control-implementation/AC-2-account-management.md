# AC-2 — Account Management

**Control ID:** AC-2  
**Control Family:** Access Control  
**Baseline:** HIGH  
**Implementation Status:** Implemented  
**Last Reviewed:** 2026-05-06

---

## Control Statement

The organization manages information system accounts, including establishing, activating, modifying, reviewing, disabling, and removing accounts in accordance with defined procedures.

---

## Organization-Defined Parameters

| Parameter | Value |
|-----------|-------|
| Account review frequency | Every 90 days |
| Termination — disable within | 24 hours |
| Termination — remove within | 30 days |
| Notification recipients | ISSO, department manager |

---

## Implementation Details

### Account Types

| Type | Description | Approval Required |
|------|-------------|------------------|
| Standard user | Clinical and administrative staff | Manager + ITSM ticket |
| Privileged (admin) | IT administrators | ISSO + Manager |
| Service account | Application-to-application | ISSO approval, documented purpose |
| Emergency access | Break-glass PHI access | ISSO approval, auto-expires 8 hrs |

### Lifecycle Procedures

1. **Provisioning:** Initiated via ITSM ticket → manager approval → IT Operations creates account → ISSO notified
2. **Modification:** ITSM ticket for role changes → original approver re-approves → audit log entry
3. **Review:** Automated quarterly report generated; managers certify active accounts via email; unconfirmed accounts disabled within 10 days of notification
4. **Termination:** HR system triggers ITSM workflow → account disabled within 24 hrs → access revoked from all systems → account removed at 30 days

### Technical Controls

- Azure AD manages all user accounts (SSO)
- Vault EHR application maps Azure AD groups to RBAC roles
- Group membership changes trigger immediate permission update (< 5 min propagation)
- All account events logged to Splunk SIEM

---

## Evidence

| Evidence | Location | Last Updated |
|----------|----------|-------------|
| Account management policy | SharePoint/Policies | 2026-01-15 |
| ITSM provisioning workflow | ITSM system | Continuous |
| Quarterly review reports | SharePoint/Audit | Quarterly |
| ISSO notification alerts | Splunk dashboard | Continuous |

---

## Related Controls

- AC-3 (Access Enforcement)
- AC-6 (Least Privilege)
- AU-2 (Audit logging of account events)
- IA-2 (Authentication tied to managed accounts)
