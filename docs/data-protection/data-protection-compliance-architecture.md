# Data Protection & Compliance Architecture
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Last Updated: March 2026 | Version: 1.0*

---

## Compliance Posture

| Metric | Value |
|--------|-------|
| HIPAA/HITECH Compliance Manager | ~80%+ |
| Beazley cyber insurance application | Q1–Q24 completed with technical evidence |

## Microsoft Purview DLP

- DLP policies across Exchange, SharePoint, OneDrive, and Teams
- ePHI pattern detection using built-in HIPAA sensitive information types
- Policy tips enabled for end-user awareness
- Audit mode → enforce mode progression documented per policy
- Endpoint DLP scoped to Intune-managed Windows 11 devices

## Sensitivity Labeling

- Label taxonomy aligned to HIPAA data classification (Internal, PHI, Confidential)
- Auto-labeling configured for known ePHI patterns
- Label inheritance enforced on containers

## Retention Governance

- Retention policies aligned to HIPAA/HITECH record-keeping obligations
- Scope: Exchange, SharePoint, OneDrive
- Disposition review configured for end-of-retention records

## HIPAA Technical Safeguards Mapping

| Safeguard | Control |
|-----------|---------|
| §164.312(a)(1) Access Control | Entra ID RBAC, Conditional Access, MFA |
| §164.312(a)(2)(ii) Emergency Access | Break-glass accounts with documented governance |
| §164.312(b) Audit Controls | Azure Log Analytics, Entra logs, Defender telemetry |
| §164.312(c)(1) Integrity | Defender for Business, ASR, tamper protection |
| §164.312(d) Authentication | FIDO2 MFA, Conditional Access |
| §164.312(e)(1) Transmission Security | TLS enforced, AutoVPN, Duo MFA for remote access |
| §164.308(a)(6) IR Procedures | IR Plan v1.0 + 7-runbook Playbook |
