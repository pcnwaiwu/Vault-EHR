# SC-8 — Transmission Confidentiality and Integrity

**Control ID:** SC-8 (with SC-8(1) enhancement)  
**Implementation Status:** Implemented  
**Last Reviewed:** 2026-05-06

---

## Cryptographic Standards in Use

| Protocol | Usage | Minimum Version | Notes |
|----------|-------|-----------------|-------|
| TLS | All HTTPS traffic | TLS 1.3 | TLS 1.0/1.1 disabled at WAF |
| mTLS | Internal service-to-service | TLS 1.3 | Mutual certificate auth |
| IPSec/IKEv2 | VPN (on-prem to cloud) | IKEv2 | AES-256-GCM, SHA-384 |
| SFTP | Clearinghouse billing data | SFTP with AES-256 | EDI 837 files |

## Certificate Management

- Public certificates: AWS Certificate Manager (auto-renewal)
- Internal CA: AWS Private CA for mTLS service mesh
- Certificate validity: 90 days maximum
- Expiry alerting: 30 days before expiration via CloudWatch alarm

## Cipher Suite Configuration

Allowed cipher suites (TLS 1.3):
- `TLS_AES_256_GCM_SHA384`
- `TLS_CHACHA20_POLY1305_SHA256`
- `TLS_AES_128_GCM_SHA256`

Deprecated suites explicitly disabled: RC4, DES, 3DES, MD5, SHA-1.

## Evidence

- AWS WAF TLS policy configuration (screenshot in SharePoint)
- SSL Labs scan results: Grade A+ (last scan: 2026-04-15)
- Network diagram showing encrypted channels
