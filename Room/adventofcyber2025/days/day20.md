# 🏎️ TryHackMe – Advent of Cyber 2025  
## Day 20: Race Conditions – *Toy to The World*

---

## 🖼️ Room Banner

![Race Conditions – Toy to The World](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1763451486547.png)

---

## 📌 Room Overview

**Room Name:** Race Conditions – Toy to The World  
**Difficulty:** Beginner → Intermediate  
**Duration:** ~30 minutes  
**Category:** Web Security / Logic Flaws  
**Attack Type:** Race Condition  
**Status:** ✅ Completed (100%)

This room demonstrates how **race condition vulnerabilities** can allow attackers to manipulate web applications by sending **multiple concurrent requests**, leading to issues such as **overselling stock**, **duplicate transactions**, and **logic bypasses**.

---

## 🎯 Learning Objectives

- Understand what **race conditions** are
- Learn how **concurrent requests** affect shared resources
- Exploit a race condition using **Burp Suite**
- Observe how inventory values can become **negative**
- Learn **mitigation techniques** to prevent race conditions

---

## 📖 Task 1 – Introduction (Story)

TBFC (The Best Festival Company) launched a **limited-edition SleighToy** with **only 10 units available**.  
At midnight, thousands attempted to purchase it simultaneously.

Despite the stock limit, **more than 10 customers received successful order confirmations**.

The cause?  
⚠️ A **race condition vulnerability** exploited by Sir Carrotbane’s Bandit Bunnies.

---

## 🧠 Task 2 – Understanding Race Conditions

A **race condition** occurs when:
- Two or more actions run **at the same time**
- The system outcome depends on **execution timing**
- Shared resources are accessed **without proper synchronisation**

### 🔁 Common Types of Race Conditions

#### 1️⃣ Time-of-Check to Time-of-Use (TOCTOU)
- The system checks a condition (e.g., stock available)
- The condition changes before the action completes
- Example: Two users buy the “last item” simultaneously

#### 2️⃣ Shared Resource Race
- Multiple users modify the same data at the same time
- Final state depends on which request finishes last

#### 3️⃣ Atomicity Violation
- A process that should be **all-or-nothing** is split
- Another request interrupts mid-operation
- Results in inconsistent application state

---

## 🛠️ Environment Setup

### Machines Used
- **AttackBox**
- **Target Machine (TBFC Web App)**

Access the application via:
```
http://MACHINE_IP
Login Credentials
text
Copy code
Username: attacker
Password: attacker@123
🧪 Making a Legitimate Purchase
Log into the application

Locate SleighToy Limited Edition

Click Add to Cart

Proceed to Checkout

Click Confirm & Pay

Observe successful purchase confirmation

This generates a POST request to:
```


/process_checkout
⚔️ Exploiting the Race Condition
Step 1: Capture the Request
Open Burp Suite

Navigate to Proxy → HTTP History

Locate the POST request to /process_checkout

Right-click → Send to Repeater

Step 2: Prepare Parallel Requests
Go to Repeater

Right-click the request tab

Select Add tab to group

Create a group named: cart

Duplicate the request 15 times

Step 3: Send Requests in Parallel
Use the Send dropdown

Select:

text
Copy code
Send group in parallel (last-byte sync)
This forces the server to process all checkout requests at the same time, triggering the race condition.

📉 Results of Exploitation
Multiple orders processed simultaneously

Stock count updates incorrectly

Inventory value becomes negative

Flags are revealed
```
🏁 Flags
🧸 SleighToy Limited Edition
```
THM{WINNER_OF_R@CE007}
```

🐰 Bunny Plush (Blue)
```

THM{WINNER_OF_Bunny_R@ce}
```

🛡️ Mitigation Techniques
```

To prevent race condition vulnerabilities:

✅ Use atomic database transactions

✅ Perform final stock validation before committing orders

✅ Implement idempotency keys for checkout requests

✅ Apply rate limiting & concurrency controls

✅ Lock shared resources during critical operations

🧠 Key Takeaways
Race conditions exploit timing flaws, not broken authentication

Even simple logic errors can cause severe business impact

Parallel request testing is essential during security assessments

Proper backend synchronisation prevents exploitation
```

🎉 Conclusion
This room demonstrates how milliseconds matter in web security.
Without proper safeguards, attackers can manipulate application logic to gain unfair advantages.

⚠️ Always test concurrency handling in production systems.

✅ Room Completed – 100%
