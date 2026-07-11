# Building a Secure Network with OPNsense

## Overview

OPNsense serves as the security boundary for my home lab, providing routing, firewall policy, DNS services, DHCP, VPN connectivity, intrusion detection, and network segmentation.

Rather than selecting a firewall based solely on features, I wanted a platform that would allow me to better understand enterprise networking concepts while remaining flexible enough to support continuous experimentation.

---

## Objectives

The firewall should:

* Protect the internal network.
* Support secure remote administration.
* Enable network segmentation.
* Provide visibility into network traffic.
* Support future security integrations.

---

## Why OPNsense?

I selected OPNsense because it provides a modern, open-source firewall platform with capabilities commonly found in enterprise and SMB environments.

Key features include:

* Stateful firewall
* VLAN support
* WireGuard VPN
* Suricata IDS/IPS
* Unbound DNS
* Flexible routing
* Extensive logging and monitoring

It also has an active community and excellent documentation, making it an excellent platform for continuous learning.

---

## Security Design

Rather than relying on a single security control, the environment uses multiple defensive layers.

Current controls include:

* Network segmentation
* WireGuard VPN
* Suricata IDS
* CrowdSec
* DNS filtering
* Stateful firewall policies

Each layer provides additional protection while reducing reliance on any individual technology.

---

## Key Decisions

### VLAN Segmentation

IoT, media, and guest devices are separated from trusted systems to reduce unnecessary communication and limit the impact of a compromised device.

---

### DNS Protection

Unbound provides local DNS resolution while blocking known malicious, advertising, and tracking domains through community-maintained blocklists.

---

### WireGuard

Remote administration is performed through WireGuard rather than exposing management interfaces directly to the Internet.

---

### Suricata

Suricata currently operates in IDS mode.

Running in IDS mode allows me to understand normal traffic patterns, evaluate alerts, and tune detections before considering IPS enforcement.

---

## Challenges

One issue encountered during deployment involved DHCP services running simultaneously through both ISC DHCP and Dnsmasq.

After identifying the conflict, DHCP services were consolidated into Dnsmasq, simplifying administration and eliminating address conflicts.

---

## Lessons Learned

Building a firewall is relatively straightforward.

Building a network that is secure, understandable, and maintainable requires thoughtful planning and continuous refinement.

One of the most valuable lessons has been learning to make intentional design decisions instead of simply enabling every available security feature.
