
name: cwe-444-http-request-smuggling
description: Use when a web design flaw matching cwe-444 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-444, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-444 - HTTP Request Smuggling

CWE-444: ambiguous header handling (CL/TE mismatch) lets one request be interpreted differently by the front proxy and the origin server, allowing request smuggling.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-444 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a proxy and origin server disagree on request framing (Content-Length/Transfer-Encoding).

## Detection & Test

1. **Test framing.** Send a CL/TE or TE/CL mismatch (e.g. `Content-Length: 6\r\nTransfer-Encoding: chunked`).
2. **Send a state marker.** Include a request that writes a value visible to the origin only if smuggling occurred.
3. **Confirm the merge.** Show the origin merged the two requests (the marker appears where it shouldn't).
4. **Escalate.** Use the merged request to bypass a check (e.g. reach a protected resource behind the front proxy).
5. **Document the payloads, the marker, and the observed divergence.

## Example Findings

- A `Transfer-Encoding: chunked` body smuggled past a front proxy into the origin's handler.
- A CL.TE mismatch that lets a request reach a `/admin` route meant to be hidden.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).