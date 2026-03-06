# Identity & Access Security Architecture

**Organization:** Eric Feldmann, LLC
**Control Owner:** Yeray Y. Lafontaine Martinez
**Program Phase:** Cloud Security Establishment (Phase 1–2)
**Status:** Active — Point-in-Time Configuration Snapshot
**Last Updated:** February 2026

---

## 1. Purpose & Scope

This document defines the identity architecture, authentication controls, access governance model, and emergency access framework implemented within Microsoft Entra ID. It establishes:

- Authoritative identity control boundaries
- Conditional Access enforcement design
- Multi-factor authentication posture
- Emergency (Break-Glass) access governance
- Logging and audit visibility
- Licensing constraints under Microsoft 365 Business Premium

---

## 2. Identity Authority & Tenant Model

### 2.1 Directory Architecture

Microsoft Entra ID serves as the single authoritative identity provider for:
- User authentication
- Device trust
- Application access mediation
- Conditional Access enforcement
- Role-based administration

**Environment model:**
- Cloud-native (no on-premises Active Directory)
- Entra ID joined Windows 11 Pro endpoints
- Microsoft 365 Business Premium licensed
- No hybrid identity infrastructure

### 2.2 Licensing Boundary (Business Premium)

Available under Business Premium (Entra ID P1):
- Conditional Access
- MFA enforcement
- Self-Service Password Reset (SSPR)
- Group-based access management
- Entra ID joined device management

Not available (Entra ID P2):
- Identity Protection (risk-based Conditional Access)
- Privileged Identity Management (PIM)
- Access Reviews (automated)
- Entitlement Management

---

## 3. Authentication Controls

### 3.1 MFA Posture

- Tenant-wide MFA enforcement via Conditional Access (not Security Defaults)
- Primary method: Microsoft Authenticator (push notification)
- Phishing-resistant method: FIDO2 security keys (available, user-configured)
- Legacy authentication: Blocked tenant-wide via dedicated Conditional Access policy

### 3.2 Authentication Methods Policy

| Method | Status |
|--------|--------|
| Microsoft Authenticator | Enabled — primary |
| FIDO2 Security Keys | Enabled |
| SMS / Voice | Disabled |
| Email OTP | Disabled |
| Temporary Access Pass | Enabled (admin-issued for onboarding) |

---

## 4. Conditional Access Architecture

### 4.1 Policy Design Principles

- All policies are enforced in **Report-Only mode first**, then converted to **Enabled** after validation
- Break-Glass accounts are excluded from all Conditional Access policies
- Policies are scoped to All Users unless explicitly targeted

### 4.2 Core Policy Set

| Policy | Scope | Enforcement |
|--------|-------|-------------|
| Require MFA — All Users | All users, all apps | MFA required |
| Block Legacy Authentication | All users | Block |
| Require Compliant Device | All users, cloud apps | Device compliance required |
| Require MFA — Admin Roles | Directory roles | MFA required |
| Block Risky Sign-ins | All users | Block (within P1 limits) |

---

## 5. RBAC & Least Privilege Model

### 5.1 Role Assignment Principles

- Permanent Global Administrator assignments minimized to 2 accounts maximum (primary admin + break-glass)
- Scoped roles assigned where possible (e.g., Intune Administrator, Security Reader)
- No standing broad admin rights for operational tasks
- Service accounts scoped to minimum required permissions

### 5.2 Role Structure

| Role | Assignment Type | Notes |
|------|----------------|-------|
| Global Administrator | Permanent | Primary admin + break-glass only |
| Intune Administrator | Permanent | Endpoint management |
| Security Reader | Permanent | Security monitoring |
| User Administrator | Permanent | User lifecycle management |

---

## 6. Emergency Access (Break-Glass) Governance

Aligned to **HIPAA §164.312(a)(2)(i)** — Emergency Access Procedure.

### 6.1 Account Configuration

- 2 dedicated break-glass accounts provisioned
- Named with clearly identifiable convention (not tied to individual identity)
- Cloud-only accounts (not synced, not federated)
- Global Administrator role assigned permanently
- **Excluded from all Conditional Access policies**
- MFA registered using FIDO2 hardware key stored securely offline

### 6.2 Monitoring

- Sign-in activity monitored via Azure Log Analytics
- Any break-glass sign-in triggers immediate review
- Accounts tested quarterly to confirm accessibility

---

## 7. Identity Logging & Audit Visibility

### 7.1 Log Categories Collected

- Interactive sign-ins
- Non-interactive sign-ins
- Service principal sign-ins
- Administrative directory changes
- Risk detection events (P1 scope)
- Audit logs (user/group/role changes)

### 7.2 Diagnostic Settings Configuration

Entra tenant-level diagnostic settings forward logs to:

**Azure Log Analytics Workspace:** `law-mosaic-security`

Log retention: 30 days (default Log Analytics free tier); extended retention planned.

### 7.3 Key KQL Queries

```kql
// Break-glass sign-in detection
SigninLogs
| where UserPrincipalName contains "breakglass"
| project TimeGenerated, UserPrincipalName, IPAddress, ResultType, Location

// Failed sign-ins (last 24h)
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType != 0
| summarize FailureCount = count() by UserPrincipalName, IPAddress
| order by FailureCount desc

// Legacy authentication attempts
SigninLogs
| where ClientAppUsed in ("Exchange ActiveSync", "IMAP4", "POP3", "SMTP Auth", "Other clients")
| project TimeGenerated, UserPrincipalName, ClientAppUsed, IPAddress
```

---

## 8. Google Workspace Security Controls

The organization maintains a Google Workspace tenant in parallel. Hardening applied:
- OAuth application restrictions enforced
- Third-party application access governance
- Admin account MFA enforced
- Planned: Full migration to Microsoft 365 as authoritative platform (Phase 1 roadmap)
