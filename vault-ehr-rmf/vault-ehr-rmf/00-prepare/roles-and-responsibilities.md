# Roles and Responsibilities — Vault EHR

**Document ID:** VLT-PREP-002  
**Version:** 1.0  
**Date:** 2026-05-06

---

## RMF Role Assignments

| RMF Role | Title | Responsibilities |
|----------|-------|-----------------|
| Authorizing Official (AO) | Chief Information Officer (CIO) | Accepts residual risk; grants/denies ATO |
| AO Designated Representative | Deputy CIO | Reviews authorization package on AO's behalf |
| System Owner | Chief Medical Information Officer | Accountable for system mission, resources, and operations |
| ISSO | Sr. Information Security Analyst | Day-to-day security oversight; maintains SSP and POA&M |
| ISSM | Information Security Manager | Policy compliance; supervises ISSO; reports to AO |
| Common Control Provider | IT Infrastructure Team | Provides inherited controls (network, physical, AD) |
| Assessor (3PAO) | External Security Assessor | Independently assesses controls; produces SAR |
| Privacy Officer | Chief Privacy Officer | Ensures PHI/PII handling compliance with HIPAA |

---

## Detailed Responsibilities

### Authorizing Official (AO)
- Reviews and accepts the risk of operating Vault EHR
- Signs the Authorization Decision Document
- Reviews POA&M quarterly for risk posture changes
- Can revoke ATO if risk becomes unacceptable

### System Owner
- Allocates resources for security control implementation
- Approves the System Security Plan (SSP)
- Ensures system operates within the authorized boundary
- Coordinates with ISSO on changes that affect the authorization

### ISSO
- Maintains and updates the SSP, SAP, SAR, and POA&M
- Monitors security controls on a continuous basis
- Reports security incidents to the ISSM within 1 hour
- Coordinates with assessors during assessment activities
- Reviews and approves all system change requests for security impact

### ISSM
- Establishes and enforces security policy for Vault EHR
- Reviews and approves the authorization package
- Ensures ISSO has resources to fulfill responsibilities
- Briefs AO on risk posture quarterly

### 3PAO Assessor
- Develops and executes the Security Assessment Plan (SAP)
- Independently tests controls against stated implementation
- Documents findings in the Security Assessment Report (SAR)
- Provides no-cost finding remediation guidance

---

## RACI Matrix

| Activity | AO | System Owner | ISSO | ISSM | 3PAO |
|----------|----|----|----|----|-----|
| Maintain SSP | I | A | R | C | I |
| Control assessment | I | C | C | I | R |
| POA&M management | I | C | R | A | I |
| Incident response | I | C | R | A | I |
| ATO decision | R/A | C | C | C | I |
| ConMon reporting | I | I | R | A | I |

**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed
