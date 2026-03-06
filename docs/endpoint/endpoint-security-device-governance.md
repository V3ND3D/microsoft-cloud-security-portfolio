# Endpoint Security & Device Governance Architecture

**Organization:** Eric Feldmann, LLC
**Control Owner:** Yeray Y. Lafontaine Martinez
**Program Phase:** Cloud Security Establishment (Phase 1–2)
**Status:** Active — Point-in-Time Configuration Snapshot
**Last Updated:** February 2026

---

## 1. Purpose & Scope

This document defines the endpoint security architecture and device governance controls implemented using Microsoft Intune and Microsoft Defender for Business. It establishes:

- Device enrollment authority and lifecycle model
- Endpoint protection baseline
- Attack surface reduction posture
- Disk encryption enforcement
- Compliance evaluation model
- Exception handling for non-Windows assets

All controls reflect current enforced configuration under Microsoft 365 Business Premium.

---

## 2. Device Governance Model

### 2.1 Managed Fleet

| Attribute | Value |
|-----------|-------|
| MDM Authority | Microsoft Intune |
| OS | Windows 11 Pro |
| Join Type | Entra ID joined (cloud-native) |
| Enrollment | Intune enrolled |
| Licensing | Microsoft 365 Business Premium |
| BYOD | Not permitted |
| Hybrid AD Join | Not in use |

### 2.2 Device Lifecycle Pipeline

```
Autopilot Registration
        ↓
Entra ID Join + Intune Enrollment
        ↓
Configuration Profiles Applied
        ↓
Security Baselines Deployed
        ↓
Compliance Policy Evaluated
        ↓
Conditional Access Enforcement
```

---

## 3. Microsoft Defender for Business

### 3.1 EDR Configuration

| Setting | Value |
|---------|-------|
| EDR Mode | Block Mode (active remediation) |
| Tamper Protection | Enabled |
| Cloud-delivered Protection | Enabled |
| Automatic Sample Submission | Enabled |
| Real-time Protection | Enabled |

### 3.2 Attack Surface Reduction (ASR) Rules

| Rule | State |
|------|-------|
| Block executable content from email / webmail | Enabled |
| Block Office apps from creating child processes | Enabled |
| Block Office apps from injecting into processes | Enabled |
| Block JavaScript/VBScript launching executables | Enabled |
| Block execution of potentially obfuscated scripts | Enabled |
| Block Win32 API calls from Office macros | Enabled |
| Block credential stealing from LSASS | Enabled |
| Block untrusted/unsigned processes from USB | Enabled |
| Block persistence through WMI event subscription | Enabled |

### 3.3 Exploit Protection

System-level exploit protection applied via Intune configuration profile. Key settings:
- Control Flow Guard (CFG): On
- Data Execution Prevention (DEP): On
- Force Randomization (Mandatory ASLR): On
- Randomize Memory Allocations (Bottom-up ASLR): On

---

## 4. Intune Compliance Policy

### 4.1 Compliance Requirements

| Control | Requirement |
|---------|-------------|
| BitLocker | Required |
| Secure Boot | Required |
| TPM | Required |
| Defender | Required — running, updated |
| Firewall | Required — enabled |
| OS Version | Minimum Windows 11 build enforced |
| Device Risk | Maximum: Low |

### 4.2 Non-Compliance Behavior

- Grace period: 1 day (allows time for remediation)
- After grace period: Device marked non-compliant
- Conditional Access blocks access to M365 resources for non-compliant devices
- Notifications sent to user and admin

---

## 5. Disk Encryption (BitLocker)

| Setting | Configuration |
|---------|--------------|
| Enforcement | Required via Intune compliance policy |
| Recovery Key Escrow | Azure AD / Intune (automatic) |
| Encryption Method | XTS-AES 128-bit (OS drive) |
| Pre-boot Authentication | TPM-based |

BitLocker recovery keys are centrally stored in Entra ID and accessible to admins via Intune portal.

---

## 6. Windows LAPS (Local Administrator Password Solution)

| Setting | Configuration |
|---------|--------------|
| Status | Enabled — all managed endpoints |
| Password Rotation | Automatic post-use |
| Storage | Entra ID (cloud LAPS) |
| Standing Local Admin | Removed from all endpoints |

Standing local administrator privileges have been removed from all production endpoints. LAPS provides time-limited, auto-rotating credentials for break-fix scenarios only.

---

## 7. Security Baselines

Microsoft security baselines deployed via Intune:
- **Microsoft Defender for Business baseline** — applied to all devices
- **Windows 11 security baseline** — applied to all devices
- **Edge browser security baseline** — applied to all devices

Baselines are reviewed quarterly and updated following Microsoft releases.

---

## 8. Non-Windows Asset Exceptions

### 8.1 Linux AI Servers

| Attribute | Detail |
|-----------|--------|
| Purpose | On-site automation and Power Automate workloads |
| MDM Status | Not Intune-enrolled |
| Defender Status | Not onboarded |
| Compensating Controls | LVM full-disk encryption, wired-only network connectivity, restricted physical access |
| Roadmap | Security review planned (Phase 4) |

### 8.2 Apple iPads (Patient Intake)

See: [iPad Deployment & Configuration Record](ipad-deployment-configuration.md)

| Attribute | Detail |
|-----------|--------|
| Purpose | Patient intake forms via lobbie.com |
| MDM Status | Not enrolled (transitional) |
| Compensating Controls | Screen Time restrictions, dedicated Apple ID, single-purpose configuration |
| Roadmap | ABM enrollment + Intune MDM (pending DUNS registration) |
