# Project 04 – Group Policy Baseline

## Objective

Design and implement an enterprise-style Group Policy architecture that provides centralized management of Windows systems while establishing the security baseline for the Enterprise Security Lab.

This project introduces centralized endpoint management through Group Policy and establishes the foundational auditing and logging capabilities that future projects will build upon, including Windows Event Forwarding (WEF), Microsoft Defender, Wazuh, and Microsoft Sentinel.

---

# Learning Objectives

- Design a scalable Group Policy architecture.
- Understand Group Policy processing and inheritance.
- Implement Advanced Audit Policies.
- Configure PowerShell logging and transcription.
- Develop enterprise logging standards.
- Validate Group Policy deployment using native Windows tools.
- Prepare the environment for centralized security monitoring.

---

# Technologies

## Implemented

- Active Directory Domain Services
- Group Policy Management Console (GPMC)
- Advanced Audit Policy Configuration
- Windows PowerShell Logging
- Windows PowerShell Transcription
- Windows Event Viewer
- Windows Server 2022
- Windows 11 Enterprise

## Future Projects

- Windows Event Forwarding (WEF)
- Microsoft Defender
- Windows Defender Firewall
- Administrative Templates
- Windows Security Options
- Windows Update
- Wazuh Integration
- Microsoft Sentinel Integration

---

# Progress

## ✅ Infrastructure

- [x] Created Workstation Baseline GPO
- [x] Created Domain Controller Baseline GPO
- [x] Linked GPOs to Organizational Units
- [x] Validated Group Policy processing
- [x] Created recovery snapshots

---

## ✅ Audit & Accountability

- [x] Configured Credential Validation auditing
- [x] Configured User Account Management auditing
- [x] Configured Logon auditing
- [x] Configured Logoff auditing
- [x] Validated Advanced Audit Policy deployment

---

## ✅ PowerShell Visibility

- [x] Enabled Script Block Logging
- [x] Enabled Script Block Invocation Logging
- [x] Enabled Module Logging
- [x] Enabled PowerShell Transcription
- [x] Validated PowerShell Operational logging
- [x] Validated PowerShell Transcription

---

## ✅ Project Validation

- [x] Validated Group Policy processing
- [x] Validated Advanced Audit Policy
- [x] Validated PowerShell logging
- [x] Validated Active Directory health
- [x] Verified workstation communication with the domain
- [x] Completed project documentation

---

# Group Policy Architecture

```text
Group Policy Objects
│
├── Default Domain Policy
├── Default Domain Controllers Policy
├── GPO - Workstation Baseline
└── GPO - Domain Controller Baseline
```

## GPO Links

| GPO | Linked To |
|------|-----------|
| GPO - Workstation Baseline | Workstations OU |
| GPO - Domain Controller Baseline | Domain Controllers OU |

Custom Group Policy Objects are intentionally linked only to the Organizational Units they manage. No custom GPOs are linked at the domain root.

---

# Capability Summary

## Audit & Accountability

Enterprise auditing was implemented using Advanced Audit Policy Configuration.

Configured policies include:

- Credential Validation
- User Account Management
- Logon
- Logoff

These policies establish visibility into authentication activity and administrative account changes while avoiding legacy audit policy conflicts.

Validation was performed using:

```cmd
auditpol /get /category:*
```

---

## PowerShell Visibility

PowerShell logging was implemented to improve visibility into administrative activity and provide telemetry for future security monitoring platforms.

Configured capabilities include:

- Script Block Logging
- Script Block Invocation Logging
- Module Logging
- PowerShell Transcription

Validation confirmed:

- Event ID 4103 (Module Logging)
- Event ID 4104 (Script Block Logging)
- Event IDs 4105/4106 (Invocation Logging)
- PowerShell transcript generation

These logs provide detailed administrative visibility and will later be collected through Windows Event Forwarding and forwarded to Wazuh and Microsoft Sentinel.

---

# Validation

The following native Windows tools were used throughout this project.

