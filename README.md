# VAULT EHR (Electronic Health Record Management System)
A simulated NIST RMF portfolio project for Vault, a fictional Electronic Healthcare Records (EHR) management system. It includes system categorization, security control selection, System Security Plan (SSP), risk assessment, Plan of Action and Milestones (POA&M), Authorization to Operate (ATO), and continuous monitoring. Developed solely for educational and learning purposes.


# PROJECT NAME

# 🏥 VAULT — ELECTRONIC HEALTHCARE MANAGEMENT SYSTEM
|Field | Details |
|------|--------|
|**Document Type:** | System Overview |
|**System Name:** | Vault |
|**Version:** | 1.0 |
|**Status:** | Draft |
|**Classification:** | Unclassified — For Portfolio Use Only |


## **OBJECTIVE**
This project is a complete end-to-end NIST Risk Management Framework (RMF) authorization process for Vault, a fictional Electronic Healthcare Management System (EHR). Its main objective is to showcase practical knowledge of system categorization, security control selection, implementation, assessment, authorization, and continuous monitoring for a healthcare system that handles Protected Health Information (PHI) and Personally Identifiable Information (PII).

This practical project is intended to develop and demonstrate real-world Governance, Risk, and Compliance (GRC) expertise, along with security documentation skills within a healthcare regulatory environment.

## **SKILLS LEARNED**

- Practical application of the NIST RMF lifecycle from categorization to
  continuous monitoring
- Understanding of FIPS 199 system categorization for healthcare systems
- Ability to select and tailor security controls from NIST SP 800-53 Rev 5
- Development of System Security Plan (SSP) documentation
- Risk assessment and risk register development for a healthcare environment
- Security Assessment Plan (SAP) and Security Assessment Report (SAR) writing
- POA&M tracking and remediation planning
- Understanding of HIPAA Security Rule requirements and how they map to
  NIST controls
- Authorization to Operate (ATO) package development
- Continuous monitoring strategy and scheduling


## **TOOLS USED**

- **NIST SP 800-53 Rev 5** — Security control selection and tailoring
- **FIPS 199** — System categorization
- **NIST SP 800-60 Vol. 1 & 2** — Information type identification
- **NIST SP 800-30** — Risk assessment methodology
- **draw.io** — Network and data flow diagrams
- **Microsoft Word / Markdown** — Security documentation
- **GitHub** — Project hosting and version control
- **NIST RMF Cybersecurity Framework** — Overall project structure


## **1. SYSTEM DESCRIPTION**

Vault is a hybrid Electronic Healthcare Management System built to streamline daily healthcare operations. It allows healthcare providers to manage patient records, appointments, billing, and clinical documentation within a secure, centralized platform.

The system processes, stores, and transmits sensitive data, including Protected Health Information (PHI) and Personally Identifiable Information (PII), making strong security controls and regulatory compliance essential priorities.


## **2. SYSTEM PURPOSE AND MISSION**

The primary mission of Vault is to:

- Support patient registration and profile management
- Enable appointment scheduling and tracking
- Maintain and manage Electronic Health Records (EHR)
- Facilitate billing and insurance coordination
- Support clinical documentation by healthcare providers
- Generate operational and compliance reports
- Maintain audit logs for security and compliance purposes


## **3. SYSTEM USERS**

| User Role | Description |
|-----------|-------------|
| **Patients** | Access personal health records and appointments |
| **Doctors** | View and update patient records and treatment notes |
| **Nurses** | Access patient information and update care notes |
| **Administrative Staff** | Manage scheduling and patient registration |
| **Billing Staff** | Process billing and insurance claims |
| **System Administrators** | Manage system configuration and user accounts |
| **Security Team** | Monitor system security and respond to incidents |

## **4. SYSTEM ENVIRONMENT**

Vault operates in a **hybrid environment** consisting of:

| Component | Environment |
|-----------|-------------|
| Web Application Server | Cloud-hosted (AWS) |
| Database Server | On-Premise |
| Authentication Service | Cloud-hosted (AWS) |
| Audit Logging Server | On-Premise |
| Backup Server | Cloud-hosted (AWS) |
| Admin Workstations | On-Premise |
| Clinician Endpoints | On-Premise |


## **5. DATA HANDLED BY VAULT**

| Data Type | Description | Sensitivity |
|-----------|-------------|-------------|
| **PHI** | Protected Health Information | High |
| **PII** | Personally Identifiable Information | High |
| **Billing Data** | Insurance and payment records | High |
| **Treatment Notes** | Clinical documentation | High |
| **Appointment Data** | Scheduling records | Moderate |
| **Audit Logs** | System activity records | Moderate |
| **Authentication Data** | Login credentials and access tokens | High |


