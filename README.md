# Microsoft Cloud Security Portfolio
### Yeray Y. Lafontaine Martinez — IT & Cloud Security Engineer

[![Portfolio](https://img.shields.io/badge/Portfolio-Notion-black?style=flat-square)](https://selective-bracket-dbc.notion.site/yeray-lafontaine-cloud-security-engineer-portfolio)
[![GitHub](https://img.shields.io/badge/GitHub-V3ND3D-181717?style=flat-square&logo=github)](https://github.com/V3ND3D)
[![Email](https://img.shields.io/badge/Email-contact%40lafontainesec.dev-blue?style=flat-square)](mailto:contact@lafontainesec.dev)

---

## Overview

This repository documents the security architecture, governance controls, and operational program I designed and built as the **sole IT and security owner** for a HIPAA-regulated, multi-site diagnostic imaging organization.

Built from scratch — no inherited security posture, no security team, no escalation path.

**Environment at a glance:**
- **6 sites** across Delaware, New York, and Puerto Rico
- **83 users / 39 managed endpoints**
- **Microsoft 365 Business Premium** (Entra ID P1, Intune, Defender for Business, Purview)
- **Cisco Meraki MX75** firewalls at every site
- **Microsoft Secure Score: ~40% → >96%**
- **HIPAA/HITECH Compliance Manager: ~80%+**
- **Beazley cyber insurance application: Q1–Q24 completed**

---

## Security Domains

### Identity & Access
- Entra ID as sole authoritative IdP — cloud-native, no hybrid join
- Conditional Access enforcing MFA, device compliance, legacy auth blocking
- Phishing-resistant MFA (FIDO2) for administrative accounts
- Least-privilege RBAC, Windows LAPS, standing local admin eliminated
- Break-glass governance aligned to HIPAA §164.312(a)(2)(i)
- Entra diagnostic logging → Azure Log Analytics (`law-mosaic-security`)

### Endpoint Security
- Microsoft Defender for Business — EDR block mode, tamper protection, ASR rules
- BitLocker, Secure Boot, TPM 2.0 health as Intune compliance conditions
- Full Autopilot → enrollment → configuration profile → compliance baseline pipeline
- No BYOD, no unmanaged production Windows endpoints

### Network Security
- **Meraki MX75 hardened at all 6 sites** — standardized from PR reference template:
  - L3 outbound deny ruleset (9 rules — ports 23, 25, 135, 137–139, 445, 1080, 3389, 4444)
  - L7 category blocking, Content Filtering, Safe Search, YouTube Strict
  - Cisco AMP, IDS Prevention/Security mode, IP spoofing protection
- Hub-and-spoke AutoVPN — `172.31.x.0/24` per site
- **Cisco Duo RADIUS MFA for Client VPN:**
  - Duo Auth Proxy 6.6.0 on Ubuntu 24.04 LTS
  - Auth flow: `Client → MX75 → Duo Auth Proxy :1812 → Duo Cloud → MFA push → access`
  - Closed compensating control CC-VPN-001 — satisfied Beazley Q5

### Data Protection & Compliance
- Purview DLP across Exchange, SharePoint, OneDrive, Teams
- Sensitivity labeling and retention governance aligned to HIPAA/HITECH
- Beazley cyber insurance application completed end-to-end (Q1–Q24)
- HIPAA/HITECH Compliance Manager: ~80%+

### Monitoring & Logging
- Azure Log Analytics receiving Entra sign-in, audit, and risk detection logs
- KQL queries for identity anomaly detection and admin activity review
- Secure Score tracked as primary posture metric

### AI Automation Governance
- Self-hosted stack: n8n + Docker + Ollama — processes ePHI/PII
- LVM encryption, non-privileged service accounts, wired-only network
- SSH hardening in progress; log forwarding to Log Analytics in implementation
- DeepSeek flagged for replacement (federal compliance risk)

---

## Repository Structure

```
docs/
├── governance/               # Security program governance & compliance summary
├── identity/                 # Entra ID, Conditional Access, MFA, Break-Glass
├── endpoint/                 # Intune, Defender, Autopilot, iPad deployment
├── data-protection/          # Purview, DLP, Sensitivity Labels, HIPAA alignment
├── monitoring/               # Azure Log Analytics, Secure Score, KQL
├── network/                  # Meraki architecture, Duo MFA, AutoVPN, 6-site deployment
├── ir/                       # Incident Response Plan, Playbook, Runbooks, HIPAA Breach Worksheet
├── vulnerability-assessment/ # Internal VA report — PR site, Nmap + Nessus
└── roadmap/                  # 2026 Security Program Roadmap
resume/
└── Yeray_Lafontaine_Resume_Updated.docx
```

---

## Documentation Index

### Governance
| Document | Description |
|----------|-------------|
| [Security & Compliance Governance Summary](docs/governance/security-compliance-program-governance.md) | Authoritative governance baseline — control ownership, HIPAA alignment, licensing boundaries |

### Identity & Access
| Document | Description |
|----------|-------------|
| [Identity & Access Security Architecture](docs/identity/identity-access-security-architecture.md) | Entra ID architecture, Conditional Access, MFA posture, Break-Glass governance |

### Endpoint & Device Management
| Document | Description |
|----------|-------------|
| [Endpoint Security & Device Governance](docs/endpoint/endpoint-security-device-governance.md) | Intune MDM, Defender for Business, Autopilot, compliance enforcement |
| [iPad Deployment & Configuration](docs/endpoint/ipad-deployment-configuration.md) | Patient intake iPad deployment, Screen Time controls, ABM roadmap |

### Data Protection & Compliance
| Document | Description |
|----------|-------------|
| [Data Protection & Compliance Architecture](docs/data-protection/data-protection-compliance-architecture.md) | Purview governance, DLP for PHI, HIPAA/HITECH safeguard alignment |

### Monitoring & Logging
| Document | Description |
|----------|-------------|
| [Cloud Monitoring, Logging & Incident Readiness](docs/monitoring/cloud-monitoring-logging-incident-readiness.md) | Azure Log Analytics, Entra diagnostic logging, KQL, Secure Score governance |

### Network & Physical Infrastructure
| Document | Description |
|----------|-------------|
| [Network & Physical Infrastructure](docs/network/network-physical-infrastructure.md) | Meraki MX75 hardening, Duo RADIUS MFA, AutoVPN, 6-site deployment |

### Incident Response
| Document | Description |
|----------|-------------|
| [Incident Response Plan v1.0](docs/ir/incident-response-plan.md) | HIPAA §164.308(a)(6) IRP — roles, severity classification, procedures |
| [Incident Severity Classification Matrix](docs/ir/incident-severity-matrix.md) | P1–P4 criteria, SLAs, HIPAA breach notification triggers |
| [Incident Response Playbook — 7 Runbooks](docs/ir/incident-response-playbook.md) | Ransomware, BEC, Credential Compromise, PACS Access, AI Server, Meraki Intrusion, Lost Device |
| [HIPAA Breach Determination Worksheet](docs/ir/hipaa-breach-determination-worksheet.md) | 45 CFR §164.402 four-factor risk assessment template |
| [Post-Incident Review Template](docs/ir/post-incident-review-template.md) | Structured PIR form for P1/P2 incidents |

### Vulnerability Assessment
| Document | Description |
|----------|-------------|
| [Internal VA Report — PR Site](docs/vulnerability-assessment/pr-site-vulnerability-assessment-2026.md) | Nmap 7.98 + Nessus Essentials — 15 findings, 3 critical remediations in 24hrs |

### Roadmap
| Document | Description |
|----------|-------------|
| [2026 Security Program Roadmap](docs/roadmap/2026-security-program-roadmap.md) | 4-phase execution plan targeting audit-defensible posture and insurance transition |

---

## Tech Stack

| Layer | Tools |
|-------|-------|
| Identity | Microsoft Entra ID (P1), Conditional Access, Cisco Duo |
| Endpoint | Microsoft Intune, Defender for Business, Windows LAPS |
| Network | Cisco Meraki MX75, Duo Auth Proxy (RADIUS), AutoVPN |
| Data Protection | Microsoft Purview (DLP, Labels, Retention) |
| Monitoring | Azure Log Analytics, KQL |
| AI/Automation | n8n, Docker, Ollama, Microsoft Power Automate |
| Assessment | Nmap 7.98, Nessus Essentials |
| DNS/CDN | Cloudflare |
| Frameworks | HIPAA Security Rule, NIST CSF, NIST 800-53, CIS Controls, MITRE ATT&CK |

---

## Certifications (In Progress / Planned)
- Microsoft Azure Fundamentals (AZ-900) — *In Progress*
- Microsoft 365 Endpoint Administrator (MD-102) — *In Progress*
- Microsoft Azure Administrator (AZ-104) — *Planned*
- CompTIA Security+ — *In Progress (WGU)*
- B.S. Cybersecurity & Information Assurance — WGU *(Expected Dec 2027)*

---

*Production security work performed under real operational and compliance constraints. Sensitive organizational details abstracted or omitted. Controls implemented within Microsoft 365 Business Premium licensing boundaries. Last updated: March 2026.*
