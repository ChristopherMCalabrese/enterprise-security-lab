# Project 05 – Sysmon and Wazuh Integration

## Overview

This project introduced enhanced Windows endpoint telemetry by deploying Sysmon on the domain controller and forwarding those events to the Wazuh SIEM platform.

The goal was to create an end-to-end detection pipeline capable of collecting detailed process, network, file, and registry activity from Windows systems and analyzing that telemetry using Wazuh detection rules and MITRE ATT&CK mappings.

---

## Objectives

- Install Sysmon on DC01.
- Apply a production-oriented Sysmon configuration.
- Verify Sysmon event generation locally.
- Install and enroll the Wazuh Windows agent.
- Forward the Sysmon Operational event channel to Wazuh.
- Validate successful ingestion and alert generation.
- Confirm MITRE ATT&CK mappings within Wazuh alerts.

---

## Environment

### Windows Endpoint

- Hostname: `DC01`
- Role: Active Directory Domain Controller
- Domain: `lab.home.arpa`
- IP Address: `10.10.10.21`

### Wazuh Server

- Hostname: `wazuh`
- IP Address: `10.10.10.25`
- Wazuh Version: `4.14.5`

### Agent Information

- Agent ID: `004`
- Agent Name: `DC01`
- Status: `Active`

---

## Sysmon Deployment

Sysmon was installed on DC01 using the 64-bit Sysinternals executable and a community-maintained configuration.

The installation created the following Windows event channel:

```text
Microsoft-Windows-Sysmon/Operational
