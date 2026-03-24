# Network & Physical Infrastructure Security Architecture
**Eric Feldmann, LLC / Mosaic Diagnostic Imaging**
*Last Updated: March 2026 | Version: 2.0*

---

## Deployed Sites

| Site | Status |
|------|--------|
| Puerto Rico (PR) | ✅ Reference site — fully hardened |
| Newark, DE | 🔄 Pending physical MX75 reconnection |
| Seaford, DE | ⏳ Replication queued |
| Milford, DE | ⏳ Replication queued |
| New York Site 1 | ⏳ Topology verification required |
| New York Site 2 | ⏳ Topology verification required |

## Core Architecture Per Site

- Verizon Business ISP gateway (wireless radios disabled)
- Cisco Meraki MX75 — routing, stateful firewall, AutoVPN, IDS
- Business-class PoE switches
- Meraki 150AX wireless access point
- UPS battery backup
- Private subnet: `172.31.x.0/24` per site
- DHCP and NAT centralized via MX appliance
- UPnP disabled at gateway level

## Firewall Hardening Standard (PR Reference)

### L3 Outbound Deny Rules (9 rules)
| Port | Protocol | Service |
|------|----------|---------|
| 23 | TCP | Telnet |
| 25 | TCP | SMTP outbound |
| 135 | TCP | RPC |
| 137-139 | TCP+UDP | NetBIOS |
| 445 | TCP | SMB |
| 1080 | TCP | SOCKS proxy |
| 3389 | TCP | RDP |
| 4444 | TCP | Metasploit default |

### L7 & Content Controls
- L7 category blocking: Gaming, Sports, Video/Music, Blogging, Advertising
- Content Filtering: full threat + content categories
- Safe Search enforcement, YouTube Strict mode
- Cisco AMP (Advanced Malware Protection) enabled
- IDS in Prevention/Security mode
- IP spoofing protection enabled
- No port forwarding rules

## AutoVPN Architecture

- Hub-and-spoke topology — PR as hub
- Encrypted site-to-site tunnels across all 6 sites
- Centralized east-west traffic visibility

## Cisco Duo RADIUS MFA — Client VPN

Deployed March 13, 2026. Closes compensating control CC-VPN-001. Satisfies Beazley Q5.

| Component | Detail |
|-----------|--------|
| Duo Auth Proxy version | 6.6.0 |
| Host OS | Ubuntu 24.04.4 LTS |
| Server | mdi-app-server-prod (172.31.200.51) |
| RADIUS port | 1812 |
| Service account | duo_authproxy_svc (non-privileged, no login shell) |
| Systemd service | duoauthproxy.service (auto-start) |
| Failmode | Safe |

**Auth flow:** `VPN Client → Meraki MX75 → Duo Auth Proxy :1812 → Duo Cloud → MFA push → access granted`

## AI Server Physical Controls

Two Linux AI servers at PR site (n8n + Docker + Ollama, ePHI-adjacent):
- LVM full disk encryption
- Wired-only — no Wi-Fi or Bluetooth
- Physically secured at PR site
- Non-privileged service accounts
- SSH hardening in progress
- Log forwarding to Log Analytics in implementation
