# Incident Report — Scenario 1: Brute Force / Failed Login Detection

**Analyst:** Andy Dela Quarshie Wright  
**Date:** [ADD DATE YOU RAN THIS]  
**Severity:** Medium  
**Status:** Detected & Documented  
**MITRE ATT&CK Technique:** T1110 — Brute Force

---

## Objective

Simulate a brute force SSH login attack against localhost and detect it using Splunk by monitoring authentication logs for repeated failed login attempts from the same source.

---

## Attack Simulation

**Command used on macOS Terminal:**

```bash
for i in {1..10}; do ssh wronguser@localhost; done
```

**What this does:**
- Attempts 10 consecutive SSH logins using an invalid username
- Each failed attempt generates an authentication failure event in system logs
- Simulates a real attacker trying to guess credentials

---

## Logs Generated

**Log source:** `/var/log/` (macOS auth/system logs)  
**Sourcetype in Splunk:** `syslog`  
**Key fields observed:**
- `user` — the attempted username
- `src_ip` — source IP (127.0.0.1 in this case)
- `event` — authentication failure message

**Sample raw log entry:**
```
[ADD YOUR RAW LOG LINE FROM SPLUNK HERE]
```

---

## SPL Detection Query

```splunk
index=main sourcetype=syslog "failed" OR "authentication failure" OR "Invalid user"
| stats count by user, src_ip
| where count > 5
| sort -count
```

**Query breakdown:**
- Searches auth logs for failure keywords
- Groups by username and source IP
- Filters for sources with more than 5 failures — threshold for brute force
- Sorts by highest count first

---

## Alert Configuration

- **Alert name:** Brute_Force_Detection
- **Trigger condition:** count > 5 within 5 minutes
- **Alert action:** Log to Splunk triggered alerts list

> 📸 **[INSERT SCREENSHOT — Splunk alert triggered view]**

---

## Findings

| Field | Value |
|-------|-------|
| Source IP | 127.0.0.1 |
| Target user | wronguser |
| Failed attempts | 10 |
| Timeframe | [ADD TIME] |
| True Positive? | Yes |

---

## Analyst Notes

The detection query successfully identified the simulated brute force activity. In a real SOC environment, the next steps would be:

1. **Escalate** to Tier 2 if the source IP is external
2. **Block** the source IP at the firewall level
3. **Check** if any attempt succeeded (look for a successful login after failures)
4. **Document** in ticketing system with IOCs

**IOC extracted:**
- Source IP: 127.0.0.1 (localhost — lab simulation)
- Username targeted: `wronguser`

---

## Conclusion

Brute force attack successfully simulated and detected using Splunk SPL alerting. Detection threshold set at 5 failed attempts within a 5-minute window — consistent with industry SOC standards.
