# Project 01 - Active Directory Foundation

## Status

🟡 In Progress

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
- [ ] DNS forwarders configured
- [ ] Domain health validated
- [ ] Baseline Proxmox snapshot created

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
| Host CPU | Provides maximum performance in a single-node Proxmox environment where live migration is unnecessary |
| VirtIO SCSI | High-performance paravirtualized storage controller |
| VirtIO Network | Optimized virtual networking with reduced CPU overhead |
| TPM 2.0 | Supports modern Windows security features and aligns with enterprise deployments |
| `lab.home.arpa` | RFC 8375 reserved namespace for private home networks, avoiding conflicts with public DNS |

---

## Implementation Notes

### Installing Windows with VirtIO

Windows Server 2022 does not include native VirtIO storage drivers. The VirtIO driver ISO must be mounted during installation so Windows Setup can detect VirtIO SCSI virtual disks.

### QEMU Guest Agent

Installing the QEMU Guest Agent inside Windows is only part of the configuration. The feature must also be enabled within Proxmox before enhanced guest management features—including IP reporting and guest communication—become available.

### Why Host CPU?

Using the **Host** CPU type exposes the physical processor's native instruction set directly to the guest operating system, maximizing virtual machine performance. This configuration is appropriate for a homelab or single-node Proxmox deployment where live migration is not required.

### Why `lab.home.arpa`?

The Active Directory forest uses the `lab.home.arpa` namespace, which is reserved by RFC 8375 for private home networks. This avoids conflicts with publicly registered domains while following current Microsoft and IETF recommendations for internal Active Directory deployments.

---

## Next Milestones

- Configure DNS forwarders
- Validate Active Directory and DNS health
- Capture a baseline Proxmox snapshot
- Deploy the first Windows workstation
- Join the workstation to `lab.home.arpa`

---

## Related Projects

This project serves as the foundation for:

- Project 02 – Windows Endpoint Deployment
- Project 03 – Sysmon Deployment
- Project 04 – Windows Event Forwarding
- Project 05 – Wazuh Integration
- Project 06 – Microsoft Sentinel
