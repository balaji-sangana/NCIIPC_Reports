# HTML Injection Vulnerability Report

> **Disclaimer**
>
> This report is a sanitized version of a vulnerability submitted through the responsible vulnerability disclosure process. Sensitive information has been removed for educational and portfolio purposes.

---

## Summary

An HTML Injection vulnerability was identified where user-controlled input is reflected without proper sanitization. An attacker can inject HTML elements, such as anchor (`<a>`) tags, into the application's response.

Although HTML Injection does not execute JavaScript by itself, it can be abused for phishing attacks, malicious redirects, UI manipulation, and malware distribution, potentially leading users to disclose sensitive information.

---

## Severity

**Critical**

---

## Vulnerability Details

| Field | Value |
|-------|--------|
| Vulnerability | HTML Injection |
| Attack Complexity | Easy |
| Attack Vector | Remote / External |
| CWE | CWE-79 (Improper Neutralization of Input During Web Page Generation) |
| OWASP | Injection |

---

## Affected Endpoint

```text
https://www.services.bis.gov.in/php/BIS_2.0/eBIS/hkm_branch_wise.php?branch_code=test
```

---

## Proof of Concept

### Payload

```html
<a href="http://example.com">Click Here</a>
```

When the payload is injected into the vulnerable parameter, the application renders the HTML directly instead of encoding it.

---

## Impact

Successful exploitation could allow an attacker to:

- Redirect users to phishing websites
- Trick users into revealing credentials
- Deliver malware through malicious links
- Modify page content displayed to users
- Damage user trust in the application

---

## Remediation

To mitigate this vulnerability:

- Validate and sanitize all user input.
- Perform proper output encoding before rendering HTML.
- Implement allow-list input validation.
- Encode special HTML characters (`<`, `>`, `"`, `'`, `&`).
- Deploy appropriate HTTP security headers, including:
  - Content-Security-Policy (CSP)
  - X-Content-Type-Options
  - X-Frame-Options
- Avoid rendering untrusted HTML directly into the DOM.

---

## References

- OWASP – HTML Injection
  - https://owasp.org/www-community/attacks/HTML_Injection

- PortSwigger Web Security Academy
  - https://portswigger.net/web-security/html-injection

- Acunetix
  - https://www.acunetix.com/blog/web-security-zone/html-injection/

---

## Proof of Concept Images

### Figure 1

Application rendering the injected HTML anchor tag.

```
<img width="975" height="510" alt="image" src="https://github.com/user-attachments/assets/5858b1d1-3c8a-4223-a275-e6e3ae53e3b2" />

```

---

### Figure 2

Source code showing the injected HTML rendered in the application's response.

```
<img width="975" height="256" alt="image" src="https://github.com/user-attachments/assets/ed4b673d-3183-4714-b404-9d9ff65c076b" />

```

---

## Status

- **Reported via:** Responsible Vulnerability Disclosure
- **Report Type:** HTML Injection
- **Report Version:** Public (Sanitized)
- **Sensitive Information:** Removed

---

## Author

**Balaji Sangana**

Cybersecurity Researcher | Web Application Penetration Tester

```
