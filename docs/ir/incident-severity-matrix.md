# Incident Severity & Classification Matrix
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Version 1.0 | March 2026*

---

## Severity Levels

| Level | Name | Criteria / Examples | Response SLA | Notification |
|-------|------|---------------------|-------------|--------------|
| P1 | Critical | Ransomware/destructive malware active; confirmed ePHI exfiltration; PACS/clinical systems unavailable; AI server compromise; complete site network outage (security event) | 1 hour | Immediate — Eric Feldmann + Jailene DeJesus via personal mobile. CIRF activation likely. Breach counsel and forensics on standby. |
| P2 | High | Credential compromise (Entra/Google/Duo); BEC or wire fraud attempt; unauthorized access to clinical system or ePHI; lost/stolen device with potential ePHI; lateral movement detected | 4 hours | Same day — Eric Feldmann + Jailene DeJesus. Assess breach determination. Document fully. |
| P3 | Medium | Malware detected and contained; phishing email clicked (no credential entry); suspicious sign-in blocked by CA; failed MFA spike; IDS alert with no confirmed impact | Next business day | Notify Eric/Jailene only if P2 escalation likely. |
| P4 | Low | Policy violation with no data exposure; anomalous log entry with no confirmed threat; minor misconfiguration caught before exploitation; security tool false positive | 72 hours | Engineer documents only. No executive notification. |

## Classification Rules

- Assigned at detection — may be upgraded as investigation progresses
- Downgrading severity requires explicit engineer justification documented in the incident record
- When in doubt, classify higher and downgrade after assessment

## HIPAA Breach Triggers

P1 and P2 incidents involving ePHI automatically trigger the HIPAA Breach Determination Worksheet. Begin the 45 CFR §164.402 four-factor assessment immediately. 60-day notification clock starts at discovery.
