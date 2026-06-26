# Enterprise Security Lab

## Overview

This repository documents my enterprise-inspired cybersecurity lab, built to develop practical skills in identity, infrastructure, networking, and security operations while applying enterprise security principles to my own home environment.

Rather than treating technologies as isolated tools, I designed this lab to better understand how identity, networking, monitoring, and layered security controls work together to reduce risk and improve operational visibility.

Everything documented here reflects technologies I actively use, decisions I've made, lessons I've learned, and areas I'm continuing to improve.

---

## Design Goals

* Apply enterprise security principles to a home environment.
* Strengthen practical skills through hands-on experimentation.
* Build and document repeatable, well-understood solutions.
* Validate security concepts before recommending similar approaches professionally.
* Continuously improve the environment as new technologies and security practices evolve.

---

## High-Level Architecture

```text
Internet
    │
Cox Gateway
    │
OPNsense Firewall
    │
UniFi Switching
    │
────────────────────────────────
│          │         │         │
Main      IoT      Media     Guest
    │
Unraid • Proxmox • Infrastructure
```

---

## Core Technologies

### Infrastructure

* Proxmox
* Unraid
* Docker

### Identity

* Microsoft Entra ID
* Active Directory *(currently under development)*

### Networking

* OPNsense
* UniFi Switching
* WireGuard VPN
* VLAN Segmentation
* DNS
* DHCP (Dnsmasq)

### Security

* Microsoft Defender
* CrowdSec
* Suricata IDS
* Unbound DNS Filtering

### Monitoring

* Grafana
* InfluxDB
* UniFi Poller
* Telegraf

---

## Repository Contents

* **docs/** — Detailed documentation covering architecture, networking, identity, monitoring, and future plans.
* **diagrams/** — Network and architecture diagrams.
* **projects/** — Individual projects, configuration decisions, and lessons learned.
* **images/** — Supporting screenshots and diagrams.

---

## Current Roadmap

* Expand Active Directory implementation.
* Integrate Microsoft Entra ID with on-premises identity.
* Forward security telemetry into Wazuh.
* Continue refining network segmentation and security monitoring.
* Document security decisions, architecture changes, and lessons learned.
