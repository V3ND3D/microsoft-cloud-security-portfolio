# Incident Response Plan v1.0
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*HIPAA §164.308(a)(6) — Security Incident Procedures*
*Version 1.0 | Effective: March 2026*

---

## Purpose & Authority

This IRP establishes procedures, roles, and responsibilities for detecting, containing, eradicating, and recovering from cybersecurity incidents. Required under HIPAA Security Rule §164.308(a)(6). Applies to all systems, users, locations, and business associates within the organization's security boundary.

## Scope

**Systems in scope:**
- Microsoft 365 tenant (Entra ID, Exchange, SharePoint, OneDrive, Teams, Defender)
- Google Workspace (mosaicdiagnostic.com)
- Cisco Meraki infrastructure — all 6 sites
- Linux AI servers at PR (mdi-app-server-prod) — n8n/Ollama automation
- PACS systems (InsiteOne) and DICOM infrastructure
- Greenbills billing system (BAA in place)
- Apple iPads — front desk patient intake
- All Intune-enrolled Windows 11 Pro workstations

**Data in scope:** ePHI, PII, financial and billing data

## Severity Classification

| Level | Name | Response SLA | Notification |
|-------|------|-------------|--------------|
| P1 | Critical | 1 hour | Eric Feldmann + Jailene DeJesus via personal mobile immediately |
| P2 | High | 4 hours | Same day — Eric + Jailene. Assess breach determination. |
| P3 | Medium | Next business day | Notify only if P2 escalation likely |
| P4 | Low | 72 hours | Engineer documents only |

## Incident Response Phases

1. **Detection & Classification** — Identify event, assign severity, activate appropriate runbook
2. **Containment** — Isolate affected systems, preserve forensic evidence
3. **Eradication** — Remove threat, patch vulnerability, validate clean state
4. **Recovery** — Restore systems, validate functionality, monitor for recurrence
5. **Post-Incident Review** — Complete PIR template within 14 days (P1/P2 required)

## Communication Protocol

For P1/P2: Use personal mobile devices only. Do NOT use corporate email or Teams during active containment. All external communications through Dr. Eric Feldmann or designated counsel.

## HIPAA Breach Assessment

Any incident with potential ePHI exposure triggers the HIPAA Breach Determination Worksheet (45 CFR §164.402). The 60-day notification clock starts at discovery — not at breach confirmation.

## Plan Maintenance

Reviewed upon any material architectural change or any P1/P2 incident revealing a gap in procedures.
