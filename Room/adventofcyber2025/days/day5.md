<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761575138937.svg" width="550">
</p>

# 🛡️ TryHackMe – Advent of Cyber 2025

## Day 05 — IDOR: Santa’s Little IDOR

*Exploiting Insecure Direct Object Reference (IDOR) vulnerabilities in a web application.*

<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/6093e17fa004d20049b6933e-1759960849816.png" alt="TryHackMe Room Screenshot" width="600">
</p>

---

## ❄️ 1. Challenge Overview

**Focus:** Web Application Security – IDOR
**Objective:** Identify and exploit an Insecure Direct Object Reference vulnerability on the *TrypresentMe* website to access unauthorized data.

---

## 🧭 2. Environment Setup

* Platform: TryHackMe AttackBox
* Access Type: Web Application
* Target: TrypresentMe
* User Context: Authenticated low‑privilege user
* Privilege Escalation: Not system‑level (logical authorization bypass)

**Tools Used:**
Web browser, URL manipulation, parameter tampering

---

## 🧸 3. Understanding IDOR

IDOR occurs when an application:

* Exposes internal object identifiers (IDs)
* Fails to properly enforce authorization checks

This allows attackers to access or modify data belonging to other users by simply changing an identifier.

---

## 🔍 4. Identifying the Vulnerability

While interacting with the application, numeric identifiers were observed in request parameters.

**Example:**

```
https://trypresentme.thm/order?id=1001
```

By modifying the `id` value, data belonging to other users became accessible.

---

## 🎯 5. Exploiting IDOR

**Technique:**

* Increment and decrement object IDs
* Observe unauthorized responses

**Result:**

* Access to other users’ orders
* Disclosure of sensitive information

➡️ **Key Finding:** Authorization checks were missing on object access.

---

## 🧾 6. Task Question Answers

| Question                          | Answer                                  |
| --------------------------------- | --------------------------------------- |
| What vulnerability was exploited? | Insecure Direct Object Reference (IDOR) |
| What technique was used?          | Parameter / ID manipulation             |
| What was bypassed?                | Authorization controls                  |

---

## 🏁 7. Final Assessment

**Skills Practiced:**

* Identifying IDOR vulnerabilities
* Web request analysis
* Authorization testing

**Blue Team Relevance:**
Applications must enforce server‑side authorization checks and avoid exposing predictable object identifiers to prevent IDOR attacks.

---

✅ *Day 05 completed — a critical web vulnerability commonly found in real‑world applications.*
