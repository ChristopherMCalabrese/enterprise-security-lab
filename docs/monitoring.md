# Security Monitoring

## Overview

Visibility is a fundamental component of cybersecurity. Security controls are only effective if they provide actionable information when systems deviate from expected behavior.

This environment uses multiple monitoring and detection platforms to improve visibility across infrastructure, networking, and endpoints while providing opportunities to develop practical Security Operations experience.

---

# Monitoring Objectives

The monitoring strategy is designed around four primary goals:

* Detect abnormal activity.
* Monitor infrastructure health.
* Improve operational visibility.
* Develop practical Security Operations skills.

---

# Monitoring Stack

## Grafana

Grafana provides centralized dashboards for infrastructure health, network performance, and service monitoring.

Current dashboards include:

* Infrastructure metrics
* UniFi network statistics
* System utilization
* Docker services

---

## InfluxDB

InfluxDB stores time-series metrics collected from infrastructure and monitoring tools.

Current data sources include:

* UniFi Poller
* Telegraf
* Infrastructure metrics

---

## Telegraf

Telegraf collects operational metrics from systems throughout the environment and forwards them into InfluxDB.

Collected metrics include:

* CPU utilization
* Memory usage
* Storage utilization
* Network throughput
* System performance

---

## UniFi Poller

UniFi Poller collects telemetry from UniFi infrastructure and provides historical reporting within Grafana.

Examples include:

* Client activity
* Switch statistics
* Wireless performance
* Interface utilization

---

# Security Monitoring

## CrowdSec

CrowdSec analyzes logs and identifies malicious behavior through collaborative threat intelligence.

Current implementation focuses on:

* Behavioral analysis
* Reputation-based detection
* Automated decision making

---

## Suricata IDS

Suricata monitors WAN traffic using approximately 41,000 IDS signatures.

The system currently operates in IDS mode to allow alert tuning before evaluating IPS deployment.

Current objectives include:

* Understand normal network behavior
* Reduce false positives
* Improve alert quality

---

## DNS Protection

Unbound provides DNS-based threat reduction using:

* HaGeZi Multi NORMAL
* Steven Black

These blocklists reduce access to known malicious, advertising, and tracking domains before connections are established.

---

# Future Enhancements

Current roadmap includes:

* Deploy Wazuh SIEM
* Forward Suricata events into Wazuh
* Centralize security event collection
* Develop custom detection rules
* Map detections to the MITRE ATT&CK framework
* Build investigation playbooks

---

# Lessons Learned

Effective monitoring is not simply collecting more logs.

The goal is to collect meaningful data, reduce noise, improve visibility, and produce information that supports investigation and decision making.
