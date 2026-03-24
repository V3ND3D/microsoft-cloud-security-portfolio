# Identity & Access Security Architecture
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Last Updated: March 2026 | Version: 2.0*

---

## Directory Architecture

Microsoft Entra ID is the single authoritative identity provider. Cloud-native — no on-premises Active Directory, no hybrid join. All Windows 11 Pro endpoints are Entra ID joined and Intune enrolled.

## Authentication Controls

- Tenant-wide MFA enforced via Conditional Access (per-user MFA disabled)
- Phishing-resistant MFA (FIDO2) for all administrative accounts
- Legacy authentication blocked across all protocols
- Sign-in risk policies within Entra P1 scope

## Conditional Access Design

- Device compliance required — non-compliant devices blocked from all resources
- Named trusted locations configured
- Session controls enforced for sensitive application access
- CA-driven enforcement replaces per-user MFA

## Access Governance

- Least-privilege RBAC — structured security groups, scoped admin roles
- No standing Global Admin for daily operations
- **Windows LAPS deployed** — standing local admin eliminated across all endpoints
- LAPS passwords rotated automatically, escrowed to Entra ID

## Break-Glass Governance

Emergency access accounts maintained per HIPAA §164.312(a)(2)(i). Accounts are cloud-only, excluded from Conditional Access, credentials stored offline, usage monitored via Log Analytics alerts.

## Audit & Logging

Entra diagnostic settings forward to `law-mosaic-security` (Azure Log Analytics):
- Interactive sign-in logs
- Non-interactive sign-in logs
- Audit logs (directory changes, admin actions)
- Risk detection events (Entra P1 scope)

KQL queries built for: failed sign-in patterns, admin role assignments, anomalous access.

## Licensing Boundary

Business Premium provides Entra ID P1. Not included: Entra ID P2 (PIM, Identity Governance, Access Reviews). Missing P2 features are acknowledged and risk-assessed.
