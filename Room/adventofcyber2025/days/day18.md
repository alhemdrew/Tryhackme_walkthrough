# 🛡️ TryHackMe – Advent of Cyber 2025  
## Day 18 — Obfuscation: The Egg Shell File

---

<!-- ================= IMAGE PLACE 1 ================= -->
<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/63588b5ef586912c7d03c4f0/room-content/63588b5ef586912c7d03c4f0-1763750150780.png" alt="Day 18 Banner – The Egg Shell File" width="650">
</p>

---

*Analyzing obfuscated PowerShell code and safely recovering malicious intent.*

---

## ❄️ Challenge Overview

WareVille is in chaos. SOC alerts are firing constantly, and among the noise, **McSkidy** spots a suspicious email posing as **northpole-hr** — a department that does not exist. Embedded inside the email is a **PowerShell script** filled with unreadable gibberish.

This challenge focuses on **obfuscation**, a technique attackers use to hide malicious logic and delay detection.

---

## 🎯 Learning Objectives

- Understand what obfuscation is and why it is used
- Differentiate between encoding, encryption, and obfuscation
- Recognize common obfuscation techniques
- Safely deobfuscate malicious scripts using CyberChef
- Analyze layered obfuscation techniques

---

## 🧠 Obfuscation Explained

**Obfuscation** makes data difficult to read or analyze without changing its functionality.

Attackers use it to:
- Evade signature-based detection
- Slow down analysts
- Hide Indicators of Compromise (IOCs)

### Obfuscation vs Encoding vs Encryption

| Technique | Purpose | Reversible | Security |
|--------|--------|------------|---------|
| Encoding | Compatibility | Yes | ❌ |
| Encryption | Confidentiality | With key | ✅ |
| Obfuscation | Evasion | Usually | ⚠️ |

---

## 🔄 Simple Obfuscation: ROT Ciphers

### ROT1 Example
ROT1 shifts each letter forward by one position.

carrot coins go brr
↓
dbsspu dpjot hp css

yaml
Copy code

### ROT13 Example
ROT13 shifts characters by 13 positions.

These methods are weak but still effective at evading basic keyword-based detection.

---

---

## 🔐 Obfuscation with XOR

XOR is a common obfuscation technique where:
- Each byte is combined with a key
- Output often contains unreadable characters
- Reversing requires the same key

### XOR Example Using CyberChef

**Input:**
carrot supremacy

makefile
Copy code

**Key:**
a (HEX)

makefile
Copy code

**Result:**
ikxxe~*yzxogkis!

yaml
Copy code

XOR obfuscation is not practical to reverse manually — tools like **CyberChef** are essential.

---

## 🔍 Detecting Obfuscation Patterns

| Technique | Visual Clues |
|--------|-------------|
| ROT1 | Letters shifted slightly, spaces intact |
| ROT13 | Common words like `the → gur` |
| Base64 | Long alphanumeric strings, ends with `=` |
| XOR | Random symbols, same length as input |

Once identified, reverse the operation in CyberChef  
(e.g., **From Base64** instead of **To Base64**).

---

## 🧪 CyberChef Magic Operation

When unsure of the encoding:
- Use **Magic** operation
- Automatically tries common decoders
- Can enable **Intensive Mode** for deeper analysis

⚠️ Magic does not always solve **custom XOR keys** or **layered obfuscation**.

---

<!-- ================= IMAGE PLACE 3 ================= -->
<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/63588b5ef586912c7d03c4f0/room-content/63588b5ef586912c7d03c4f0-1763750774807.png" alt="CyberChef Magic Operation Results" width="650">
</p>

---

## 🧅 Layered Obfuscation

Attackers often stack techniques:

Example:
1. Gzip compression
2. XOR with key
3. Base64 encoding

**Obfuscated Output:**
H4sIADKZ42gA/32PT2sqQRDE7/Mp...

pgsql
Copy code

### Correct Deobfuscation Order
Always reverse **in opposite order**:
From Base64
↓
XOR (key)
↓
Gunzip

yaml
Copy code

This layered approach significantly increases analysis difficulty.

---

## 🥚 Unwrapping the Easter Egg (Practical)

McSkidy extracted a PowerShell script named:

SantaStealer.ps1

markdown
Copy code

### Part 1 — Deobfuscation

1. Open the script in **Visual Studio**
2. Navigate to **“Start here”**
3. Follow the inline comments
4. Save and run the script:

```powershell
cd .\Desktop\
.\SantaStealer.ps1
✅ First Flag
Copy code
THM{C2_De0bfuscation_29838}
Part 2 — Obfuscation
This time, you must obfuscate the attacker’s API key using XOR, following the script’s instructions.

Apply XOR obfuscation as instructed

Run the script again

✅ Second Flag
Copy code
THM{API_Obfusc4tion_ftw_0283}
🧠 Key Takeaways
Obfuscation hides intent, not functionality

XOR is reversible with the same key

Layered obfuscation must be reversed step-by-step

CyberChef is critical for safe malware analysis

Never analyze malware directly on production systems

✅ Day 18 completed — Obfuscation analyzed, payload revealed, and flags captured.
