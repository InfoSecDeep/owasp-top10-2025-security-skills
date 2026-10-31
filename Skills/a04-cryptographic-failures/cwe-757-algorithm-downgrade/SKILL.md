
name: cwe-757-algorithm-downgrade
description: Use when testing CWE-757 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Selection of Less-Secure Algorithm (Downgrade)

CWE-757: Selection of Less-Secure Algorithm (Downgrade) occurs when an attacker or weak negotiation drives a client and server to a weaker cipher suite or protocol version than the server would otherwise support.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-757 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When TLS negotiation favors a weak cipher/version, or 3DES/RC4/anonymous ciphers are accepted.

## Detection & Test

1. **Enumerate.** `nmap --script ssl-enum-ciphers` and `openssl s_client -tls1 -tls1_1` to see supported/weak suites.
2. **Forcibly downgrade.** Attempt a weak handshake (TLS 1.0 / DES / RC4 / anonymous); capture the completed handshake.
3. **Confirm a real difference.** Weak cipher accepted != just a banner; complete the handshake.
4. **Decrypt (if possible).** With a known/weak key or if not forward-secret, capture traffic.
5. **Recommend.** Disable weak suites and pin TLS to a modern minimum.

## Example Findings

- Server accepts TLS 1.0 and 3DES_64 => Lucky13 / Sweet32.
- Anonymous ADH cipher accepted => MITM can decrypt.
- RC4 cipher negotiated on an otherwise-hardened host.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).