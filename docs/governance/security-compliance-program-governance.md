# Security & Compliance Program Governance Summary
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Last Updated: March 2026 | Classification: Internal*

---

## Program Scope

Cloud-native security architecture — no on-premises Active Directory, no hybrid identity.

| Component | Detail |
|-----------|--------|
| Platform | Microsoft 365 Business Premium |
| Sites | 6 (Newark DE, Seaford DE, Milford DE, 2x New York, Puerto Rico) |
| Users | 83 |
| Endpoints | 39 Windows 11 Pro (Intune managed) |
| Identity | Microsoft Entra ID (P1) |
| Endpoint MDM | Microsoft Intune |
| Threat Protection | Microsoft Defender for Business |
| Network | Cisco Meraki MX75 × 6 sites |
| Monitoring | Azure Log Analytics (`law-mosaic-security`) |

## Security Program Status

| Metric | Value |
|--------|-------|
| Microsoft Secure Score | ~40% → **>96%** |
| HIPAA/HITECH Compliance Manager | **~80%+** |
| Governance documents | **14 documents authored** |
| IR runbooks | **7 runbooks** |
| Beazley insurance application | **Q1–Q24 completed** |

## Regulatory Alignment

- HIPAA Security Rule (primary)
- HITECH Act
- NIST CSF
- NIST 800-53
- CIS Controls
- MITRE ATT&CK

## Licensing Boundaries (M365 Business Premium)

**Included:** Entra ID P1, Conditional Access, MFA, Defender for Business, Intune MDM, Purview baseline

**Not included:** Entra ID P2 (PIM, Identity Governance), Defender for Identity, Microsoft Sentinel, extended log retention. Missing features are risk-assessed and documented with compensating controls.

## Control Ownership

Sole security owner: Yeray Y. Lafontaine Martinez, IT & Cloud Security Engineer. All control design, implementation, documentation, and incident response responsibility.
