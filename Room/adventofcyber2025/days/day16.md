# 🛡️ TryHackMe – Advent of Cyber 2025  
## Day 16 — Forensics: Registry Furensics
![TryHackMe Banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1763317996813.svg)

*Investigating a compromised Windows system through Registry forensics.*

---
![TryHackMe Room Screenshot](https://tryhackme-images.s3.amazonaws.com/user-uploads/68d2c1e7ab94268f6271de1d/room-content/68d2c1e7ab94268f6271de1d-1763737444784.png)

## ❄️ Challenge Overview

**Focus:** Windows Registry Forensics  
**Scenario:**  
TBFC’s critical system **dispatch-srv01**, responsible for drone-based gift delivery, began malfunctioning after being compromised by King Malhare’s attackers.  
As part of the forensic team, the task was to investigate **Windows Registry hives** to uncover evidence of compromise, persistence, and attacker activity.

**Objective:**
- Understand Windows Registry structure
- Analyze offline Registry Hives
- Identify malicious activity and persistence mechanisms
- Answer forensic questions based on registry evidence

---

## 🧠 Understanding the Windows Registry

The **Windows Registry** acts as the operating system’s configuration database, storing information such as:
- Installed applications
- Startup programs
- User activity
- System configuration
- Hardware and device history

Instead of being stored in one place, registry data is split into **Registry Hives**, each responsible for different configuration data.

---

## 🗂️ Registry Hives Overview

| Hive Name | Contains | Location |
|---------|--------|---------|
| SYSTEM | Services, boot config, drivers, hardware | `C:\Windows\System32\config\SYSTEM` |
| SECURITY | Local security policies, audit settings | `C:\Windows\System32\config\SECURITY` |
| SOFTWARE | Installed programs, OS info, autostarts | `C:\Windows\System32\config\SOFTWARE` |
| SAM | Usernames, password hashes, group info | `C:\Windows\System32\config\SAM` |
| NTUSER.DAT | User preferences, recent files, Run history | `C:\Users\<username>\NTUSER.DAT` |
| USRCLASS.DAT | Shellbags, jump lists | `C:\Users\<username>\AppData\Local\Microsoft\Windows\USRCLASS.DAT` |

---

## 🔑 Registry Root Keys Mapping

| Hive on Disk | Registry Editor Location |
|------------|--------------------------|
| SYSTEM | `HKEY_LOCAL_MACHINE\SYSTEM` |
| SOFTWARE | `HKEY_LOCAL_MACHINE\SOFTWARE` |
| SECURITY | `HKEY_LOCAL_MACHINE\SECURITY` |
| SAM | `HKEY_LOCAL_MACHINE\SAM` |
| NTUSER.DAT | `HKEY_USERS\<SID>` and `HKEY_CURRENT_USER` |
| USRCLASS.DAT | `HKEY_USERS\<SID>\Software\Classes` |

> **Note:**  
`HKCR` and `HKCC` are dynamic and not backed by standalone hive files.

---

## 🔍 Registry Forensics Importance

Registry Forensics helps investigators:
- Track executed programs
- Identify persistence mechanisms
- Recover user actions
- Build timelines of attacker activity

### Key Forensic Registry Paths

| Registry Key | Evidence Provided |
|-------------|------------------|
| `HKCU\...\UserAssist` | GUI-launched programs |
| `HKCU\...\TypedPaths` | Explorer address bar history |
| `HKCU\...\RunMRU` | Commands run via Win+R |
| `HKLM\...\Run` | Startup persistence |
| `HKCU\...\RecentDocs` | Recently accessed files |
| `HKLM\...\Uninstall` | Installed applications |
| `HKLM\...\ComputerName` | Hostname |

---

## 🧰 Tool Used: Registry Explorer

Since registry analysis **must not be done on a live system**, the **Registry Explorer** tool was used to:
- Load **offline registry hives**
- Parse binary registry values
- Replay transaction logs
- Safely analyze evidence

---

## 🛠️ Practical Investigation Steps

### Step 1: Launch Registry Explorer
- Open **Registry Explorer** from the taskbar

---

### Step 2: Load Offline Registry Hives
1. Click **File → Load Hive**
2. Navigate to:
C:\Users\Administrator\Desktop\Registry Hives

yaml
Copy code
3. Select a hive (e.g., `SYSTEM`)
4. Hold **SHIFT** and click **Open** to replay transaction logs
5. Repeat for all required hives

---

### Step 3: Verify System Identity
Navigate to:
ROOT\ControlSet001\Control\ComputerName\ComputerName

markdown
Copy code

**Hostname Found:**  
DISPATCH-SRV01

yaml
Copy code

---

## 🚨 Forensic Findings (Answers)

### 🔹 Question 1  
**What application was installed on the system before abnormal activity?**

✅ **Answer:**  
DroneManager Updater

yaml
Copy code

---

### 🔹 Question 2  
**What is the full path where the application was launched from?**

✅ **Answer:**  
C:\Users\dispatch.admin\Downloads\DroneManager_Setup.exe

yaml
Copy code

---

### 🔹 Question 3  
**Which value was added to maintain persistence at startup?**

✅ **Answer:**  
"C:\Program Files\DroneManager\dronehelper.exe" --background

yaml
Copy code

This was found in the **startup registry key**, indicating persistence.

---

## 🧠 Final Analysis

**Attack Summary:**
- A malicious updater was installed shortly before system issues began
- The application was executed from the user’s Downloads directory
- A startup registry key was added to ensure persistence
- This confirms **post-compromise persistence via registry autostart**

**Blue Team Lessons:**
- Registry hives provide high-value forensic evidence
- Startup keys are common persistence mechanisms
- Offline registry analysis is essential for integrity

---

✅ **Day 16 completed — Windows Registry forensics successfully used to uncover persistence and attacker activity.**
If you want, I can:
