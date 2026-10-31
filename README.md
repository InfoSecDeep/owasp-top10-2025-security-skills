# OWASP Top 10 2025 Skills for AI Agents

This repository contains OWASP Top 10 2025 security skills for AI agents. Use them to plan web application security assessments, follow category-specific testing procedures, investigate individual weaknesses, and document findings.

The `Skills/` directory contains **260 skills**: one overall testing workflow, 10 OWASP category skills, and 249 CWE-specific skills. Each skill is a Markdown instruction document named `SKILL.md`.

## Configure in Hermes Agent

Install and configure [Hermes Agent](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart) first, then clone this repository:

```sh
git clone https://github.com/InfoSecDeep/owasp-top10-2025-security-skills.git
cd owasp-top10-2025-security-skills
```

Edit `~/.hermes/config.yaml` and add the repository's **absolute Skills directory path** under `skills.external_dirs`. Merge this into any existing `skills` section.

Linux / WSL example:

```yaml
skills:
  external_dirs:
    - /home/your-user/owasp-top10-2025-security-skills/Skills
```

Windows example:

```yaml
skills:
  external_dirs:
    - 'C:/Users/your-user/Documents/GitHub/owasp-top10-2025-security-skills/Skills'
```

Replace the example path with your clone's location. For WSL, use the path visible inside WSL. If you use a separate Hermes profile, edit that profile's configuration.

Hermes discovers skills in configured external directories, including category subdirectories, so you can keep this repository's layout. See the [Hermes skills documentation](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills#external-skill-directories).

## Load a Skill

Start a new Hermes session after updating the configuration. Check discovery from your terminal:

```sh
hermes skills list
hermes
```

Inside Hermes chat, load the overall workflow:

```text
/owasp-top10-2025-testing
```

Or load a category or individual CWE skill with a task:

```text
/owasp-a05-injection Create an injection testing plan for my local test application.
/cwe-89-sql-injection Review my application's database queries for SQL injection.
```

You can also ask naturally:

> Load the owasp-top10-2025-testing skill and help me plan an assessment of my application.

Slash commands load skill instructions on demand; see [Using Skills in Hermes](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills#using-skills).

The overall workflow references `web-security-checklist-workflow`, which is not included here. It is a separate dependency for that workflow's CSV/XLSX checklist format.

## Skills Directory

This abbreviated tree shows the category folders and one example CWE skill. Each category contains its OWASP skill and many more CWE-specific skills.

```text
Skills/
├── a01-broken-access-control/
├── a02-security-misconfiguration/
├── a03-software-supply-chain/
├── a04-cryptographic-failures/
├── a05-injection/
│   ├── owasp-a05-injection/
│   │   └── SKILL.md
│   ├── cwe-89-sql-injection/
│   │   └── SKILL.md
│   └── ... many more CWE skills
├── a06-insecure-design/
├── a07-authentication-failures/
├── a08-software-data-integrity/
├── a09-logging-alerting-failures/
├── a10-exceptional-conditions/
└── owasp-top10-2025-testing/
    ├── SKILL.md
    └── references/
        ├── owasp2025-cwe-catalog.md
        └── reporting.md
```
