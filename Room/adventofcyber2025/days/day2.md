<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1761552541867.svg" width="550">
</p>

# 🛡️ TryHackMe – Advent of Cyber 2025

## Day 02 — Phishing: Merry Clickmas ✅

*Hands-on phishing simulation using the Social-Engineer Toolkit (SET).*

<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1763362766183.jpg" alt="TryHackMe Room Screenshot" width="600">
</p>

---

## ❄️ 1. Challenge Overview

**Focus:** Social Engineering & Phishing  
**Objective:** Understand how phishing campaigns are built and delivered, and how credential harvesting works in real-world scenarios.

**Status:** Completed (100%)  
**Estimated Time:** ~30 minutes

---

## 🧭 2. Environment Setup

- **Platform:** TryHackMe AttackBox  
- **Access Type:** Web-based VM  
- **Scenario:** Attacker simulation (training-only environment)  
- **Privilege Escalation:** Not required  

**Tools Used:**  
`setoolkit`, `browser`, hosted phishing page

---

## 🎣 3. Phishing Fundamentals

Phishing is a form of **social engineering** that targets people rather than systems. It relies on psychological triggers such as:

- Urgency  
- Curiosity  
- Authority  

The goal is to trick users into revealing sensitive information like:
- Usernames
- Passwords
- Email credentials

---

## 🧰 4. Social-Engineer Toolkit (SET)

SET is an open-source framework designed for social engineering attacks.

**Capabilities demonstrated in this room:**
- Crafting phishing email messages
- Sending emails via a mass mailer
- Hosting fake login pages
- Capturing submitted credentials

SET lowers the technical barrier, showing how easily phishing attacks can be launched.

---

## 📧 5. Phishing Exercise (TBFC Scenario)

A phishing campaign was simulated against a fictional organization (TBFC).

**Attack Flow:**
1. Hosted a fake TBFC login portal to harvest credentials  
2. Used SET Mass Mailer to send a convincing phishing email  
3. Spoofed a trusted sender related to shipping operations  
4. Waited for victim interaction  
5. Captured credentials entered on the fake page  
6. Tested for **password reuse** on the email portal  

**Outcome:**  
- Credentials were successfully harvested, demonstrating how effective phishing can be.

---

## 🧠 6. Security Awareness Insight

This exercise reinforces that:
- Well-crafted phishing emails are hard to detect
- Humans are often the weakest link in security
- Password reuse significantly increases impact after compromise

---

## 🧾 7. Task Question Answers

| Question                                   | Answer                  |
| ------------------------------------------ | ----------------------- |
| Phished TBFC portal password               | `unranked-wisdom-anthem` |
| Total number of toys expected for delivery | `1,984,000`             |
| Toolkit used                               | Social-Engineer Toolkit (SET) |
| Attack type                                | Credential harvesting phishing |

---

## 🏁 8. Final Assessment

**Skills Practiced:**
- Understanding phishing workflows
- Using SET for social engineering simulations
- Identifying real-world phishing risks

**Blue Team Relevance:**  
Defenders must prioritize:
- Continuous user awareness training  
- Strong email filtering and monitoring  
- Password hygiene and multi-factor authentication  

---

✅ *Day 02 completed — a strong foundation in phishing tactics and defensive awareness.*
