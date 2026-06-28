# Wazuh

## Overview

Wazuh serves as the Security Information and Event Management (SIEM) platform for the lab. It provides centralized visibility into security events, log collection, file integrity monitoring, vulnerability detection, and endpoint security.

The goal of deploying Wazuh is to gain practical experience building a Security Operations Center (SOC)-style environment while improving visibility into systems throughout the network.

---

# Objectives

The Wazuh deployment is designed to:

- Centralize security events
- Improve endpoint visibility
- Detect suspicious activity
- Develop incident investigation skills
- Build practical SIEM experience

---

# Architecture

Current deployment includes:

- Wazuh Manager
- Wazuh Dashboard
- Elasticsearch / OpenSearch backend
- Endpoint Agents
- Syslog Integration (planned)

---

# Current Capabilities

- Security event collection
- Endpoint monitoring
- File Integrity Monitoring (FIM)
- Vulnerability Detection
- Security Configuration Assessment
- MITRE ATT&CK Mapping
- Dashboard Visualizations

---

# Future Enhancements

- Suricata log integration
- CrowdSec integration
- Windows Event Forwarding
- Active Directory auditing
- Microsoft Defender integration
- Custom detection rules

---

# Lessons Learned

Deploying Wazuh has provided valuable insight into how enterprise SIEM platforms aggregate, correlate, and present security events. Building detections and reducing alert noise has reinforced the importance of tuning, context, and visibility when operating a security monitoring platform.
