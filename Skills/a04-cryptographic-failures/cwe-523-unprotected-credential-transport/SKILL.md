
name: cwe-523-unprotected-credential-transport
description: Use when testing CWE-523 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Unprotected Transport of Credentials

CWE-523: Unprotected Transport of Credentials occurs when a username/password or connection-string credential is transmitted without protection (cleartext or no integrity), letting an observer capture the credential directly.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-523 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When credentials travel over cleartext HTTP, or an unsigned/encrypted-but-readable transport.

## Detection & Test

1. **Intercept login / DB flow.** Capture username+password or connection-string transmission.
2. **Check channel.** http:// vs https://; TLS present?
3. **Check placement.** Credentials in URL, header, or body over cleartext are all exposed.
4. **Confirm capture.** A passive observer on the path reads the credential.
5. **Note follow-up.** Cleartext credentials are also stored in referrer/cache if echoed.

## Example Findings

- `POST /login` with username/password in the body over http://.
- JDBC connection string in a URL query over http.
- Basic-auth password sent unencrypted.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).