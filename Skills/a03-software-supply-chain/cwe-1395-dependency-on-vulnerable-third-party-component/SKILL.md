
name: cwe-1395-dependency-on-vulnerable-third-party-component
description: Use when a dependency (direct/transitive) is vulnerable.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1395, supply-chain, pentest, owasp, a03]
category: pentesting-skills
related_skills:
  - owasp-a03-software-supply-chain-detect
---

# CWE-1395 - Dependency on Vulnerable Third-Party Component

CWE-1395: Dependency on a Vulnerable Third-Party Component - the application depends on a third-party component that is vulnerable, whether directly or via a transitive dependency.

## Parent Skill

This is a sub-skill of `owasp-a03-software-supply-chain-detect` (OWASP A03 Software Supply Chain Failures, Top 10 2025).
Load the parent for overall A03 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-1395 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a third-party dependency (direct or transitive) is known to be vulnerable.

## Detection & Test

1. Enumerate the dependency tree (package.json, lockfile, vendor/).
2. Identify any known-vulnerable dependency, including transitive ones.
3. Confirm the vulnerable dependency is actually used (not just present).
4. Cross-check the version against the advisory's fixed version.

## Example Requests

```http
GET /package-lock.json (list of transitive deps)
```
```http
GET /vendor/ (directory listing of bundled components)
```

## Bypass Tricks

- Find a vulnerable dependency in the lockfile (direct or transitive).
- Check if the vulnerable dep is actually required (not just optional).
- Exploit a known CVE in the vulnerable dependency.
- Recommend an upgrade or patch to the vulnerable dependency.

## Impact

- Exploitable behavior from a vulnerable transitive dependency that the application relies on.

## See Also

- `owasp-a03-software-supply-chain-detect` - parent skill (A03 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).