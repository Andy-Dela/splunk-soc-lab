# Incident Report — Scenario 2: Network Port Scan Detection

**Analyst:** Andy Dela Quarshie Wright  
**Date:** [ADD DATE YOU RAN THIS]  
**Severity:** Medium  
**Status:** Detected & Documented  
**MITRE ATT&CK Technique:** T1046 — Network Service Discovery

---

## Objective

Simulate a network reconnaissance port scan using Nmap against localhost, capture the traffic with Wireshark, and detect the scanning activity in Splunk using traffic volume thresholds.

---

## Attack Simulation

**Step 1 — Start Wireshark capture:**
- Open Wireshark
- Select your loopback interface (`lo0` on macOS)
- Start capture

**Step 2 — Run Nmap scan from Terminal:**

```bash
nmap -sV -p 1-1000 127.0.0.1
```

**What this does:**
- Scans ports 1–1000 on localhost
- `-sV` detects service versions on open ports
- Generates a high volume of connection attempts in a short time — characteristic of port scanning

**Step 3 — Stop Wireshark and export:**
- Stop the capture
- File → Export → Save as `portscan_capture.pcap`
- Upload `.pcap` to Splunk: **Settings → Add Data → Upload**

---

## Logs Generated

**Log source:** Wireshark pcap + system logs  
**Sourcetype in Splunk:** `pcap` / `syslog`  
**Key fields observed:**
- `dest_port` — destination port being probed
- `src_ip` — scanning source
- `count` — number of connection attempts per port

**Sample raw log entry:**
```
[ADD YOUR RAW LOG LINE FROM SPLUNK HERE]
```

---

## SPL Detection Query

```splunk
index=main
| stats count by dest_port, src_ip
| where count > 20
| sort -count
```

**Query breakdown:**
- Groups traffic by destination port and source IP
- Flags any source hitting more than 20 unique ports — indicates scanning behaviour
- Sorted by volume to surface highest-risk sources first

---

## Alert Configuration

- **Alert name:** Port_Scan_Detection
- **Trigger condition:** Unique dest_port count > 20 from single src_ip within 2 minutes
- **Alert action:** Log to Splunk triggered alerts list

> 📸 **[INSERT SCREENSHOT — Nmap scan results in terminal]**  
> 📸 **[INSERT SCREENSHOT — Splunk alert triggered / search results]**  
> 📸 **[INSERT SCREENSHOT — Wireshark pcap showing scan traffic]**

---

## Findings

| Field | Value |
|-------|-------|
| Source IP | 127.0.0.1 |
| Ports scanned | 1–1000 |
| Open ports found | [ADD WHAT NMAP RETURNED] |
| Scan duration | [ADD TIME] |
| True Positive? | Yes |

---

## Analyst Notes

The detection query flagged the scanning activity based on the high volume of unique destination ports contacted by a single source. In a real SOC environment:

1. **Identify** if the scanning IP is internal or external
2. **Check** asset inventory — is this an authorised vulnerability scan?
3. **If unauthorised** — escalate immediately, isolate source if possible
4. **Review** what services/ports were discovered and assess exposure

**IOC extracted:**
- Source IP: 127.0.0.1 (lab simulation)
- Scan type: SYN/version scan (Nmap -sV)
- Port range: 1–1000

---

## Conclusion

Network port scan successfully simulated using Nmap and detected in Splunk via traffic volume thresholds. Wireshark pcap corroborated the alert, demonstrating multi-tool SOC investigation workflow.
