# Software Engineer — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows. Every workflow follows three phases: **Pre-work** (specify before coding), **Execution** (implement the change), **Post-work** (review and verify output before merge).

## Pre-work Skills

| Skill | File | When to use |
|---|---|---|
| spec-writing | @core/skills/software-engineer/spec-writing.md | Write a testable spec before implementation begins |
| tech-debt | @core/skills/software-engineer/tech-debt.md | Identify, assess, and plan remediation of technical debt |

## Execution Skills

| Skill | File | When to use |
|---|---|---|
| debugging | @core/skills/software-engineer/debugging.md | Diagnose and fix a specific reported bug |
| refactoring | @core/skills/software-engineer/refactoring.md | Improve structure without changing behaviour |
| migration | @core/skills/software-engineer/migration.md | Plan and execute schema, data, or API migrations |
| dependency-update | @core/skills/software-engineer/dependency-update.md | Update dependencies safely with regression verification |

## Post-work Skills

| Skill | File | When to use |
|---|---|---|
| code-review | @core/skills/software-engineer/code-review.md | Review human-authored code before merge |
| agent-output-review | @core/skills/software-engineer/agent-output-review.md | Verify AI-generated code for drift, logic gaps, missing edge cases |

## Composite Workflows

Composite skills chain pre-work, execution, and post-work into a single invocable workflow.

| Skill | File | Phase chain |
|---|---|---|
| ship-feature | @core/skills/software-engineer/ship-feature.md | spec-writing (pre-work) → implementation (execution) → code-review or agent-output-review (post-work) |
| intrapreneur-workflow | @core/skills/software-engineer/intrapreneur-workflow.md | innovation-discovery (pre-work) → spec-writing → ship-feature (execution) → agent-output-review → stakeholder communication (post-work) |
