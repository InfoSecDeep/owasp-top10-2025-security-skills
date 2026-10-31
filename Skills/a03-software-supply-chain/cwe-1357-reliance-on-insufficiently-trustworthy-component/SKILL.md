
name: cwe-1357-reliance-on-insufficiently-trustworthy-component
description: Use when a component is unverified, unsigned, or untrusted.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1357, supply-chain, pentest, owasp, a03]
category: pentesting-skills
related_skills:
  - owasp-a03-software-supply-chain-detect
---

# CWE-1357 - Reliance on Insufficiently Trustworthy Component

CWE-1357: Reliance on an Insufficiently Trustworthy Component - the application uses a component whose trustworthiness cannot be confirmed (unsigned, unverified source, low reputation).

## Parent Skill

This is a sub-skill of `owasp-a03-software-supply-chain-detect` (OWASP A03 Software Supply Chain Failures, Top 10 2025).
Load the parent for overall A03 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-1357 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a component's trustworthiness is in doubt (unverified source, low reputation, unsigned).

## Detection & Test

1. Check the component's signing status and source reputation.
2. Verify the component's origin (official registry, unverified CDN, GitHub fork).
3. Look for typosquats or lookalike package names.
4. Note the component's trustworthiness level in the report.

## Example Requests

```http
GET / (load a script from an unverified CDN)
```
```http
curl -sI https://cdn-unknown.com/lib.js (no SRI)
```

## Bypass Tricks

- Flag a script loaded from an unverified source without SRI.
- Check for a typosquat package name in the manifest.
- Verify the component's origin against a known-good registry.
- Look for unsigned components or those with a low reputation.

## Impact

- Potential for a malicious or compromised component to execute in the application context.

## See Also

- `owasp-a03-software-supply-chain-detect` - parent skill (A03 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).