
name: cwe-337-predictable-prng-seed
description: Use when testing CWE-337 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Predictable Seed in PRNG

CWE-337: Predictable Seed in PRNG occurs when a pseudo-random generator is seeded from a value the attacker can observe or recover (e.g. session id, timestamp leaked to the client), enabling reproduction of the output stream.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-337 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an attacker can see the value used to seed a PRNG and tokens follow.

## Detection & Test

1. **Capture tokens and inputs together.** Record tokens alongside any client-visible values (session id, timestamp, request id).
2. **Find the seeding relation.** Test whether output equals `PRNG(seen_value)`.
3. **Reproduce.** Feed the observed seed into the identified algorithm and match a live token.
4. **Predict forward.** Forecast the next server value and confirm.

## Example Findings

- Java `new Random(sessionid)` => next token recoverable from the session id.
- `srand(timestamp)` where the timestamp is sent back to the client.
- `random.seed(req.request_id)` replayable.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).