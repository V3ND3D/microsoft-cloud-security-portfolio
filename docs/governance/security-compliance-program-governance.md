# Security & Compliance Program Governance Summary

**Organization:** Eric Feldmann, LLC
**Control Owner:** Yeray Y. Lafontaine Martinez
**Program Phase:** Cloud Security Establishment (Phase 1–2)
**Status:** Active — Authoritative Governance Baseline
**Last Updated:** February 2026

---

## 1. Purpose & Authority

This document defines the overarching governance framework for the organization's cloud security program. It establishes:

- Control ownership and accountability
- Regulatory alignment strategy (HIPAA/HITECH)
- Microsoft 365 Business Premium capability boundaries
- Risk management methodology
- Secure Score governance interpretation
- Exception and transitional state handling

This document serves as the authoritative summary of the organization's IT security posture.

---

## 2. Security Program Scope

The organization operates under a cloud-first security architecture utilizing:

| Component | Role |
|-----------|------|
| Microsoft Entra ID | Identity Authority |
| Microsoft Intune | Device Governance Authority |
| Microsoft Defender for Business | Endpoint Protection |
| Microsoft Defender for Office 365 | Email Protection |
| Microsoft Purview | Data Protection & Compliance |
| Azure Log Analytics | Identity Log Centralization |
| Cisco Meraki | Network Infrastructure |

There is no on-premises Active Directory or hybrid identity model.

---

## 3. Control Ownership

In accordance with HIPAA §164.308(a)(2), the designated Security Program Control Owner is:

**Yeray Y. Lafontaine Martinez**

Responsibilities include:
- Identity governance
- Endpoint security configuration
- Logging oversight
- Conditional Access policy management
- Compliance posture review
- Infrastructure oversight
- Incident response coordination
- Security documentation authorship

---

## 4. Regulatory Alignment

### 4.1 HIPAA Security Rule

The program aligns with the HIPAA Security Rule across three safeguard categories:

- **Administrative Safeguards (§164.308)** — Security officer designation, workforce access controls, contingency planning, evaluation
- **Physical Safeguards (§164.310)** — Workstation use policies, device and media controls
- **Technical Safeguards (§164.312)** — Access control, audit controls, integrity, transmission security

### 4.2 Compliance Manager Posture

- **HIPAA/HITECH Assessment:** ~80%+
- Microsoft-managed controls: High coverage
- Organization-managed controls: Progressively implemented
- Compliance Manager is used to identify gaps, track remediation, and document the shared responsibility model — it does not replace formal risk analysis documentation

### 4.3 Supporting Frameworks

| Framework | Application |
|-----------|-------------|
| NIST CSF | Overall program structure |
| NIST 800-53 | Control family mapping |
| CIS Controls | Hardening baselines |
| MITRE ATT&CK | Defensive control mapping |

---

## 5. Licensing Boundary

The organization operates under **Microsoft 365 Business Premium**, which provides:

- Entra ID P1 (Conditional Access, MFA, SSPR)
- Microsoft Intune (MDM/MAM)
- Microsoft Defender for Business
- Microsoft Defender for Office 365 Plan 1
- Microsoft Purview (basic DLP, sensitivity labels, retention)
- Azure Log Analytics (via Entra diagnostic settings)

**Capabilities NOT available under Business Premium:**
- Entra ID P2 (no Identity Protection risk policies, no PIM)
- Microsoft Sentinel (SIEM — evaluated in Phase 4)
- Defender for Identity
- Defender for Cloud Apps (full CASB)
- Purview advanced eDiscovery / Insider Risk Management

Where premium features are unavailable, compensating controls are documented.

---

## 6. Secure Score Governance

| Metric | Value |
|--------|-------|
| Baseline Score | ~40% |
| Current Score | >96% |
| Methodology | Structured control implementation + configuration hardening |

Secure Score is used as a posture measurement tool, not a compliance certification. Score items are evaluated against licensing boundaries and operational context before implementation.

---

## 7. Exception Handling

Known exceptions with documented compensating controls:

| Asset | Gap | Compensating Control |
|-------|-----|----------------------|
| Linux AI servers | Not Intune-managed, not Defender-onboarded | LVM encryption, wired-only network, restricted physical access |
| iPads (patient intake) | Not ABM/MDM enrolled | Screen Time restrictions, dedicated Apple ID, manual configuration — ABM enrollment planned |
| Static IPs | Not provisioned at all sites | Flagged; pending ISP coordination |

---

## 8. Document Inventory

| Document | Domain |
|----------|--------|
| Identity & Access Security Architecture | Identity |
| Endpoint Security & Device Governance Architecture | Endpoint |
| Data Protection & Compliance Architecture | Data Protection |
| Cloud Monitoring, Logging & Incident Readiness Architecture | Monitoring |
| Network & Physical Infrastructure Security Architecture | Network |
| iPad Deployment & Configuration Record | Endpoint |
