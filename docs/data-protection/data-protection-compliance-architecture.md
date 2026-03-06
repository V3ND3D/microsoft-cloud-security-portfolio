# Data Protection & Compliance Architecture

**Organization:** Eric Feldmann, LLC
**Control Owner:** Yeray Y. Lafontaine Martinez
**Program Phase:** Cloud Security Establishment (Phase 1–2)
**Status:** Active — Point-in-Time Configuration Snapshot
**Last Updated:** February 2026

---

## 1. Purpose & Scope

This document defines the data protection, information governance, and regulatory alignment controls implemented within Microsoft 365 using Microsoft Purview. It establishes:

- Sensitivity labeling model
- Data Loss Prevention (DLP) enforcement
- Retention governance
- Compliance Manager posture
- HIPAA/HITECH alignment
- Licensing boundaries under Business Premium

---

## 2. Compliance Framework Alignment

### 2.1 Regulatory Scope

| Framework | Alignment |
|-----------|-----------|
| HIPAA Security Rule | Technical safeguards for ePHI |
| HITECH Act | Breach notification, enforcement |
| NIST CSF | Overall program structure |
| CIS Controls | Data protection control mapping |

### 2.2 Compliance Manager Posture

| Metric | Value |
|--------|-------|
| HIPAA/HITECH Assessment | ~80%+ |
| Microsoft-managed controls | High coverage |
| Organization-managed controls | Progressively implemented |

Compliance Manager is used to:
- Identify technical control gaps
- Track remediation tasks
- Document shared responsibility model

It does **not** replace formal risk analysis documentation.

---

## 3. Sensitivity Labeling Framework

### 3.1 Label Taxonomy

| Label | Scope | Application |
|-------|-------|-------------|
| Internal | General organizational data | Default for internal communications |
| Confidential | Sensitive business data | Applied manually or via auto-labeling |
| PHI | Protected Health Information | Applied to clinical data containing ePHI |
| Highly Confidential | Legal, financial, executive | Restricted distribution |

### 3.2 Label Enforcement

- Labels applied via Microsoft 365 Apps (Word, Excel, Outlook, Teams)
- Auto-labeling policies configured for PHI detection patterns
- Label-based protection (encryption + access restrictions) applied at Confidential and above
- Labels persist with documents across cloud and endpoint surfaces

---

## 4. Data Loss Prevention (DLP)

### 4.1 Policy Scope

DLP policies are enforced across:
- Exchange Online (email)
- SharePoint Online
- OneDrive for Business
- Microsoft Teams
- Windows endpoints (Endpoint DLP)

### 4.2 PHI Detection Rules

Sensitive information types monitored:
- U.S. Social Security Numbers
- U.S. Health Insurance Numbers
- ICD-9 / ICD-10 medical codes
- Drug Enforcement Agency (DEA) numbers
- U.S. Medical License numbers
- Patient name + date of birth combinations

### 4.3 DLP Policy Actions

| Trigger | Action |
|---------|--------|
| PHI detected in outbound email | Block send + notify user |
| PHI detected in Teams message | Block + notify |
| PHI shared externally via SharePoint | Block + alert admin |
| PHI on endpoint (USB/print attempt) | Audit + notify |

### 4.4 Licensing Boundary Note

Full Endpoint DLP and advanced policy conditions require Purview compliance add-on beyond Business Premium. Current implementation uses available Business Premium Purview capabilities with documented gaps.

---

## 5. Retention Governance

| Workload | Retention Period | Policy |
|----------|-----------------|--------|
| Exchange Online (email) | 7 years | Compliance retention label |
| SharePoint / OneDrive | 7 years | Retention policy |
| Teams messages | 7 years | Teams retention policy |
| Audit logs | 90 days (M365 default) | Extended via Log Analytics |

Retention policies are aligned to HIPAA medical records retention requirements.

---

## 6. Audit Log Configuration

Microsoft 365 unified audit logging is enabled for:
- User sign-in and access events
- File access, modification, sharing events
- Admin configuration changes
- DLP policy matches
- Sensitivity label activity

Audit logs are retained for 90 days in Microsoft 365 and forwarded to Azure Log Analytics (`law-mosaic-security`) for extended retention and correlation.

---

## 7. HIPAA Technical Safeguards Mapping

| HIPAA Standard | Control | Implementation |
|---------------|---------|----------------|
| §164.312(a)(1) — Access Control | Unique user identification | Entra ID user accounts, no shared credentials |
| §164.312(a)(2)(i) — Emergency Access | Break-glass procedure | Documented break-glass accounts in Entra ID |
| §164.312(a)(2)(ii) — Auto Logoff | Session timeout | Conditional Access session controls |
| §164.312(a)(2)(iii) — Encryption/Decryption | Data encryption | Sensitivity labels + BitLocker + TLS in transit |
| §164.312(b) — Audit Controls | Audit logging | M365 audit logs + Azure Log Analytics |
| §164.312(c)(1) — Integrity | Data integrity controls | SharePoint versioning, DLP, retention |
| §164.312(d) — Person Authentication | MFA | Conditional Access MFA enforcement |
| §164.312(e)(1) — Transmission Security | Encryption in transit | TLS 1.2+ enforced across M365 |
