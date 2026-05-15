# Incident Report — Scenario 2: Network Port Scan Detection

**Analyst:** Andy Dela Quarshie Wright  
**Date:** May 8, 2025  
**Severity:** Medium  
**Status:** Detected & Documented  
**MITRE ATT&CK:** T1046 — Network Service Discovery

---

## Objective

Detect automated port scanning activity against an internal server and identify which services were exposed to the attacker.

---

## Log Source

Realistic UFW firewall log simulating an Nmap port scan from an external attacker against wright-server (10.0.0.5). Mixed scan techniques — SYN, NULL, FIN, XMAS flags across TCP and UDP.

**Uploaded to:** Splunk Cloud — sourcetype: syslog

---

## Sample Log Events
---

## SPL Detection Queries

**Detect high port volume from single source:**
**Results:** 194.165.16.73 — 52 ports scanned

**Detailed port breakdown:**
---

## Alert

- **Name:** Port_Scan_Detection
- **Trigger:** Number of results > 10
- **Severity:** High

---

## High-Value Ports Identified

- Port 22 (SSH) — Remote access, brute force target
- Port 445 (SMB) — Ransomware, EternalBlue exploitation
- Port 3389 (RDP) — Remote desktop, credential attacks
- Port 3306 (MySQL) — Database access, data exfiltration
- Port 80/443 (HTTP/HTTPS) — Web application vulnerabilities
- Port 23 (Telnet) — Unencrypted, credential interception risk

---

## Findings

- 194.165.16.73 probed 52 ports in under 30 seconds — automated scan
- Mixed scan flags (NULL, XMAS, FIN) used to evade basic IDS detection
- Port 22 returned SYN-ACK — SSH service exposed and reachable
- Port 443 returned SYN-ACK — HTTPS service exposed
- Pattern consistent with Nmap aggressive reconnaissance

---

## Analyst Response

1. Verify — is 194.165.16.73 an authorised vulnerability scanner?
2. If not authorised — block at perimeter firewall immediately
3. Cross-reference on VirusTotal, Shodan, AbuseIPDB
4. Alert infrastructure team — SSH and SMB exposure needs review
5. Restrict SSH to VPN/jumpbox — not exposed to public internet
6. Monitor for follow-up exploit attempts from same IP range

---

## IOCs

- Attacker IP: 194.165.16.73
- Scan type: Full port scan — SYN, NULL, FIN, XMAS
- Ports scanned: 52 including 22, 445, 3389, 3306
- Duration: Under 30 seconds
