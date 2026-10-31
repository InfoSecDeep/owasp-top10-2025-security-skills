
name: cwe-470-unsafe-reflection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-470, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-470 - Unsafe Reflection

CWE-470: user input is used in a reflection API (Class.forName, Method.invoke, Object.getClass) to load or invoke a class/method, allowing the attacker to call an unintended method.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-470 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is used in a reflection API to dynamically load or invoke a class or method.

## Detection & Test

1. **Find the reflection sink.** Look for `Class.forName`, `Method.invoke`, `getDeclaredMethod`, `Object.getClass` with a user-controlled argument.
2. **Inject a class name.** Send a fully-qualified class name that the app shouldn't load.
3. **Confirm the class is loaded.** Verify the class is loaded and a method is invoked.
4. **Escalate.** Use the reflected class to call a dangerous method (e.g. `Runtime.getRuntime().exec`).
5. **Document the class, method, and proof.

## Example Findings

- `Class.forName(user_input)` where input = `java.lang.Runtime`.
- `method.invoke(obj, user_input)` where input selects an unintended method.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).