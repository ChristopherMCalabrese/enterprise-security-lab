# Project 04 – Group Policy Baseline

## Objective

Design and implement an enterprise-style Group Policy architecture that provides centralized management of Windows systems while establishing the security baseline for the Enterprise Security Lab.

This project introduces centralized endpoint management through Group Policy and lays the foundation for future projects involving endpoint hardening, logging, Microsoft Defender, Windows Event Forwarding (WEF), Wazuh, Microsoft Sentinel, and other enterprise security technologies.

---

# Learning Objectives

- Design a scalable Group Policy architecture.
- Understand Group Policy processing and inheritance.
- Implement Advanced Audit Policies.
- Configure PowerShell logging.
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
- Windows Event Viewer
- Windows Server 2022
- Windows 11 Enterprise

## Planned

- Windows Event Log Management
- Microsoft Defender
- Windows Defender Firewall
- Windows Security Options
- Windows Update
- Administrative Templates
- Windows Event Forwarding (WEF)

---

# Progress

## ✅ Infrastructure

- [x] Created Workstation Baseline GPO
- [x] Created Domain Controller Baseline GPO
- [x] Linked Workstation Baseline GPO
- [x] Linked Domain Controller Baseline GPO
- [x] Validated Group Policy processing
- [x] Created recovery snapshots

---

## ✅ Audit & Accountability

- [x] Configured Credential Validation auditing
- [x] Configured User Account Management auditing
- [x] Configured Logon auditing
- [x] Configured Logoff auditing
- [x] Validated Advanced Audit Policy

---

## ✅ PowerShell Visibility

- [x] Enabled Script Block Logging
- [x] Enabled Script Block Invocation Logging
- [x] Enabled Module Logging
- [x] Validated PowerShell Operational logging
- [ ] Configure PowerShell Transcription

---

## 🚧 Event Log Management

- [ ] Configure Security Log Size
- [ ] Configure Application Log Size
- [ ] Configure System Log Size
- [ ] Configure Setup Log Size

---

## ⏳ Endpoint Protection

- [ ] Configure Microsoft Defender
- [ ] Configure Windows Defender Firewall

---

## ⏳ Operating System Security

- [ ] Configure Security Options
- [ ] Configure Windows Update
- [ ] Configure Administrative Templates

---

## ⏳ Future Integration

- [ ] Windows Event Forwarding (WEF)
- [ ] Wazuh Integration
- [ ] Microsoft Sentinel Integration

---

# Group Policy Architecture

```
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

Custom policies are intentionally linked only to the Organizational Units they manage. No custom Group Policy Objects are linked at the domain root.

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

Configured features include:

- Script Block Logging
- Script Block Invocation Logging
- Module Logging

Validation was performed using:

```powershell
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational"
```

Validation confirmed:

- Event ID 4103 (Module Logging)
- Event ID 4104 (Script Block Logging)
- Event IDs 4105/4106 (Invocation Start/Stop)

These events will later be collected through Windows Event Forwarding and ingested into Wazuh and Microsoft Sentinel.

---

## Event Log Management

This capability is currently in progress.

The objective is to increase Windows Event Log retention to better support enterprise monitoring and forensic investigations.

Planned configuration:

- Security Log
- Application Log
- System Log
- Setup Log

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

# Engineering Decisions

| Decision | Reason |
|----------|--------|
| Separate workstation and domain controller baselines | Independent management and reduced administrative risk |
| Link GPOs to Organizational Units | Limits policy scope and follows enterprise best practices |
| Use Advanced Audit Policies | Provides granular auditing and avoids legacy audit policy conflicts |
| Visibility before hardening | Logging is established before restrictive security controls are applied |
| Validate every configuration | Native Windows tools verify effective policy rather than assuming successful deployment |
| Capability-driven implementation | Security features are implemented and validated one capability at a time |

---

# Challenges Encountered

During initial testing, Remote Desktop sessions to WIN11-01 disconnected immediately following Group Policy refreshes.

Investigation determined:

- Group Policy processed successfully.
- Advanced Audit Policies applied correctly.
- PowerShell logging functioned as expected.
- The issue coincided with memory pressure and active swap usage on the Proxmox host.

Following host maintenance and a Proxmox reboot:

- Swap usage returned to zero.
- RDP stability was restored.
- Group Policy updates completed successfully without interruption.

This reinforced the importance of validating hypervisor health before attributing issues to guest operating system configuration.

---

# Outcome

Project 04 successfully established the Enterprise Security Lab's Group Policy architecture while implementing enterprise-grade auditing and PowerShell visibility.

The Windows environment now generates centralized authentication, account management, and PowerShell telemetry that will serve as the foundation for future endpoint monitoring, Windows Event Forwarding, Wazuh, and Microsoft Sentinel integration.

---

**Project Status:** 🚧 In Progress

**Completed Capabilities**

- ✅ Infrastructure
- ✅ Audit & Accountability
- ✅ PowerShell Visibility

**Current Capability**

- 🚧 Event Log Management

**Next Capability**

- Endpoint Protection
