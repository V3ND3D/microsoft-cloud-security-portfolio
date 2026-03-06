# Microsoft Cloud Security Portfolio
### Yeray Y. Lafontaine Martinez — IT & Cloud Security Engineer

[![Portfolio](https://img.shields.io/badge/Portfolio-Notion-black?style=flat-square)](https://selective-bracket-dbc.notion.site/yeray-lafontaine-cloud-security-engineer-portfolio)
[![Email](https://img.shields.io/badge/Email-contact%40lafontainesec.dev-blue?style=flat-square)](mailto:contact@lafontainesec.dev)
[![Clearance](https://img.shields.io/badge/Clearance-U.S.%20Secret%20(Previously%20Held)-red?style=flat-square)]()

---

## Overview

This repository documents a production cloud security program designed, implemented, and operated as the **sole security owner** for a multi-site healthcare organization operating under HIPAA.

The program spans **Identity, Endpoint, Data Protection, Monitoring, and Network** domains — built cloud-native on Microsoft 365 Business Premium with no on-premises Active Directory.

**Program highlights:**
- Microsoft Secure Score: **~40% → >96%**
- HIPAA/HITECH Compliance Manager posture: **~80%+**
- 5 clinical sites across Delaware, fully deployed under standardized Meraki architecture
- All controls designed, implemented, and documented within M365 Business Premium licensing boundaries

---

## Stack

| Domain | Technology |
|--------|-----------|
| Identity | Microsoft Entra ID (P1), Conditional Access, FIDO2, MFA |
| Endpoint | Microsoft Intune (MDM), Defender for Business, Autopilot |
| Data Protection | Microsoft Purview (DLP, Sensitivity Labels, Retention) |
| Email Security | Defender for Office 365 (Safe Links, Safe Attachments, ZAP) |
| Monitoring | Azure Log Analytics (`law-mosaic-security`), Secure Score |
| Network | Cisco Meraki MX75, 150AX APs, AutoVPN hub-and-spoke |
| Frameworks | HIPAA Security Rule, NIST CSF, NIST 800-53, CIS Controls, MITRE ATT&CK |

---

## Repository Structure

```
docs/
├── governance/          # Security program governance & compliance summary
├── identity/            # Entra ID, Conditional Access, MFA, Break-Glass
├── endpoint/            # Intune, Defender, Autopilot, iPad deployment
├── data-protection/     # Purview, DLP, Sensitivity Labels, HIPAA alignment
├── monitoring/          # Azure Log Analytics, Secure Score, Incident Readiness
└── network/             # Meraki architecture, AutoVPN, multi-site deployment
resume/
└── Yeray_Lafontaine_Resume_v2.docx
```

---

## Documentation Index

### Governance
| Document | Format | Description |
|----------|--------|-------------|
| [Security & Compliance Program Governance Summary](docs/governance/security-compliance-program-governance.md) | MD \| [DOCX](docs/governance/Security___Compliance_Program_Governance_Summary.docx) | Authoritative governance baseline — control ownership, HIPAA alignment, licensing boundaries |

### Identity & Access
| Document | Format | Description |
|----------|--------|-------------|
| [Identity & Access Security Architecture](docs/identity/identity-access-security-architecture.md) | MD \| [DOCX](docs/identity/Identity___Access_Security_Architecture.docx) | Entra ID architecture, Conditional Access, MFA, Break-Glass governance |

### Endpoint & Device Management
| Document | Format | Description |
|----------|--------|-------------|
| [Endpoint Security & Device Governance Architecture](docs/endpoint/endpoint-security-device-governance.md) | MD \| [DOCX](docs/endpoint/Endpoint_Security___Device_Governance_Architecture.docx) | Intune MDM, Defender for Business, Autopilot, compliance enforcement |
| [iPad Deployment & Configuration Record](docs/endpoint/ipad-deployment-configuration.md) | MD \| [DOCX](docs/endpoint/iPad_Deployment___Configuration_Record.docx) | Patient intake iPad deployment, Screen Time controls, ABM roadmap |

### Data Protection & Compliance
| Document | Format | Description |
|----------|--------|-------------|
| [Data Protection & Compliance Architecture](docs/data-protection/data-protection-compliance-architecture.md) | MD \| [DOCX](docs/data-protection/Data_Protection___Compliance_Architecture.docx) | Purview governance, DLP for PHI, HIPAA/HITECH safeguard alignment |

### Monitoring & Incident Readiness
| Document | Format | Description |
|----------|--------|-------------|
| [Cloud Monitoring, Logging & Incident Readiness](docs/monitoring/cloud-monitoring-logging-incident-readiness.md) | MD \| [DOCX](docs/monitoring/Cloud_Monitoring__Logging___Incident_Readiness_Architecture.docx) | Azure Log Analytics, Entra diagnostic logging, Secure Score governance |

### Network & Physical Infrastructure
| Document | Format | Description |
|----------|--------|-------------|
| [Network & Physical Infrastructure Security Architecture](docs/network/network-physical-infrastructure.md) | MD \| [DOCX](docs/network/Network___Physical_Infrastructure_Security_Architecture.docx) | Meraki MX75 deployment, hub-and-spoke AutoVPN, 5-site architecture |

---

## Resume

📄 [Download Resume (DOCX)](resume/Yeray_Lafontaine_Resume_v2.docx)

Full portfolio: [selective-bracket-dbc.notion.site](https://selective-bracket-dbc.notion.site/yeray-lafontaine-cloud-security-engineer-portfolio)

---

## Education & Certifications

**B.S. Cybersecurity & Information Assurance** — Western Governors University *(Expected Dec 2027)*

Program includes: CompTIA A+, Network+, Security+, CySA+, PenTest+, Data+, Project+, ITIL 4, LPI Linux Essentials, SSCP (ISC² Associate), CCSP

In progress: AZ-900 · MD-102

---

*All documentation reflects production configuration state as of February 2026. Organization and patient data is redacted. Controls are implemented within Microsoft 365 Business Premium licensing boundaries.*
