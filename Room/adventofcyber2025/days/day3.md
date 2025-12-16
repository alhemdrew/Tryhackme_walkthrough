![TryHackMe Banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1763451154082.png)

# 🛡️ TryHackMe – Advent of Cyber 2025

## Day 03 — Splunk Basics: Did You SIEM? ✅

*Hands-on SIEM investigation using Splunk to analyze logs, detect attacks, and trace an intrusion.*

![TryHackMe Room Screenshot](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1763099571417.png)

---

## ❄️ 1. Challenge Overview

**Focus:** SIEM, Log Analysis & Incident Detection  
**Objective:** Gain practical experience using Splunk to investigate logs, detect malicious activity, and reconstruct a real attack chain.

**Status:** Completed (100%)  
**Estimated Time:** ~60 minutes  

---

## 🧭 2. Environment Setup

- **Platform:** TryHackMe AttackBox  
- **SIEM Tool:** Splunk  
- **Role:** Blue Team / Security Analyst  
- **Privilege Escalation:** Not required  

### Log Sources
- `web_traffic` — Web server access logs  
- `firewall_logs` — Network allow/deny events  

---

## 🗂️ 3. Initial Log Exploration

### Base Query
```splunk
index=main
Observations:

Two datasets identified: web_traffic and firewall_logs

Automatic field extraction (IP, path, user_agent, status)

Clear traffic spike indicating a likely attack window

📈 4. Timeline & Traffic Analysis
Events per Day
splunk
Copy code
index=main sourcetype=web_traffic | timechart span=1d count
Finding:

Abnormal spike detected on 2025-10-12

Identified as the primary attack phase

🔍 5. Anomaly Detection
Suspicious User Agents
Filtered out legitimate browsers:

splunk
Copy code
sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox*
Result:

One IP responsible for most malicious activity

Automated tools detected: curl, wget, sqlmap, Havij

🧨 6. Attack Chain Reconstruction
🕵️ Reconnaissance
Probing sensitive files: /.env, /.git, phpinfo

Tools: curl, wget

Responses: 401, 403, 404

🧪 Enumeration & Exploitation
Path traversal attempts (../../)

SQL Injection confirmed using:

sqlmap

Havij

Time-based payloads (SLEEP(5))

📦 Data Exfiltration
Download attempts for:

backup.zip

logs.tar.gz

Large outbound transfers observed

🧬 RCE & Ransomware Staging
Web shell execution: shell.php?cmd=

Ransomware payload: bunnylock.bin

Confirmed Remote Code Execution (RCE)

🔗 7. Firewall Log Correlation (C2)
splunk
Copy code
sourcetype=firewall_logs src_ip="10.10.1.5" dest_ip="<ATTACKER_IP>" action="ALLOWED"
Findings:

Successful outbound C2 communication

Significant data exfiltration to attacker infrastructure

🧾 8. Task Question Answers

| Question                                                | Answer        |
| ------------------------------------------------------- | ------------- |
| What is the attacker IP found attacking the web server? | 198.51.100.55 |
| Which day was the peak traffic in the logs?             | 2025-10-12    |
| Count of Havij `user_agent` events in the logs?         | 993           |
| Number of path traversal attempts to sensitive files?   | 658           |
| Bytes transferred to the C2 server from the web server? | 126,167       |


🏁 9. Final Assessment
Skills Practiced
SIEM navigation and searches

Log correlation (web + firewall)

Timeline and anomaly detection

Full attack-chain reconstruction

Blue Team Relevance
This room demonstrates how SIEM tools like Splunk are critical for:

Early threat detection

Incident response and forensics

Understanding attacker behavior and impact

✅ Day 03 completed — strong foundational SIEM and incident-handling skills using Splunk.
