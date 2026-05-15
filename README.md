# Splunk SOC Monitoring Lab

**Analyst:** Andy Dela Quarshie Wright  
**Role:** SOC Level 1 Analyst  
**Tools:** Splunk Cloud, Wireshark, Nmap, Kali Linux  

---

## Overview

Home SIEM lab built using Splunk Cloud to simulate and detect real-world threats. Three scenarios covering a full attack chain — from initial reconnaissance through to data exfiltration — all detected using custom SPL queries and Splunk alerts.

---

## Scenarios

| # | Scenario | Attacker IP | Severity | MITRE ATT&CK |
|---|----------|-------------|----------|--------------|
| 1 | Brute Force / Failed Login Detection | 185.220.101.48 | High | T1110 |
| 2 | Network Port Scan Detection | 194.165.16.73 | Medium | T1046 |
| 3 | Malware, C2 Beaconing & Exfiltration | 185.220.101.48 / 194.165.16.73 | Critical | T1059, T1053, T1136, T1041, T1003 |

---

## Incident Reports

- [Scenario 1 — Brute Force Detection](scenarios/brute-force.md)
- [Scenario 2 — Network Port Scan Detection](scenarios/network-scan.md)
- [Scenario 3 — Malware, C2 & Exfiltration](scenarios/malware-simulation.md)

---

## Full SOC Incident Report

Full structured report with screenshots and analyst findings:  
[Andy_Wright_SOC_Incident_Report_v2.pdf](reports/Andy_Wright_SOC_Incident_Report_v2.pdf)

---

## SPL Detection Queries

All queries used across the three scenarios:  
[detections/spl-queries.md](detections/spl-queries.md)

---

## Setup

[setup/splunk-setup-guide.md](setup/splunk-setup-guide.md)

---

## Skills Demonstrated

- Splunk Cloud — data ingestion, SPL search, alert creation
- Log analysis — Linux auth logs, UFW firewall logs, audit logs
- Threat detection — brute force, port scan, malware, C2 beaconing, exfiltration
- MITRE ATT&CK mapping across all three scenarios
- Structured SOC incident report documentation

---

## Certifications

- CompTIA Security+
- TryHackMe SOC Level 1
- Google Cybersecurity Professional Certificate
