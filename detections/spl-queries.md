# SPL Detection Queries — Splunk SOC Lab

All queries used across the three scenarios.

---

## Scenario 1 — Brute Force Detection

**All failed login events:**
**Aggregate by source — threshold detection:**
**Results:** 185.220.101.48 — andy: 6, pi: 5

**Detect successful login after failures:**
---

## Scenario 2 — Port Scan Detection

**Detect high port volume from single source:**
**Results:** 194.165.16.73 — 52 ports scanned

**Detailed port breakdown:**
---

## Scenario 3 — Malware, C2 & Exfiltration

**All malware activity events:**
**LOLBin command detection:**
**C2 beaconing detection:**
**Results:** Regular 30-second intervals to 194.165.16.73 on port 443 — confirmed C2 beaconing.

---

## General Utility

**Check all indexed data:**
**Check sourcetypes available:**
**Count events by hour:**
