# iPad Deployment & Configuration Record
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Last Updated: March 2026 | Version: 1.0*

---

## Purpose

Documents the deployment of Apple iPad devices for front desk patient intake across clinical office locations. Devices are used exclusively for patient intake form submission via browser-based workflow at lobbie.com.

## Current State

Devices configured using dedicated organizational Apple ID (`applemdm@mosaicdiagnostic.com`). Apple Business Manager enrollment was not possible at time of deployment due to missing DUNS documentation.

## Configuration Standards

- Single dedicated Apple ID across all devices
- Screen Time enabled with shared configuration
- Time-based usage limitations enforced
- App Store installation restrictions enabled
- Browser restricted to intake workflow URL

## MDM Gap & Compensating Controls

iPads are not enrolled in Intune MDM. This is a documented exception. Current compensating controls:
- Screen Time restrictions limit device usage scope
- Devices are physically supervised at front desk
- No ePHI stored locally on devices
- iCloud Find My enabled for lost/stolen device response

## Roadmap

Upon receipt of DUNS registration documentation:
1. Apple Business Manager enrollment
2. Supervised device mode
3. Intune MDM integration
4. Centralized auditing and lifecycle control
