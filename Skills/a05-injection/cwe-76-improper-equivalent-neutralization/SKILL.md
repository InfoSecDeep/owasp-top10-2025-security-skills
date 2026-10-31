
name: cwe-76-improper-equivalent-neutralization
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-76, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-76 - Improper Neutralization of Equivalent Special Elements

CWE-76: the app neutralizes one representation of a special character but not an equivalent one (e.g. blocks `%3C` but not `<` or `&#60;`), so the filter is bypassed.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-76 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a filter blocks one encoding but not another of the same character.

## Detection & Test

1. **Identify the filter.** Send the raw special character and note the neutralization behavior.
2. **Test equivalents.** Send URL-encoded, HTML-entity, XML-entity, double-encoded, and Unicode variants.
3. **Confirm the bypass.** Show the filter passes an equivalent that still reaches the sink with special meaning.
4. **Prove impact.** Use the bypassed encoding to achieve the same injection as the raw character.
5. **Document all bypasses.** List every equivalent that slipped through.

## Example Findings

- `<` is blocked but `&lt;` and `%3C` are not.
- A regex strips `script` but not `ScRiPt` or `scr<script>ipt`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).