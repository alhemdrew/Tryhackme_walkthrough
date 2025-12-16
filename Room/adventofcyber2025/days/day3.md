<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1763451154082.png" width="550">
</p>

# 🛡️ TryHackMe – Advent of Cyber 2025

## Day 03 — Splunk Basics: Did you SIEM?

*Learn to ingest and parse custom log data using Splunk for security monitoring.*

<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1763099571417.png" alt="TryHackMe Room Screenshot" width="600">
</p>

---

## ❄️ 1. Challenge Overview

**Focus:** Log Analysis & SIEM Fundamentals
**Objective:** Gain hands-on experience with Splunk by ingesting log files, creating searches, and identifying events of interest.

---

## 🧭 2. Environment Setup

* Platform: TryHackMe AttackBox
* Access Type: Web-based VM
* User Context: Analyst / Security Observer
* Privilege Escalation: Not required

**Tools Used:**
`Splunk Web Interface`, `search queries`, `filters`, `dashboards`

---

## 🗂️ 3. Log Ingestion & Exploration

**Steps Taken:**

1. Upload custom logs to Splunk
2. Configure data inputs
3. Verify successful ingestion

**Key Findings:**

* Logs successfully parsed into events
* Fields automatically extracted for timestamp, source, and message

---

## 🔍 4. Searching & Filtering Events

**Commands / Queries:**

```splunk
index=main sourcetype=custom_log | stats count by user
index=main sourcetype=custom_log | search "failed login"
```

**Discovery:**

* Several failed login attempts detected
* User `socmas` had multiple login failures
  ➡️ **Key 1**: Evidence of possible brute-force attempt

---

## 📊 5. Creating Dashboards & Reports

* Built a simple dashboard to visualize failed login attempts
* Applied filters to highlight high-risk users

**Insight:** Dashboards allow quick identification of anomalies and security events

---

## 🧾 6. Task Question Answers

| Question                                  | Answer                  |
| ----------------------------------------- | ----------------------- |
| Which platform was used for log analysis? | Splunk                  |
| What query identifies failed logins?      | `search "failed login"` |
| What was the key user identified?         | socmas                  |

---

## 🏁 7. Final Assessment

**Skills Practiced:**

* Ingesting and parsing logs
* Using Splunk search queries
* Creating dashboards for monitoring

**Blue Team Relevance:**
Splunk provides a central point for log aggregation, event detection, and real-time monitoring to detect suspicious activity efficiently.

---

✅ *Day 03 completed — foundational SIEM skills for monitoring and incident detection.*
