# Project 04 – Group Policy Baseline

## Objective

Design and implement an enterprise-style Group Policy architecture that provides centralized management of Windows systems while establishing the security baseline for the Enterprise Security Lab.

This project introduces centralized endpoint management through Group Policy and lays the foundation for future projects involving endpoint hardening, logging, Microsoft Defender, Windows Event Forwarding (WEF), Wazuh, and Microsoft Sentinel.

---

# Learning Objectives

- Design a scalable Group Policy architecture.
- Understand Group Policy processing and inheritance.
- Deploy Advanced Audit Policies.
- Validate Group Policy deployment using native Windows tools.
- Establish centralized security management for Windows endpoints.
- Prepare the environment for enterprise security monitoring.

---

# Technologies

## Implemented

- Windows Server 2022
- Active Directory Domain Services
- Group Policy Management Console (GPMC)
- Advanced Audit Policy Configuration
- Windows 11 Enterprise

## Planned

- PowerShell Logging
- Windows Event Logging
- Microsoft Defender
- Windows Firewall
- Windows Update Management
- Windows Security Options
- Administrative Templates
- Windows Event Forwarding

---

# Progress

- [x] Created Workstation Baseline GPO
- [x] Created Domain Controller Baseline GPO
- [x] Linked Workstation Baseline GPO
- [x] Linked Domain Controller Baseline GPO
- [x] Validated Group Policy processing
- [x] Configured Advanced Audit Policy
- [x] Validated Advanced Audit Policy
- [x] Created recovery snapshots
- [ ] Configure PowerShell Logging
- [ ] Configure Windows Event Logs
- [ ] Configure Microsoft Defender
- [ ] Configure Windows Firewall
- [ ] Configure Windows Update
- [ ] Configure Security Options
- [ ] Configure Administrative Templates
- [ ] Final validation

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

### GPO Links

| GPO | Linked To |
|------|-----------|
| GPO - Workstation Baseline | Workstations OU |
| GPO - Domain Controller Baseline | Domain Controllers OU |

The baseline architecture intentionally avoids linking custom policies at the domain root, limiting scope to only the systems each policy is intended to manage.

---

# Advanced Audit Policy

The first security capability implemented focused on establishing visibility before applying additional endpoint hardening.

## Configured Audit Policies

| Policy | Configuration |
|---------|---------------|
| Credential Validation | Success, Failure |
| User Account Management | Success, Failure |
| Logon | Success, Failure |
| Logoff | Success |

These policies provide foundational auditing for authentication activity, account management, and user logon events.

---

# Validation

Group Policy deployment was validated using native Windows administration tools.

## Group Policy

```cmd
gpupdate /force
gpresult /r
```

Validation confirmed:

- Workstation received the Workstation Baseline GPO.
- Policies were processed successfully from DC01.
- Group Policy inheritance functioned as expected.

---

## Audit Policy

```cmd
auditpol /get /category:*
```

Validation confirmed:

- Credential Validation auditing enabled.
- User Account Management auditing enabled.
- Logon auditing enabled.
- Logoff auditing enabled.

---

# Engineering Decisions

| Decision | Reason |
|----------|--------|
| Separate baseline GPOs | Provides independent management of workstations and domain controllers. |
| Link GPOs to OUs | Limits policy scope and follows enterprise best practices. |
| Advanced Audit Policy | Provides granular auditing and avoids legacy audit policy conflicts. |
| Visibility before hardening | Logging is established before restrictive security controls are introduced. |
| Validate every configuration | Native Windows tools verify effective policy rather than assuming successful deployment. |

---

# Challenges Encountered

During initial deployment, the RDP session to WIN11-01 disconnected immediately following a Group Policy refresh.

Investigation confirmed:

- Group Policy successfully applied.
- Advanced Audit Policies were configured correctly.
- Audit policies did not impact remote connectivity.
- The disconnect appeared to be a temporary interruption during policy refresh rather than a configuration issue.

This reinforced the importance of validating Group Policy changes incrementally and confirming effective configuration using native administration tools.

---

# Outcome

Project 04 successfully established the Enterprise Security Lab's Group Policy architecture and deployed the first centralized security controls through Advanced Audit Policy.

The environment now supports centralized Windows configuration management and provides foundational auditing that will support future security monitoring through Windows Event Forwarding, Wazuh, Microsoft Defender, and Microsoft Sentinel.

---

**Project Status:** 🚧 In Progress

**Completed Capability:** Audit & Accountability

**Next Capability:** PowerShell Visibility
