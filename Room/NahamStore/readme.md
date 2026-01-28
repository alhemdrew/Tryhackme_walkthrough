# NahamStore – Penetration Testing Report

<p align="center">
  <img src="eb2479259872aa3d4fc761156cfe5bfd.png" alt="NahamStore Banner" width="800">
</p>

<p align="center">
  <strong>Author:</strong> Alhemdrew Davenchi | 
  <strong>Difficulty:</strong> Intermediate | 
  <strong>Category:</strong> Web Application Security
</p>

<p align="center">
  <strong>Vulnerabilities:</strong> <br>
  <code>SQLi</code> • <code>XSS</code> • <code>RCE</code> • <code>LFI</code> • <code>SSRF</code> • <code>IDOR</code> • <code>XXE</code> • <code>CSRF</code>
</p>

---


## 📌 Overview

This repository contains a **detailed penetration testing report** for **NahamStore**, documenting critical vulnerabilities discovered during a structured security assessment.  
The report covers **reconnaissance, exploitation, post‑exploitation**, and **mitigation strategies**, aligned with real‑world penetration testing methodologies.

---

## 📑 Table of Contents

1. Methodology  
2. Findings  
3. Exploitation Details  
4. TryHackMe Tasks & Answers  
5. Tools Used  
6. Recommendations  
7. Conclusion  

---

## 1️⃣ Methodology

1. **Information Gathering**  
   - Collected target system details using network scanning tools (e.g., Nmap).

2. **Enumeration**  
   - Enumerated open ports, services, and directories.

3. **Vulnerability Identification**  
   - Used automated tools and manual inspection to identify vulnerabilities such as SQL Injection, XSS, LFI, and SSRF.

4. **Exploitation**  
   - Executed exploits to gain unauthorized access to sensitive areas.

5. **Post‑Exploitation**  
   - Escalated privileges to gain administrative-level access.

6. **Documentation & Reporting**  
   - Documented findings and provided mitigation strategies.

---

## 2️⃣ Findings

| Vulnerability | Description | Impact |
|---------------|------------|--------|
| Open HTTP Port (80) | Web server exposed and running vulnerable services | Unauthorized access |
| Directory Enumeration | Hidden directories discovered using Gobuster | Data leakage |
| SQL Injection (SQLi) | Login authentication bypass | Database compromise |
| Weak Credentials | Default admin credentials found | Admin takeover |
| File Upload Vulnerability | Web shell upload allowed | Remote Code Execution |

---

## 3️⃣ Exploitation Details

### 🔍 Step 1: Enumeration with Nmap

```bash
nmap -sC -sV -oN nmap_scan.txt <target_ip>
```

**Results**
- Open Port: `80 (HTTP)`
- Service: `Apache HTTP Server 2.4.29`

---

### 📁 Step 2: Directory Enumeration

```bash
gobuster dir -u http://<target_ip>/ -w /usr/share/wordlists/dirb/common.txt
```

**Discovered Directories**
- `/admin/`
- `/uploads/`

---

### 🔐 Step 3: SQL Injection (Login Bypass)

```sql
' OR 1=1--
```

✔ Successfully bypassed authentication  
✔ Gained access to the admin panel

---

### 🐚 Step 4: Web Shell Upload (RCE)

- Uploaded `shell.php` via `/uploads/`
- Accessed shell at:

```text
http://<target_ip>/uploads/shell.php
```

✔ Remote Code Execution achieved

---

### ⬆️ Step 5: Privilege Escalation

**Weak SSH Credentials**
- Username: `admin`
- Password: `admin123`

✔ SSH access gained  
✔ Full system control achieved

---

## 4️⃣ TryHackMe Tasks & Answers

### Task 3 – Recon
- **Jimmy Jones SSN:** `521–61–6392`

---

### Task 4 – XSS

| Question | Answer |
|--------|--------|
| Vulnerable URL | `http://marketing.nahamstore.thm/?error=` |
| Stored XSS Header | `User-Agent` |
| Escaped HTML Tag | `title` |
| Escaped JavaScript Variable | `search` |
| Hidden Parameter | `q` |
| Returns Page Tag | `textarea` |
| H1 Tag Value | `Page Not Found` |
| Other XSS Parameter | `discount` |

---

### Task 5 – Open Redirect
- Open Redirect One: `r`  
- Open Redirect Two: `redirect_url`

---

### Task 6 – CSRF
- Vulnerable URL:  
  `http://nahamstore.thm/account/settings/password`
- Removed Field: `csrf_protect`
- Encoding Used: `base64`

---

### Task 7 – IDOR
- First Line of Address: `160 Broadway`
- Order ID 3 Date & Time: `22/02/2021 11:42:13`

---

### Task 8 – Local File Inclusion (LFI)
- **Flag:** `{7ef60e74b711f4c3a1fdf5a131ebf863}`

---

### Task 9 – SSRF
- **Credit Card Number:** `5190216301622131`

---

### Task 🔟 XXE
- XXE Flag: `{9f18bd8b9acaada53c4c643744401ea8}`
- Blind XXE Flag: `{d6b22cb3e37bef32d800105b11107d8f}`

---

### Task 11 – Remote Code Execution
- First RCE Flag: `{b42d2f1ff39874d56132537be62cf9e3}`
- Second RCE Flag: `{93125e2a845a38c3e1531f72c250e676}`

---

### Task 12 – SQL Injection
- Flag 1: `{d890234e20be48ff96a2f9caab0de55c}`
- Flag 2 (Blind): `{212ec3b036925a38b7167cf9f0243015}`

---

## 🧰 Tools Used

- **Nmap** – Network scanning  
- **Gobuster** – Directory enumeration  
- **Burp Suite** – Web exploitation  
- **Custom Scripts** – Payload delivery and exploitation  

---

## 🛡️ Recommendations

- Implement prepared statements to prevent SQL Injection  
- Enforce strong authentication and credential policies  
- Validate and sanitize all user inputs  
- Restrict file upload execution permissions  
- Implement CSRF tokens and secure headers  
- Apply the principle of least privilege  

---

## ✅ Conclusion

NahamStore suffers from **multiple critical vulnerabilities** that allow **full system compromise**.  
Adopting secure development practices, regular penetration testing, and defense‑in‑depth strategies is essential to mitigate these risks.

---
