# 🛡️ TryHackMe – Advent of Cyber 2025

<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1763538536985.png" width="550">
</p>
---

## Day 15 — Web Attack Forensics: *Drone Alone* 🕸️

*Investigating malicious web activity and host compromise using Splunk.*

**Platform:** TryHackMe  
**Duration:** 30 min  
**Status:** Completed (100%)

---

## ❄️ 1. Challenge Overview

**Focus:** Web Attack Forensics & Incident Triage  
**Objective:** Detect malicious HTTP requests, analyze Apache logs, trace host-level compromise using Sysmon, and decode obfuscated attacker payloads.

TBFC’s drone scheduler web UI was targeted with long, suspicious HTTP requests containing Base64-encoded payloads. Alerts indicated Apache spawning unusual processes, suggesting command injection and possible remote code execution.

<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1761554754985.png" width="550">
</p>

---

## 🎯 2. Learning Objectives

* Detect malicious web activity in Apache access logs
* Investigate server-side errors indicating exploitation
* Correlate web attacks with OS-level process execution
* Identify and decode Base64-encoded PowerShell payloads
* Reconstruct the attacker’s full kill chain using Splunk

---

## 🧭 3. Environment Setup

* **AttackBox:** Started
* **Target VM:** Started
* **SIEM Tool:** Splunk
* **Access URL:** `http://MACHINE_IP:8000`

**Splunk Credentials:**

* **Username:** Blue  \
* **Password:** Pass1234

---

## 🔍 4. Detecting Suspicious Web Requests

To identify possible command injection attempts, Apache access logs were queried for common command execution keywords.

```spl
index=windows_apache_access (cmd.exe OR powershell OR "powershell.exe" OR "Invoke-Expression")
| table _time host clientip uri_path uri_query status
```

**Findings:**

* Requests contained long Base64-encoded strings
* Suspicious PowerShell usage within URL parameters
* Indication of command injection via `/cgi-bin/hello.bat`

---

## 🧬 5. Decoding Obfuscated Payloads

One Base64-encoded PowerShell string was extracted:

```text
VABoAGkAcwAgAGkAcwAgAG4AbwB3ACAATQBpAG4AZQAhACAATQBVAEEASABBAEEASABBAEEA
```

After decoding, the payload revealed attacker intent, confirming malicious experimentation rather than legitimate traffic.

---

## ⚠️ 6. Apache Error Log Analysis

Apache error logs were examined to confirm backend execution attempts.

```spl
index=windows_apache_error ("cmd.exe" OR "powershell" OR "Internal Server Error")
```

**Observations:**

* Multiple `500 Internal Server Error` responses
* Errors tied to malicious query strings
* Strong indication that attacker input reached backend execution logic

---

## 🖥️ 7. Tracing Host-Level Compromise (Sysmon)

To confirm whether Apache spawned system-level processes:

```spl
index=windows_sysmon ParentImage="*httpd.exe"
```

**Critical Finding:**

* Apache (`httpd.exe`) spawned system executables
* Clear evidence of command injection leading to OS-level execution

---

## 🧪 8. Attacker Reconnaissance Activity

Attackers often verify privileges using reconnaissance commands such as `whoami`.

```spl
index=windows_sysmon *cmd.exe* *whoami*
```

This confirmed that the attacker successfully executed reconnaissance commands on the host.

---

## 🔐 9. Encoded PowerShell Execution Check

To identify encoded PowerShell execution attempts:

```spl
index=windows_sysmon Image="*powershell.exe"
(CommandLine="*enc*" OR CommandLine="*-EncodedCommand*" OR CommandLine="*Base64*")
```

**Result:**

* No successful encoded PowerShell execution detected
* Indicates partial compromise or blocked execution

---

## 🧾 10. Task Question Answers

| Question                                         | Answer           |
| ------------------------------------------------ | ---------------- |
| What is the reconnaissance executable file name? | `whoami.exe`     |
| What executable did the attacker attempt to run? | `PowerShell.exe` |

---

## 🛡️ 11. Blue Team Takeaways

* Long Base64 strings in URLs are a major red flag
* Apache spawning system processes indicates severe compromise
* Correlating web logs with Sysmon provides full attack visibility
* Encoded PowerShell is a common attacker evasion technique
* Splunk is powerful for reconstructing complete attack chains

✅ **Day 15 completed — mastering web attack forensics and Splunk-based investigation.**
