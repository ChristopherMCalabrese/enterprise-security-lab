# Asset Inventory

## Overview

This document provides an inventory of the systems and infrastructure that make up the Enterprise Security Lab. It documents each asset's role, purpose, operating system, and function within the environment.

Maintaining an accurate asset inventory is a foundational cybersecurity practice that supports asset management, vulnerability management, incident response, and change management. This inventory serves as the authoritative reference for the lab environment and is updated as the infrastructure evolves.

> [!NOTE]
> Hostnames, network topology, and infrastructure details have been sanitized where appropriate. No production credentials, public IP addresses, or sensitive configuration data are included in this repository.
> 
---
Asset ID | Hostname | Role              | Purpose                                     | OS                  | Network Zone      | Status     |
-------- | -------- | ----------------- | ------------------------------------------- | ------------------- | ----------------- | ---------- |
VM-001   | DC01     | Domain Controller | Active Directory, DNS, Group Policy         | Windows Server 2022 | Server VLAN       | Production |
VM-002   | WIN11-01 | Endpoint          | User workstation for monitoring and testing | Windows 11          | User VLAN         | Production |
VM-003   | UBU01    | Linux Server      | Docker-hosted security services             | Ubuntu Server       | Server VLAN       | Production |
VM-004   | ATTACK01 | Attack VM         | Atomic Red Team and adversary emulation     | Windows 11          | Isolated Lab VLAN | Testing    |
---
Document Owner: Christopher M Calabrese

Last Updated: 2026-07-09

**Environment:** Enterprise Security Lab
---
