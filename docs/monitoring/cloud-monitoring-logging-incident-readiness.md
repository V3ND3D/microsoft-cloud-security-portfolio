# Cloud Monitoring, Logging & Incident Readiness Architecture
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Last Updated: March 2026 | Version: 2.0*

---

## Monitoring Architecture

No Sentinel (M365 Business Premium licensing constraint). Log Analytics + KQL is the detection layer.

## Azure Log Analytics Workspace

Workspace: `law-mosaic-security`

Log categories forwarded via Entra diagnostic settings:
- Interactive sign-in logs
- Non-interactive sign-in logs
- Service principal sign-in logs
- Audit logs (directory changes, admin actions)
- Risk detection events (Entra P1 scope)

## KQL Detection Queries

```kql
// Failed sign-ins by user — last 24 hours
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType != "0"
| summarize FailureCount = count() by UserPrincipalName, ResultDescription
| order by FailureCount desc

// Admin role assignments — last 7 days
AuditLogs
| where TimeGenerated > ago(7d)
| where OperationName contains "Add member to role"
| project TimeGenerated, InitiatedBy, TargetResources
```

## Secure Score Governance

Secure Score tracked as primary posture metric. Progression: ~40% → **>96%**. Weekly regression checks performed. Score drops investigated before next working day.

## Alert Cadence

| Frequency | Activity |
|-----------|----------|
| Daily | Defender for Business alert triage |
| Weekly | Secure Score review and regression check |
| Monthly | Log Analytics sign-in anomaly review |
| On-event | Conditional Access block review |

## Incident Readiness

IR Plan v1.0 active — HIPAA §164.308(a)(6) compliant. Covers all 8 Meraki sites, M365 tenant, PACS systems, Linux AI servers, and iPads. 7 IR runbooks operational.
