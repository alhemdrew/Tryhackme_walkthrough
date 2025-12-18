# 🛡️ TryHackMe – Advent of Cyber 2025  
## Day 17 — CyberChef: Hoperation Save McSkidy

---

<!-- ================= IMAGE PLACE 1 ================= -->
<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/68baea2454c82afe90fd7020/room-content/68baea2454c82afe90fd7020-1763533892160.png" alt="Day 17 Banner / Quantum Fortress" width="650">
</p>

---

*Using encoding, decoding, and CyberChef recipes to break layered access controls.*

---

## ❄️ Challenge Overview

**Focus Areas:**
- Encoding & Decoding concepts
- CyberChef practical usage
- Web inspection (headers, debugger, logic)
- Chained data transformations

**Scenario:**
McSkidy is imprisoned inside **King Malhare’s Quantum Fortress**.  
Five digital locks protect the escape route. Each lock uses different encoding logic, and clues are hidden inside:
- Encoded chat messages
- HTTP headers
- Client-side login logic

Your mission is to **break all five locks** and rescue McSkidy.

---

## 🎯 Learning Objectives

- Understand encoding vs encryption
- Use CyberChef to reverse complex encodings
- Extract useful data from web apps
- Analyze login logic and reverse transformations

---

## 🧠 Encoding vs Encryption

| Encoding | Encryption |
|-------|-----------|
| Compatibility | Security |
| No secrecy | Confidential |
| Standardized | Algorithm + Key |
| Fast | Slower |
| Example: Base64 | Example: TLS |

**Decoding** is simply reversing encoded data to its original form.

---

## 🧰 CyberChef Overview

CyberChef is known as the **Cyber Swiss Army Knife**.

### Main Areas

| Area | Purpose |
|----|--------|
| Operations | Available transformations |
| Recipe | Chained operations |
| Input | Data to process |
| Output | Final result |

---



CyberChef allows **chaining multiple operations** to reverse layered encodings.

---

## 🏰 Lock 1 — Outer Gate

### 🔐 Logic
- Username: Guard name encoded in Base64
- Password:
  - Guard replies with Base64
  - Login logic uses **single Base64 encoding**

### 🛠️ Steps
1. Encode guard name → Base64
2. Encode magic question → Base64
3. Send question in chat
4. Decode guard’s response
5. Use plaintext password

### ✅ Password
Iamsofluffy

yaml
Copy code

---

## 🧱 Lock 2 — Outer Wall

### 🔐 Logic
- Password is **Base64 encoded twice**

### 🛠️ Steps
1. Retrieve encoded password from guard
2. Decode Base64 → Decode Base64 again
3. Use stored Base64 username

### ✅ Password
Itoldyoutochangeit!

yaml
Copy code

---

## 🏠 Lock 3 — Guard House

### 🔐 Logic
- Password is:
  1. XOR’d with a key
  2. Then Base64 encoded

**XOR Key:**
cyberchef

vbnet
Copy code

### 🧠 XOR Property
Applying XOR **twice with the same key restores the original value**.

### 🛠️ Reverse Recipe
From Base64
↓
XOR (key: cyberchef)

shell
Copy code

### ✅ Password
BugsBunny

yaml
Copy code

---

## 🏰 Lock 4 — Inner Castle

### 🔐 Logic
- Password is stored as an **MD5 hash**
- Guard response reveals the hash

### 🧠 MD5 Insight
MD5 is one-way, but known hashes can be cracked using **hash databases**.

### 🛠️ Steps
1. Decode guard response
2. Copy MD5 hash
3. Use CrackStation
4. Retrieve plaintext password

### ✅ Password
passw0rd1

yaml
Copy code

---

## 🗼 Lock 5 — Prison Tower (Final Lock)

---


---

### 🔐 Logic
- Encoding changes dynamically
- **Recipe ID** is revealed via HTTP headers
- Each recipe has a unique reverse logic

### 📜 Recipe Cheat Sheet

| Recipe ID | Reverse Logic |
|---------|--------------|
| 1 | From Base64 → Reverse → ROT13 |
| 2 | From Base64 → From Hex → Reverse |
| 3 | ROT13 → From Base64 → XOR (key) |
| 4 | ROT13 → From Base64 → ROT47 |

### 🛠️ Steps
1. Identify recipe ID from headers
2. Build correct reverse recipe in CyberChef
3. Decode final password

### ✅ Password
51rBr34chBl0ck3r

yaml
Copy code

---

## 🚩 Final Flag

THM{M3D13V4L_D3C0D3R_4D3P7}

yaml
Copy code

---

## 🎉 Epilogue

McSkidy escapes the Quantum Fortress and returns to **Wareville** just in time to prevent another disaster at TBFC.

---
<!-- ================= IMAGE PLACE 2 ================= -->
<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/68baea2454c82afe90fd7020/room-content/68baea2454c82afe90fd7020-1763536556206.png" alt="CyberChef Interface Example" width="650">
</p>

---
## 🧠 Key Takeaways

- Encoding is often layered and chained
- Web apps leak critical info via headers & JS logic
- CyberChef is essential for decoding complex workflows
- Understanding transformation order is critical

---

✅ **Day 17 completed — CyberChef mastery achieved and McSkidy rescued.**
