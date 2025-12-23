# 🎄 Advent of Cyber 2024 – Side Quest Walkthrough

<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1732868736978.png" alt="AoC 2024 Side Quest Banner" width="700">

--------------------------------------------------

## Overview

**Room:** Advent of Cyber '24 Side Quest  
**Focus:** Advanced challenges for experienced users  
**Difficulty:** Hard → Insane  
**Goal:** Help Elf McSkidy recover access to compromised servers and defeat the Frosty Five ransomware gang.  
**Keycards:** Hidden in the main Advent of Cyber 2024 challenges.

--------------------------------------------------

## How Side Quest Works

- **L1 Keycard:** Days 1–4  
- **L2 Keycard:** Days 5–8  
- **L3 Keycard:** Days 9–12  
- **L4 Keycard:** Days 13–17  
- **L5 Keycard:** Days 18–22  

Each keycard gives access to the corresponding VM, where you can solve challenges.

--------------------------------------------------

## Task 1 – Operation Tiny Frostbite

<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1732869002545.png" alt="Frostbite Fox Mugshot" width="700">

**Challenge:** Frostbite Fox has attacked McSkidy's machine. Recover stolen passwords from the ZIP file.  

**ZIP File:** `http://MACHINE_IP/aoc_sq_1.zip`  
**MD5:** `044a78a6a1573c562bc18cefb761a578`

**Answers:**
- Password the attacker used to register: `QU9DMjAyNHtUaW55X1R`  
- Password captured by attacker: `pbnlfVGlueV9TaDNsbF`  
- ZIP file password: `9jYW5fRW5jcnlwVF9iVXR`  
- McSkidy’s password in database: `faXRfSXNfTjB0X0YwMGxwcm8wZn0=`

--------------------------------------------------

## Task 2 – Yin and Yang

<img style="text-align:center;" src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1732869022070.png" width="700">

**Challenge:** Penguin Zero has hacked YIN and YANG robotic systems. Must hack both simultaneously.  

**Credentials:**  
- Username: `yin`  
- Password: `yang`  

**Answers:**
- YIN flag: `THM{Yin.cannot.exist.without.a.little.bit.of.Yang}`  
- YANG flag: `THM{Yang.also.needs.Yin.to.survive}`

--------------------------------------------------

## Task 3 – Escaping the Blizzard

<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1732869127635.png" alt="Blizzard Bear Mugshot" width="700">

**Challenge:** Blizzard Bear compromised the construction permit server. Recover control.  

**Answers:**
- `foothold.txt`: `THM{th1s-1s-jusT-th3-B3g1nn1ng}`  
- `user.txt`: `THM{h4v1ng-fun-w1th-a-g00d-old-heap-overflowww-in-a-l4t3st-gl1bc}`  
- `root.txt`: `THM{w00t-w00t-y0u-escap3-the-may0r-permits}`

--------------------------------------------------

## Task 4 – Krampus Festival

<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1732869203432.png" width="700">

**Challenge:** Kewl Krampus compromised Active Directory. Recover access.  

**Answers:**
- `flag.txt`: `THM{unlock_the_door_to_darkness_0nly_f0r_the_brave}`  
- `user.txt`: `THM{krampu5_h00ked_y0ur_l00t}`  
- `root.txt`: `THM{krampu5_&_p0tat0_5alad}`

--------------------------------------------------

## Task 5 – An Avalanche of Web Apps

<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1732869145704.png" alt="Avalanche Leopard Mugshot" width="700">

**Challenge:** Avalanche Leopard compromised web applications. Retrieve all flags.  

**Answers:**
- Flag 1: `THM{09a3f8918a32ea38a2c833c98214336a}`  
- Flag 2: `THM{647aff4143b04972ba816f040e9b81c2}`  
- Flag 3: `THM{ff2e079bc7bc3eb925478aa5bc2466a6}`  
- Flag 4: `THM{05a830d2f52649c96318cce20c562b63}`

--------------------------------------------------

## Task 6 – The End

**Note:** Users must complete a short survey to get the final flag.

**Survey Flag:** `THM{bigger_and_maybe_not_as_mean_in_2025}`

---

### ✅ Key Takeaways

- Side Quest is for advanced users → Hard → Insane  
- Each task is tied to a hidden keycard in the main Advent of Cyber room  
- Tools needed: ZIP extraction, forensic analysis, VM access  
- Challenges range from forensic analysis, password recovery, exploitation, to web app security  

---

