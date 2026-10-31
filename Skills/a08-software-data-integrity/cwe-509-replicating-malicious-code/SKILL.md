
name: cwe-509-replicating-malicious-code
description: Use when testing cwe-509 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-509, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-509 - Replication of Malicious Code

CWE-509: the application replicates or spreads malicious code to other resources or systems, so the malicious code spreads beyond its original location.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-509 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When malicious code is replicated or spread to other resources, files, or systems.

## Detection & Test

1. **Identify the replication mechanism.** Find where the app copies, propagates, or syncs a resource.
2. **Inject the malicious code.** Place the malicious code in a source that the app will replicate.
3. **Confirm the code is replicated.** Show the malicious code appears in the destination.
4. **Escalate.** Use the replicated code to achieve RCE, data access, or persistence.
5. **Document the mechanism, the code, and proof.

## Example Findings

- A file sync that copies a malicious script to all nodes in a cluster.
- A template engine that includes a malicious partial in every page.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).