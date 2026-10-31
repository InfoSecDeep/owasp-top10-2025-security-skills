
name: cwe-942-permissive-cross-domain-policy
description: Use when crossdomain.xml allows * or an untrusted domain.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-942, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-942 - Permissive Cross-Domain Policy with Untrusted Domains

CWE-942: Permissive Cross-Domain Policy with Untrusted Domains - the application's cross-domain policy (`crossdomain.xml`) allows access from an untrusted domain, enabling cross-origin data reads.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-942 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when `crossdomain.xml` or `clientaccesspolicy.xml` allows access from `*` or an untrusted domain.

## Detection & Test

1. Fetch `crossdomain.xml` and `clientaccesspolicy.xml`.
2. Check for `<allow-access-from domain="*"/>`.
3. Confirm the domain is untrusted (e.g., `*` or `attacker.com`).
4. Use a cross-origin request to read data from the target.

## Example Requests

```http
GET /crossdomain.xml (allow-access-from domain="*")
```

## Bypass Tricks

- Fetch a `crossdomain.xml` with `domain="*"`.
- Exploit a Flash/Silverlight app that uses the permissive policy.
- Use a cross-origin `fetch` to read data from the target.
- Check `clientaccesspolicy.xml` for the same permissive rule.

## Impact

- Cross-origin data read via a permissive cross-domain policy.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).