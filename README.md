# Enterprise Security Lab

## Overview

This repository documents my enterprise-inspired cybersecurity lab, built to develop practical skills in identity, infrastructure, networking, virtualization, and security operations while applying enterprise security principles to my own home environment.

Rather than treating technologies as isolated tools, I designed this lab to understand how identity, networking, monitoring, virtualization, and layered security controls work together to reduce risk, improve operational visibility, and build resilient infrastructure.

Everything documented here reflects technologies I actively use, architectural decisions I've made, lessons learned, and areas I'm continuously improving.

---

# Design Goals

- Apply enterprise security principles to a home environment.
- Strengthen practical skills through hands-on experimentation.
- Build and document repeatable, well-understood solutions.
- Validate security concepts before recommending similar approaches professionally.
- Continuously improve the environment as new technologies and security practices evolve.
- Treat operational failures as learning opportunities by documenting root causes, recovery procedures, and infrastructure improvements.

---

# Operational Philosophy

This lab is operated using the same engineering principles applied in enterprise environments.

Changes are implemented through documented projects, validated before being considered complete, and followed by lessons learned whenever unexpected issues occur.

Major milestones are protected with virtual machine snapshots, infrastructure changes are documented, and operational improvements become standards for future projects.

The objective is not simply to build infrastructure, but to understand how to deploy, operate, troubleshoot, recover, and continuously improve enterprise systems.

---

# High-Level Architecture

```
                    Internet
                        │
                   Cox Gateway
                        │
                 OPNsense Firewall
                        │
                 UniFi Switching
                        │
────────────────────────────────────────────────────────
│              │              │               │
Main         IoT           Media           Guest
                        │
       ┌──────────────────────────────────┐
       │                                  │
   Unraid                          Proxmox VE
       │                                  │
 Docker Containers              Windows Infrastructure
       │                                  │
Grafana / InfluxDB             Active Directory
Telegraf                       Windows 11
UniFi Poller                   Wazuh SIEM
```

---

# Core Technologies

## Infrastructure

- Proxmox VE
- Unraid
- Docker

## Identity

- Microsoft Active Directory
- Microsoft Entra ID *(planned integration)*

## Networking

- OPNsense
- UniFi Switching
- WireGuard VPN
- VLAN Segmentation
- DNS
- DHCP (Dnsmasq)

## Security

- Microsoft Defender
- Wazuh SIEM
- Sysmon
- CrowdSec
- Suricata IDS
- Unbound DNS Filtering

## Monitoring

- Grafana
- InfluxDB
- Telegraf
- UniFi Poller

---

# Current Project Status

| Project | Status |
|----------|:------:|
| 01 - Active Directory Foundation | ✅ |
| 02 - Windows Endpoint Deployment | ✅ |
| 03 - Active Directory Administration | ✅ |
| 04 - Group Policy Baseline | ✅ |
| 05 - Endpoint Telemetry and SIEM Integration | ✅ |
| 06 - Detection Engineering | 🚧 In Progress |

---

# Skills Demonstrated

- Active Directory Administration
- Windows Server Administration
- Group Policy Management
- Windows Endpoint Deployment
- Virtualization with Proxmox
- Enterprise Networking
- VLAN Design
- Firewall Administration
- SIEM Deployment
- Endpoint Telemetry Collection
- Sysmon Configuration
- Security Monitoring
- MITRE ATT&CK Mapping
- PowerShell
- Documentation
- Troubleshooting
- Root Cause Analysis

---

# Repository Structure

```
Enterprise-Security-Lab/
│
├── architecture/
│   ├── network-diagrams.md
│   └── vm-inventory.md
│
├── case-studies/
│
├── docs/
│
├── homelab/
│
├── projects/
│   ├── 01 - Active Directory Foundation
│   ├── 02 - Windows Endpoint Deployment
│   ├── 03 - Active Directory Administration
│   ├── 04 - Group Policy Baseline
│   ├── 05 - Endpoint Telemetry and SIEM Integration
│   └── 06 - Detection Engineering
│
├── opnsense-firewall/
│
├── LICENSE
└── README.md
```

---

# Featured Projects

- **Project 01 – Active Directory Foundation**
- **Project 02 – Windows Endpoint Deployment**
- **Project 03 – Active Directory Administration**
- **Project 04 – Group Policy Baseline**
- **Project 05 – Endpoint Telemetry and SIEM Integration**
- **Project 06 – Detection Engineering** *(In Progress)*

---

# Current Roadmap

## Identity

- Expand Active Directory implementation.
- Integrate Microsoft Entra ID with on-premises identity.

## Infrastructure

- Standardize virtual machine lifecycle management.
- Configure LVM Thin Pool auto-extension.
- Continue refining network segmentation.
- Improve backup and recovery procedures.

## Monitoring

- Integrate Proxmox host metrics into Grafana.
- Monitor LVM Thin Pool utilization.
- Create infrastructure health alerts.
- Expand Wazuh telemetry collection.

## Security

- Continue hardening Windows and Linux systems.
- Expand endpoint visibility.
- Improve centralized logging.
- Develop custom Wazuh detection rules.
- Perform attack simulations and incident response exercises.

## Documentation

- Continue documenting projects.
- Record architectural decisions.
- Maintain lessons learned from operational incidents.
- Document recovery procedures and infrastructure standards.

---

# Operational Standards

## Snapshot Policy

- Create one disk-only snapshot before each major project.
- Do not include VM memory unless troubleshooting.
- Validate project completion before removing older snapshots.
- Maintain one milestone snapshot per virtual machine.

## Documentation Policy

Every major project includes:

- Objectives
- Implementation
- Validation
- Lessons Learned
- Future Improvements

## Monitoring Policy

Critical infrastructure should generate alerts for:

- Storage utilization
- Host availability
- Virtual machine availability
- Backup failures
- Security monitoring health

---

# Lessons Learned

One of the primary goals of this lab is learning through both successful implementations and operational failures.

Notable lessons include:

- Infrastructure issues often present as operating system problems.
- Thin-provisioned storage requires active monitoring.
- Disk-only snapshots are preferable to memory snapshots for long-term rollback points.
- Root cause analysis is more valuable than simply restoring service.
- Operational standards evolve through real-world experience.

These lessons are documented alongside each project to continuously improve both the lab and my operational practices.

---

# Purpose

This repository represents the ongoing development of a practical enterprise security environment.

Rather than focusing solely on individual technologies, the objective is to understand how infrastructure, identity, networking, monitoring, and security controls work together to create a resilient, maintainable, and secure environment.

As the lab evolves, the documentation evolves with it—capturing not only successful implementations, but also the troubleshooting, recovery, and operational improvements that are part of managing enterprise infrastructure.
