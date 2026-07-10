# Project 01 - Active Directory Foundation

## Status

🟡 In Progress

## Objective

Deploy a Windows Server 2022 domain controller to serve as the identity platform for the Enterprise Security Lab. This server will provide Active Directory Domain Services (AD DS), DNS, and Group Policy for future security monitoring and detection projects.

---

## Learning Objectives

- Deploy a Windows Server 2022 virtual machine using Proxmox VE.
- Configure enterprise virtualization settings using VirtIO.
- Install Active Directory Domain Services.
- Configure DNS for an internal domain.
- Join Windows endpoints to the domain.
- Prepare the environment for centralized security monitoring.

---

## Technologies

- Proxmox VE 9
- Windows Server 2022
- VirtIO Drivers
- Active Directory (planned)
- DNS (planned)
- Group Policy (planned)

---

## Progress

- [x] Project created
- [x] Windows Server 2022 ISO downloaded
- [x] VirtIO driver ISO downloaded
- [x] Installation media uploaded to Proxmox
- [x] Windows Server virtual machine created
- [x] Enterprise virtualization settings configured
☑ Windows installation initiated
☑ VirtIO storage driver loaded
☑ Virtual disk detected
- [x] Windows Server installed
- [ ] Rename server to DC01
- [ ] Configure static networking
- [ ] Install AD DS
- [ ] Promote to Domain Controller
- [ ] Create baseline snapshot

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

## Lessons Learned

### Using VirtIO with Windows Server

Windows Server 2022 does not include native VirtIO storage drivers. The VirtIO driver ISO must be attached during installation so Windows Setup can detect the virtual disk when using VirtIO SCSI.

### Why Host CPU?

Using **Host** CPU exposes the physical processor's native instruction set to the guest operating system, improving performance. This configuration is appropriate for a single Proxmox host where live migration is not required.

---

## Next Steps

- Install Windows Server 2022.
- Configure static IP addressing.
- Rename the server to **DC01**.
- Install Active Directory Domain Services.
- Promote the server to the first domain controller.
- Create a Proxmox snapshot after the baseline configuration is complete.
