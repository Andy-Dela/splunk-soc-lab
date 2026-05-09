# Splunk Setup Guide

## Environment Used

This lab was built using Splunk Cloud (free trial) — no local installation required.

---

## Step 1 — Create a Free Splunk Account

1. Go to: https://www.splunk.com
2. Click Products → Free Trials & Downloads
3. Select Splunk Cloud → Start Free Trial
4. Fill in your details and verify your email
5. Log in — Splunk Cloud opens in your browser

---

## Step 2 — Upload Log Data

Logs were uploaded directly into Splunk Cloud:

1. Settings → Add Data → Upload
2. Select your log file from your Desktop
3. Set the sourcetype:
   - Auth logs → syslog
   - Firewall logs → syslog
   - Malware/audit logs → malware_activity_log
4. Index → Default
5. Click Review → Submit

---

## Step 3 — Verify Data Ingestion

In Search and Reporting, run:
If events appear — data is ingested correctly.

---

## Step 4 — Run Searches

Go to Apps → Search and Reporting and use the SPL queries in detections/spl-queries.md

Set time range to All time for lab data.

---

## Step 5 — Create Alerts

After running a detection query:
1. Click Save As → Alert
2. Set title, trigger condition, and severity
3. Add action: Add to Triggered Alerts
4. Save

View saved alerts under Activity → Triggered Alerts

---

## Log Files Generated

All log files were generated using Python scripts on macOS:

- auth_brute_force.log — Brute Force — syslog
- portscan.log — Port Scan — syslog
- malware_activity.log — Malware/C2 — malware_activity_log
