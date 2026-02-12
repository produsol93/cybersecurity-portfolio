# Authentication Vulnerabilities – PortSwigger Web Security Academy

## Overview
This section explores common **authentication-related vulnerabilities** identified through PortSwigger Web Security Academy labs. The objective was to understand how weak authentication mechanisms can be exploited to gain unauthorized access to user accounts.

Topics covered:
- Username enumeration
- Brute-force attacks
- Broken authentication logic
- Two-factor authentication (2FA) bypass

---

## Lab 1 — Username Enumeration via Error Messages

**Severity:** Medium  
**OWASP:** A07 – Identification and Authentication Failures  

### Description
The application returns different error messages depending on whether the username exists. This behavior allows attackers to identify valid usernames.

### Exploitation Steps
1. Attempt login using random username and password.
2. Observe error responses:
   - **"Invalid username"** → Username does not exist
   - **"Incorrect password"** → Username exists
3. Identify a valid username.
4. Perform targeted password brute-force attack.

### Impact
- Enables targeted brute-force attacks
- Increases likelihood of account compromise

### Mitigation
- Use generic authentication error messages
- Implement rate limiting and login attempt monitoring
- Enable account lockout after multiple failed attempts

---

## Lab 2 — Broken Brute-force Protection

**Severity:** High  
**OWASP:** A07 – Identification and Authentication Failures  

### Description
The application does not properly prevent repeated login attempts, allowing automated password guessing.

### Exploitation
Used **Burp Suite Intruder** to automate login attempts after identifying a valid username.

### Impact
- Attackers can guess weak passwords
- Leads to account takeover

### Mitigation
- Implement rate limiting
- Enforce CAPTCHA
- Lock accounts after repeated failed login attempts
- Monitor suspicious login behavior

---

## Lab 3 — Two-Factor Authentication (2FA) Bypass

**Severity:** High  
**OWASP:** A07 – Identification and Authentication Failures  

### Description
The 2FA verification step can be bypassed due to improper server-side validation.

### Exploitation
Accessed authenticated endpoints without completing the 2FA process by skipping the verification step.

### Impact
- Full account takeover possible
- Sensitive user data exposure
- Authentication flow integrity compromised

### Mitigation
- Enforce server-side verification of authentication flow
- Bind session strictly to completed login + 2FA
- Prevent direct access to authenticated resources without full verification

---

## Key Takeaways
- Authentication mechanisms must not leak system behavior.
- Username enumeration significantly increases attack success.
- Brute-force protections are critical for login security.
- 2FA must always be enforced server-side.
- Authentication and authorization are separate security controls.

---

## Tools Used
- Burp Suite (Proxy, Intruder)
- Browser Developer Tools

---

## Skills Gained
- Identifying authentication vulnerabilities
- Performing brute-force attack analysis
- Understanding authentication bypass techniques
- Evaluating secure authentication design

---

## Conclusion
Authentication flaws remain one of the most common and critical security risks in web applications. Proper login validation, brute-force protection, and strict authentication flow enforcement are essential to prevent unauthorized access and account compromise.

