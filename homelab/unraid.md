# Unraid Infrastructure

## Overview

This Unraid server serves as the core of my enterprise security lab and home infrastructure. It provides centralized storage, virtualization, container hosting, monitoring, network services, and media management while remaining resilient against hardware failures.

The server is designed to simulate a small enterprise environment where infrastructure, networking, security, and monitoring platforms work together.

---

# Objectives

* Centralized NAS for enterprise-style storage
* Docker container platform
* Infrastructure monitoring and observability
* Security monitoring and log aggregation
* Identity and network service integration
* Enterprise backup and recovery testing
* Media streaming and home services

---

# Hardware

| Component          | Details                         |
| ------------------ | ------------------------------- |
| Motherboard        | Supermicro X11SSL-CF            |
| CPU                | Intel Xeon E3-1275 v6           |
| Memory             | 64 GB ECC DDR4                  |
| Storage Controller | Broadcom / LSI SAS3008 SAS3 HBA |
| Cache Drive        | Samsung 860 EVO 250 GB SSD      |
| Boot Device        | SanDisk Cruzer Fit USB          |

---

# Array Configuration

## Parity

* 1 × 26 TB Seagate Exos

## Data Drives

* 3 × 12 TB Western Digital Ultrastar
* 4 × 16 TB Seagate Exos

Approximate usable capacity:

* 100 TB
* Single parity protection

---

# Services

The server hosts multiple production Docker containers including:

## Infrastructure

* Grafana
* InfluxDB
* Telegraf

Used for system metrics, dashboards, and long-term monitoring.

---

## Security

* CrowdSec
* Wazuh Agent

Provides host monitoring, behavioral analysis, and centralized security visibility.

---

## Networking

* AdGuard Home
* UniFi Network Application

Responsible for DNS filtering, network management, and infrastructure administration.

---

## Home Automation

* Home Assistant

Central management platform for IoT devices.

---

## Media

* Plex Media Server
* Sonarr
* Radarr
* Prowlarr
* qBittorrent

Automated media management and streaming platform.

---

## Password Management

* Vaultwarden

Self-hosted Bitwarden-compatible password manager.

---

## Photo Management

* Immich

Self-hosted photo backup and management solution.

---

# Monitoring

System metrics are collected through Telegraf and stored in InfluxDB.

Grafana dashboards monitor:

* CPU utilization
* Memory usage
* Disk throughput
* Docker containers
* Network traffic
* Storage utilization
* System health

---

# Storage Design

The storage subsystem uses Unraid's parity-based architecture rather than traditional RAID.

Benefits include:

* Individual disks remain independently readable
* Mixed drive sizes are supported
* Lower power consumption
* Easier future expansion

---

# Networking

The server integrates into a segmented network managed by OPNsense and UniFi infrastructure.

Current services include:

* Management LAN
* IoT VLAN
* Media VLAN
* Guest Network

Static addressing is used for infrastructure services.

---

# Remote Management

The server utilizes the onboard Supermicro IPMI controller for:

* Out-of-band management
* Remote console (KVM)
* BIOS access
* Power control
* Hardware monitoring

This allows complete administration even when the operating system is unavailable.

---

# Troubleshooting Experience

During a scheduled parity drive upgrade from 16 TB to 26 TB, the array experienced an unexpected second reconstruction after replacing a failing data drive.

Investigation included:

* Reviewing Unraid md driver status
* Monitoring reconstruction progress via CLI
* Analyzing SMART diagnostics
* Validating SAS controller connectivity
* Replacing SATA/SAS cabling
* Verifying parity consistency
* Confirming successful rebuild completion

This incident reinforced practical experience with:

* Unraid recovery procedures
* Disk replacement workflows
* SMART analysis
* Hardware troubleshooting
* Data integrity validation

---

# Lessons Learned

Key operational lessons include:

* ECC memory significantly improves storage reliability.
* IPMI provides critical recovery capabilities during outages.
* Continuous monitoring enables proactive maintenance.
* Enterprise SAS controllers offer greater reliability than consumer SATA implementations.
* Documentation greatly simplifies troubleshooting during hardware failures.

---

# Future Improvements

Planned enhancements include:

* Secondary backup NAS
* Automated off-site backups
* Prometheus integration
* CrowdSec remediation automation
* Additional Grafana dashboards
* Infrastructure-as-Code documentation
* Automated disaster recovery testing
