# Asset Inventory

## Overview

This document provides an inventory of the systems and infrastructure that make up the Enterprise Security Lab. It includes each asset's purpose, operating system, role, and function within the environment.

The inventory serves as a foundational reference for system administration, vulnerability management, incident response, and security operations.

Maintaining an accurate asset inventory is a foundational security practice that supports system administration, vulnerability management, incident response, and change management.

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
**Document Owner:** Christopher McCalabrese

Last Updated: 2026-07-09

**Environment:** Enterprise Security Lab
---
