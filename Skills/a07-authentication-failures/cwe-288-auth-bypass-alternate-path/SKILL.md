
name: cwe-288-auth-bypass-alternate-path
description: Use when a web auth flaw matches cwe-288.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-288, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-288 - Authentication Bypass via Alternate Path or Channel

CWE-288: an alternate path or channel to the same resource is available without the usual authentication, allowing the attacker to reach it via the weaker route.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-288 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a resource has multiple paths (URLs, ports, endpoints) and one of them is unauthenticated.

## Detection & Test

1. **Map paths to the resource.** Identify all paths (URLs, ports, endpoints) that reach the same resource.
2. **Test the unauthenticated path.** Send the same request to the alternate path without credentials.
3. **Confirm the resource is reached.** Verify the resource is accessible via the weaker path.
4. **Escalate.** Use the unauthenticated path to reach the resource.
5. **Document the paths, the unauthenticated one, and proof.

## Example Findings

- A resource at `/api/data` that also serves at `/data` without auth.
- An endpoint on port 8080 that the front proxy doesn't check.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).