
name: cwe-283-unverified-ownership
description: Use when an ownership claim from input grants access.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-283, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-283 - Unverified Ownership

CWE-283: Unverified Ownership - a credential/token is signed by an entity that did not genuinely own it, and the app trusts the claim.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-283 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an app grants access/ownership based on an unverified ownership claim from user input.

## Detection & Test

1. Accept a signed token/attestation from an entity that has no real authority (e.g., self-issued).
2. Verify the application trusts the signature/claim without checking the signer's authority.
3. Forge ownership/attestation and confirm the resource is granted.
4. Check that the entity vouching is the true authority.

## Example Requests

```http
Sign token for role=admin and access admin page
```

## Bypass Tricks

- Forge a signed/attested token that claims ownership of a resource.
- Self-issue an ownership proof the app trusts without a trusted-signer check.
- Replay another user's ownership token.


## Impact

- Resource granted based on untrusted owner/attestation.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).