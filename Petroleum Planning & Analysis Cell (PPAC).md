# Reflected Cross-Site Scripting (XSS) – Petroleum Planning & Analysis Cell (PPAC)

> **Disclaimer**
>
> This report is a sanitized version of a vulnerability submitted through the responsible vulnerability disclosure process. Sensitive information has been removed where necessary for public disclosure.

---

## Summary

A **Reflected Cross-Site Scripting (XSS)** vulnerability was identified in the search functionality of the Petroleum Planning & Analysis Cell (PPAC) website. The application reflects user-supplied input without proper output encoding, allowing arbitrary JavaScript execution in a victim's browser.

An attacker can craft a malicious URL containing JavaScript code. When a victim visits the URL, the injected script executes within the trusted context of the application.

---

## Severity

**Critical**

---

## Vulnerability Details

| Field | Value |
|-------|--------|
| Vulnerability | Reflected Cross-Site Scripting (XSS) |
| Severity | Critical |
| Attack Complexity | Easy |
| Attack Vector | Remote / External |
| CWE | CWE-79 |
| OWASP Top 10 | A03:2021 – Injection |

---

## Affected Endpoint

```text
https://ppac.gov.in/home/search
```

---

## Steps to Reproduce

1. Open the affected search page.
2. Enter the following payload into the search box.
3. Submit the request.
4. Observe that the payload executes in the browser.

---

## Proof of Concept

### Payload

```html
<script>alert("hello")</script>
```

The application reflects the payload in the response without proper output encoding, resulting in JavaScript execution.

---

## Impact

Successful exploitation may allow an attacker to:

- Execute arbitrary JavaScript in a victim's browser
- Steal cookies and session tokens
- Hijack authenticated user sessions
- Conduct phishing attacks
- Redirect users to malicious websites
- Deliver malware through malicious scripts
- Damage user trust and the application's reputation

---

## Remediation

To mitigate this vulnerability:

- Validate and sanitize all user inputs.
- Perform context-aware output encoding.
- Implement a strict **Content Security Policy (CSP)**.
- Enable security headers such as:
  - Content-Security-Policy
  - X-Content-Type-Options
  - X-Frame-Options
- Avoid rendering untrusted input directly into HTML responses.

---

## References

- OWASP – Cross-Site Scripting (XSS)
  - https://owasp.org/www-community/attacks/xss/

- PortSwigger Web Security Academy
  - https://portswigger.net/web-security/cross-site-scripting

- Acunetix
  - https://www.acunetix.com/blog/web-security-zone/what-is-cross-site-scripting/

---

## Proof of Concept Images

### Figure 1

**Reflected XSS Alert**

<img width="975" height="529" alt="image" src="https://github.com/user-attachments/assets/d4eae17e-5aca-4495-a2a7-1b5eea84676c" />


---

### Figure 2

**Injected Payload Reflected in Source Code**

<img width="975" height="219" alt="image" src="https://github.com/user-attachments/assets/045316ef-5014-4270-a954-1044f0ca184b" />


---

## Status

- **Reported via:** Responsible Vulnerability Disclosure
- **Vulnerability:** Reflected Cross-Site Scripting (XSS)
- **Status:** Fixed
- **Public Version:** Sanitized (Sensitive information removed)

---

## Author

**Balaji Sangana**

Cybersecurity Researcher | Web Application Penetration Tester
