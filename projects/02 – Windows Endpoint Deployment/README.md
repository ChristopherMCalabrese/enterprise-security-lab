# Project 02 – Windows Endpoint Deployment

## Status

🟡 In Progress

---

## Objective

Deploy a Windows 11 Enterprise workstation, join it to the Active Directory domain, and validate centralized authentication. This workstation will become the primary endpoint used throughout the remainder of the Enterprise Security Lab for Group Policy, Sysmon, Windows Event Forwarding, Wazuh, and Microsoft Sentinel.

---

## Why This Project Matters

Enterprise security begins at the endpoint. Deploying a domain-joined Windows 11 Enterprise workstation provides a realistic client system for identity management, Group Policy, endpoint monitoring, log collection, and attack simulation. This workstation will become the primary managed endpoint used throughout the remainder of the Enterprise Security Lab.

---

## Learning Objectives

- Deploy a Windows 11 Enterprise virtual machine.
- Configure enterprise virtualization settings.
- Join a workstation to Active Directory.
- Validate domain authentication.
- Verify DNS integration.
- Prepare the endpoint for future security tooling.

---

## Technologies

### Implemented

- Proxmox VE 9
- Windows 11 Enterprise Evaluation
- VirtIO Drivers
- Active Directory
- DNS

### Planned

- Group Policy
- Sysmon
- Windows Event Forwarding
- Wazuh Agent
- Microsoft Sentinel

---

## Progress

- [ ] Windows 11 Enterprise ISO downloaded
- [ ] VirtIO driver ISO attached
- [ ] Installation media uploaded to Proxmox
- [ ] Windows 11 virtual machine created
- [ ] Enterprise virtualization settings configured
- [ ] TPM 2.0 configured
- [ ] Secure Boot enabled
- [ ] Windows 11 installed
- [ ] VirtIO drivers installed
- [ ] QEMU Guest Agent installed and configured
- [ ] Networking configured
- [ ] Joined to `lab.home.arpa`
- [ ] Domain authentication validated
- [ ] Group Policy verified
- [ ] Baseline Proxmox snapshot created

---

## Planned Virtual Machine Configuration

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
| Secure Boot | Enabled |
| QEMU Guest Agent | Enabled |
| Operating System | Windows 11 Enterprise Evaluation |

---

## Engineering Decisions

| Decision | Reason |
|----------|--------|
| Windows 11 Enterprise | Provides enterprise features including Group Policy, BitLocker, Microsoft Defender, and centralized management |
| UEFI + Secure Boot | Aligns with modern enterprise deployment standards |
| TPM 2.0 | Required by Windows 11 and enterprise security features |
| Host CPU | Maximizes virtual machine performance |
| VirtIO Storage & Networking | Optimized virtualization performance with reduced overhead |
| Domain Join | Enables centralized authentication, Group Policy, and identity management |

---

## Validation

The deployment will be validated by confirming:

- Successful domain join
- Domain user authentication
- Active Directory DNS resolution
- Communication with DC01
- QEMU Guest Agent functionality
- Successful Group Policy retrieval (`gpupdate /force`)
- Successful communication with the domain controller

---

## Outcome

This workstation will become the primary managed endpoint used throughout the Enterprise Security Lab and serve as the target system for future security monitoring, endpoint hardening, threat detection, and incident response exercises.

---

## Next Project

**Project 03 – Sysmon Deployment**

Objectives:

- Deploy Sysmon
- Install the SwiftOnSecurity configuration
- Validate Sysmon event generation
- Prepare the endpoint for centralized log collection

---

## Related Projects

- Project 01 – Active Directory Foundation
- Project 03 – Sysmon Deployment
- Project 04 – Windows Event Forwarding
- Project 05 – Wazuh Integration
- Project 06 – Microsoft Sentinel
