
name: cwe-441-confused-deputy
description: Use when a privileged component is tricked into acting.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-441, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-441 - Confused Deputy

CWE-441: Confused Deputy - an attacker causes a more privileged entity to act on the attacker's behalf.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-441 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a privileged component is tricked into performing an action on the attacker's behalf.

## Detection & Test

1. Find privileged components that act on attacker-influenced parameters (callbacks, webhooks, signed requests).
2. Supply attacker-controlled input that makes the privileged component act in the attacker's favor.
3. Confirm the deputy's privileges were used for the attacker's benefit.
4. Check that the deputy validated the requester's authority/source.

## Example Requests

```http
Callback to /privileged?target=attacker
```
```http
Signed request forged to privileged endpoint
```

## Bypass Tricks

- Trick a privileged callback into acting on attacker input.
- Forge a signed/webhook request the privileged endpoint trusts.
- Exploit a service that acts on an unvalidated `target` parameter.
- Abuse a high-priv component to read/write on the attacker's behalf.


## Impact

- Privileged action performed on the attacker's behalf.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).