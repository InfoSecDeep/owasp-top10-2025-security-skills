
name: cwe-1329-reliance-on-component-not-updatable
description: Use when a component can't be updated (license/firmware).
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1329, supply-chain, pentest, owasp, a03]
category: pentesting-skills
related_skills:
  - owasp-a03-software-supply-chain-detect
---

# CWE-1329 - Reliance on Component That Is Not Updatable

CWE-1329: Reliance on a Component That Is Not Updateable - the application relies on a component for which no update is available, leaving known vulnerabilities unpatched.

## Parent Skill

This is a sub-skill of `owasp-a03-software-supply-chain-detect` (OWASP A03 Software Supply Chain Failures, Top 10 2025).
Load the parent for overall A03 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-1329 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a component cannot be updated (license, no newer version, embedded in hardware/firmware).

## Detection & Test

1. Identify components that are locked at a version (license, embedded, firmware).
2. Check if the vendor offers any update path or security patch.
3. Note any known CVEs in the locked version.
4. Flag the component as 'not updatable' in the report.

## Example Requests

```http
GET / (embedded/locked framework version)
```
```http
GET /package.json (a dependency locked to a specific version)
```

## Bypass Tricks

- Identify a component stuck at an old version (e.g., a browser-locked library).
- Check the component's license for update restrictions.
- Exploit a known CVE in the locked version.
- Recommend mitigation if no update is available.

## Impact

- Permanent exposure to unpatched vulnerabilities in a component that cannot be updated.

## See Also

- `owasp-a03-software-supply-chain-detect` - parent skill (A03 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).