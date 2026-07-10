# Virtual Machine Inventory

## Overview

This document provides an inventory of all virtual machines used in the Enterprise Security Lab. It includes each system's purpose, operating system, assigned resources, network configuration, and role within the environment.

Maintaining an accurate asset inventory is a foundational security practice that supports system administration, vulnerability management, incident response, and change management.

---
| Hostname | Role              | OS                  | Network Zone      | Addressing        |
| -------- | ----------------- | ------------------- | ----------------- | ----------------- |
| DC01     | Domain Controller | Windows Server 2022 | Server VLAN       | Static private IP |
| WIN11-01 | Workstation       | Windows 11          | User VLAN         | DHCP reservation  |
| UBU01    | Linux Server      | Ubuntu Server       | Server VLAN       | Static private IP |
| ATTACK01 | Testing VM        | Windows 11          | Isolated Lab VLAN | Static private IP |
