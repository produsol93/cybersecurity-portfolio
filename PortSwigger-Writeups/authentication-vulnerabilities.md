# Authentication Vulnerabilities – PortSwigger Web Security Academy

## Overview
This document contains full writeups for all Authentication labs completed in PortSwigger Web Security Academy.  
The objective was to analyze weaknesses in authentication mechanisms and understand how attackers bypass login protections.

Covered topics:
- Username enumeration
- Brute-force attacks
- Broken authentication logic
- Password reset flaws
- Two-factor authentication bypass
- Session handling weaknesses

---

## Lab 1 — Username Enumeration via Error Messages
**Severity:** Medium  
**OWASP:** A07 – Identification and Authentication Failures  

### Description
Different error messages reveal whether a username exists.

### Exploitation Steps
(Describe how you detected valid username)

### Result
Successfully identified a valid username.

### Mitigation
Use generic error messages and rate limiting.

---

## Lab 2 — Broken Brute-force Protection
**Severity:** High  

### Exploitation
Used Burp Intruder to brute-force password.

### Result
Password guessed successfully.

### Mitigation
Account lockout, CAPTCHA, rate limiting.

---

## Lab 3 — Username Enumeration via Response Timing

### Description
Response time difference reveals valid username.

### Exploitation
Measured server response time using Burp Intruder.

### Result
Identified valid username.

---

## Lab 4 — Username Enumeration via Account Lock

### Exploitation
Observed account lock behavior to determine valid username.

---

## Lab 5 — Broken Brute-force Protection, IP Block Bypass

### Exploitation
Used header/IP manipulation to bypass login protection.

---

## Lab 6 — Username Enumeration via Password Reset

### Exploitation
Password reset behavior reveals valid user.

---

## Lab 7 — Password Reset Poisoning

### Exploitation
Manipulated password reset link to hijack account.

---

## Lab 8 — Password Reset Broken Logic

### Exploitation
Abused flawed password reset flow.

---

## Lab 9 — Broken Authentication Cookie

### Exploitation
Manipulated "stay logged in" cookie.

---

## Lab 10 — Offline Password Cracking

### Exploitation
Extracted hash and cracked password offline.

---

## Lab 11 — 2FA Simple Bypass

### Exploitation
Skipped 2FA step and accessed account.

---

## Lab 12 — 2FA Broken Logic

### Exploitation
Abused flawed verification logic.

---

## Lab 13 — Brute-forcing 2FA Code

### Exploitation
Automated guessing of verification code.

---

## Lab 14 — Advanced Authentication Bypass

### Exploitation
Combined logic flaws to bypass authentication.

---

## Key Takeaways
- Authentication must not leak system behavior
- Brute-force protection is critical
- Password reset flows are common attack surface
- 2FA must always be validated server-side
- Session security is essential

---

## Tools Used
- Burp Suite (Proxy, Intruder)
- Burp Repeater
- Browser Developer Tools

---

## Skills Gained
- Username enumeration techniques
- Brute-force attack analysis
- Authentication bypass
- Password reset exploitation
- Session & cookie manipulation

---

## Conclusion
Authentication flaws remain one of the most critical risks in modern web applications. Proper validation, brute-force protection, and secure authentication flow enforcement are essential to prevent unauthorized access.

