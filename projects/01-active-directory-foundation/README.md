# Project 01 - Active Directory Foundation

## Status

🟡 In Progress

## Objective

Build the foundational identity infrastructure for the Enterprise Security Lab by deploying a Windows Server 2022 domain controller. This project establishes Active Directory Domain Services (AD DS), DNS, and Group Policy to support future security monitoring, endpoint management, and detection engineering projects.

---

## Why This Project Matters

Active Directory remains the identity platform for most enterprise Windows environments. Designing, deploying, and securing an Active Directory environment from the ground up provides the foundation for security monitoring, threat hunting, identity management, Group Policy, and incident response. This project establishes the core infrastructure that future projects—including Sysmon, Windows Event Forwarding, Microsoft Sentinel, and Microsoft Defender—will build upon.

---

Learning Objectives

- Build an enterprise Active Directory environment.
- Configure centralized identity management.
- Deploy DNS to support Active Directory.
- Establish the foundation for Windows Event Forwarding.
- Prepare endpoints for Microsoft Sentinel and Sysmon integration.

---

## Technologies

- Proxmox VE 9
- Windows Server 2022
- VirtIO Drivers

Planned Technologies

- Active Directory Domain Services
- DNS Server
- Group Policy

---

## Progress

Completed

☑ Project created
☑ Windows Server 2022 ISO downloaded
☑ VirtIO driver ISO downloaded
☑ Installation media uploaded to Proxmox
☑ Windows Server virtual machine created
☑ Enterprise virtualization settings configured
☑ Windows installation initiated
☑ VirtIO storage driver loaded
☑ Virtual disk detected

Upcoming

⬜ Complete Windows Server installation
⬜ Rename server to DC01
⬜ Configure static networking
⬜ Install Active Directory Domain Services
⬜ Promote to Domain Controller
⬜ Create baseline snapshot

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
| QEMU Guest Agent | Planned |
| Operating System | Windows Server 2022 Standard Evaluation (Desktop Experience)

---

## Engineering Decisions

| Decision | Reason |
|----------|--------|
| UEFI (OVMF) | Modern firmware standard for Windows Server deployments |
| Q35 Machine Type | Modern chipset emulation with improved compatibility |
| Host CPU | Maximum performance in a single-node Proxmox environment |
| VirtIO SCSI | High-performance paravirtualized storage |
| VirtIO Network | Optimized virtual networking with reduced CPU overhead |
| TPM 2.0 | Supports modern Windows security features and aligns with enterprise deployments |

---

## Implementation Notes

### Using VirtIO with Windows Server

Windows Server 2022 does not include native VirtIO storage drivers. The VirtIO driver ISO must be attached during installation so Windows Setup can detect the virtual disk when using VirtIO SCSI.

### Why Host CPU?

Using **Host** CPU exposes the physical processor's native instruction set to the guest operating system, improving performance. This configuration is appropriate for a single Proxmox host where live migration is not required.

---

## Next Milestones

• Complete Windows Server installation
• Configure baseline operating system settings
• Establish static networking
• Promote the server to the first domain controller
• Validate Active Directory and DNS functionality
• Capture a baseline Proxmox snapshot

---

## Related Projects

This project serves as the foundation for:

- Project 02 – Windows Endpoint Deployment
- Project 03 – Sysmon Deployment
- Project 04 – Windows Event Forwarding
- Project 05 – Wazuh Integration
- Project 06 – Microsoft Sentinel
