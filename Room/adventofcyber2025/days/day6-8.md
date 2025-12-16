# TryHackMe Advent of Cyber 2025 - Days 6 to 8 Answers

## Day 6 - Malware Analysis: Egg-xecutable

**Room Completed:** ✅

**Tasks and Answers:**

### Static Analysis
- **SHA256Sum of HopHelper.exe:**  
`F29C270068F865EF4A747E2683BFA07667BF64E768B38FBB9A2750A3D879CA33`
- **Flag within strings of HopHelper.exe:**  
`THM{STRINGS_FOUND}`

### Dynamic Analysis
- **Registry value modified by HopHelper.exe for persistence:**  
`HKU\S-1-5-21-1966530601-3185510712-10604624-1008\Software\Microsoft\Windows\CurrentVersion\Run\HopHelper`
- **Network protocol used by HopHelper.exe (filtered via ProcMon for TCP):**  
`http`
- **Bonus:** Web panel that HopHelper.exe communicates with  
_No answer needed_

---

## Day 7 - Network Discovery: Scan-ta Clause

**Room Completed:** ✅

**Tasks and Answers:**

- **Evil message on the top of the website:**  
`Pwned by HopSec`
- **First key part found on the FTP server:**  
`3aster_`
- **Second key part found in the TBFC app:**  
`15_th3_`
- **Third key part found in the DNS records:**  
`n3w_xm45`
- **Port MySQL database was running on:**  
`3306`
- **Flag found in the database:**  
`THM{4ll_s3rvice5_d1sc0vered}`

---

## Day 8 - Prompt Injection: Sched-yule conflict

**Room Completed:** ✅

**Tasks and Answers:**

- **Flag provided when SOC-mas is restored in the calendar:**  
`THM{XMAS_IS_COMING__BACK}`

