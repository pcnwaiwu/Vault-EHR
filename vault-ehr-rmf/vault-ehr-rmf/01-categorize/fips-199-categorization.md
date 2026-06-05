# FIPS 199 Security Categorization — Vault EHR

**Document ID:** VLT-CAT-001  
**Version:** 1.0  
**Date:** 2026-05-06  
**Reference:** FIPS 199, NIST SP 800-60 Vol. 2

---

## 1. Purpose

This document establishes the security category for Vault EHR in accordance with FIPS Publication 199, *Standards for Security Categorization of Federal Information and Information Systems*.

---

## 2. Information Types

### 2.1 Health Records (SP 800-60: C.3.1.1)

| Security Objective | Impact Level | Rationale |
|-------------------|-------------|-----------|
| Confidentiality | **HIGH** | Unauthorized disclosure of PHI causes severe harm to patients (discrimination, identity theft, reputational damage). HIPAA mandates protection. |
| Integrity | **HIGH** | Corruption or unauthorized modification of clinical records could result in incorrect treatment, medication errors, or patient death. |
| Availability | **MODERATE** | Loss of access for ≤ 4 hours is acceptable with paper fallback procedures. Extended outages (> 24 hrs) jeopardize patient care. |

**Information Type Category:** SC Health Records = {(C, HIGH), (I, HIGH), (A, MODERATE)}

---

### 2.2 Patient Billing and Insurance (SP 800-60: C.3.1.2)

| Security Objective | Impact Level | Rationale |
|-------------------|-------------|-----------|
| Confidentiality | **HIGH** | Billing data contains SSNs, insurance IDs, financial account info. Breach causes financial harm and identity theft. |
| Integrity | **HIGH** | Incorrect billing data causes financial loss, fraud, and regulatory penalties (False Claims Act). |
| Availability | **MODERATE** | Billing can tolerate short delays; manual workarounds available. |

**Information Type Category:** SC Billing = {(C, HIGH), (I, HIGH), (A, MODERATE)}

---

### 2.3 Appointment and Scheduling Data (SP 800-60: C.3.1.3)

| Security Objective | Impact Level | Rationale |
|-------------------|-------------|-----------|
| Confidentiality | **MODERATE** | Appointment data reveals care-seeking behavior; exposure causes privacy harm. |
| Integrity | **HIGH** | Incorrect scheduling could result in missed critical appointments (chemotherapy, dialysis). |
| Availability | **HIGH** | Scheduling disruption directly impacts patient care delivery and provider workflow. |

**Information Type Category:** SC Scheduling = {(C, MODERATE), (I, HIGH), (A, HIGH)}

---

### 2.4 System Audit Logs (SP 800-60: C.3.1.4)

| Security Objective | Impact Level | Rationale |
|-------------------|-------------|-----------|
| Confidentiality | **MODERATE** | Logs contain access patterns; disclosure could reveal security posture. |
| Integrity | **HIGH** | Tampered logs undermine accountability and incident investigation. |
| Availability | **LOW** | Short-term unavailability of logs is acceptable. |

**Information Type Category:** SC Audit Logs = {(C, MODERATE), (I, HIGH), (A, LOW)}

---

## 3. System Security Category

Per FIPS 199, the overall system security category is determined by the **high-water mark** across all information types.

| Security Objective | Applicable Impact Level |
|-------------------|------------------------|
| Confidentiality | **HIGH** |
| Integrity | **HIGH** |
| Availability | **HIGH** |

> **SC Vault EHR = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}**

**Overall System Impact Level: HIGH**

---

## 4. Resulting Control Baseline

A **HIGH** impact level mandates the **NIST SP 800-53 Rev 5 HIGH baseline** as the starting point for control selection, prior to tailoring.

---

## 5. Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| ISSO | [ISSO Name] | ____________ | 2026-05-06 |
| System Owner | [Owner Name] | ____________ | 2026-05-06 |
| ISSM | [ISSM Name] | ____________ | 2026-05-06 |
