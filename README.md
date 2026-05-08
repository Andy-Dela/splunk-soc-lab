# 🛡️ Splunk SOC Monitoring Lab

**Author:** Andy Dela Quarshie Wright  
**Role Target:** SOC Level 1 Analyst  
**Tools Used:** Splunk Enterprise, Wireshark, Nmap, macOS System Logs  

---

## Overview

This project documents a home SIEM lab built using Splunk Enterprise to simulate and detect real-world threats in a controlled environment. The lab covers three core SOC analyst scenarios:

| # | Scenario | Technique |
|---|----------|-----------|
| 1 | Brute Force / Failed Login Detection | Auth log analysis, SPL alerting |
| 2 | Network Port Scan Detection | Traffic analysis, Nmap, Wireshark |
| 3 | Malicious File Activity Detection | File event monitoring, IOC matching |

Each scenario follows a structured **incident report format** — objective, attack simulation, logs generated, SPL detection query, alert screenshot, and analyst findings — mirroring real SOC workflows.

---

## Lab Architecture

```
macOS Host
│
├── Splunk Enterprise (localhost:8000)   ← SIEM
├── Splunk Universal Forwarder           ← Log ingestion
├── /var/log/ (system & auth logs)       ← Data source
├── Wireshark                            ← Packet capture
└── Nmap                                 ← Attack simulation
```

---

## Environment Setup

See [setup/splunk-setup-guide.md](setup/splunk-setup-guide.md) for full installation steps.

**Quick summary:**
- Splunk Enterprise (Free tier — 500MB/day)
- Universal Forwarder configured to ship `/var/log/` to Splunk
- Splunk running at `http://localhost:8000`

---

## Scenarios

- [Scenario 1 — Brute Force Detection](scenarios/brute-force.md)
- [Scenario 2 — Network Port Scan Detection](scenarios/network-scan.md)
- [Scenario 3 — Malicious File Activity Detection](scenarios/malware-simulation.md)

---

## SPL Detection Queries

See [detections/spl-queries.md](detections/spl-queries.md) for all queries used in this lab.

---

## Screenshots

All Splunk dashboard and alert screenshots are in the [screenshots/](screenshots/) folder.

---

## Key Skills Demonstrated

- SIEM configuration and log ingestion (Splunk)
- SPL (Splunk Search Processing Language) query writing
- Alert creation and threshold tuning
- Threat detection and incident triage
- Structured incident report documentation
- Understanding of MITRE ATT&CK techniques: T1110 (Brute Force), T1046 (Network Scanning), T1204 (Malicious File Execution)

---

## Certifications Supporting This Work

- CompTIA Security+
- TryHackMe SOC Level 1
- Google Cybersecurity Professional Certificate
