# IA-2 — Identification and Authentication

**Control ID:** IA-2  
**Implementation Status:** Implemented (compensating control for IA-2(1) — see tailoring-decisions.md)  
**Last Reviewed:** 2026-05-06

---

## Authentication Mechanism

All users authenticate via Azure AD (SAML 2.0 federation) before accessing Vault EHR. The application does not maintain a separate credential store.

## MFA Requirements

| Account Type | MFA Method | Enforcement |
|-------------|------------|-------------|
| Standard clinical/admin | Microsoft Authenticator (TOTP) | Conditional Access policy |
| Privileged (admin) | TOTP + IP restriction | Conditional Access + firewall ACL |
| Service accounts | Certificate-based | No interactive MFA |
| Emergency break-glass | TOTP + ISSO approval | Manual process, logged |

## Session Management

- Standard user session timeout: 15 minutes inactivity
- Admin session timeout: 5 minutes inactivity
- Concurrent session limit: 3 per user
- Session tokens: JWT with 15-minute expiry, refresh token 8 hours

## Failed Authentication

- Lockout threshold: 5 consecutive failures
- Lockout duration: 30 minutes
- Lockout events: Alert sent to Splunk + ISSO email notification
