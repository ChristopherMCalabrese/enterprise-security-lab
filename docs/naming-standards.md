# Naming Standards

## Overview

This document defines the naming conventions used throughout the Enterprise Security Lab. Consistent naming improves administration, simplifies troubleshooting, supports automation, and aligns the environment with enterprise best practices.

These standards apply to Active Directory objects, virtual machines, Group Policy Objects, service accounts, documentation, and supporting infrastructure.

---

# User Accounts

## Standard User Accounts

Format:

```text
first initial + last name
```

Examples:

```text
ccalabrese
jdoe
asmith
```

Purpose:

- Daily user activities
- Workstation logon
- Email and productivity
- Non-administrative operations

---

## Administrative Accounts

Format:

```text
adm-username
```

Examples:

```text
adm-ccalabrese
adm-jdoe
```

Purpose:

- Server administration
- Active Directory management
- DNS administration
- Group Policy management
- Enterprise infrastructure administration

Administrative accounts should never be used for routine workstation activities unless administrative privileges are required.

---

# Service Accounts

Format:

```text
svc-servicename
```

Examples:

```text
svc-wazuh
svc-sentinel
svc-wef
svc-backup
```

Purpose:

- Application authentication
- Scheduled tasks
- Windows services
- Automated processes

---

# Computer Names

## Domain Controllers

Format:

```text
DC##
```

Examples:

```text
DC01
DC02
```

---

## Windows Workstations

Format:

```text
WIN11-##
```

Examples:

```text
WIN11-01
WIN11-02
```

---

## Windows Servers

Format:

```text
ROLE##
```

Examples:

```text
APP01
WEB01
SQL01
WEC01
WSUS01
```

---

## Linux Servers

Format:

```text
UBU##
```

Examples:

```text
UBU01
UBU02
```

---

## Security / Attack Systems

Format:

```text
ATTACK##
```

Examples:

```text
ATTACK01
```

---

# Organizational Units

Use descriptive singular names.

Examples:

```text
Administrative
Groups
Servers
Service Accounts
Users
Workstations
```

Administrative child OUs:

```text
Administrative
├── Groups
└── Users
```

---

# Security Groups

Format:

```text
GG-Description
```

Examples:

```text
GG-Workstation-Admins
GG-Server-Admins
GG-Helpdesk
GG-Wazuh-Admins
GG-Sentinel-Admins
```

**GG** denotes a **Global Group**, following Microsoft's recommended Active Directory group scope conventions.

---

# Group Policy Objects

Format:

```text
GPO - Description
```

Examples:

```text
GPO - Workstation Baseline
GPO - Server Baseline
GPO - Microsoft Defender
GPO - Windows Firewall
GPO - Sysmon
GPO - Windows Update
```

---

# Virtual Machine Names

Virtual machines follow the same naming convention as their operating system role.

Examples:

```text
DC01
WIN11-01
UBU01
ATTACK01
```

---

# Proxmox Snapshots

Format:

```text
Project-##-Complete
```

Examples:

```text
Project-01-Complete
Project-02-Complete
Pre-Sysmon
Pre-Wazuh
Pre-Sentinel
```

Snapshots should represent meaningful milestones rather than arbitrary points in time.

---

# Project Naming

Project folders use a numeric prefix followed by a descriptive name.

Format:

```text
##-project-name
```

Examples:

```text
01-active-directory-foundation
02-windows-endpoint-deployment
03-active-directory-administration
04-sysmon-deployment
05-windows-event-forwarding
06-wazuh-integration
07-microsoft-sentinel
08-microsoft-defender
09-attack-simulation
```

---

# Documentation

Documentation files use lowercase letters and hyphens.

Examples:

```text
asset-inventory.md
network-diagram.md
naming-standards.md
roadmap.md
virtualization.md
```

---

# Object Descriptions

Where applicable, Active Directory objects should include a meaningful description.

Examples:

| Object | Description |
|---------|-------------|
| User | Administrative account |
| User | Standard user account |
| Group | Administrators of Windows workstations |
| Group | Administrators of Windows servers |
| Group | Tier 1 support personnel |
| Service Account | Runs the Wazuh Manager service |

Descriptions should clearly communicate the purpose of the object without requiring administrators to inspect memberships or permissions.

---

## Guiding Principles

The Enterprise Security Lab follows four core naming principles:

- **Consistency** — Similar objects follow the same naming pattern.
- **Readability** — Object names should clearly communicate purpose.
- **Scalability** — Naming conventions should support future growth.
- **Enterprise Alignment** — Conventions reflect common enterprise Active Directory and infrastructure management practices.

---

**Document Owner:** Christopher M. Calabrese

**Last Updated:** 2026-07-11

**Environment:** Enterprise Security Lab
