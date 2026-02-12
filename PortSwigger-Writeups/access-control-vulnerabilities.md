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

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/7c96c18f-9a10-4a63-83a5-2327702a4918" />

### Result
Discovered the **/admin** interface and accessed the administrative panel directly.

### Mitigation
Restrict access using proper authentication and authorization checks.

---

## Lab 2 — Unprotected Admin Functionality with Unpredictable URL

### Description
Admin panel was located at an unpredictable location, but the location is disclosed somewhere in the application.

### Exploitation
1. Analyzed the application structure using **Burp Suite Target → Site Map**.
2. During the analysis, discovered the hidden administrative endpoint **/admin-xxxx** and confirmed that the admin panel was accessible directly without authentication.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/9a76b821-d563-4fb0-b21b-2fe2db769af5" />

### Result
Used the administrative functionality to delete the target user account, successfully reproducing the vulnerability.

### Mitigation
- Protect the admin panel with proper authentication and authorization.
- Do not rely on hidden or unpredictable URLs for security.
- Restrict access to administrative functions to authorized users only.

---

## Lab 3 — User Role Controlled by Request Parameter

### Description
Admin panel was accessible with editing forgeable cookie.

### Exploitation
1. Accessed the admin page.
2. Sent the request to Repeater and modified the `role` parameter using Burp Suite to gain administrative privileges.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/070abf1e-8a2f-478b-bb81-be32489b819a" />

### Result
Gained admin privileges, and deleted targer user account.

### Mitigation
- Enforce proper server-side authorization checks for all sensitive actions.
- Do not trust client-side parameters such as `role` for access control decisions.
- Restrict administrative functions to authorized users only.

---

## Lab 4 — User Role can be modified in User Profile

### Description
Admin panel was only accessible to logged-in users with a roleid of 2.

### Exploitation
1. logged-in the supplied credential, and access "my account" page.
2. Sent the provided features in page, and observed it.
3. Added the roleid value into the request body.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/29afc8c3-bf8c-48b4-bb54-4951f190543a" />

### Result
Gained admin privileges, and deleted targer user account.

### Mitigation
- Enforce strict server-side authorization checks for all privileged actions.
- Store and manage user roles securely on the server side (e.g., session or database), and ignore any role-related values sent by the client.
- Implement proper access control validation to ensure only authorized users can access administrative functionality.
- Log and monitor privilege changes to detect and prevent unauthorized role escalation.

---

## Lab 5 — URL-based access control can be circumvented

### Description
the back-end application is built on a framework that supports the X-Original-URL header.

### Exploitation
1. Intercepted request to /admin and sent to Burp Repeater.
2. Added header to bypass frontend control: X-Original-Url, and checked the response.
3. Identified delete endpoint, and sent crafted request.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/093bf504-dd35-42a5-99e3-4452b50257f3" />

### Result
Target account sucessfully deleted.

### Mitigation
- Do not trust client-controlled routing headers such as `X-Original-URL` or `X-Rewrite-URL`.
- Enforce authorization checks on the backend after request routing is fully resolved.
- Log and monitor abnormal header usage and path override attempts.

---

## Lab 6 — Method-based access control can be circumvented

### Description
exploit the flawed access controls to promote yourself to become an administrator.

### Exploitation
Used IDOR + role change to gain admin privileges.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/c9990913-9d67-40fb-8021-1ed74965b2ae" />


### Result



### Mitigation

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
