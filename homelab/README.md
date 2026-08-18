## Home Lab
# Overview

This repository documents the design, implementation, troubleshooting, and continuous development of my personal home lab.

The lab is designed as a hands-on environment for developing practical skills in:

Enterprise networking
Infrastructure administration
Virtualization
Identity management
Cybersecurity
Security monitoring
Automation
Systems integration
Infrastructure recovery

Rather than building a collection of isolated systems, the environment is designed as an interconnected infrastructure platform where networking, identity, security, monitoring, automation, and application services work together.

The lab also serves as a controlled environment for experimenting with technologies, testing security concepts, troubleshooting failures, and documenting real-world engineering decisions.

Goals

The primary goals of the lab are:

Develop practical infrastructure and cybersecurity skills.
Understand enterprise networking concepts through hands-on implementation.
Build and maintain a segmented and security-focused network.
Develop experience with Windows and Linux infrastructure.
Practice identity and access management.
Implement security monitoring and detection capabilities.
Build event-driven automation workflows.
Develop troubleshooting and recovery skills.
Document engineering decisions and lessons learned.
Architecture

The lab is built around several major infrastructure layers.

                         Internet
                            |
                            v
                     +-------------+
                     |   OPNsense  |
                     |   Firewall  |
                     +------+------+
                            |
                       Network Core
                            |
             +--------------+--------------+
             |              |              |
        Virtualization    Storage       Wireless
          Platform       Platform      Infrastructure
             |              |              |
       +-----+-----+        |        +-----+-----+
       |     |     |        |        |     |     |
      AD   Security Apps   Data     Trusted IoT Guest

The architecture is intentionally modular so individual services can be developed, replaced, or recovered without requiring the entire environment to be rebuilt.

Exact network addressing, hostnames, management interfaces, credentials, and other sensitive operational information are intentionally excluded from the public repository.

Core Platforms
Network Security

OPNsense

Provides the primary security boundary for the environment, including:

Routing
Stateful firewalling
Network segmentation
DNS services
DHCP
WireGuard
Intrusion detection
Security monitoring integrations

See:

Building a Secure Network with OPNsense

Virtualization

Proxmox VE

Provides the virtualization platform used to host infrastructure and application workloads.

The virtualization environment provides an opportunity to develop experience with:

Virtual machines
Linux and Windows workloads
Virtual networking
Storage management
Snapshots
Guest agents
Infrastructure recovery
Storage

Unraid

Provides the primary storage and application platform for the lab.

The environment is used to develop experience with:

Array management
Parity protection
Enterprise storage hardware
Docker applications
Storage troubleshooting
Hardware diagnostics
Recovery procedures

A major storage upgrade and recovery operation is documented separately as a case study.

Identity

Active Directory

The lab includes an Active Directory environment used as the foundation for Windows enterprise security projects.

The environment provides experience with:

Active Directory Domain Services
DNS
Group Policy
Windows authentication
Domain-joined endpoints
Windows security monitoring

See:

Project 01 - Active Directory Foundation

Security Monitoring

The lab is being developed as a security monitoring and detection engineering environment.

Technologies include:

Wazuh
Sysmon
Windows Event Forwarding
Microsoft Sentinel
Suricata
CrowdSec
DNS filtering
Grafana
InfluxDB

These technologies provide opportunities to study:

Endpoint telemetry
Network detection
Log collection
Alerting
Security visibility
Threat detection
Incident investigation
Automation

The lab also includes an event-driven automation platform built around Home Assistant and n8n.

The platform integrates physical sensors, APIs, webhooks, workflow logic, and automated actions.

See:

Project 07 - Intelligent Presence Automation

Engineering Philosophy

The lab is built around several principles.

Learn by Building

Technologies are implemented rather than simply studied theoretically.

Each system provides an opportunity to understand how infrastructure behaves under real operating conditions.

Document the Why

Documentation focuses not only on configuration, but also on the reasoning behind engineering decisions.

Validate Before Declaring Success

Systems are tested after implementation rather than assuming that a successful installation means the system is functioning correctly.

Troubleshoot Methodically

When something fails, the goal is to understand the underlying problem rather than immediately rebuilding or replacing the system.

Design for Recovery

Infrastructure should be recoverable.

Configuration backups, snapshots, documentation, and tested recovery procedures are treated as important parts of the environment.

Security by Design

Security is incorporated into architecture decisions rather than added only after deployment.

Continuous Improvement

The lab is intentionally unfinished.

Systems are continuously refined as new technologies are introduced, existing designs are evaluated, and lessons are learned.

Projects

The lab is organized into individual projects that build upon one another.

Project	Description	Status
Project 01	Active Directory Foundation	Complete
Project 02	Windows Endpoint Deployment	Planned / In Progress
Project 03	Sysmon Deployment	Planned
Project 04	Windows Event Forwarding	Planned
Project 05	Wazuh Integration	Planned
Project 06	Microsoft Sentinel	Planned
Project 07	Intelligent Presence Automation	In Progress

Projects are documented independently so that implementation details, validation results, troubleshooting, and lessons learned can be maintained without turning the main repository documentation into a single large configuration guide.

Case Studies

In addition to project documentation, significant infrastructure events are documented as case studies.

Case studies focus on real problems encountered during operation of the lab.

They document:

The problem
Investigation
Diagnostics
Recovery
Validation
Engineering decisions
Lessons learned

Examples include:

Recovering an Unraid Array During a Parity Upgrade
Rebuilding and Restoring the OPNsense Firewall
Future infrastructure recovery and security investigations

These case studies demonstrate the troubleshooting and operational side of infrastructure engineering.

Documentation

The repository separates documentation into several categories.

Architecture

High-level descriptions of how systems interact.

Projects

Detailed implementation and learning objectives for individual technologies.

Case Studies

Real-world troubleshooting, recovery, and engineering experiences.

Current State

A high-level view of the technologies currently deployed in the lab.

Lessons Learned

Important technical and operational knowledge gained through experimentation and troubleshooting.

Public Documentation

This repository is intentionally written as a public-facing technical portfolio.

Sensitive operational information is excluded.

The public documentation does not contain:

Passwords
API tokens
Private keys
Recovery codes
Internal credentials
Management credentials
Sensitive host information
Private network addressing
Internal management URLs
Other information that could compromise the environment

The goal is to demonstrate architecture, engineering decisions, troubleshooting methodology, and technical skills without exposing the operational security of the environment.

Current Focus

Current development is focused on expanding the security and automation capabilities of the lab.

Areas of active development include:

OPNsense network security
Active Directory
Windows endpoint security
Security monitoring
Wazuh
Sysmon
Home Assistant
n8n
Presence detection
Event-driven automation
Infrastructure recovery
Skills Demonstrated

The lab provides hands-on experience across multiple areas of infrastructure and cybersecurity, including:

Network administration
Firewall administration
VLAN architecture
Virtualization
Windows Server administration
Active Directory
DNS
DHCP
Linux administration
Docker
Storage administration
Security monitoring
Endpoint telemetry
IDS/IPS
VPN administration
API integration
Webhooks
Workflow automation
Infrastructure troubleshooting
Disaster recovery
Technical documentation
Philosophy

The goal of this lab is not to build the most complicated infrastructure possible.

The goal is to build systems that I understand.

Every major implementation should provide an opportunity to answer four questions:

Why was this technology selected?
How was it implemented?
How was it validated?
What was learned from operating it?

The lab will continue to evolve as new technologies, security concepts, and engineering challenges are introduced.
