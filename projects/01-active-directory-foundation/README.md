# Project 01 - Active Directory Foundation

## Status

🟡 In Progress

## Objective

Deploy a Windows Server 2022 domain controller to serve as the identity platform for the Enterprise Security Lab. This server will provide Active Directory Domain Services (AD DS), DNS, and Group Policy for future security monitoring and detection projects.

## Learning Objectives

- Deploy a Windows Server 2022 virtual machine using Proxmox.
- Configure enterprise virtualization settings using VirtIO.
- Install Active Directory Domain Services.
- Configure DNS for an internal domain.
- Join Windows endpoints to the domain.
- Prepare the environment for centralized security monitoring.

## Build Decisions

| Decision | Reason |
|----------|--------|
| Proxmox VE | Enterprise-grade virtualization platform |
| VirtIO | Optimized storage and network performance |
| UEFI | Modern firmware standard |
| Windows Server 2022 | Current enterprise Windows Server platform |

## Technologies

- Proxmox VE
- Windows Server 2022
- Active Directory (planned)
- DNS (planned)
- Group Policy (planned)

## Progress

- [x] Project created
- [x] Windows Server 2022 ISO downloaded
- [x] VirtIO drivers downloaded
- [x] ISOs uploaded to Proxmox
- [ ] VM created
- [ ] Windows installed
- [ ] Rename server to DC01
- [ ] Configure static networking
- [ ] Install AD DS
- [ ] Promote to Domain Controller

## Lessons Learned

### Using VirtIO with Windows Server

Windows Server 2022 does not include the VirtIO storage drivers required for paravirtualized disks in Proxmox. The VirtIO driver ISO must be attached during installation so Windows Setup can detect the virtual disk.
