# System Categorization Report — Vault EHR

**Document ID:** VLT-CAT-003  
**Version:** 1.0  
**Date:** 2026-05-06

---

## Summary

This report summarizes the security categorization process and result for Vault EHR, conducted in accordance with FIPS 199 and NIST SP 800-60 Vol. 2.

---

## Categorization Process

1. Identified all information types processed, stored, or transmitted by Vault EHR (see `data-inventory.md`)
2. Mapped each information type to SP 800-60 Volume 2 categories
3. Assessed Confidentiality, Integrity, and Availability impact levels for each type
4. Applied the high-water mark principle to derive the system-level impact
5. Obtained approval from System Owner, ISSO, and ISSM

---

## Final Security Category

**SC Vault EHR = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}**

**System Impact Level: HIGH**

---

## Impact Level Justification

**Confidentiality — HIGH:** Vault EHR processes PHI for approximately 2.1 million patients. Unauthorized disclosure would cause severe harm including identity theft, insurance discrimination, reputational damage to patients, and HIPAA penalties up to $1.9M per violation category per year.

**Integrity — HIGH:** Clinical records (diagnoses, medications, allergies, orders) directly drive patient care decisions. Unauthorized modification of these records could result in incorrect medication dosing, missed diagnoses, or contraindicated treatments — constituting a direct patient safety risk.

**Availability — HIGH:** While the organization has paper fallback procedures for short outages, extended unavailability (> 4 hours) would significantly impair clinical operations, delay care for critical patients, and prevent access to emergency medication histories.

---

## Approval Signatures

| Role | Name | Date | Signature |
|------|------|------|-----------|
| ISSO | [Name] | 2026-05-06 | ____________ |
| System Owner | [Name] | 2026-05-06 | ____________ |
| ISSM | [Name] | 2026-05-06 | ____________ |
