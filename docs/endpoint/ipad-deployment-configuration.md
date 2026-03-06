# iPad Deployment & Configuration Record

**Organization:** Eric Feldmann, LLC — Mosaic Diagnostic Imaging
**Control Owner:** Yeray Y. Lafontaine Martinez
**Program Phase:** Operational Deployment
**Status:** Active — Point-in-Time Deployment Record
**Last Updated:** February 2026

---

## 1. Purpose & Scope

This document records the deployment and configuration of Apple iPad devices used for front desk patient intake across clinical office locations. Devices are designated strictly for patient intake form submission via browser-based workflow at [lobbie.com](https://www.lobbie.com).

This document provides configuration transparency for auditing, operational continuity, and future MDM enrollment alignment.

---

## 2. Deployment Rationale

iPads were configured using the dedicated organizational Apple ID: `applemdm@mosaicdiagnostic.com`

This approach was selected due to missing documentation required for Apple Business Manager (ABM) enrollment at the time of deployment. To prevent operational delays at clinical offices, devices were manually configured to ensure timely rollout.

**This manual configuration state is documented as transitional and operationally necessary.**

---

## 3. Planned MDM Transition

Upon receipt of required documentation (DUNS registration + ABM eligibility):

1. Apple Business Manager enrollment
2. Supervised device enrollment
3. Integration into MDM governance (Intune)
4. Centralized auditing and lifecycle control
5. Removal of manual Screen Time configuration (replaced by MDM-pushed profiles)

---

## 4. Standardized Configuration

All deployed iPads follow identical configuration to ensure consistent, business-only usage:

| Control | Setting |
|---------|---------|
| Apple ID | Shared organizational account (`applemdm@mosaicdiagnostic.com`) |
| Screen Time | Enabled with shared passcode |
| App Store | Disabled (no new installs permitted) |
| App Deletion | Restricted |
| Account Modification | Restricted |
| In-App Purchases | Disabled |
| AirDrop | Disabled |
| Time-Based Limits | Enforced (business hours only) |
| Primary Use | lobbie.com patient intake (Safari) |

---

## 5. Security Posture Assessment

| Control Area | Status | Notes |
|-------------|--------|-------|
| MDM Enrollment | ❌ Not enrolled | Transitional — ABM planned |
| Device Encryption | ✅ Native iOS encryption | Enabled by default on modern iPads |
| App Restriction | ✅ Screen Time enforced | Manual — to be replaced by MDM |
| Network | ✅ Site Wi-Fi only | No cellular data |
| Physical Access | ✅ Front desk only | Supervised use during intake |
| PHI Exposure | ⚠️ Limited | Intake forms only; no PHI stored locally |

---

## 6. Compensating Controls

Given the transitional MDM state, the following compensating controls are in place:

- **Dedicated Apple ID** — organizational account, not personal
- **Screen Time passcode** — prevents configuration changes by unauthorized users
- **Single-purpose use** — devices configured for lobbie.com intake workflow only
- **Physical supervision** — devices remain at front desk under staff supervision during business hours
- **No local PHI storage** — intake workflow is browser-based; no data persists on device

---

## 7. Remediation Roadmap

| Action | Dependency | Target Phase |
|--------|-----------|--------------|
| Obtain DUNS registration | Organization admin | Phase 1 |
| Enroll in Apple Business Manager | DUNS + ABM approval | Phase 1 |
| Configure Intune MDM for supervised iPads | ABM enrollment | Phase 2 |
| Deploy managed app configuration for lobbie.com | Intune enrollment | Phase 2 |
| Retire manual Screen Time configuration | MDM enforcement active | Phase 2 |
