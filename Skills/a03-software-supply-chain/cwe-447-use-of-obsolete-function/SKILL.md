
name: cwe-447-use-of-obsolete-function
description: Use when the target relies on deprecated/obsolete functions.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-447, supply-chain, pentest, owasp, a03]
category: pentesting-skills
related_skills:
  - owasp-a03-software-supply-chain-detect
---

# CWE-447 - Use of Obsolete Function

CWE-447: Use of Obsolete Function - the application uses a function or API that is officially obsolete (deprecated or removed), which often carries known defects or missing security fixes.

## Parent Skill

This is a sub-skill of `owasp-a03-software-supply-chain-detect` (OWASP A03 Software Supply Chain Failures, Top 10 2025).
Load the parent for overall A03 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-447 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when the target relies on functions or APIs officially marked deprecated/obsolete with known issues.

## Detection & Test

1. Fingerprint the runtime and major libraries (headers, JS bundle names, asset paths).
2. Identify obsolete APIs in the stack (e.g., MD5/SHAdesired digest, `Math.random()`, old jQuery, deprecated endpoints).
3. Check the vendor advisory for the obsolete function and note the replacement.
4. Confirm the obsolete function is actually invoked in a reachable code path.

## Example Requests

```http
GET / (Server + X-Powered-By + JS bundle name)
```
```http
GET /assets/app-1.3.2.min.js (jQuery 1.x - obsolete)
```

## Bypass Tricks

- Exploit a function that was deprecated specifically due to a security fix (e.g., an old `XMLHttpRequest` usage).
- Chain an obsolete TLS function with a downgrade attack.
- Use an obsolete digest (MD5) to predict a weak token.
- Trigger a deprecated endpoint that lacks modern input validation.

## Impact

- Exposure to defects in code that no longer receives security fixes.

## See Also

- `owasp-a03-software-supply-chain-detect` - parent skill (A03 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).