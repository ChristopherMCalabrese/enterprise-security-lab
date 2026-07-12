# Project 03 – Active Directory Administration

## Status

🟡 In Progress

---

## Objective

Transform the Active Directory deployment into a manageable enterprise environment by implementing an organizational unit (OU) structure, administrative delegation, security groups, and baseline Group Policy Objects (GPOs). This project establishes the administrative framework that will support endpoint hardening, centralized management, and future security monitoring initiatives.

---

## Why This Project Matters

Enterprise Active Directory environments are organized around logical administration rather than individual systems. Organizational Units, security groups, and Group Policy enable centralized management, delegated administration, and consistent security configuration across all domain-joined systems.

This project establishes the administrative structure that future projects—including Sysmon, Windows Event Forwarding, Wazuh, Microsoft Defender, and Microsoft Sentinel—will leverage for automated deployment and policy enforcement.

---

## Learning Objectives

- Design an enterprise Organizational Unit (OU) structure.
- Implement logical administrative separation.
- Create administrative and standard user accounts.
- Implement role-based security groups.
- Create and link custom Group Policy Objects.
- Validate Group Policy inheritance and processing.
- Prepare the environment for centralized endpoint management.

---

## Technologies

### Implemented

- Active Directory Domain Services
- Active Directory Users and Computers
- Group Policy Management
- DNS

### Planned

- Sysmon
- Windows Event Forwarding
- Wazuh Agent
- Microsoft Defender
- Microsoft Sentinel

---

## Progress

- [ ] Design Organizational Unit structure
- [ ] Create Administrative OU
- [ ] Create Servers OU
- [ ] Create Workstations OU
- [ ] Create Users OU
- [ ] Create Groups OU
- [ ] Create Service Accounts OU
- [ ] Create administrative user account
- [ ] Create standard user account
- [ ] Create administrative security groups
- [ ] Create workstation security groups
- [ ] Move WIN11-01 into the Workstations OU
- [ ] Create Workstation Baseline GPO
- [ ] Create Server Baseline GPO
- [ ] Create Windows Firewall GPO
- [ ] Create Microsoft Defender GPO
- [ ] Validate Group Policy processing
- [ ] Validate Group Policy inheritance
- [ ] Document OU hierarchy
- [ ] Baseline Proxmox snapshot created

---

## Proposed Organizational Structure

```text
lab.home.arpa
│
├── Domain Controllers
│
├── Administrative
│   ├── Users
│   └── Groups
│
├── Servers
│
├── Workstations
│
├── Users
│
├── Groups
│
└── Service Accounts
```

---

## Engineering Decisions

| Decision | Reason |
|----------|--------|
| Separate OUs by administrative function | Simplifies administration and Group Policy targeting |
| Dedicated administrative accounts | Supports least-privilege administration |
| Separate administrative and standard users | Reduces administrative exposure and aligns with enterprise security practices |
| Security groups for permissions | Enables role-based access control and scalable permission management |
| Custom Group Policy Objects | Preserves default policies and simplifies troubleshooting |
| Separate workstation and server policies | Allows security baselines to evolve independently |

---

## Validation

The deployment will be validated by confirming:

- Organizational Units created successfully
- Administrative and standard user authentication
- Security group membership
- Correct OU placement of domain objects
- Successful Group Policy inheritance
- Successful `gpupdate /force`
- Successful `gpresult /r`

---

## Outcome

Upon completion, the Active Directory environment will support centralized administration through Organizational Units, security groups, and custom Group Policy Objects. This administrative framework will provide the foundation for enterprise endpoint hardening, automated software deployment, centralized logging, and security monitoring throughout the remainder of the Enterprise Security Lab.

---

## Next Project

**Project 04 – Sysmon Deployment**

Objectives:

- Deploy Sysmon
- Deploy the SwiftOnSecurity configuration
- Validate event generation
- Prepare centralized log collection

---

## Related Projects

- Project 01 – Active Directory Foundation
- Project 02 – Windows Endpoint Deployment
- Project 04 – Sysmon Deployment
- Project 05 – Windows Event Forwarding
- Project 06 – Wazuh Integration
- Project 07 – Microsoft Sentinel
