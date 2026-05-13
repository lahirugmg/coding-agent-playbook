# Security Engineer — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows.

## Atomic Skills

| Skill | File | When to use |
|---|---|---|
| security-audit | @core/skills/security-engineer/security-audit.md | Review a system, codebase, or configuration for security vulnerabilities |
| threat-modeling | @core/skills/security-engineer/threat-modeling.md | Identify assets, threat actors, attack surface, and trust boundaries for a system |
| vulnerability-assessment | @core/skills/security-engineer/vulnerability-assessment.md | Assess and prioritise known vulnerabilities in a system or dependency set |
| dependency-vulnerability | @core/skills/security-engineer/dependency-vulnerability.md | Identify and triage security vulnerabilities in project dependencies |
| compliance-review | @core/skills/security-engineer/compliance-review.md | Assess a system against a compliance framework (SOC 2, GDPR, PCI-DSS, etc.) |

## Composite Skills

Composite skills invoke other skills in sequence. Sub-skills are listed in execution order.

| Skill | File | Sub-skills |
|---|---|---|
| security-review | @core/skills/security-engineer/security-review.md | threat-modeling → security-audit → vulnerability-assessment |
