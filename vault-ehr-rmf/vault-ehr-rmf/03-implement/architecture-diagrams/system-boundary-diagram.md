# System Boundary Diagram — Vault EHR

**Document ID:** VLT-IMPL-002  
**Version:** 1.0  
**Date:** 2026-05-06

---

## Authorization Boundary Diagram (Text Representation)

```
╔══════════════════════════════════════════════════════════════════════╗
║              VAULT EHR AUTHORIZATION BOUNDARY                        ║
║                                                                      ║
║  ┌──────────────────────┐    ┌───────────────────────────────────┐  ║
║  │   ON-PREMISES ZONE   │    │     AWS GOVCLOUD (us-gov-west-1)  │  ║
║  │                      │    │                                   │  ║
║  │  [App Server Node 1] │    │  [WAF + Application Load Balancer]│  ║
║  │  [App Server Node 2] │◄──►│  [EC2 Auto Scaling Group]        │  ║
║  │  [App Server Node 3] │    │  [RDS PostgreSQL Multi-AZ]       │  ║
║  │  [Internal DB]       │    │  [S3 — PHI documents + backups]  │  ║
║  │                      │    │  [CloudTrail + CloudWatch]        │  ║
║  │  VLAN 20             │    │  [Splunk SIEM]                    │  ║
║  └──────────┬───────────┘    └───────────────┬───────────────────┘  ║
║             │                                │                       ║
║             └──────── AWS Direct Connect ────┘                       ║
║                        (IPSec overlay)                               ║
╚══════════════════════════════════════════════════════════════════════╝
         │                          │
         ▼                          ▼
[Azure AD - INHERITED]    [Internet - Patients/Providers]
                                    │
                              [TLS 1.3 HTTPS]
                                    │
                          ┌─────────┴──────────┐
                          │   EXTERNAL PARTNERS │  (Outside boundary)
                          ├────────────────────┤
                          │ State HIE (HL7)     │
                          │ Change Healthcare   │
                          │ LabCore (HL7)       │
                          │ MedDispense (API)   │
                          └────────────────────┘
```

---

## Component Inventory

| Component | Type | Location | OS/Platform | Function |
|-----------|------|----------|-------------|---------|
| App Server 1–3 | Physical server | On-premises DC | RHEL 9 | Application hosting |
| Internal DB | Physical server | On-premises DC | PostgreSQL 15 | Legacy data |
| EC2 ASG | Virtual (AWS) | GovCloud | Amazon Linux 2023 | App hosting (cloud) |
| RDS PostgreSQL | Managed DB (AWS) | GovCloud | PostgreSQL 15 | Primary PHI database |
| S3 PHI bucket | Object storage | GovCloud | AWS managed | Document storage |
| S3 backup bucket | Object storage | GovCloud | AWS managed | Backup and DR |
| WAF | Managed (AWS) | GovCloud | AWS managed | Web application firewall |
| ALB | Managed (AWS) | GovCloud | AWS managed | Load balancing |
| CloudTrail | Managed (AWS) | GovCloud | AWS managed | API audit logging |
| Splunk | Virtual (AWS) | GovCloud | Amazon Linux 2023 | SIEM / log analysis |

---

## Data Flow Summary

1. Users access Vault EHR via HTTPS (TLS 1.3) through the WAF → ALB → EC2
2. EC2 instances query RDS PostgreSQL for PHI (mTLS, VPC internal)
3. Documents stored/retrieved from S3 PHI bucket (VPC endpoint, no public access)
4. Audit logs stream to CloudTrail → CloudWatch → Splunk in real time
5. On-premises servers sync with cloud via AWS Direct Connect + IPSec
6. External partner connections via TLS 1.3 over internet to WAF endpoint
