# SPL Detection Queries — Splunk SOC Lab

All Splunk Search Processing Language (SPL) queries used in this lab, organised by scenario.

---

## Scenario 1 — Brute Force Detection

**Basic failed login search:**
```splunk
index=main sourcetype=syslog "failed" OR "authentication failure" OR "Invalid user"
| table _time, user, src_ip, _raw
```

**Aggregate by source — detect threshold breach:**
```splunk
index=main sourcetype=syslog "failed" OR "authentication failure" OR "Invalid user"
| stats count by user, src_ip
| where count > 5
| sort -count
```

**Time-based detection (rolling 5-minute window):**
```splunk
index=main sourcetype=syslog "failed" OR "Invalid user"
| bucket _time span=5m
| stats count by _time, src_ip, user
| where count > 5
```

---

## Scenario 2 — Network Port Scan Detection

**High port volume from single source:**
```splunk
index=main
| stats count by dest_port, src_ip
| where count > 20
| sort -count
```

**Top scanning sources:**
```splunk
index=main
| stats dc(dest_port) as unique_ports by src_ip
| where unique_ports > 15
| sort -unique_ports
```

**Timeline of scan activity:**
```splunk
index=main src_ip="127.0.0.1"
| timechart count by dest_port
```

---

## Scenario 3 — Malicious File Detection

**IOC keyword match:**
```splunk
index=main ("eicar" OR "EICAR" OR "eicar_test")
| table _time, host, source, _raw
| sort -_time
```

**Regex field extraction — filename:**
```splunk
index=main source="/tmp/file_events.log"
| rex field=_raw "File created: (?<filename>\S+)"
| table _time, filename, host
```

**Suspicious file creation on Desktop:**
```splunk
index=main "Desktop" ("eicar" OR ".exe" OR ".bat" OR ".sh")
| table _time, host, _raw
```

---

## General Utility Queries

**Check all indexed data:**
```splunk
index=main | head 50
```

**Check what sourcetypes are available:**
```splunk
index=main | stats count by sourcetype
```

**Search across all time:**
```splunk
index=main earliest=0 | head 20
```

**Count events by hour:**
```splunk
index=main
| timechart span=1h count
```
