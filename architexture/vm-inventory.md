# Asset Inventory

## Overview

This document provides an inventory of all virtual machines used in the Enterprise Security Lab. It includes each system's purpose, operating system, assigned resources, network configuration, and role within the environment.

Maintaining an accurate asset inventory is a foundational security practice that supports system administration, vulnerability management, incident response, and change management.

> [!NOTE]
> Hostnames, network topology, and infrastructure details have been sanitized where appropriate. No production credentials, public IP addresses, or sensitive configuration data are included in this repository.
> 
---
| Hostname | Role              | Purpose                                     | OS                  | Network Zone      | Status     |
| -------- | ----------------- | ------------------------------------------- | ------------------- | ----------------- | ---------- |
| DC01     | Domain Controller | Active Directory, DNS, Group Policy         | Windows Server 2022 | Server VLAN       | Production |
| WIN11-01 | Endpoint          | User workstation for monitoring and testing | Windows 11          | User VLAN         | Production |
| UBU01    | Linux Server      | Docker-hosted security services             | Ubuntu Server       | Server VLAN       | Production |
| ATTACK01 | Attack VM         | Atomic Red Team and adversary emulation     | Windows 11          | Isolated Lab VLAN | Testing    |
---
**Document Owner:** Christopher McCalabrese

**Last Updated:** July 2026

**Environment:** Enterprise Security Lab
---
