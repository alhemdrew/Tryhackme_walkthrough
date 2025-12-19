# 🎄 TryHackMe – Advent of Cyber 2025  
<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/63c131e50a24c3005eb34678/room-content/63c131e50a24c3005eb34678-1763818313841.png" alt="Day 19 Banner - ICS Modbus Claus for Concern" width="650">
</p>
## Day 19 — ICS / Modbus: Claus for Concern (DETAILED WALKTHROUGH)

---


## 📖 Scenario Overview

TBFC’s drone delivery system is behaving strangely.  
Although dashboards show a **98% success rate**, citizens are receiving **chocolate eggs instead of Christmas gifts**.

A taunting message appears briefly:

🐰 **EGGSPLOIT v6.66 – Property of HopSec Island**  
*"Why should Christmas have all the fun?" — King Malhare*

This indicates a **logic manipulation attack** on an **Industrial Control System (ICS)** rather than a system failure.

---

## 🎯 Learning Objectives

- Understand **SCADA** systems
- Learn the role of **PLCs**
- Understand **Modbus TCP**
- Identify insecure ICS configurations
- Safely remediate a compromised control system
- Avoid destructive trap logic

---

## 🏭 SCADA Explained

SCADA (Supervisory Control and Data Acquisition) systems act as the **control center** for industrial operations.

They:
- Monitor physical processes
- Collect sensor data
- Control machinery via PLCs
- Provide dashboards, CCTV, and alarms

At TBFC, SCADA controls:
- Drone routing
- Package selection
- Inventory verification
- Conveyor belts
- Safety mechanisms

---

## 🧠 PLC & Modbus Basics

### PLC (Programmable Logic Controller)

A PLC is an industrial-grade computer designed to:
- Run continuously (24/7)
- Respond in real time
- Control physical machinery
- Survive harsh environments

---

### Modbus Protocol

Modbus is a **legacy industrial protocol** created in 1979.

Key weaknesses:
- ❌ No authentication
- ❌ No encryption
- ❌ No authorization
- ✅ Default TCP port: **502**

Anyone who can access port 502 can **read or write PLC memory directly**.

---

## 📦 Modbus Data Types

| Type | Description | Writable |
|---|---|---|
| Coils | Boolean flags | Yes |
| Holding Registers | Numeric values | Yes |
| Discrete Inputs | Sensor states | No |
| Input Registers | Sensor values | No |

---

## 📝 Maintenance Note (Critical Clue)

### Holding Registers
- **HR0** – Package Type  
  - 0 = Christmas Gifts  
  - 1 = Chocolate Eggs  
  - 2 = Easter Baskets  

- **HR1** – Delivery Zone  
  - 1–9 = Normal  
  - 10 = Ocean Dump  

- **HR4** – System Signature

### Coils
- **C10** – Inventory Verification  
- **C11** – Protection / Override  
- **C12** – Emergency Dump  
- **C13** – Audit Logging  
- **C14** – Christmas Restored  
- **C15** – Self-Destruct  

⚠️ **WARNING:**  
Never change **HR0 while C11 = True**  
→ Triggers self-destruct countdown

---

## 🔍 Task 4 – Practical Investigation

### Step 1: Network Reconnaissance

```bash
nmap -sV -p 22,80,502 MACHINE_IP
Findings:

Port 80 → CCTV Web Interface

Port 502 → Modbus TCP (PLC access)

🖼️ IMAGE PLACEHOLDER 2
(Insert screenshot of CCTV feed showing chocolate eggs)

👀 Visual Confirmation
Open in browser:

cpp
Copy code
http://MACHINE_IP
Observed:

Conveyor belts active

Drones loading Easter eggs

System status: Compromised

This confirms a logic-level attack.

🧪 Modbus Reconnaissance (Python)
Connect to PLC
python
Copy code
from pymodbus.client import ModbusTcpClient

client = ModbusTcpClient("MACHINE_IP", port=502)
client.connect()
⚠️ No authentication required.

Read Holding Registers
HR0 – Package Type

Copy code
1 → Chocolate Eggs
HR1 – Delivery Zone

css
Copy code
5 → Normal zone
HR4 – System Signature

Copy code
666 → Eggsploit confirmed
Read Coils
Coil	Value	Meaning
C10	False	Inventory verification disabled
C11	True	Protection active
C12	False	Emergency dump inactive
C13	False	Logging disabled
C15	False	Self-destruct not armed

🪤 Trap Logic Explained
If HR0 is changed while C11 is True:

C15 arms self-destruct

30-second countdown starts

C12 activates emergency dump

HR1 changes to Zone 10

Inventory dumped into ocean

Mission fails

🛠️ Safe Remediation Order
Disable C11 (Protection)

Set HR0 = 0 (Christmas Gifts)

Enable C10 (Inventory Verification)

Enable C13 (Audit Logging)

Confirm C15 remains False

🎁 Restoration Result
After applying fixes:

Drones deliver Christmas gifts

Inventory checks enabled

Logging restored

Trap avoided

🎯 Flag
powershell
Copy code
THM{eGgMas0V3r}
🖼️ IMAGE PLACEHOLDER 3
(Insert screenshot showing Christmas restored / victory screen)

🧠 Post-Incident Analysis
King Malhare:

Exploited unauthenticated Modbus access

Manipulated PLC registers directly

Disabled logging and verification

Implemented trap logic

Left signature value (666)

The maintenance note was critical in preventing total system failure.

✅ Conclusion
You successfully:

Investigated an ICS compromise

Interacted safely with a PLC

Avoided destructive failsafes

Restored TBFC’s delivery system

🎄 Christmas is saved.
