# Asset Inventory

## Overview

This document provides an inventory of the systems and infrastructure that make up the Enterprise Security Lab. It documents each asset's role, purpose, operating system, and function within the environment.

Maintaining an accurate asset inventory is a foundational cybersecurity practice that supports asset management, vulnerability management, incident response, and change management. This inventory serves as the authoritative reference for the lab environment and is updated as the infrastructure evolves.

> [!NOTE]
> Hostnames, network topology, and infrastructure details have been sanitized where appropriate. No production credentials, public IP addresses, or sensitive configuration data are included in this repository.

---

| Asset ID | Hostname | Classification | Role | Purpose | Operating System | Network | Status |
|----------|----------|----------------|------|---------|------------------|---------|--------|
| INF-001 | Proxmox | Infrastructure | Hypervisor | Virtualization platform hosting enterprise infrastructure | Proxmox VE 9 | Infrastructure | Production |
| INF-002 | OPNsense | Infrastructure | Firewall | Routing, firewall, DHCP, DNS, WireGuard VPN | OPNsense | Infrastructure | Production |
| VM-001 | DC01 | Server | Domain Controller | Active Directory, Active Directory-integrated DNS, and Group Policy | Windows Server 2022 | Main (10.10.10.0/24) | Production |
| VM-002 | WIN11-01 | Workstation | Domain Workstation | Domain-joined Windows Enterprise endpoint for administration, security monitoring, and testing | Windows 11 Enterprise | Main (DHCP) | Production |
| VM-003 | UBU01 | Server | Linux Server | Docker-hosted security services | Ubuntu Server | Main | Planned |
| VM-004 | ATTACK01 | Workstation | Attack Workstation | Atomic Red Team and adversary emulation | Windows 11 Enterprise | Isolated Lab VLAN | Planned |

---

## Current Environment Summary

| Category | Count |
|----------|------:|
| Hypervisors | 1 |
| Firewalls | 1 |
| Domain Controllers | 1 |
| Windows Workstations | 1 |
| Linux Servers | 0 |
| Attack Workstations | 0 |

---

**Document Owner:** Christopher M. Calabrese

**Last Updated:** 2026-07-11

**Environment:** Enterprise Security Lab
