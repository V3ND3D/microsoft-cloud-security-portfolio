# Incident Response Playbook — 7 Runbooks
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Version 1.0 | March 2026*

---

## Playbook Index

| # | Runbook | Default Severity |
|---|---------|-----------------|
| PB-01 | Ransomware / Destructive Malware | P1 |
| PB-02 | Business Email Compromise / Wire Fraud | P2 |
| PB-03 | Credential Compromise | P2 |
| PB-04 | Unauthorized PACS / ePHI Access | P2 |
| PB-05 | AI Server (Agent Rob) Compromise | P1 |
| PB-06 | Meraki Network Intrusion | P2 |
| PB-07 | Lost or Stolen Device | P2/P3 |

> All playbooks assume IRP communication protocol is active. Use personal mobile (not corporate email or Teams) for P1/P2 notifications during active containment.

---

## PB-01 — Ransomware / Destructive Malware (P1)

**Detection sources:** Defender for Business alert; user reports encrypted files or ransom note; systems unresponsive; Meraki AMP/IDS alert

**HIPAA breach risk:** HIGH — Assume ePHI breach until 4-factor assessment proves otherwise.

> ⚠️ DO NOT power off affected systems unless they cannot be isolated any other way. Volatile memory contains forensic evidence.
> ⚠️ DO NOT pay any ransom without legal counsel authorization.

**Steps:**
1. Notify Eric Feldmann + Jailene DeJesus via personal mobile within 15 minutes
2. Isolate affected endpoints in Defender portal — initiate device isolation
3. Identify patient zero — review Defender alert timeline
4. Disable affected user accounts in Entra ID
5. Disconnect site AutoVPN if lateral movement suspected
6. Preserve forensic evidence — do not wipe until forensics team approves
7. Begin HIPAA Breach Determination Worksheet
8. Engage forensics firm and breach counsel
9. Document all actions with timestamps

---

## PB-02 — Business Email Compromise / Wire Fraud (P2)

**Detection sources:** Finance/admin reports suspicious wire request; Defender for Office 365 alert; user reports impersonation email

**Steps:**
1. Notify Eric Feldmann + Jailene DeJesus same day
2. If wire transfer pending — contact bank immediately to halt/reverse
3. Investigate sender headers — determine if account compromise or spoofing
4. Review Entra sign-in logs for account compromise indicators
5. If account compromised — escalate to PB-03 (Credential Compromise)
6. Preserve email evidence before any deletion
7. Review and tighten mail flow rules in Exchange

---

## PB-03 — Credential Compromise (P2)

**Detection sources:** Entra sign-in risk alert; impossible travel; unfamiliar location sign-in; user reports unexpected MFA prompt

**Steps:**
1. Revoke all active sessions in Entra ID immediately
2. Reset password and re-register MFA
3. Review sign-in logs for unauthorized access scope
4. Check for mail forwarding rules, app consents, or OAuth grants added
5. Review Defender for Business alerts on associated endpoint
6. If ePHI accessed — begin HIPAA Breach Determination Worksheet
7. Document timeline and evidence

---

## PB-04 — Unauthorized PACS / ePHI Access (P2)

**Detection sources:** InsiteOne access log anomaly; Defender alert on clinical workstation; user reports unexpected access

**Steps:**
1. Notify Eric Feldmann + Jailene DeJesus same day
2. Contact InsiteOne support (Kyle/Joseph) to pull access logs
3. Identify scope of unauthorized access — which studies, which patient records
4. Disable or isolate the account used for unauthorized access
5. Begin HIPAA Breach Determination Worksheet immediately
6. Document number of records affected and data types involved

---

## PB-05 — AI Server Compromise (P1)

**Detection sources:** Unusual process activity on mdi-app-server-prod; unexpected outbound connections; n8n workflow anomalies; SSH login from unknown IP

**HIPAA breach risk:** HIGH — Server processes ePHI/PII via n8n automation.

**Steps:**
1. Notify Eric Feldmann + Jailene DeJesus immediately via personal mobile
2. Contact Brandon (sole SSH access holder) to verify any recent legitimate activity
3. Disconnect server from network at switch level if compromise confirmed
4. Preserve logs before any remediation
5. Review SSH auth logs, n8n execution logs, Docker container state
6. Begin HIPAA Breach Determination Worksheet
7. Assess whether ePHI was accessed, exfiltrated, or modified
8. Full OS rebuild required before returning to production

---

## PB-06 — Meraki Network Intrusion (P2)

**Detection sources:** Meraki IDS Prevention mode alert; unexpected inbound connection; AMP detection; Meraki Dashboard security event

**Steps:**
1. Review Meraki Dashboard security events and IDS alert details
2. Identify source IP and connection type
3. Verify no port forwarding rules were added or modified
4. Check AutoVPN tunnel status across all sites
5. Review firewall rule change logs in Dashboard
6. If internal compromise suspected — escalate to P1 and isolate affected site
7. Document IDS alert details and response actions

---

## PB-07 — Lost or Stolen Device (P2/P3)

**Detection sources:** User reports; iCloud Find My (iPads); Intune device status (Windows endpoints)

**Steps:**

*For Intune-managed Windows endpoint:*
1. Initiate remote wipe in Intune immediately
2. Revoke user sessions in Entra ID
3. Reset user credentials
4. Review Defender for Business for any pre-loss activity
5. Assess ePHI exposure — if any, begin HIPAA Breach Determination Worksheet

*For iPad (not MDM enrolled):*
1. Use iCloud Find My to locate device
2. Initiate iCloud remote wipe if unrecoverable
3. Change Apple ID password for `applemdm@mosaicdiagnostic.com`
4. Assess patient intake data exposure risk
5. Document incident — note MDM gap as contributing factor
