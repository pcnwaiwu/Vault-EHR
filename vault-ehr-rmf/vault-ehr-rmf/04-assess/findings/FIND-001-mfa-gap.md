# FIND-001 — MFA Not Enforced for All Privileged Accounts

**Finding ID:** FIND-001  
**Severity:** High  
**Control:** IA-2(1) — Multifactor Authentication to Privileged Accounts  
**Status:** Open  
**Identified:** 2026-06-18  
**Reported By:** 3PAO Assessor  
**POA&M Item:** POA&M-001

---

## Description

During testing of privileged account authentication, the assessor identified that 3 of 8 IT administrator accounts are not enrolled in MFA. These accounts have full administrative access to Vault EHR application servers and the AWS GovCloud environment, including the ability to access and export PHI.

The organization's compensating control (TOTP via Microsoft Authenticator) was documented in the SSP, but enrollment was not enforced for all privileged accounts through Azure AD Conditional Access policies.

---

## Evidence

- Azure AD Conditional Access policy shows MFA excluded for `Vault-EHR-Admins` group in one legacy policy
- 3 admin accounts identified: `svc-vaultadmin1`, `itadmin-jsmith`, `itadmin-bwilliams`
- Screenshot evidence retained by 3PAO (not included in this repo per data handling policy)

---

## Impact

**Likelihood:** Moderate (accounts require network access and credentials)  
**Impact:** High (admin account compromise gives full system access including PHI export)  
**Risk Rating:** High

An attacker who compromises one of these admin credentials could access, modify, or exfiltrate patient PHI without triggering MFA challenges, and could disable audit logging to cover activity.

---

## Recommended Remediation

1. Remove legacy MFA exclusion policy in Azure AD Conditional Access
2. Force MFA enrollment for all members of `Vault-EHR-Admins` group
3. For service accounts, implement certificate-based authentication (no MFA exemption)
4. Conduct review of all Conditional Access policies for any remaining MFA exclusions

**Estimated Effort:** Low (4–8 hours configuration)  
**Estimated Cost:** $0 (within existing Azure AD licensing)

---

## Remediation Target Date

**2026-08-21** (60 days from SAR delivery)

---

## Remediation Verification

ISSO to provide:
- Screenshot of updated Conditional Access policy
- Azure AD sign-in logs showing MFA challenges for all 3 accounts
- Confirmation from IT Operations that service accounts use certificate auth
