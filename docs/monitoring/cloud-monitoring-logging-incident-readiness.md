# Cloud Monitoring, Logging & Incident Readiness Architecture

**Organization:** Eric Feldmann, LLC
**Control Owner:** Yeray Y. Lafontaine Martinez
**Program Phase:** Cloud Security Establishment (Phase 1–2)
**Status:** Active — Point-in-Time Configuration Snapshot
**Last Updated:** February 2026

---

## 1. Purpose & Scope

This document defines the centralized monitoring, identity logging, audit visibility, and security posture evaluation mechanisms implemented within the Microsoft cloud environment. It establishes:

- Identity and administrative audit logging controls
- Diagnostic log forwarding configuration
- Log Analytics workspace governance
- Alerting framework
- Secure Score posture governance model
- Incident readiness position

The organization operates under Microsoft 365 Business Premium licensing.

---

## 2. Monitoring Architecture Overview

### 2.1 Control Plane Monitoring Model

| Component | Role |
|-----------|------|
| Microsoft Entra ID | Native identity and audit log generation |
| Microsoft Defender for Business | Endpoint security telemetry and alerts |
| Azure Log Analytics (`law-mosaic-security`) | Centralized log ingestion and retention |
| Microsoft Secure Score | Posture measurement and governance |
| Compliance Manager | Regulatory posture tracking |

---

## 3. Entra Identity Logging

### 3.1 Log Categories Collected

| Log Type | Content |
|----------|---------|
| SignInLogs | Interactive, non-interactive, service principal sign-ins |
| AuditLogs | User, group, role, policy, and app configuration changes |
| RiskyUsers | P1 risk detection events |
| RiskySignIns | Sign-in risk events within P1 scope |
| DirectoryLogs | Directory-level administrative operations |

### 3.2 Diagnostic Settings

Tenant-level diagnostic settings configured under:
`Microsoft Entra ID → Monitoring & Health → Diagnostic Settings`

Destination: **Azure Log Analytics Workspace** — `law-mosaic-security`

---

## 4. Azure Log Analytics Workspace

### 4.1 Workspace Configuration

| Setting | Value |
|---------|-------|
| Workspace Name | `law-mosaic-security` |
| Retention | 30 days (default free tier) |
| Data Sources | Entra diagnostic logs |
| Region | Aligned to M365 tenant region |

### 4.2 KQL Query Library

**Break-glass account monitoring:**
```kql
SigninLogs
| where UserPrincipalName contains "breakglass"
| project TimeGenerated, UserPrincipalName, IPAddress, ResultType, Location, AppDisplayName
| order by TimeGenerated desc
```

**Failed sign-ins — last 24 hours:**
```kql
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType != 0
| summarize FailureCount = count() by UserPrincipalName, IPAddress, ResultType
| order by FailureCount desc
```

**Legacy authentication attempts:**
```kql
SigninLogs
| where ClientAppUsed in ("Exchange ActiveSync", "IMAP4", "POP3", "SMTP Auth", "Other clients")
| project TimeGenerated, UserPrincipalName, ClientAppUsed, IPAddress, AppDisplayName
| order by TimeGenerated desc
```

**Admin role assignments — last 7 days:**
```kql
AuditLogs
| where TimeGenerated > ago(7d)
| where Category == "RoleManagement"
| where OperationName contains "Add member to role"
| project TimeGenerated, InitiatedBy, TargetResources, OperationName
```

**MFA registration changes:**
```kql
AuditLogs
| where OperationName contains "User registered security info"
   or OperationName contains "User deleted security info"
| project TimeGenerated, TargetResources, InitiatedBy, OperationName
| order by TimeGenerated desc
```

**Sign-ins from new countries (baseline deviation):**
```kql
SigninLogs
| where TimeGenerated > ago(7d)
| where ResultType == 0
| summarize Countries = make_set(Location) by UserPrincipalName
| where array_length(Countries) > 1
```

---

## 5. Secure Score Governance

| Metric | Value |
|--------|-------|
| Baseline Score | ~40% |
| Current Score | >96% |
| Review Cadence | Monthly |

### 5.1 Governance Principles

- Score items are evaluated against **licensing boundaries** before implementation
- Items requiring Entra P2 or Sentinel are tracked as deferred — not marked as "risk accepted" without review
- Score improvement is treated as posture measurement, not compliance certification
- Documented exceptions exist for licensing-constrained items

---

## 6. Incident Readiness Position

### 6.1 Current Capabilities

| Capability | Status |
|-----------|--------|
| Identity log ingestion | ✅ Active (Log Analytics) |
| Endpoint telemetry | ✅ Active (Defender for Business) |
| Email threat detection | ✅ Active (Defender for Office 365) |
| Alert triage | ✅ Manual (Defender portal) |
| Incident response documentation | ✅ In progress |
| SIEM correlation | ⚠️ Not available (Business Premium) |
| Automated response playbooks | ⚠️ Limited (no Sentinel) |

### 6.2 Incident Response Process (Lean Model)

**Detection:**
- Defender for Business alerts
- Entra sign-in anomalies (Log Analytics)
- User-reported incidents

**Triage:**
- Review Defender incident queue
- Cross-reference Entra sign-in logs
- Assess scope (single user vs. tenant-wide)

**Containment:**
- Disable compromised account in Entra ID
- Revoke active sessions (Entra → Revoke Sign-in Sessions)
- Isolate endpoint via Defender (device isolation)
- Block sender / update DLP policy if email-borne

**Recovery:**
- Reset credentials + re-enroll MFA
- Re-image endpoint via Autopilot if necessary
- Review and close Defender incident

**Post-Incident:**
- Document timeline and actions taken
- Update Conditional Access / DLP policies as needed
- Review Secure Score impact

### 6.3 Licensing Gap: SIEM

Microsoft Sentinel is not available under Business Premium. Evaluated for Phase 4 roadmap. Current compensating posture:
- Manual log review via Log Analytics KQL
- Defender portal alert monitoring
- Structured incident response process documented above
