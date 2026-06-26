# Network Design

## Overview

The network is designed around the principle of segmentation. Rather than placing every device on a single trusted network, systems are separated into dedicated VLANs based on their purpose and required level of access. This approach reduces the potential impact of a compromised device while improving visibility and control over network traffic.

OPNsense serves as the routing, firewall, DHCP, and DNS platform, while UniFi provides switching and wireless infrastructure.

---

## Network Design Philosophy

The environment follows a defense-in-depth approach rather than relying on a single security control. Security is applied through multiple complementary layers, including network segmentation, firewall policy, DNS filtering, intrusion detection, secure remote access, and centralized monitoring.

Design principles include:

* Network segmentation using VLANs
* Centralized routing and firewall policy enforcement
* Dedicated infrastructure addressing
* Secure remote administration through WireGuard VPN
* Layered monitoring and intrusion detection
* DNS-based threat reduction using blocklists

---

## Physical Topology

```text
                    Internet (Cox)
                          │
                    Cox Gateway
                          │
                  WAN (192.168.0.x)
                          │
                    OPNsense Firewall
                     LAN (10.10.10.1)
                          │
                    UniFi Pro XG
                     10 Gb Uplink
                          │
               UniFi Pro Max 16 PoE
                          │
      ┌────────────┬────────────┬────────────┐
      │            │            │
   Clients     Wireless AP   Infrastructure
```

---

## Core Infrastructure

| Device               | Address     | Purpose                      |
| -------------------- | ----------- | ---------------------------- |
| Cox Gateway          | 192.168.0.1 | ISP Edge Router              |
| OPNsense             | 10.10.10.1  | Firewall, Routing, DHCP, DNS |
| UniFi Pro XG         | 10.10.10.2  | Core Switching               |
| UniFi Pro Max 16 PoE | 10.10.10.3  | Access Switching             |
| UniFi U7 Pro Max     | 10.10.10.4  | Wireless Access Point        |
| Unraid               | 10.10.10.10 | Infrastructure & Docker Host |

---

## Network Segmentation

The environment is divided into dedicated VLANs based on trust level and device purpose.

### Main Network

**Subnet:** 10.10.10.0/24

Primary trusted network used for workstations, servers, and infrastructure management.

**SSID:** Linksys501

---

### IoT Network

**Subnet:** 192.168.20.0/24

IoT devices are isolated from trusted systems to reduce the impact of a compromised smart device.

**SSID:** Covid-19-IoT

---

### Media Network

**Subnet:** 192.168.30.0/24

Dedicated network for streaming and media devices, minimizing unnecessary communication with trusted systems.

**SSID:** DIRECT-TV-4K

---

### Guest Network

**Subnet:** 192.168.40.0/24

Provides Internet access for guest devices while preventing access to trusted internal resources.

**SSID:** The Force

---

## DHCP

Dnsmasq provides DHCP services across all network segments.

Configuration includes:

* Dynamic address pools for client devices
* Static reservations for infrastructure devices
* Centralized DHCP management across all VLANs

ISC DHCP has been disabled to eliminate service conflicts.

---

## DNS

Unbound provides local DNS resolution and DNS-based threat reduction.

Current protection includes:

* HaGeZi Multi NORMAL blocklist
* Steven Black blocklist

These blocklists reduce access to known malicious, advertising, and tracking domains before connections are established.

---

## Secure Remote Access

WireGuard provides encrypted remote connectivity into the environment.

Administrative access is performed through the VPN rather than exposing management interfaces directly to the Internet.

---

## Intrusion Detection

Suricata is deployed on the WAN interface in IDS mode with approximately 41,000 detection rules.

Running in IDS mode allows alerts to be evaluated and tuned before considering IPS enforcement, reducing the likelihood of unnecessary false positives.

---

## Design Decisions

### Why OPNsense?

I selected OPNsense because it provides enterprise-class routing, firewalling, WireGuard integration, Suricata IDS, DNS filtering, and extensive monitoring while remaining open source. It allows me to build practical experience with technologies commonly deployed in SMB and enterprise environments.

### Why VLAN Segmentation?

Rather than relying on endpoint security alone, the network separates devices according to trust level and function. This limits unnecessary communication between systems and reduces the potential impact of a compromised endpoint.

### Why WireGuard?

WireGuard provides secure, encrypted remote administration without exposing management interfaces directly to the public Internet.

---

## Future Improvements

* Create a dedicated Management VLAN for infrastructure devices.
* Expand Active Directory deployment.
* Integrate Microsoft Entra ID with on-premises identity.
* Forward Suricata alerts into Wazuh for centralized security monitoring.
* Continue documenting architecture changes and security decisions as the environment evolves.
