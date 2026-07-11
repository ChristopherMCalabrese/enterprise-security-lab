# Project 01 - Active Directory Foundation

## Status

🟢 Complete

---

## Objective

Build the foundational identity infrastructure for the Enterprise Security Lab by deploying a Windows Server 2022 domain controller. This project establishes Active Directory Domain Services (AD DS), DNS, and Group Policy to support future security monitoring, endpoint management, and detection engineering projects.

---

## Why This Project Matters

Active Directory remains the identity platform for most enterprise Windows environments. Designing, deploying, and securing an Active Directory environment from the ground up provides the foundation for identity management, security monitoring, threat hunting, Group Policy, and incident response. This project establishes the core infrastructure that future projects—including Sysmon, Windows Event Forwarding, Wazuh, and Microsoft Sentinel—will build upon.

---

## Learning Objectives

- Build an enterprise Active Directory environment.
- Configure centralized identity management.
- Deploy Active Directory-integrated DNS.
- Establish the foundation for Windows Event Forwarding.
- Prepare endpoints for Microsoft Sentinel and Sysmon integration.

---

## Technologies

### Implemented

- Proxmox VE 9
- Windows Server 2022 Standard Evaluation
- VirtIO Drivers
- Active Directory Domain Services
- DNS Server
- QEMU Guest Agent

### Planned

- Group Policy
- Windows Event Forwarding
- Sysmon
- Microsoft Sentinel
- Wazuh

---

## Progress

- [x] Project created
- [x] Windows Server 2022 ISO downloaded
- [x] VirtIO driver ISO downloaded
- [x] Installation media uploaded to Proxmox
- [x] Windows Server virtual machine created
- [x] Enterprise virtualization settings configured
- [x] Windows Server installation completed
- [x] VirtIO storage driver loaded
- [x] Virtual disk detected
- [x] VirtIO drivers installed
- [x] QEMU Guest Agent installed and configured
- [x] Server renamed to DC01
- [x] Static networking configured
- [x] Active Directory Domain Services installed
- [x] DNS Server installed
- [x] New Active Directory forest created (`lab.home.arpa`)
- [x] Domain controller promoted
- [x] DNS forwarders configured
- [x] Domain health validated
- [x] Baseline Proxmox snapshot created

---

## Virtual Machine Configuration

| Setting | Value |
|---------|-------|
| Hypervisor | Proxmox VE 9 |
| Firmware | OVMF (UEFI) |
| Machine Type | Q35 |
| CPU Type | Host |
| vCPU | 2 |
| Memory | 8 GB |
| Disk | 80 GB VirtIO SCSI |
| Network Adapter | VirtIO |
| TPM | TPM 2.0 |
| QEMU Guest Agent | Enabled |
| Operating System | Windows Server 2022 Standard Evaluation (Desktop Experience) |

---

## Engineering Decisions

| Decision | Reason |
|----------|--------|
| UEFI (OVMF) | Modern firmware standard for Windows Server deployments |
| Q35 Machine Type | Modern chipset emulation with improved compatibility |
| Host CPU | Maximum performance in a single-node Proxmox environment |
| VirtIO SCSI | High-performance paravirtualized storage |
| VirtIO Network | Optimized virtual networking with reduced CPU overhead |
| TPM 2.0 | Supports modern Windows security features |
| `lab.home.arpa` | RFC 8375 reserved namespace for private home networks |
| Static IP (10.10.10.21) | Ensures reliable AD and DNS service discovery |

---

## Implementation Notes

### Installing Windows with VirtIO

Windows Server 2022 does not include native VirtIO storage drivers. The VirtIO driver ISO must be mounted during installation so Windows Setup can detect VirtIO SCSI virtual disks.

### QEMU Guest Agent

Installing the QEMU Guest Agent inside Windows is only part of the configuration. The feature must also be enabled within Proxmox before enhanced guest management features—including IP reporting, graceful shutdown, and guest communication—become available.

### Active Directory DNS

The domain controller hosts an Active Directory-integrated DNS zone for `lab.home.arpa`. External DNS queries are forwarded to AdGuard Home (10.10.10.5), allowing internal name resolution while preserving centralized DNS filtering.

### Why `lab.home.arpa`?

The Active Directory forest uses the `lab.home.arpa` namespace, which is reserved by RFC 8375 for private home networks. Using a reserved namespace avoids conflicts with publicly registered domains while following current Microsoft recommendations.

---

## Validation

The completed deployment was validated using:

- `dcdiag`
- `dcdiag /test:dns`
- `nslookup google.com`
- `nslookup dc01.lab.home.arpa`

Validation confirmed:

- Active Directory healthy
- DNS forwarders operational
- Internal DNS resolution functioning
- External DNS resolution functioning
- SYSVOL successfully shared
- Domain controller advertising correctly

---

## Outcome

Project 01 established the identity foundation for the Enterprise Security Lab.

The environment now includes:

- Active Directory Forest: `lab.home.arpa`
- Domain Controller: `DC01`
- Integrated DNS
- Functional QEMU Guest Agent
- Static infrastructure addressing
- Baseline Proxmox snapshot for future recovery

This environment now serves as the foundation for all future Windows-based enterprise security projects.

---

## Next Project

**Project 02 – Windows Endpoint Deployment**

Objectives:

- Deploy Windows 11 Enterprise
- Join the workstation to `lab.home.arpa`
- Validate domain authentication
- Prepare the endpoint for Group Policy, Sysmon, and Windows Event Forwarding

---

## Related Projects

- Project 02 – Windows Endpoint Deployment
- Project 03 – Sysmon Deployment
- Project 04 – Windows Event Forwarding
- Project 05 – Wazuh Integration
- Project 06 – Microsoft Sentinel
