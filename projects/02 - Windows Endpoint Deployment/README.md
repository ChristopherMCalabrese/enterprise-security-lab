# Project 02 – Windows Endpoint Deployment

## Status

🟢 Complete

---

## Objective

Deploy a Windows 11 Enterprise workstation, join it to the Active Directory domain, and validate centralized authentication. This workstation will serve as the primary managed endpoint for future Group Policy, Sysmon, Windows Event Forwarding, Wazuh, Microsoft Defender, and Microsoft Sentinel projects.

---

## Why This Project Matters

Enterprise security depends on centrally managed endpoints. Deploying a domain-joined Windows 11 Enterprise workstation provides a realistic platform for identity management, policy enforcement, endpoint monitoring, log collection, attack simulation, and incident response exercises.

---

## Learning Objectives

- Deploy a Windows 11 Enterprise virtual machine.
- Configure enterprise virtualization settings.
- Join a workstation to Active Directory.
- Validate domain authentication.
- Verify Active Directory DNS integration.
- Confirm Group Policy processing.
- Prepare the endpoint for future security tooling.

---

## Technologies

### Implemented

- Proxmox VE 9
- Windows 11 Enterprise Evaluation
- VirtIO Drivers
- QEMU Guest Agent
- Active Directory Domain Services
- Active Directory-integrated DNS
- Group Policy
- Remote Desktop Protocol

### Planned

- Sysmon
- Windows Event Forwarding
- Wazuh Agent
- Microsoft Defender integration
- Microsoft Sentinel

---

## Progress

- [x] Windows 11 Enterprise Evaluation ISO downloaded
- [x] Installation media uploaded to Proxmox
- [x] VirtIO driver ISO attached
- [x] Windows 11 virtual machine created
- [x] Enterprise virtualization settings configured
- [x] TPM 2.0 configured
- [x] Secure Boot enabled
- [x] Windows 11 Enterprise installed
- [x] VirtIO storage and network drivers installed
- [x] QEMU Guest Agent installed and configured
- [x] DHCP networking validated
- [x] DNS configured to use DC01
- [x] Workstation renamed to `WIN11-01`
- [x] Workstation joined to `lab.home.arpa`
- [x] Domain authentication validated
- [x] Group Policy processing validated
- [x] Remote Desktop enabled and tested
- [x] Installation media unmounted
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
| Secure Boot | Enabled |
| QEMU Guest Agent | Enabled |
| Operating System | Windows 11 Enterprise Evaluation |

---

## Engineering Decisions

| Decision | Reason |
|----------|--------|
| Windows 11 Enterprise | Provides enterprise features including domain join, Group Policy, BitLocker, Microsoft Defender, and centralized management |
| UEFI and Secure Boot | Aligns the workstation with modern enterprise deployment standards |
| TPM 2.0 | Supports Windows 11 security requirements and future credential protection features |
| Host CPU | Exposes native processor capabilities and improves performance in a single-node Proxmox environment |
| VirtIO Storage and Networking | Provides optimized virtual disk and network performance with reduced virtualization overhead |
| DHCP Addressing | Reflects standard enterprise workstation deployment practices |
| DC01 as DNS Server | Allows the endpoint to resolve Active Directory service records required for domain discovery and authentication |
| Domain Join | Enables centralized identity, authentication, policy management, and security monitoring |
| RDP for Administration | Provides a more responsive administrative experience than the browser-based Proxmox console |

---

## Implementation Notes

### VirtIO Driver Installation

Windows 11 installation media does not include the VirtIO SCSI driver required to detect the virtual disk. The VirtIO driver ISO was attached during installation, and the appropriate storage driver was loaded before Windows was installed.

The complete VirtIO guest tools package was installed after setup to provide optimized storage, networking, memory management, and Proxmox guest integration.

### QEMU Guest Agent

The QEMU Guest Agent was installed inside Windows and enabled within the Proxmox VM configuration. Successful integration was confirmed through guest IP reporting and host-to-guest communication.

### Active Directory DNS

The workstation continues to receive its IP address and default gateway through DHCP. Its DNS configuration was changed to use DC01 so it could resolve the Active Directory DNS records required to locate and join `lab.home.arpa`.

This change was applied only to the lab endpoint and did not alter DNS or DHCP behavior for the rest of the home network.

### Domain Join

`WIN11-01` was joined to the `lab.home.arpa` Active Directory domain using domain administrative credentials. After rebooting, domain authentication was verified using the `LAB\Administrator` account.

### Remote Administration

The Proxmox noVNC console introduced noticeable display and input latency despite low guest resource utilization. Remote Desktop was enabled and used for normal Windows administration, resulting in a significantly more responsive experience.

---

## Validation

The deployment was validated using:

```cmd
hostname
whoami
echo %USERDOMAIN%
gpupdate /force
nslookup dc01.lab.home.arpa
