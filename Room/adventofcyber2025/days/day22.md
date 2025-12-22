# 🎄 Advent of Cyber 2025 – Day 22  
## C2 Detection – Command & Carol (DETAILED WALKTHROUGH)
<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761803168624.svg" width="550">
</p>
---

## 📌 Room Overview

**Room Name:** C2 Detection – Command & Carol  
**Focus:** Network Forensics & C2 Detection  
**Tools Used:** Zeek, RITA  
**Time:** ~60 minutes  
**Goal:** Identify Command-and-Control (C2) traffic from a PCAP file using analytics instead of signatures.

---

## 🎯 Learning Objectives

- Convert PCAP files into Zeek logs
- Import Zeek logs into RITA
- Analyze RITA output to detect C2 infrastructure
- Understand beaconing, prevalence, and threat modifiers
- Perform structured threat hunting

---

## 🧠 Task 1 – Introduction

The TBFC SOC suspects that malicious actors are communicating with internal systems using stealthy Command-and-Control (C2) channels.  
Instead of manually inspecting massive packet captures, we use **RITA (Real Intelligence Threat Analytics)** to analyze network behavior at scale.

RITA works by:
- Correlating connection metadata
- Identifying beacon patterns
- Highlighting rare, suspicious traffic
- Leveraging threat intelligence feeds

---

## 🖥️ Environment Setup

### 1️⃣ Start the Target Machine
- Click **Start Machine**
- Wait ~2 minutes for the VM to boot
- Open a terminal once ready

---

## 🧩 Task 2 – Detecting C2 with RITA

---

## 🔍 Understanding the Tooling

### 🔹 What is Zeek?
Zeek is a Network Security Monitoring (NSM) tool that:
- Parses raw PCAP traffic
- Produces structured logs (DNS, HTTP, SSL, connections, etc.)
- Does **not** block traffic — only observes and records

### 🔹 What is RITA?
RITA analyzes Zeek logs to detect:
- C2 beaconing
- DNS tunneling
- Long-lived connections
- Data exfiltration
- Rare or suspicious communication patterns

---
```
## 🗂️ Step 1 – Explore Available Files

bash
```
ls
```
You should see:
```
pcaps/ → raw packet captures

zeek_logs/ → output directory for Zeek logs
```
🔄 Step 2 – Convert PCAP to Zeek Logs
We convert the provided PCAP into Zeek logs.
```
bash
Copy code
zeek readpcap pcaps/AsyncRAT.pcap zeek_logs/asyncrat
📌 This command:

Starts Zeek

Reads the PCAP

Writes structured logs into zeek_logs/asyncrat
```
📁 Step 3 – Verify Zeek Logs
bash
Copy code
```
cd zeek_logs/asyncrat
ls
```
You should see logs such as:

conn.log

dns.log

http.log

ssl.log

x509.log

These logs contain enriched metadata used by RITA.

📊 Step 4 – Import Zeek Logs into RITA
bash
```
Copy code
rita import --logs ~/zeek_logs/asyncrat/ --database asyncrat
```
What happens here:

Logs are parsed

Traffic is normalized

Threat intelligence feeds are checked

Behavioral analytics are applied

🖥️ Step 5 – View RITA Analysis
bash
Copy code
```
rita view asyncrat
```
This opens the RITA interactive interface with:

🔹 Search Bar
Press / to search

Press ? for filter help

🔹 Results Pane
Shows:

Severity score

Source & destination

Beacon likelihood

Connection duration

Threat intel matches

🔹 Details Pane
Shows:

Threat modifiers

Connection metadata

Port & protocol usage

🚨 Interpreting RITA Results
Suspicious Indicators Found
Long, unusual FQDNs (e.g. trycloudflare subdomains)

Rare TLS signatures

Long-lived connections

Non-standard ports

Low prevalence destinations

These are classic C2 characteristics.

🕵️ Final Challenge – Analyze New PCAP
Now analyze:

bash
Copy code
```
pcaps/rita_challenge.pcap
```
Steps:
bash
Copy code
```
zeek readpcap pcaps/rita_challenge.pcap zeek_logs/rita_challenge
rita import --logs ~/zeek_logs/rita_challenge/ --database rita_challenge
rita view rita_challenge
```

📝 Answers & Findings
✅ How many hosts are communicating with malhare.net?
```
Answer: 6
```

✅ Which Threat Modifier shows the number of hosts?
```
Answer: prevalence
```
✅ Highest number of connections to rabbithole.malhare.net?
```
Answer: 40
```
✅ Search filter for beacon score >70 and sorted by duration:
text
Copy code
```
dst:rabbithole.malhare.net beacon:>=70 sort:duration-desc
```
✅ Which port did 10.0.0.13 use?
```
Answer: 80
```
🛡️ Key Takeaways
C2 traffic can be detected without payload inspection

Beaconing behavior is a strong indicator of compromise

Rare signatures and low-prevalence destinations matter

RITA is ideal for threat hunting, not just alerts

🎉 Conclusion
This room demonstrates how defenders:

Scale network analysis

Detect stealthy C2 channels

Use behavioral analytics instead of signatures

Room Status: ✅ 100% Completed
Skill Gained: Practical C2 Threat Hunting

