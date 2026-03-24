# 2026 Security Program Roadmap
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Owner: Yeray Y. Lafontaine | Last Updated: March 2026*

---

## Objective

Build a security posture defensible enough to self-insure — transitioning from annual cyber coverage to a per-incident model backed by a funded reserve. **Target: July 2026.**

---

## Phase Overview

| Phase | Name | Status |
|-------|------|--------|
| Phase 0 | Stabilization | ✅ Complete |
| Phase 1 | Identity Consolidation | ✅ Complete |
| Phase 2 | Resilience & IR Readiness | ✅ Complete |
| Phase 3 | Monitoring Operationalization | 🔄 In Progress |
| Phase 4 | Network Replication | 🔄 In Progress |

---

## Phase 0 — Stabilization ✅

- Defined program roadmap
- Froze new tool deployment
- Established weekly security engineering block
- Documented cyber insurance value/cost
- Obtained executive sign-off on per-incident insurance strategy
- Established Cyber Incident Reserve Fund planning

---

## Phase 1 — Identity Consolidation ✅

- Audited Google Workspace; applied OAuth restrictions
- Enforced MFA universally via Conditional Access
- Cleaned up admin roles — scoped RBAC, removed standing Global Admin
- Validated break-glass governance
- Blocked legacy authentication across all protocols
- Implemented Windows LAPS; eliminated standing local admin

---

## Phase 2 — Resilience & IR Readiness ✅

- Authored IR Plan v1.0 (HIPAA §164.308(a)(6))
- Authored Incident Severity Classification Matrix (P1–P4)
- Authored IR Playbook with 7 runbooks
- Authored HIPAA Breach Determination Worksheet
- Authored Post-Incident Review Template
- Deployed Cisco Duo RADIUS MFA for Client VPN
- Completed Beazley cyber insurance application (Q1–Q24)
- Conducted internal vulnerability assessment (Nmap + Nessus)
- Authored Cyber Incident Reserve Fund proposal

---

## Phase 3 — Monitoring Operationalization 🔄

- ✅ Log Analytics workspace (`law-mosaic-security`) validated
- ✅ KQL queries built for identity anomaly detection
- ⏳ Formal alert review cadence — defining
- ⏳ SSH audit log forwarding from AI servers → Log Analytics
- ⏳ Sentinel evaluation — deferred pending licensing budget

---

## Phase 4 — Network Replication 🔄

- ✅ PR site — reference template complete
- ⏳ Seaford, DE — queued
- ⏳ Milford, DE — queued
- 🔄 Newark, DE — pending physical MX75 reconnection + static IP
- ⏳ NY Site 1 — topology verification required
- ⏳ NY Site 2 — topology verification required

> P2P blocking evaluated per-site. PACS/clinical sites require DICOM traffic — blanket P2P blocking is not appropriate.

---

## Open Items

**Infrastructure:**
- Newark MX75 physical reconnection + static IP configuration
- Firewall template replication to 5 remaining sites
- Client VPN access audit
- Meraki Dashboard 2FA enforcement
- mricom.com Cloudflare org transfer

**Security/Compliance:**
- Disable SSH password auth on AI servers
- SSH logs → Log Analytics
- Remove personal Gmail from GTM admin
- Confirm GTM not on ePHI-touching pages
- Confirm Brandon formal BAA status
- DeepSeek replacement evaluation (Llama/Mistral/Phi)
