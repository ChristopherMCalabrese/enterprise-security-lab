# Network Design

## Overview

The network is designed around the principle of segmentation. Rather than placing every device on a single trusted network, systems are separated into dedicated VLANs based on their purpose and required level of access. This approach reduces the potential impact of a compromised device while improving visibility, security, and control over network traffic.

The environment is built around OPNsense for routing and security, UniFi for switching and wireless infrastructure, and Unraid as the primary infrastructure and application platform. Core services are containerized using Docker and centrally monitored through Grafana and InfluxDB.

---

## Network Design Philosophy

The environment follows a defense-in-depth strategy rather than relying on a single security control. Security is applied through multiple complementary layers, including network segmentation, firewall policy, DNS filtering, intrusion detection, secure remote access, and centralized monitoring.

Key design principles include:

- Network segmentation using dedicated VLANs
- Centralized routing and firewall policy enforcement
- Dedicated infrastructure addressing
- Secure remote administration using WireGuard VPN
- DNS-based filtering through AdGuard Home
- Intrusion detection using Suricata
- Infrastructure monitoring using Grafana, InfluxDB, and Telegraf
- Out-of-band server management through IPMI

---

## Physical Topology

```text
                    Internet (Cox)
                          │
                    Cox Gateway
                          │
                    OPNsense Firewall
                     10.10.10.1
                          │
                  UniFi Pro XG (Core)
                     10 Gb Uplink
                          │
               UniFi Pro Max 16 PoE
                          │
     ┌─────────────┬──────────────┬──────────────┐
     │             │              │
  Unraid       UniFi U7 Pro     Client Devices
     │
 Docker Infrastructure
 │
 ├── AdGuard Home
 ├── Grafana
 ├── InfluxDB
 ├── Home Assistant
 ├── UniFi Network Application
 ├── UniFi Poller
 ├── Plex
 ├── Immich
 ├── Vaultwarden
 ├── Sonarr
 ├── Radarr
 ├── Prowlarr
 ├── qBittorrent
 ├── CrowdSec
 └── Wazuh Agent
```

---

# Core Infrastructure

| Device / Service | Address | Purpose |
|------------------|----------|---------|
| Cox Gateway | 192.168.0.1 | ISP edge gateway |
| OPNsense (bastion.internal) | 10.10.10.1 | Firewall, inter-VLAN routing, Kea DHCP, Unbound DNS |
| UniFi USW Pro XG | 10.10.10.2 | Core switching |
| UniFi USW Pro Max 16 PoE | 10.10.10.3 | Access and PoE switching |
| UniFi U7 Pro Max | 10.10.10.4 | Wireless access point |
| AdGuard Home | 10.10.10.5 | DNS filtering and upstream DNS resolution |
| Unraid (tower) | 10.10.10.10 | Storage, Docker, monitoring, and application hosting |
| Tower IPMI (ipmi.home.arpa) | 10.10.10.11 | Out-of-band management, remote KVM, hardware monitoring |
| UniFi Network Application | https://10.10.10.10:8443 | Network management platform |

---

# Network Segmentation

The environment is divided into dedicated VLANs based on trust level and device purpose.

## Main Network

**Subnet:** 10.10.10.0/24

Primary trusted network used for workstations, servers, management interfaces, and infrastructure.

**SSID:** Linksys501

---

## IoT Network

**Subnet:** 192.168.20.0/24

Dedicated network for smart home and embedded devices. Devices are isolated from trusted systems through firewall policy to reduce attack surface.

**SSID:** Covid-19-IoT

---

## Media Network

**Subnet:** 192.168.30.0/24

Dedicated network for streaming devices and media appliances, reducing unnecessary communication with trusted systems.

**SSID:** DIRECT-TV-4K

---

## Guest Network

**Subnet:** 192.168.40.0/24

Internet-only guest access with no access to trusted internal resources.

**SSID:** The Force

---

# DHCP

Kea DHCP provides centralized address management across all VLANs.

Configuration includes:

- Dynamic address pools
- Static reservations for infrastructure devices
- VLAN-aware DHCP scopes
- Centralized lease management
- Reserved management addressing

Kea was selected as the modern DHCP implementation supported by OPNsense.

---

# DNS

DNS services are provided through OPNsense Unbound and AdGuard Home.

Responsibilities are separated to simplify management and improve security.

### AdGuard Home

- DNS filtering
- Malware protection
- Advertising and tracker blocking
- Upstream DNS forwarding
- Query logging

### Unbound DNS

