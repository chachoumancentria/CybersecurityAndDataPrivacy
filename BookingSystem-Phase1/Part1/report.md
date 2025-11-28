# 1️⃣ Introduction

**Tester(s):**  
- Joseph Couprie & Nassim Boudekhani

**Purpose:**  
- Find security related vulnerabilities in the registration system

**Scope:**  
- Tested components:  Account registration page
- Exclusions:  Missing Privacy Policy, Terms of Service, and Cookie Policy pages, and any other page not related to registration.
- Test approach: Gray-box

**Test environment & dates:**  
- Start:  23.11.2025
- End:  23.11.2025
- Test environment details (OS, runtime, DB, browsers): Arch linux + Docker engine, Firefox browser

**Assumptions & constraints:**  
- None

---

# :two: Executive Summary

**Short summary:**  

- We found some vulnerabilities and design flaws, some of them highly serious, that needs to be fixed immediately.

**Overall risk level:**

- 🔴 Critical

**Top 5 immediate actions:**  
1. You are not supposed to be able to create an administrator account directly from the website. You should remove this option.
2. You are not verifying the email adress, which can lead to DoS and email adress steal (one user using someone else's adress to create an account). You should send a verification email to check it's validity.
3. It is possible to bypass the UI and thus create accounts with empty passwords and/or invalid emails. This can lead to conflicts when using automatic programs to send emails. It may also allow SQL injection. The email and password check should also be server side.
4. The birth date of users are not checked. This can lead to legal issues. Implement a simple age verification when creating an account.
5. It is possible to create an account with very weak passwords (ie : abc or 123). You force passwords to be complicated enough (8 characters minimum, should include Upper and Lower case letters, and use at least 1 special symbol).

---

# 3️⃣ Severity scale & definitions

|  **Severity Level**  | **Description**                                                                                                              | **Recommended Action**           |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
|      🔴 **High**     | A serious vulnerability that can lead to full system compromise or data breach (e.g., SQL Injection, Remote Code Execution). | *Immediate fix required*         |
|     🟠 **Medium**    | A significant issue that may require specific conditions or user interaction (e.g., XSS, CSRF).                              | *Fix ASAP*                       |
|      🟡 **Low**      | A minor issue or configuration weakness (e.g., server version disclosure).                                                   | *Fix soon*                       |
| 🔵 **Info** | No direct risk, but useful for system hardening (e.g., missing security headers).                                            | *Monitor and fix in maintenance* |


---

# 4️⃣ Findings

| ID | Severity | Finding | Description | Evidence / Proof |
|------|-----------|----------|--------------|------------------|
| F-01 | 🔴 High | No administrator account barrier | Users can select the "administrator" option when creating an account |  |
| F-02 | 🔴 High | Email is not verified | Users can enter a fake email, or another person's email. This could lead to DoS attacks and identity fraud |  |
| F-03 | 🟠 Medium | Faulty credentials | It is possible to bypass client-side checks by manually sending the HTTP form. This allows emails like "a" and passwords like "1234", or even no password. This could break automated scripts running on your database and cause crashes. Moreover, this could be an SQL injection entry point when connected to the rest of the app. |  |
| F-04 | 🟡 Low | Weak password policy | Accepts passwords like "12345" |  |
| F-05 | 🟡 Low | Young users are allowed to register with invlaid birth dates | The age of a user should be checked to determine if the user is legally authorized to use the website. Also, an account should not be created for invalid birth dates (i.e. 01.01.2045) |  |

---

# 5️⃣ OWASP ZAP Test Report (Attachment)

**Purpose:**  
- Attach or link your OWASP ZAP scan results (Markdown format preferred).

---

**Instructions (CMD version):**
1. Run OWASP ZAP baseline scan:  
   ```bash
   zap-baseline.py -t https://example.com -r zap_report_round1.html -J zap_report.json
   ```
2. Export results to markdown:  
   ```bash
   zap-cli report -o zap_report_round1.md -f markdown
   ```
3. Save the report as `zap_report_round1.md` and link it below.

---
> [!NOTE]
> 📁 **Attach full report:** → `check itslearning` → **Add a link here**

---
