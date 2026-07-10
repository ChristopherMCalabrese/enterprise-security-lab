# Network Design

## Overview

This homelab was designed to simulate a modern small-to-medium business network while providing a platform for learning enterprise networking, systems administration, monitoring, and security.

Rather than placing every device on a single trusted network, systems are separated into dedicated VLANs based on purpose and trust level. Security is enforced through layered controls including network segmentation, centralized firewall policies, DNS filtering, intrusion detection, secure remote access, and infrastructure monitoring.

Core infrastructure consists of OPNsense, UniFi switching and wireless, an Unraid storage platform, and a Docker-based services environment.

---

# Design Philosophy

The environment follows a defense-in-depth strategy.

Security is implemented using multiple overlapping controls rather than relying on any single technology.

Primary objectives include:

- Network segmentation
- Least-privilege firewall policies
- Secure remote administration
- DNS filtering
- Intrusion detection
- Infrastructure monitoring
- Centralized logging
- High availability where practical

---

# Physical Topology

```text
                Internet
                    │
              ISP Gateway
                    │
             OPNsense Firewall
                    │
             Core 10Gb Switch
                    │
          Access PoE Switch
                    │
      ┌─────────┬──────────┬───────────┐
      │         │          │
   Storage    Wireless   Client Devices
   Platform      AP
      │
 Docker Infrastructure
```

---

# Core Infrastructure

| Component | Purpose |
|-----------|---------|
| OPNsense | Firewall, Routing, DHCP, DNS |
| UniFi Switching | Layer 2 switching |
| UniFi Wireless | Wireless networking |
| Storage Platform | File storage and Docker host |
| AdGuard Home | DNS filtering |
| IPMI | Out-of-band server management |
| Grafana | Visualization |
| InfluxDB | Time-series database |
| Telegraf | Metrics collection |
| Wazuh | Endpoint monitoring |
| CrowdSec | Threat detection |

---

# Network Segmentation

The network is divided into multiple VLANs based on trust level.

## Trusted Network

Used for workstations, servers, and administrative systems.

---

## IoT Network

Dedicated network for smart home devices.

Traffic is isolated from trusted systems through firewall policy.

---

## Media Network

Dedicated network for streaming devices.

---

## Guest Network

Internet-only access for guest devices.

Internal resources remain inaccessible.

---

# DHCP

Centralized DHCP services provide:

- Dynamic address allocation
- Static infrastructure reservations
- VLAN-aware address scopes
- Centralized lease management

---

# DNS

DNS services combine a local resolver with DNS filtering.

Responsibilities include:

- Local hostname resolution
- DNS caching
- Malware protection
- Ad and tracker blocking
- DNS query logging

Layered DNS filtering reduces access to malicious domains before connections are established.

---

# Firewall

Centralized firewall policies enforce communication between VLANs.

Examples include:

- Guest network restricted to Internet access
- IoT devices isolated from trusted systems
- Infrastructure services accessible only from trusted networks
- Explicitly permitted inter-VLAN communication

---

# Secure Remote Access

Remote administration is performed through WireGuard VPN.

Management interfaces are not exposed directly to the Internet.

---

# Intrusion Detection

Suricata monitors WAN traffic using community threat signatures.

IDS mode is used for alerting while minimizing operational impact.

---

# Monitoring

Infrastructure monitoring is performed using:

- Grafana
- InfluxDB
- Telegraf
- UniFi Poller

Collected metrics include:

- CPU utilization
- Memory utilization
- Storage utilization
- Network throughput
- Interface statistics
- System temperatures

---

# Containerized Services

The storage platform hosts infrastructure applications using Docker.

Representative services include:

- DNS filtering
- Infrastructure monitoring
- Network management
- Home automation
- Media management
- Password management
- Photo management
- Security monitoring

Docker simplifies deployment, upgrades, and application isolation.

---

# Storage Platform

The storage environment provides:

- Parity-protected storage
- SSD cache
- Container hosting
- Network file shares
- Backup storage

The platform supports both infrastructure services and user data while allowing online expansion.

---

# Out-of-Band Management

Dedicated server management hardware provides:

- Remote power control
- Hardware health monitoring
- BIOS access
- Remote console
- KVM over IP

This enables hardware administration independent of the operating system.

---

# Design Decisions

## Why OPNsense?

Provides enterprise-class routing, firewalling, VPN, IDS, DNS services, and monitoring while remaining open source.

---

## Why VLAN Segmentation?

Separating devices according to trust level limits lateral movement and reduces the impact of compromised systems.

---

## Why Docker?

Containerization provides application isolation, simplified deployment, reproducible environments, and efficient resource utilization.

---

## Why WireGuard?

WireGuard provides secure, high-performance remote administration without exposing management services directly to the Internet.

---

# Lessons Learned

Building and operating this environment provided hands-on experience with:

- Enterprise firewall administration
- VLAN design
- DNS architecture
- Docker administration
- Infrastructure monitoring
- Storage management
- Secure remote access
- IDS deployment
- Incident troubleshooting
- Infrastructure documentation
- Change management

Real-world troubleshooting included storage recovery, parity rebuilds, DNS architecture redesign, container debugging, and service restoration.

---

# Future Improvements

- Dedicated management network
- Automated infrastructure backups
- Infrastructure-as-Code
- Centralized identity services
- Enhanced security monitoring
- Automated alerting
- Additional monitoring integrations
- Configuration management
