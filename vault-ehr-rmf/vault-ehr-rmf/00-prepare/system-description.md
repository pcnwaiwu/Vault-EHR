# System Description — Vault EHR

**Document ID:** VLT-PREP-001  
**Version:** 1.0  
**Date:** 2026-05-06  
**Author:** ISSO  
**Status:** Approved

---

## 1. System Identification

| Field | Value |
|-------|-------|
| System Name | Vault Electronic Health Record (Vault EHR) |
| System Abbreviation | Vault EHR |
| System Owner | Chief Medical Information Officer (CMIO) |
| ISSO | Information System Security Officer |
| Deployment Model | Hybrid (on-premises + AWS GovCloud) |
| Operating Environment | Production |
| FIPS 199 Impact Level | HIGH |
| System Status | Operational |
| Authorization Type | Authority to Operate (ATO) |

---

## 2. System Purpose and Description

Vault EHR is a hybrid Electronic Healthcare Management System built to streamline daily healthcare operations. The platform enables healthcare providers to:

- Manage patient records (clinical notes, lab results, imaging)
- Schedule and track appointments
- Process billing and insurance claims
- Produce and store clinical documentation
- Coordinate care across providers within the same organization

The system is the primary platform for processing, storing, and transmitting Protected Health Information (PHI) and Personally Identifiable Information (PII) across the organization.

---

## 3. System Boundary

The Vault EHR authorization boundary includes:

**In Scope:**
- Vault EHR application servers (on-premises, 3 nodes)
- AWS GovCloud tenant (us-gov-west-1): EC2, RDS, S3, CloudTrail
- Web application layer (patient portal, provider portal)
- Internal clinical APIs
- Database layer (PostgreSQL RDS instances)
- Identity provider integration (Azure AD — inherited)
- Network security layer (firewall, WAF, VPN)

**Out of Scope / Inherited:**
- Azure Active Directory (separate authorization boundary)
- Organization-wide email infrastructure
- Physical building security (handled by Facilities)

---

## 4. System Users

| User Type | Count (Approx.) | Access Level |
|-----------|-----------------|--------------|
| Clinical staff (physicians, nurses) | 450 | Read/Write PHI |
| Administrative staff (billing, scheduling) | 120 | Read/Write PII, limited PHI |
| IT administrators | 8 | System administration, no PHI access |
| Security team | 4 | Audit log access, no PHI |
| Patients (portal) | ~12,000 | Read-only own records |
| Third-party assessors | As needed | Read-only audit artifacts |

---

## 5. Data Types Processed

| Data Type | Sensitivity | Volume |
|-----------|-------------|--------|
| Protected Health Information (PHI) | HIGH | ~2.1M patient records |
| Personally Identifiable Information (PII) | HIGH | ~2.1M patients + ~600 staff |
| Billing and insurance data | HIGH | ~850K claims/year |
| Clinical documentation (notes, orders) | HIGH | ~4M documents |
| Audit and access logs | MODERATE | ~500GB/year |
| System configuration data | MODERATE | Minimal |

---

## 6. System Interconnections

| Connected System | Organization | Data Exchanged | Connection Type | Agreement |
|-----------------|--------------|----------------|-----------------|-----------|
| State Health Information Exchange (HIE) | State DOH | PHI (HL7 FHIR) | TLS 1.3 API | ISA + MOU |
| Insurance clearinghouse (Change Healthcare) | Third party | Billing data | SFTP/EDI 837 | BAA + ISA |
| Lab Information System (LabCore) | Internal | Lab results (HL7) | VPN tunnel | ISA |
| Pharmacy system (MedDispense) | Internal | Medication orders | TLS 1.3 API | ISA |
| Azure AD | Microsoft | Authentication tokens | SAML 2.0 | BAA |

---

## 7. Laws, Regulations, and Standards

- HIPAA Privacy Rule (45 CFR Part 164 Subpart E)
- HIPAA Security Rule (45 CFR Part 164 Subpart C)
- HITECH Act
- NIST SP 800-37 Rev 2 (RMF)
- NIST SP 800-53 Rev 5 (Security Controls)
- FIPS 199, FIPS 200
- State health data privacy laws (applicable jurisdiction)

---

## 8. Architecture Summary

```
[Patients / Providers]
        |
  [WAF + Load Balancer]  <-- AWS GovCloud
        |
  [Application Tier]     <-- EC2 Auto Scaling Group
        |
  [API Gateway / Internal]
        |
  [Database Tier]        <-- RDS PostgreSQL (Multi-AZ, encrypted at rest)
        |
  [Audit & Monitoring]   <-- CloudTrail, CloudWatch, SIEM
```

On-premises components connect to AWS GovCloud via AWS Direct Connect with IPSec overlay.

---

## 9. Document Control

| Version | Date | Author | Change Summary |
|---------|------|--------|----------------|
| 1.0 | 2026-05-06 | ISSO | Initial release |
