# Technical Architect — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows.

## Atomic Skills

| Skill | File | When to use |
|---|---|---|
| system-design | @core/skills/technical-architect/system-design.md | Design the architecture for a new system or major component |
| architecture-review | @core/skills/technical-architect/architecture-review.md | Review an existing or proposed architecture against requirements and constraints |
| adr-writing | @core/skills/technical-architect/adr-writing.md | Document an architectural decision with context, alternatives, and rationale |
| technical-spec | @core/skills/technical-architect/technical-spec.md | Write a detailed technical specification for implementation teams |
| feasibility-analysis | @core/skills/technical-architect/feasibility-analysis.md | Assess whether a proposed approach is technically achievable within given constraints |

## Composite Skills

Composite skills invoke other skills in sequence. Sub-skills are listed in execution order.

| Skill | File | Sub-skills |
|---|---|---|
| design-and-document | @core/skills/technical-architect/design-and-document.md | system-design → adr-writing → technical-spec |