- Local DNS resolution
- Internal hostname resolution
- DNS forwarding
- DNS caching

Current DNS protection includes:

- HaGeZi Multi NORMAL
- Steven Black Hosts

This layered approach blocks known malicious, advertising, and tracking domains before connections are established.

---

# Firewall

OPNsense provides centralized routing and firewall policy enforcement between VLANs.

Firewall policies are designed using least-privilege principles.

Examples include:

- Guest devices restricted to Internet access only
- IoT devices isolated from trusted systems
- Infrastructure services accessible only from trusted networks
- Inter-VLAN communication explicitly permitted where required

---

# Secure Remote Access

WireGuard provides encrypted remote connectivity into the environment.

Administrative access is performed exclusively through the VPN rather than exposing management interfaces directly to the Internet.

Benefits include:

- Secure remote administration
- Encrypted management traffic
- Reduced attack surface
- Multi-device support

---

# Intrusion Detection

Suricata is deployed on the WAN interface in IDS mode.

Configuration includes approximately 41,000 detection rules.

Running in IDS mode allows alerts to be evaluated and tuned before enabling IPS functionality, reducing unnecessary false positives while maintaining visibility into potential threats.

---

# Monitoring

Infrastructure monitoring is performed using a centralized observability stack.

Components include:

- Grafana
- InfluxDB
- Telegraf
- UniFi Poller
- Wazuh Agent

Collected metrics include:

- CPU utilization
- Memory utilization
- Storage utilization
- Network throughput
- Temperature monitoring
- Interface statistics
- Wireless statistics
- Infrastructure availability

---

# Core Services

The Unraid platform hosts the majority of infrastructure services using Docker.

Core applications include:

- AdGuard Home
- Grafana
- InfluxDB
- Home Assistant
- UniFi Network Application
- UniFi Poller
- Plex Media Server
- Immich
- Vaultwarden
- qBittorrent
- Sonarr
- Radarr
- Prowlarr
- CrowdSec
- Wazuh Agent

Docker allows services to remain isolated while simplifying deployment, upgrades, and backup operations.

---

# Storage Platform

Unraid provides centralized storage and application hosting.

Current configuration includes:

- Single parity protection
- Multiple enterprise-class HDDs
- Dedicated SSD cache
- Docker application hosting
- SMB network shares
- Media storage
- Backup storage

Recent infrastructure improvements included replacement of a failed 16 TB parity drive followed by a complete parity rebuild and validation.

---

# Out-of-Band Management

A dedicated Supermicro IPMI interface provides independent hardware management.

Capabilities include:

- Remote power control
- Hardware health monitoring
- Remote KVM
- BIOS configuration
- Console access independent of the operating system

Management Address:

```
10.10.10.11
```

---

# Design Decisions

## Why OPNsense?

OPNsense provides enterprise-grade firewalling, routing, WireGuard VPN, Suricata IDS, DNS services, and detailed monitoring while remaining open source. It offers practical experience with technologies commonly deployed within SMB and enterprise environments.

---

## Why VLAN Segmentation?

Separating devices according to trust level significantly reduces lateral movement opportunities and minimizes the impact of compromised systems.

---

## Why Unraid?

Unraid combines flexible storage management with integrated Docker virtualization, allowing infrastructure services, monitoring, media applications, and backups to coexist on a single platform while maintaining redundancy and ease of administration.

---

## Why Docker?

Docker provides application isolation, simplified deployment, straightforward upgrades, and reproducible infrastructure while minimizing resource overhead.

---

## Why WireGuard?

WireGuard offers modern cryptography, excellent performance, and secure remote administration without exposing management services to the Internet.

---

## Lessons Learned

Building the environment provided practical experience with:

- Enterprise firewall deployment
- VLAN design
- DNS architecture
- Docker administration
- Infrastructure monitoring
- Storage management
- Secure remote access
- IDS deployment
- Infrastructure troubleshooting
- Documentation and change management

Several real-world incidents—including DNS resolution failures, Docker container troubleshooting, storage hardware replacement, parity rebuilds, and service recovery—provided valuable operational experience beyond initial deployment.

---

# Future Improvements

- Create a dedicated Management VLAN
- Implement automated configuration backups
- Restore Docker container monitoring in Telegraf
- Integrate UPS monitoring and graceful shutdown
- Expand Active Directory deployment
- Integrate Microsoft Entra ID
- Forward Suricata alerts into Wazuh
- Deploy Prometheus alongside InfluxDB
- Continue documenting infrastructure changes and security decisions
- Develop infrastructure-as-code for repeatable deployments