## Group Policy

```cmd
gpupdate /force
gpresult /r
```

---

## Advanced Audit Policy

```cmd
auditpol /get /category:*
```

---

## PowerShell Logging

```powershell
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational"
```

---

## Active Directory

```cmd
dcdiag
repadmin /replsummary
```

Validation confirmed:

- Active Directory healthy
- DNS healthy
- SYSVOL healthy
- Replication healthy
- Group Policy processing successfully

---

# Engineering Decisions

| Decision | Reason |
|----------|--------|
| Separate workstation and domain controller baselines | Independent management and reduced administrative risk |
| Link GPOs to Organizational Units | Limits policy scope and follows enterprise best practices |
| Use Advanced Audit Policies | Provides granular auditing while avoiding legacy audit policy conflicts |
| Enable visibility before hardening | Logging should exist before restrictive security controls are applied |
| Validate every configuration | Native Windows tools verify effective policy instead of assuming success |
| Capability-driven implementation | Features are implemented and validated one capability at a time |

---

# Challenges Encountered

During project validation, multiple infrastructure issues affected the virtual lab environment.

## WIN11-01

Remote Desktop sessions disconnected intermittently while the virtual machine remained operational.

Initial investigation included:

- Group Policy
- Remote Desktop Services
- PowerShell Logging
- VirtIO drivers
- Windows Event Logs

No Group Policy configuration was identified as the cause.

---

## DC01

Following a scheduled Proxmox host reboot, the domain controller entered the Windows Recovery Environment and would not boot normally.

Investigation verified:

- EFI boot configuration
- VirtIO storage drivers
- GPT partition layout
- VM configuration
- Active Directory services

---

## Root Cause

Further investigation identified the Proxmox LVM-Thin storage pool had reached **100% utilization**.

This prevented new thin volumes from being created and introduced storage pressure capable of affecting guest virtual machines.

Corrective actions included:

- Extending the LVM-Thin storage pool
- Removing unnecessary RAM snapshots
- Rolling back the domain controller to the Project04 milestone snapshot

Following recovery:

- Active Directory health validated successfully
- Group Policy processing confirmed
- PowerShell logging remained operational
- Infrastructure stability restored

This incident reinforced the importance of validating hypervisor health before troubleshooting guest operating systems.

---

# Lessons Learned

- Infrastructure failures can present as operating system failures.
- Thin-provisioned storage requires continuous monitoring.
- Disk-only snapshots are preferable to memory snapshots for long-term rollback points.
- Root cause analysis is more valuable than immediately rebuilding systems.
- Enterprise operations require validating the infrastructure layer before troubleshooting applications or operating systems.

---

# Outcome

Project 04 successfully established the foundational Group Policy architecture for the Enterprise Security Lab.

Implemented capabilities include:

- Enterprise Group Policy architecture
- Advanced Audit Policy
- PowerShell Operational Logging
- PowerShell Transcription
- Enterprise validation procedures

The project also highlighted the importance of virtualization infrastructure health. During validation, a full Proxmox LVM-Thin storage pool caused guest operating system instability, emphasizing that hypervisor health must be verified before attributing issues to Windows configuration.

The environment now provides centralized policy management and foundational endpoint telemetry for future projects involving Windows Event Forwarding, Microsoft Defender, Wazuh, and Microsoft Sentinel.

---

# Project Status

## ✅ Completed

### Completed Capabilities

- ✅ Group Policy Architecture
- ✅ Organizational Unit Design
- ✅ Advanced Audit Policy
- ✅ PowerShell Logging
- ✅ PowerShell Transcription
- ✅ Group Policy Validation
- ✅ Active Directory Validation
- ✅ Documentation

---

## Future Projects

- Windows Event Forwarding (WEF)
- Microsoft Defender Baseline
- Windows Defender Firewall
- Administrative Templates
- Windows Security Options
- Windows Update Management
- Wazuh Integration
- Microsoft Sentinel Integration
