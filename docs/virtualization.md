# Virtualization

## Overview

Virtualization provides the foundation for the lab by allowing services, operating systems, and security tools to be deployed in isolated environments while efficiently utilizing hardware resources.

The environment is designed to resemble a small enterprise infrastructure where services can be deployed, tested, updated, and restored without affecting production systems.

---

# Objectives

The virtualization platform supports several goals:

- Isolate workloads
- Improve resource utilization
- Simplify testing and experimentation
- Reduce recovery time
- Support future expansion

---

# Virtualization Platform

## Proxmox VE

Proxmox serves as the primary hypervisor for the lab.

Reasons for selecting Proxmox include:

- Enterprise-grade virtualization
- Built-in snapshot capability
- Flexible storage options
- Excellent networking support
- Strong community documentation
- Open-source platform

---

# Storage Platform

## Unraid

Unraid provides centralized storage and hosts Docker containers supporting infrastructure and application services.

Benefits include:

- Flexible storage expansion
- Docker support
- Simple administration
- Reliable data storage
- Home lab flexibility

---

# Container Platform

Docker is used to isolate applications into individual containers, simplifying deployment, updates, and maintenance.

Current services include:

### Infrastructure

- UniFi Network Application
- UniFi Database

### Monitoring

- Grafana
- InfluxDB
- Telegraf
- UniFi Poller

### Security

- CrowdSec

### Productivity

- Vaultwarden
- Home Assistant
- Immich

### Media

- Plex
- Sonarr
- Radarr
- Prowlarr
- qBittorrent

---

# Design Principles

The virtualization environment is designed around several principles.

## Isolation

Applications are deployed independently whenever practical to reduce dependencies and simplify maintenance.

---

## Scalability

The environment is designed to support future expansion without significant architectural changes.

---

## Reliability

Snapshots, backups, and containerization reduce downtime during upgrades and experimentation.

---

## Learning Through Practice

Virtualization provides a safe environment to deploy new technologies, validate configurations, and understand enterprise infrastructure without impacting production systems.

---

# Future Enhancements

Current roadmap includes:

- Expand Windows Server environment
- Deploy additional Linux servers
- Evaluate Kubernetes
- Expand security monitoring workloads
- Increase automation
- Continue documenting architecture decisions

---

# Lessons Learned

Virtualization has become one of the most valuable components of the lab.

Being able to quickly deploy, modify, snapshot, and recover systems has significantly accelerated learning while reducing the risk associated with experimentation.
