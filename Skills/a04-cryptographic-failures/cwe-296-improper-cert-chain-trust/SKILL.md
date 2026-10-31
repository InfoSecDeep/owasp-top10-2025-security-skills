
name: cwe-296-improper-cert-chain-trust
description: Use when testing CWE-296 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Improper Following of Certificate Chain of Trust

CWE-296: Improper Following of Certificate Chain of Trust occurs when a client fails to verify a server certificate's chain of trust (self-signed or untrusted CA accepted, hostname mismatch allowed), enabling MITM.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-296 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a client trusts a self-signed cert, skips hostname validation, or accepts chain mismatches.

## Detection & Test

1. **Observe the chain.** Check the server cert issuer, chain, and validity dates via `openssl s_client`.
2. **Check for self-signed / untrusted CA.** A cert issued by an untrusted or self-signed CA indicates weak trust handling.
3. **Test hostname validation.** Present the cert to a different host or SNI and see if it still passes.
4. **Probe chain building.** Confirm the client builds to a known root, not an issuer it trusts blindly.
5. **Recommend.** Enforce full-chain validation against a trusted CA store and validate the hostname.

## Example Findings

- A self-signed cert accepted by the client.
- Cert hostname mismatch with the requested SNI accepted.
- Chain terminates at a non-trusted issuer without an error.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).