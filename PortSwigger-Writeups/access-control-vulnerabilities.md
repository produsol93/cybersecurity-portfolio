
# Access Control Vulnerabilities – PortSwigger Web Security Academy

## Overview
This document contains full writeups for Access Control labs completed in PortSwigger Web Security Academy.  
The objective was to understand how broken access control allows attackers to access unauthorized data, escalate privileges, and bypass security restrictions.

Covered topics:
- Insecure Direct Object Reference (IDOR)
- Vertical privilege escalation
- Horizontal privilege escalation
- Parameter manipulation
- Forced browsing
- Access control logic flaws

---

## Lab 1 — Unprotected Admin Functionality
**Severity:** High  
**OWASP:** A01 – Broken Access Control  

### Description
Admin panel was accessible without authentication.

### Exploitation Steps
1. Analyzed the application structure via **Burp Suite Target → Site Map**.
2. Performed content discovery using the **Burp Suite Crawler** to identify hidden endpoints.
3. Discovered the **/admin** interface and accessed the administrative panel directly.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/7c96c18f-9a10-4a63-83a5-2327702a4918" />

### Result

Accessed administrative functionality without login.

### Mitigation
Restrict access using proper authentication and authorization checks.

---

## Lab 2 — Unprotected Admin Functionality with Unpredictable URL

### Exploitation
Discovered hidden admin URL via source code / robots / guessing.

### Result
Accessed admin functionality.

---

## Lab 3 — User Role Controlled by Request Parameter

### Exploitation
Modified role parameter in request using Burp.

### Result
Gained admin privileges.

---

## Lab 4 — User Role Stored in Cookie

### Exploitation
Modified cookie value to escalate privileges.

---

## Lab 5 — Horizontal Privilege Escalation (IDOR)

### Description
User ID parameter allowed access to other user accounts.

### Exploitation
Changed user identifier in request.

### Result
Accessed another user's data.

---

## Lab 6 — Horizontal to Vertical Privilege Escalation

### Exploitation
Used IDOR + role change to gain admin privileges.

---

## Lab 7 — Insecure Direct Object Reference (Password Change)

### Exploitation
Modified request to change another user's password.

---

## Lab 8 — URL-based Access Control Bypass

### Exploitation
Accessed restricted endpoint directly.

---

## Lab 9 — Method-based Access Control Bypass

### Exploitation
Changed HTTP method (GET → POST) to bypass restriction.

---

## Lab 10 — Multi-step Process with Broken Access Control

### Exploitation
Skipped validation step to perform restricted action.

---

## Lab 11 — Referer-based Access Control

### Exploitation
Modified Referer header to bypass restriction.

---

## Lab 12 — Location-based Access Control

### Exploitation
Bypassed IP/location restriction using headers.

---

## Key Takeaways
- Access control must always be enforced server-side.
- Never trust user input (parameters, cookies, headers).
- IDOR is one of the most common real-world vulnerabilities.
- Privilege escalation can occur due to weak validation.
- Hidden URLs are NOT secure.

---

## Tools Used
- Burp Suite (Proxy, Repeater)
- Browser Developer Tools

---

## Skills Gained
- Identifying broken access control
- Performing privilege escalation
- Exploiting IDOR vulnerabilities
- Manipulating HTTP requests
- Analyzing authorization logic

---

## Conclusion
Broken access control is one of the most critical and common vulnerabilities in modern web applications. Proper server-side validation, strict role enforcement, and secure authorization logic are essential to prevent unauthorized access and privilege escalation.
