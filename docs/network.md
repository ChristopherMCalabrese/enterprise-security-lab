# Network Design

## Overview

The network is designed around the principle of segmentation. Rather than placing every device on a single trusted network, systems are separated into dedicated VLANs based on their purpose and required level of access. This approach reduces the potential impact of a compromised device while improving visibility and control over network traffic.

OPNsense serves as the routing, firewall, and DHCP platform, while UniFi provides switching and wireless infrastructure.

---

# Physical Topology

```text
Internet (Cox)

        │

Cox Gateway
        │
WAN (192.168.0.x)

        │

OPNsense Firewall
        │
LAN (10.10.10.1)

        │

UniFi Pro XG
        │
10 Gb Uplink
        │
UniFi Pro Max 16 PoE
        │
─────────────────────────────────────
│                │                 │
Clients      Wireless AP      Infrastructure
```

---

# Network Infrastructure

| Device               | Address     | Purpose                      |
| -------------------- | ----------- | ---------------------------- |
| OPNsense             | 10.10.10.1  | Firewall, Routing, DHCP, DNS |
| UniFi Pro XG         | 10.10.10.2  | Core Switching               |
| UniFi Pro Max 16 PoE | 10.10.10.3  | Access Switching             |
| UniFi U7 Pro Max     | 10.10.10.4  | Wireless                     |
| Unraid               | 10.10.10.10 | Infrastructure & Docker Host |

Infrastructure devices use static IP assignments while client systems receive addresses through DHCP.

---

# VLAN Design

## Main Network

**Subnet:** 10.10.10.0/24

Primary trusted network used for workstations, servers, and management.

---

## IoT Network

**Subnet:** 192.168.20.0/24

Devices with limited trust are isolated from the primary network to reduce the attack surface if an IoT device is compromised.

SSID:

* Covid-19-IoT

---

## Media Network

**Subnet:** 192.168.30.0/24

Dedicated network for media devices to reduce unnecessary communication with trusted systems.

SSID:

* DIRECT-TV-4K

---

## Guest Network

**Subnet:** 192.168.40.0/24

Provides Internet access for guest devices while preventing access to trusted internal resources.

SSID:

* The Force

---

# DHCP

Dnsmasq provides DHCP services for all VLANs.

Configuration includes:

* Static leases for infrastructure devices
* Dynamic address pools for client devices
* Centralized DHCP management

ISC DHCP has been disabled to eliminate service conflicts.

---

# DNS

Unbound provides local DNS resolution.

Security enhancements include:

* HaGeZi Multi Normal blocklist
* Steven Black blocklist

These blocklists reduce access to known malicious, advertising, and tracking domains.

---

# Secure Remote Access

WireGuard provides encrypted remote connectivity into the environment.

Remote administration is performed through the VPN rather than exposing management interfaces directly to the Internet.

---

# Design Principles

The network is built around several core principles:

* Minimize the attack surface through segmentation.
* Separate trusted and untrusted devices.
* Centralize routing and policy enforcement.
* Prefer secure remote access over exposed management services.
* Maintain visibility through monitoring and logging.
