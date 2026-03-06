# Network & Physical Infrastructure Security Architecture

**Organization:** Eric Feldmann, LLC
**Control Owner:** Yeray Y. Lafontaine Martinez
**Program Phase:** Cloud Security Establishment (Phase 1–2)
**Status:** Active — Point-in-Time Configuration Snapshot
**Last Updated:** February 2026

---

## 1. Purpose & Scope

This document defines the physical infrastructure, network topology, connectivity governance, and site-level security controls deployed across organizational locations. It establishes:

- Network boundary architecture
- Site-to-site connectivity model
- Firewall authority
- Wireless governance
- Non-standard asset physical safeguards
- Deferred segmentation roadmap

---

## 2. Deployed Sites

| Site | Location | Status |
|------|----------|--------|
| Site 1 | Newark, DE | Active |
| Site 2 | Wilmington, DE | Active |
| Site 3 | Dover, DE | Active |
| Site 4 | Milford, DE | Active |
| Site 5 | Seaford, DE | Active |

All sites follow an identical architecture model for consistency and operational simplicity.

---

## 3. Network Architecture

### 3.1 Core Components Per Site

| Component | Model / Type | Role |
|-----------|-------------|------|
| ISP | Verizon Business | WAN connectivity |
| Firewall / Router | Cisco Meraki MX75 | Routing, firewall, AutoVPN termination |
| Switches | Business-class PoE | LAN distribution |
| Wireless AP | Cisco Meraki MR 150AX | Wi-Fi access |
| UPS | Battery backup | Power conditioning |

The Meraki MX75 serves as the authoritative routing and security boundary at every site.

### 3.2 IP Addressing Schema

| Site | Subnet |
|------|--------|
| Newark | 172.31.1.0/24 |
| Wilmington | 172.31.2.0/24 |
| Dover | 172.31.3.0/24 |
| Milford | 172.31.4.0/24 |
| Seaford | 172.31.5.0/24 |

- All sites use RFC 1918 private addressing
- DHCP managed by Meraki MX per site
- No overlapping subnets across sites

### 3.3 WAN Connectivity

| Setting | Configuration |
|---------|--------------|
| ISP | Verizon Business |
| Connection Type | Fiber / Business gateway |
| ISP Gateway Mode | Bridge (MX handles routing) |
| Static IPs | Deferred — pending ISP coordination |
| Failover | Not currently configured |

---

## 4. AutoVPN (Hub-and-Spoke)

### 4.1 Topology

All sites are connected in a **hub-and-spoke AutoVPN** topology managed via Meraki Dashboard.

```
          [Hub — Primary Site]
               |
    ┌──────────┼──────────┐
    │          │          │
[Newark]  [Wilmington] [Dover]
              │
         [Milford]
              │
         [Seaford]
```

### 4.2 AutoVPN Configuration

| Setting | Value |
|---------|-------|
| Mode | Hub-and-spoke |
| Encryption | AES-256 |
| Authentication | Pre-shared key (PSK) |
| Tunnel Type | Full tunnel (split tunnel not used) |
| Management | Centralized via Meraki Dashboard |

---

## 5. Firewall & Security Policy

### 5.1 MX75 Firewall Posture

| Control | Configuration |
|---------|--------------|
| Default inbound rule | Deny all |
| Outbound policy | Permit required business traffic |
| IDS/IPS | Enabled (Meraki Advanced Security) |
| Content filtering | Enabled |
| Geo-IP blocking | Applied to high-risk regions |
| Malware protection | Enabled (Cisco AMP integration) |

### 5.2 DNS

- DNS provided via ISP / Meraki DHCP
- No split-DNS currently configured
- DNS-over-HTTPS: not enforced at network level (enforced via browser policy)

---

## 6. Wireless Architecture

### 6.1 SSID Configuration

| SSID | Purpose | Security |
|------|---------|---------|
| Staff Network | Employee devices | WPA3 / WPA2-Personal, hidden |
| Patient / Guest | Patient intake iPads | Isolated, internet-only, captive portal |

### 6.2 AP Configuration

| Setting | Value |
|---------|-------|
| Model | Cisco Meraki MR 150AX |
| Management | Meraki Dashboard (cloud) |
| Channel | Auto-optimized |
| Band | 2.4GHz + 5GHz (dual-band) |
| Client Isolation | Enabled on guest SSID |

---

## 7. Non-Standard Assets

### 7.1 Linux AI Servers

| Attribute | Detail |
|-----------|--------|
| Purpose | On-site automation / Power Automate workloads |
| OS | Ubuntu Linux |
| Network Connection | Wired only (no Wi-Fi) |
| Encryption | LVM full-disk encryption |
| MDM | Not enrolled |
| Physical Access | Restricted — server room / locked area |
| Roadmap | Security review and potential Defender onboarding (Phase 4) |

### 7.2 iPads (Patient Intake)

See: [iPad Deployment & Configuration Record](../endpoint/ipad-deployment-configuration.md)

---

## 8. Deferred Items & Roadmap

| Item | Status | Target Phase |
|------|--------|-------------|
| Static IP provisioning (all sites) | Deferred — ISP coordination required | Phase 0 |
| VLAN segmentation (staff / clinical / IoT) | Planned | Phase 3 |
| Network Access Control (NAC) | Evaluated post-segmentation | Phase 4 |
| WAN failover / secondary ISP | Evaluated | Phase 4 |
| NVR / IP camera retention policy | Deferred | Phase 3 |
| Sentinel network telemetry ingestion | Pending Sentinel evaluation | Phase 4 |
