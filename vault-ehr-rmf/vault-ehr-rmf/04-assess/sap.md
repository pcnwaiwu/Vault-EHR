# Security Assessment Plan (SAP) — Vault EHR

**Document ID:** VLT-ASSESS-001  
**Version:** 1.0  
**Date:** 2026-05-06  
**Assessment Type:** Initial Authorization Assessment  
**Assessor:** [3PAO Organization Name]

---

## 1. Purpose

This Security Assessment Plan (SAP) describes the scope, objectives, methodology, and schedule for the independent security assessment of Vault EHR in support of its Authority to Operate (ATO).

---

## 2. Assessment Scope

**In Scope:**
- All controls documented in `03-implement/ssp.md`
- Application layer (Vault EHR web application and APIs)
- AWS GovCloud infrastructure components
- On-premises application servers
- System interconnections (HL7 interfaces, billing clearinghouse)

**Out of Scope:**
- Inherited controls (physical security, Azure AD, HR/personnel)
- Connected partner systems (HIE, LabCore, MedDispense)

---

## 3. Assessment Objectives

1. Determine the extent to which security controls are implemented correctly
2. Determine whether controls operate as intended
3. Determine whether controls produce the desired outcomes with respect to meeting HIPAA and NIST SP 800-53 requirements
4. Identify gaps and deficiencies that require remediation before authorization

---

## 4. Assessment Methods

| Method | Description | Controls Assessed |
|--------|-------------|------------------|
| Document Review | Review of SSP, policies, procedures, configurations | All controls |
| Interview | Structured interviews with ISSO, system owner, administrators | AC, AU, IR, PL |
| Examination | Review of system screenshots, config files, scan results | AC, AU, IA, SC, SI |
| Testing | Active testing — port scans, auth testing, injection testing | AC, IA, SC, SI |
| Penetration Testing | Scoped external + internal pen test | AC, SC, SI |

---

## 5. Assessment Schedule

| Activity | Start Date | End Date | Responsible |
|----------|-----------|---------|-------------|
| Kickoff meeting | 2026-06-01 | 2026-06-01 | 3PAO + ISSO |
| Document review | 2026-06-02 | 2026-06-10 | 3PAO |
| Interviews | 2026-06-11 | 2026-06-14 | 3PAO + ISSO |
| Technical testing | 2026-06-15 | 2026-06-25 | 3PAO |
| Penetration testing | 2026-06-22 | 2026-06-26 | 3PAO (pen test team) |
| Draft SAR delivery | 2026-07-07 | 2026-07-07 | 3PAO |
| ISSO/system owner review | 2026-07-08 | 2026-07-14 | ISSO |
| Final SAR delivery | 2026-07-21 | 2026-07-21 | 3PAO |

---

## 6. Assessment Team

| Role | Organization | Responsibilities |
|------|-------------|-----------------|
| Lead Assessor | 3PAO | Overall assessment, document review, interviews |
| Technical Tester | 3PAO | Network/application testing |
| Pen Tester | 3PAO | Penetration testing |
| ISSO Liaison | Vault EHR Org | Coordinate access, answer questions, review findings |

---

## 7. Rules of Engagement

- All testing conducted during off-peak hours (10pm–6am EST) unless coordinated otherwise
- No destructive testing; denial-of-service techniques prohibited
- Production PHI data must not be accessed, exfiltrated, or retained
- All test accounts created and removed within 24 hours of testing completion
- Any critical finding discovered must be reported to ISSO within 24 hours
- Emergency stop: ISSO can halt testing at any time via designated contact

---

## 8. Required Access and Resources

| Resource | Purpose | Provided By |
|----------|---------|-------------|
| Read-only AWS IAM role | CloudTrail, CloudWatch, config review | Cloud Ops |
| Test user accounts (3) | Application testing | IT Operations |
| Network access (VPN) | Internal system access | IT Operations |
| SSP and policy documents | Document review | ISSO |
| Vulnerability scan results | Evidence review | ISSO |
