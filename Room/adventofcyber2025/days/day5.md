![TryHackMe Banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761575138937.svg)

# 🛡️ TryHackMe – Advent of Cyber 2025

## Day 05 — IDOR: Santa’s Little IDOR ✅

*Exploiting Insecure Direct Object Reference (IDOR) vulnerabilities in a web application.*

![TryHackMe Room Screenshot](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/6093e17fa004d20049b6933e-1759960849816.png)

---

## ❄️ 1. Challenge Overview

**Focus:** Web Application Security – IDOR  
**Objective:** Identify and exploit an Insecure Direct Object Reference vulnerability on *TrypresentMe* to access unauthorized data.

**Status:** Completed (100%)  
**Estimated Time:** ~45 minutes  

---

## 🧭 2. Environment Setup

- **Platform:** TryHackMe AttackBox  
- **Target:** TrypresentMe web application  
- **User Role:** Authenticated low‑privilege user  
- **Privilege Escalation:** Logical / Horizontal only  

**Tools Used:**  
Web browser, Developer Tools, URL parameter tampering  

---

## 🧸 3. Understanding IDOR

Insecure Direct Object Reference (IDOR) occurs when:

- Applications expose internal object identifiers (IDs)  
- Authorization checks are missing  

Attackers can access or manipulate other users’ data by altering identifiers.

---

## 🔍 4. Identifying the Vulnerability

Example URL observed:

https://trypresentme.thm/order?id=1001
**Observation:** Changing the `id` allowed access to orders of other users.

---

## 🎯 5. Exploiting IDOR

**Technique:**  
- Increment/decrement object IDs  
- Monitor unauthorized responses  

**Outcome:**  
- Accessed other users’ accounts and sensitive data  
- Key Issue: Missing server-side authorization checks

---

## 🧾 6. Task Question Answers

| Question                                                       | Answer                                  |
| -------------------------------------------------------------- | --------------------------------------- |
| What does IDOR stand for?                                      | Insecure Direct Object Reference        |
| What type of privilege escalation do most IDOR cases represent?| Horizontal                              |
| Exploiting the view_accounts IDOR, parent with 10 children has user_id | 15                                      |
| Vulnerability exploited                                         | Insecure Direct Object Reference (IDOR)|
| Technique used                                                  | Parameter / ID manipulation             |
| What was bypassed?                                             | Authorization controls                  |

---

## 🏁 7. Final Assessment

**Skills Practiced:**

- Identifying and exploiting IDOR vulnerabilities  
- Web request analysis  
- Testing authorization logic  

**Blue Team Relevance:**  
Enforce server-side authorization checks, avoid exposing predictable object IDs, and monitor failed access attempts to prevent IDOR exploitation.

---

✅ **Day 05 completed** — practical understanding of a critical web application vulnerability.
