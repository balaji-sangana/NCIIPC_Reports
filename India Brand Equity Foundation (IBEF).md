# Reflected Cross-Site Scripting (XSS) – India Brand Equity Foundation (IBEF)

> **Disclaimer**
>
> This report is a sanitized version of a vulnerability submitted through the responsible vulnerability disclosure process. Sensitive information has been retained only where already publicly accessible or necessary for understanding the vulnerability.

---

## Summary

A **Reflected Cross-Site Scripting (XSS)** vulnerability was identified in the IBEF website search functionality. The application reflects user-supplied input into the HTML response without proper output encoding, allowing arbitrary JavaScript execution in the victim's browser.

An attacker can exploit this issue by crafting a malicious URL containing JavaScript payloads. When a victim visits the link, the injected script executes in the context of the trusted application.

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
https://www.ibef.org/home/search
```

---

## Steps to Reproduce

1. Navigate to the search functionality.
2. Intercept the search request using Burp Suite.
3. Inject the following payload into the search parameter.
4. Forward the request.
5. Observe that the JavaScript executes in the browser.

---

## Proof of Concept

### Payload

```html
<script>alert("hello")</script>
```

The application reflects the payload without proper output encoding, causing the browser to execute the injected JavaScript.

---

## Impact

Successful exploitation may allow an attacker to:

- Execute arbitrary JavaScript in a victim's browser
- Steal session cookies or authentication tokens
- Hijack authenticated user sessions
- Display phishing content
- Redirect users to malicious websites
- Deliver malware through malicious scripts
- Damage user trust and application reputation

---

## Remediation

To mitigate this vulnerability:

- Validate and sanitize all user input.
- Apply context-aware output encoding.
- Use parameterized rendering where applicable.
- Implement a strict **Content Security Policy (CSP)**.
- Set security headers such as:
  - Content-Security-Policy
  - X-Content-Type-Options
  - X-Frame-Options
- Avoid rendering untrusted input directly into HTML.

---

## References

- OWASP Cross-Site Scripting (XSS)
  - https://owasp.org/www-community/attacks/xss/

- PortSwigger Web Security Academy
  - https://portswigger.net/web-security/cross-site-scripting

- Acunetix
  - https://www.acunetix.com/blog/web-security-zone/what-is-cross-site-scripting/

---

## Proof of Concept Images

### Figure 1

**XSS Alert Executed**

<img width="975" height="573" alt="image" src="https://github.com/user-attachments/assets/dd71868a-1892-4bda-ac29-314084e735ab" />


---

### Figure 2

**Source Code Showing Reflected Payload**

<img width="975" height="481" alt="image" src="https://github.com/user-attachments/assets/e12f6391-4d63-44f7-94e6-3b95a7832cdd" />

---

## Status

- **Reported via:** Responsible Vulnerability Disclosure
- **Vulnerability:** Reflected Cross-Site Scripting (XSS)
- **Report Type:** Public (Sanitized)
- **Sensitive Information:** Removed

---

## Author

**Balaji Sangana**

Cybersecurity Researcher | Web Application Penetration Tester
