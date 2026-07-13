# Project 03 – Active Directory Organization and Administration

## Objective

Design and implement an enterprise-style Active Directory organizational structure by creating Organizational Units (OUs), administrative accounts, standard user accounts, and security groups following least-privilege and role-based access control (RBAC) principles.

This project establishes the identity management foundation that will support Group Policy, endpoint management, delegated administration, Windows Event Forwarding, Wazuh, Microsoft Defender, and Microsoft Sentinel throughout the remainder of the Enterprise Security Lab.

---

# Learning Objectives

- Design an enterprise Organizational Unit (OU) hierarchy.
- Separate administrative and standard user identities.
- Implement Role-Based Access Control (RBAC).
- Create Global Security Groups following Microsoft best practices.
- Establish naming standards for Active Directory objects.
- Prepare the directory structure for Group Policy deployment.

---

# Technologies

## Implemented

- Windows Server 2022
- Active Directory Domain Services
- Active Directory Users and Computers (ADUC)
- Active Directory PowerShell Module
- DNS
- Windows 11 Enterprise

## Planned

- Group Policy
- Sysmon
- Windows Event Forwarding
- Wazuh
- Microsoft Defender
- Microsoft Sentinel

---

# Progress

- [x] Administrative OU created
- [x] Administrative Users OU created
- [x] Administrative Groups OU created
- [x] Workstations OU created
- [x] Administrative account created
- [x] Standard user account created
- [x] Administrative account renamed using enterprise naming standards
- [x] Administrative account added to Domain Admins
- [x] Standard user validated
- [x] Built-in Administrator account disabled
- [x] Global Security Groups created
- [x] Administrative group memberships assigned
- [x] Naming standards documented
- [ ] Workstation Baseline GPO created
- [ ] Group Policy validated
- [ ] Baseline snapshot created

---

# Organizational Unit Structure

```text
lab.home.arpa
│
├── Administrative
│   ├── Groups
│   └── Users
│
├── Workstations
│
├── Builtin
├── Computers
├── Domain Controllers
├── ForeignSecurityPrincipals
├── Managed Service Accounts
├── Service Accounts
└── Users
```

---

# Administrative Accounts

| Account | Purpose |
|----------|---------|
| adm-ccalabrese | Enterprise administration |
| ccalabrese | Daily user account |

The built-in **Administrator** account has been disabled after validating administrative access through the dedicated administrative account.

---

# Security Groups

| Group | Purpose |
|---------|---------|
| Domain Admins | Domain-wide administration |
| GG-Server-Operators | Windows server administration |
| GG-Workstation-Admins | Windows workstation administration |
| GG-Helpdesk | Tier 1 support (reserved) |
| GG-Wazuh-Admins | Wazuh administration |
| GG-Sentinel-Admins | Microsoft Sentinel administration |

---

# Engineering Decisions

| Decision | Reason |
|----------|--------|
| Separate admin account | Enforces least privilege and aligns with enterprise security practices |
| Disable built-in Administrator | Reduces attack surface and encourages named administrative identities |
| Administrative OU | Centralizes privileged identities and administrative groups |
| Global Security Groups | Implements Role-Based Access Control (RBAC) |
| Enterprise naming standards | Improves consistency, scalability, and maintainability |

---

# Validation

The project was validated by confirming:

- Administrative account successfully authenticates
- Standard user successfully authenticates
- Administrative privileges function correctly
- Built-in Administrator account disabled
- Organizational Units created successfully
- Security Groups created successfully
- Administrative memberships validated
- Active Directory PowerShell management functional

---

# Challenges Encountered

During implementation, Active Directory Users and Computers (ADUC) intermittently became unresponsive after object modifications. Investigation determined:

- Active Directory services remained healthy.
- LDAP queries completed successfully.
- PowerShell administration functioned normally.
- Directory objects were created and modified successfully despite ADUC UI freezes.

PowerShell was used to validate Active Directory functionality and continue administration while troubleshooting the management console.

This reinforced the importance of validating directory health independently of graphical management tools.

---

# Outcome

The Enterprise Security Lab now includes a structured Active Directory environment built around enterprise identity management principles.

Administrative identities, standard user accounts, Organizational Units, naming standards, and role-based security groups provide a scalable foundation for future projects involving Group Policy, endpoint hardening, centralized logging, endpoint monitoring, and security operations.

---

**Project Status:** ✅ Complete (Pending Group Policy Baseline)

**Next Project:** Project 04 – Group Policy Baseline
