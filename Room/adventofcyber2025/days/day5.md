
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