## **6. SYSTEM COMPONENTS**

| Component | Function |
|-----------|----------|
| **Web Application Server** | Hosts the Vault user interface and application logic |
| **Database Server** | Stores patient records, billing data, and system data |
| **Authentication Service** | Manages user identity verification and access control |
| **Audit Logging Server** | Captures and stores all system activity logs |
| **Backup Server** | Maintains encrypted backups of critical system data |
| **Admin Workstations** | Used by IT and security staff to manage the system |
| **Clinician Endpoints** | Devices used by doctors and nurses to access Bundle |

## **7. COMPLIANCE AND REGULATORY SCOPE**

| Framework / Regulation | Relevance |
|-----------------------|-----------|
| **HIPAA** | Vault processes PHI and must meet HIPAA Security Rule requirements |
| **NIST SP 800-53 Rev 5** | Primary control framework for RMF authorization |
| **FIPS 199** | Used to categorize Bundle based on impact levels |
| **NIST SP 800-60** | Used to identify information types handled by Bundle |
| **GDPR** | Applicable if Vault handles data of EU-based individuals |


## **STEPS**

### **STEP 1 — SYSTEM OVERVIEW AND BOUNDARY DEFINITION**
Definition of what Vault is, who uses it, what data it handles,
and where the system boundary begins and ends.

*Ref 1: Architecture Diagram*
[![Architecture Diagram](./diagrams/Architecture_Diagram.png)](https://github.com/pcnwaiwu/Architecture_Diagram.png)


### **STEP 2 — SYSTEM CATEGORIZATION**
Categorize Vault using FIPS 199 and NIST SP 800-60 based on
the sensitivity of data handled.

*Ref 2: FIPS 199 Categorization Table*
![Categorization Table](./vault-ehr-rmf/vault-ehr-rmf/01-categorize/fips-199-categorization.md)]

### **STEP 3 — CONTROL SELECTION**
Select and tailor security controls from NIST SP 800-53 Rev 5
based on Vault's High impact categorization.

*Ref 3: Control Baseline Summary*
![Control Baseline](./vault-ehr-rmf/vault-ehr-rmf/02-select/control-baseline.md)


### **STEP 4 — SYSTEM SECURITY PLAN**
Document how each selected control is implemented within Vault.

*Ref 4: SSP Cover Page*
![SSP](./vault-ehr-rmf/vault-ehr-rmf/03-implement/ssp.md)


### **STEP 5 — RISK ASSESSMENT**
Identify threats and vulnerabilities specific to a healthcare
environment and rate them by likelihood and impact.

*Ref 5: Risk Register*
![Risk Register](./vault-ehr-rmf/vault-ehr-rmf/05-authorize/risk-register.md)


### **STEP 6 — SECURITY ASSESSMENT**
Develop a SAP and SAR to test whether Vault's controls
are working as intended.

*Ref 6: SAR Findings Summary*
![SAR](./vault-ehr-rmf/vault-ehr-rmf/04-assess/sar.md)


### **STEP 7 — POA&M**
Track all findings and weaknesses with remediation plans
and target completion dates.

*Ref 7: POA&M Tracker*
![POAM](./vault-ehr-rmf/vault-ehr-rmf/05-authorize/poam.md)


### **STEP 8 — AUTHORIZATION**
Compile the full ATO package and make an authorization
recommendation based on Vault's risk posture.

*Ref 8: Authorization Recommendation*
![ATO](./vault-ehr-rmf/vault-ehr-rmf/05-authorize/ato-package/ato-package.md)


### **STEP 9 — CONTINUOUS MONITORING**
Document how Vault will be monitored on an ongoing basis
after authorization.

*Ref 9: Continuous Monitoring Schedule*
![ConMon](./vault-ehr-rmf/vault-ehr-rmf/06-monitor/conmon-strategy.md)



## **KEY ASSUMPTIONS**

- Vault is a fictional system created for portfolio and learning purposes
- All data, scenarios, and documentation are simulated
- Security controls are selected based on a High impact baseline
- The hybrid environment assumes AWS as the cloud service provider
- No real PHI or PII is used anywhere in this project


## **DOCUMENT CONTROL**

| Field | Detail |
|-------|--------|
| **Author** | Philippa Nwaiwu |
| **Created** | 02/01/2026 |
| **Last Updated** | 04/15/2026 |
| **Next Review** | [Date] |
| **Version** | 1.0 |



⚠️ **DISCLAIMER**
Vault is a fictional system created solely for educational and portfolio
demonstration purposes. All data, scenarios, and documentation within
this project are simulated and do not represent any real organization,
system, or individual.
