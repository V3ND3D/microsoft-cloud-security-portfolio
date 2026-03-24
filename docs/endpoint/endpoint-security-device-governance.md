# Endpoint Security & Device Governance Architecture
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Last Updated: March 2026 | Version: 1.0*

---

## Fleet Overview

| Metric | Value |
|--------|-------|
| Managed endpoints | 39 Windows 11 Pro |
| MDM authority | Microsoft Intune (sole) |
| Enrollment method | Autopilot + Entra ID join |
| BYOD | None |
| Unmanaged production endpoints | None |

## Device Lifecycle Pipeline

Autopilot → Entra ID Join → Intune Enrollment → Configuration Profiles → Security Baselines → Compliance Enforcement

## Microsoft Defender for Business

- EDR in block mode — active remediation
- Tamper protection enabled
- ASR rules deployed via Intune policy
- Real-time protection, cloud-delivered protection, PUA blocking enforced

## Compliance Framework

| Control | Enforcement |
|---------|-------------|
| BitLocker encryption | Intune compliance policy — key escrow to Entra |
| Secure Boot | Required for compliance |
| TPM 2.0 health | Required for compliance |
| Defender real-time protection | Required for compliance |
| OS version minimum | Enforced via compliance policy |

Non-compliant devices blocked from all corporate resources via Conditional Access.

## Windows LAPS

Windows LAPS deployed across all managed endpoints. Standing local admin privileges eliminated. Passwords rotated automatically and escrowed to Entra ID.

## Exceptions

**Linux AI Servers:** Not Intune-managed. Compensating controls: LVM full disk encryption, wired-only, non-privileged service accounts, restricted physical access, SSH hardening in progress.

**iPads (Patient Intake):** Manually configured with Screen Time restrictions. Apple Business Manager enrollment pending upon DUNS registration. Documented transitional state.
