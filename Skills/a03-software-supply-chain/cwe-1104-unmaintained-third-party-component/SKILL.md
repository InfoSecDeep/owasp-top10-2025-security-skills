
name: cwe-1104-unmaintained-third-party-component
description: Use when a component is abandoned, unmaintained, or stalled.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1104, supply-chain, pentest, owasp, a03]
category: pentesting-skills
related_skills:
  - owasp-a03-software-supply-chain-detect
---

# CWE-1104 - Use of Unmaintained Third-Party Components

CWE-1104: Use of Unmaintained Third-Party Components - the application uses a third-party component that is no longer maintained or has an abandoned upstream.

## Parent Skill

This is a sub-skill of `owasp-a03-software-supply-chain-detect` (OWASP A03 Software Supply Chain Failures, Top 10 2025).
Load the parent for overall A03 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-1104 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a component has no active maintainers, abandoned upstream, or stalled releases.

## Detection & Test

1. Check the component's upstream repository for last commit/release age.
2. Look for archived repos, `no maintainers`, or a 'no updates since X' notice.
3. Cross-reference the component with a CVE database for open issues in the unmaintained version.
4. Note the component in the report with the 'unmaintained' flag.

## Example Requests

```http
GET /package.json (last-release field)
```
```http
GET / (X-Powered-By header on an old, unmaintained framework)
```

## Bypass Tricks

- Flag a component whose upstream is `archived` or has no releases in 18+ months.
- Check for `deprecated` or `no-maintainer` notices.
- Exploit any unpatched CVE in the unmaintained version.
- Report the component as an unmaintained risk regardless of current CVEs.

## Impact

- Long-term exposure to unpatched vulnerabilities in a component with no one to fix them.

## See Also

- `owasp-a03-software-supply-chain-detect` - parent skill (A03 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).