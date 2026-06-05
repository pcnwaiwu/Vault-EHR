# Data Inventory — Vault EHR

**Document ID:** VLT-CAT-002  
**Version:** 1.0  
**Date:** 2026-05-06

---

## PHI Data Elements

| Data Element | Storage Location | Transmission | Encrypted at Rest | Encrypted in Transit |
|-------------|-----------------|--------------|-------------------|----------------------|
| Patient name | RDS PostgreSQL | HL7 FHIR API | Yes (AES-256) | Yes (TLS 1.3) |
| Date of birth | RDS PostgreSQL | HL7 FHIR API | Yes | Yes |
| Social Security Number | RDS PostgreSQL | EDI billing | Yes | Yes |
| Diagnosis codes (ICD-10) | RDS PostgreSQL | HIE, lab | Yes | Yes |
| Medication records | RDS PostgreSQL | Pharmacy API | Yes | Yes |
| Lab results | RDS + S3 (PDFs) | Lab API | Yes | Yes |
| Clinical notes | RDS PostgreSQL | Provider portal | Yes | Yes |
| Medical images (DICOM) | S3 (separate bucket) | HTTPS | Yes | Yes |
| Insurance member ID | RDS PostgreSQL | Clearinghouse | Yes | Yes |
| Emergency contacts | RDS PostgreSQL | Internal only | Yes | Yes |

---

## PII Data Elements (Staff)

| Data Element | Storage Location | Purpose |
|-------------|-----------------|---------|
| Employee name | RDS (HR table) | User account management |
| Employee ID | RDS (HR table) | System access |
| Email address | RDS + Azure AD | Authentication |
| Work phone | RDS | Directory |
| NPI number | RDS | Provider credentialing |
| DEA number | RDS (encrypted) | Controlled substance prescribing |

---

## Data Retention Schedule

| Data Type | Retention Period | Legal Basis |
|-----------|-----------------|-------------|
| Adult patient records | 10 years from last encounter | HIPAA + state law |
| Minor patient records | Until age 28 | State law |
| Audit logs | 7 years | HIPAA Security Rule |
| Billing records | 7 years | CMS requirements |
| Staff PII | Duration of employment + 7 years | HR policy |

---

## Data Flow Summary

1. Patient data enters via clinical staff input or HL7 interface from connected systems
2. Data stored in encrypted RDS (primary) with daily snapshots to S3 (encrypted)
3. Backups replicated to secondary AWS region (us-gov-east-1) for DR
4. PHI transmitted externally only via TLS 1.3 to authorized partners with signed BAAs
5. Audit logs streamed to CloudWatch → SIEM (Splunk) in real time
