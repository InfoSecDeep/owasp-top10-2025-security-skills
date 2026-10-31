
name: cwe-5-j2ee-misconfig-plaintext
description: Use when a J2EE app's traffic is downgraded to cleartext.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-5, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-5 - J2EE Misconfiguration - Data Transmission Without Encryption

CWE-5: J2EE Misconfiguration - Data Transmission Without Encryption - the application accepts cleartext HTTP for data that should be confidential.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-5 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a J2EE/Java web app accepts or serves traffic that can be downgraded to cleartext.

## Detection & Test

1. Identify whether the endpoint only accepts HTTP or accepts both HTTP/HTTPS.
2. Check the HSTS header and the `httpsOnly` constraint in the deployment descriptor.
3. Probe a known HTTPS-only page and see if it still answers on port 80.
4. Confirm the app does not enforce TLS when handling sensitive data.

## Example Requests

```http
curl -k http://target/secure
```
```http
GET /login (no redirect to https)
```

## Bypass Tricks

- Bypass the HSTS preload with a non-preloaded subdomain.
- Downgrade a user by forcing HTTP (e.g., a link to http:// in a known page).
- Exploit an SSL-termination load balancer that forwards to backend over HTTP.
- Use a `?` fragment to strip the TLS requirement on a specific path.

## Impact

- Session/credential theft via cleartext transport.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).