# Enterprise Security Lab

## Overview

This repository documents an enterprise-inspired home lab designed to strengthen practical cybersecurity, infrastructure, and security operations skills.

Rather than focusing on individual technologies, this environment emphasizes layered security, network segmentation, identity management, monitoring, and operational visibility.

The lab serves two purposes:

- Protect my home environment using enterprise security principles.
- Develop hands-on experience with technologies commonly found in modern business environments.

---

# Architecture

Internet

↓

Cox Gateway

↓

OPNsense Firewall

↓

UniFi Switching

↓

Segmented VLANs

↓

Servers / Clients / IoT / Guest

---

## Core Infrastructure

Firewall

- OPNsense

Virtualization

- Proxmox

Storage

- Unraid

Container Platform

- Docker

Wireless

- UniFi U7 Pro Max

Switching

- UniFi Pro XG
- UniFi Pro Max PoE

---

## Security

Identity

- Microsoft Entra ID
- Active Directory (in progress)

Network Security

- VLAN Segmentation
- WireGuard VPN
- Suricata IDS
- CrowdSec

DNS Protection

- Unbound
- HaGeZi Blocklists
- Steven Black List

Monitoring

- Grafana
- InfluxDB
- UniFi Poller
- Telegraf

---

## Objectives

- Identity & Access Management
- Detection Engineering
- Security Monitoring
- Incident Response
- Secure Network Architecture
- Infrastructure Automation
