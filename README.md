# 🛡️ Splunk SOC Monitoring Lab

**Analyst:** Andy Dela Quarshie Wright  
**Role:** SOC Level 1 Analyst  
**Tools:** Splunk Cloud, Wireshark, Nmap, Kali Linux, macOS  

---

## Overview

Home SIEM lab built using Splunk Cloud to simulate and detect real-world threats. Three scenarios covering a full attack chain — from initial reconnaissance through to data exfiltration — all detected using custom SPL queries and Splunk alerts.

| # | Scenario | Attacker IP | Severity | MITRE ATT&CK |
|---|----------|-------------|----------|--------------|
| 1 | Brute Force / Failed Login Detection | 185.220.101.48 | High | T1110 |
| 2 | Network Port Scan Detection | 194.165.16.73 | Medium | T1046 |
| 3 | Malware, C2 Beaconing & Exfiltration | 185.220.101.48 / 194.165.16.73 | Critical | T1059, T1053, T1136, T1041, T1003 |

---

## Scenarios

- [Scenario 1 — Brute Force Detection](scenarios/brute-force.md)
- [Scenario 2 — Network Port Scan Detection](scenarios/network-scan.md)
- [Scenario 3 — Malware, C2 & Exfiltration](scenarios/malware-simulation.md)

---

## SPL Detection Queries

See [detections/spl-queries.md](detections/spl-queries.md)

---

## Incident Report

Full structured SOC incident report with screenshots:  
📄 [Andy_Wright_SOC_Incident_Report_v2.pdf](reports/Andy_Wright_SOC_Incident_Report_v2.pdf)

---

## Setup

See [setup/splunk-setup-guide.md](setup/splunk-setup-guide.md)

---

## Key Skills Demonstrated

- Splunk Cloud — data ingestion, SPL search, alert creation
- Log analysis — Linux auth logs, UFW firewall logs, audit logs
- Threat detection — brute force, port sca

cat > ~/Desktop/splunk-soc-lab/scenarios/brute-force.md << 'ENDOFFILE'
# Incident Report — Scenario 1: Brute Force / Failed Login Detection

**Analyst:** Andy Dela Quarshie Wright  
**Date:** May 8, 2025  
**Severity:** High  
**Status:** Detected & Documented  
**MITRE ATT&CK:** T1110 — Brute Force

---

## Objective

Detect repeated SSH login failures from a single external IP and identify whether the attack resulted in a successful compromise.

---

## Log Source

Realistic Linux auth log simulating an external attacker brute-forcing SSH credentials against wright-server. Attacker used a known Tor exit node IP cycling through common usernames.

**Uploaded to:** Splunk Cloud — sourcetype: syslog

---

## Sample Log Events
---

## SPL Detection Queries

**All failed login events:**
**Aggregate by source:**
**Results:**
185.220.101.48 — andy: 6, pi: 5

**Detect successful login:**
---

## Alert

- **Name:** Brute_Force_Detection
- **Trigger:** Number of results > 5
- **Severity:** High

---

## Findings

- 185.220.101.48 made 35+ failed SSH login attempts in under 2 minutes
- Usernames targeted: admin, root, andy, pi, ubuntu, deploy, guest, administrator
- Attack succeeded at 02:16:33 — logged in as andy
- Root shell spawned immediately — uid=0 — full system compromise

---

## Analyst Response

1. Isolate wright-server from the network immediately
2. Block 185.220.101.48 at firewall
3. Check for lateral movement to other internal systems
4. Reset all credentials — assume fully compromised
5. Escalate to Tier 2 / IR — root-level access is P1
6. Preserve memory and disk image for forensics

---

## IOCs

- Attacker IP: 185.220.101.48
- Attack type: SSH Brute Force — Successful Login
- Compromised account: andy
- Time of compromise: 02:16:33, May 8 2025
