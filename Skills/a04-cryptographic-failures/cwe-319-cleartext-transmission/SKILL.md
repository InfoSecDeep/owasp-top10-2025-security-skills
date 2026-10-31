
name: cwe-319-cleartext-transmission
description: Use when testing CWE-319 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Cleartext Transmission of Sensitive Information

CWE-319: Cleartext Transmission of Sensitive Information occurs when sensitive data (passwords, tokens, PII) is transmitted over an unencrypted channel or embedded in a URL, cookie, or header, letting an eavesdropper capture it.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-319 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a login, password reset, payment, or PII flow uses cleartext HTTP or puts secrets in URL/body/header.

## Detection & Test

1. **Capture the flow.** Intercept login, password reset, payment, and any PII-bearing request.
2. **Check the channel.** http:// vs https://; TLS present?
3. **Check placement.** Are `password`, `token`, `ssn`, `card` in URL, query string, header, or body? Body over cleartext is still exposed.
4. **Confirm exposure.** A passive observer on the path reads the field.
5. **Note caching/referrer.** Cleartext responses may be logged or cached server-side.

## Example Findings

- `GET /login?password=supersecret` on http://.
- `password` in the query string.
- PII returned in a plain-`http` AJAX response.
- JWT in a URL fragment over http.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).