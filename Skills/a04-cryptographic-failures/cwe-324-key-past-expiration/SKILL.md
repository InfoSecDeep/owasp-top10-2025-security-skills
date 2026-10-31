
name: cwe-324-key-past-expiration
description: Use when testing CWE-324 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Use of Key Past Expiration Date

CWE-324: Use of Key Past Expiration Date occurs when a key that has passed its expiry is still accepted for encryption, signing, or authentication.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-324 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an expired key continues to authenticate or decrypt.

## Detection & Test

1. **Identify keys with validity windows.** TLS certs, API keys, JWT `exp`, signing keys.
2. **Check enforcement.** Submit an expired key/token and confirm the server still accepts it.
3. **Confirm the window.** Read the expiry claim/cert dates and compare to current time.
4. **Note cause.** Clock skew, missing expiry check, or a never-rotated key.
5. **Recommend.** Enforce expiry server-side and rotate proactively.

## Example Findings

- JWT still accepted after `exp` (server ignores expiry).
- TLS certificate accepted after its NotAfter date.
- An API key still valid months after its documented rotation.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).