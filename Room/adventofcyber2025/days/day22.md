# 🎄 Advent of Cyber 2025 – Day 22
## C2 Detection – Command & Carol (DETAILED WALKTHROUGH)

Room: C2 Detection – Command & Carol  
Focus: Network Forensics & C2 Detection  
Tools: Zeek, RITA  
Time: ~60 minutes  
Status: 100% Completed  

--------------------------------------------------

LEARNING OBJECTIVES
- Convert PCAP files into Zeek logs
- Import Zeek logs into RITA
- Analyze RITA output to detect C2 traffic
- Understand beaconing, prevalence, and threat modifiers
- Perform structured threat hunting

--------------------------------------------------

TASK 1 – INTRODUCTION

The TBFC SOC suspects stealthy Command-and-Control (C2) activity within the network.
Instead of manually reviewing large PCAP files, defenders rely on RITA (Real Intelligence Threat Analytics).

RITA works by:
- Correlating network metadata
- Detecting beaconing behavior
- Highlighting rare or suspicious connections
- Using threat intelligence feeds

--------------------------------------------------

ENVIRONMENT SETUP

1. Start the Target Machine
2. Wait ~2 minutes for it to boot
3. Open a terminal on the machine

--------------------------------------------------

TASK 2 – DETECTING C2 WITH RITA

UNDERSTANDING THE TOOLS

Zeek:
- Network Security Monitoring (NSM) tool
- Converts PCAPs into structured logs
- Observes traffic only (no blocking)

RITA:
- Analyzes Zeek logs
- Detects C2 beaconing
- Identifies DNS tunneling
- Flags long-lived connections
- Highlights low-prevalence destinations

--------------------------------------------------

STEP 1 – LIST AVAILABLE FILES

Command:
ls

Expected directories:
pcaps       (raw packet captures)
zeek_logs   (Zeek output directory)

--------------------------------------------------

STEP 2 – CONVERT PCAP TO ZEEK LOGS

Command:
zeek readpcap pcaps/AsyncRAT.pcap zeek_logs/asyncrat

What this does:
- Starts Zeek
- Reads AsyncRAT.pcap
- Writes logs to zeek_logs/asyncrat

--------------------------------------------------

STEP 3 – VERIFY ZEEK LOGS

Commands:
cd zeek_logs/asyncrat
ls

Expected logs:
conn.log
dns.log
http.log
ssl.log
x509.log

These logs contain enriched metadata used by RITA.

--------------------------------------------------

STEP 4 – IMPORT ZEEK LOGS INTO RITA

Command:
rita import --logs ~/zeek_logs/asyncrat/ --database asyncrat

What happens:
- Logs are parsed
- Traffic is normalized
- Threat intel feeds are checked
- Behavioral analytics are applied

--------------------------------------------------

STEP 5 – VIEW RITA RESULTS

Command:
rita view asyncrat

RITA INTERFACE

Search Bar:
- Press / to search
- Press ? for help

Results Pane:
- Severity score
- Source and destination
- Beacon likelihood
- Connection duration
- Threat intel matches

Details Pane:
- Threat modifiers
- Connection metadata
- Ports and protocols

--------------------------------------------------

INTERPRETING RESULTS

Suspicious indicators include:
- Long, unusual FQDNs (e.g. trycloudflare domains)
- Rare TLS signatures
- Long-lived connections
- Non-standard ports
- Low-prevalence destinations

These are classic C2 characteristics.

--------------------------------------------------

FINAL CHALLENGE – NEW PCAP ANALYSIS

Target PCAP:
pcaps/rita_challenge.pcap

Commands:
zeek readpcap pcaps/rita_challenge.pcap zeek_logs/rita_challenge
rita import --logs ~/zeek_logs/rita_challenge/ --database rita_challenge
rita view rita_challenge

--------------------------------------------------

ANSWERS

How many hosts are communicating with malhare.net?
Answer: 6

Which Threat Modifier shows the number of hosts?
Answer: prevalence

Highest number of connections to rabbithole.malhare.net?
Answer: 40

Search filter for beacon score >= 70 and sorted by duration:
dst:rabbithole.malhare.net beacon:>=70 sort:duration-desc

Which port did host 10.0.0.13 use?
Answer: 80

--------------------------------------------------

KEY TAKEAWAYS

- C2 traffic can be detected without payload inspection
- Beaconing behavior is a strong indicator of compromise
- Rare signatures and low-prevalence destinations matter
- RITA is excellent for proactive threat hunting

--------------------------------------------------

CONCLUSION

This room demonstrates how defenders can:
- Scale network analysis
- Detect stealthy C2 channels
- Use behavioral analytics instead of signatures

Room Status: 100% Completed
Skill Gained: Practical C2 Threat Hunting
