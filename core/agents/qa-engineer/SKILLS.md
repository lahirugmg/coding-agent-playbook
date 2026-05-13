# QA Engineer — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows.

## Atomic Skills

| Skill | File | When to use |
|---|---|---|
| test-planning | @core/skills/qa-engineer/test-planning.md | Define the scope, approach, and coverage targets for a testing effort |
| test-writing | @core/skills/qa-engineer/test-writing.md | Write test cases or automated tests for a specific feature or code path |
| bug-report | @core/skills/qa-engineer/bug-report.md | Produce a well-formed bug report with reproduction steps and expected behaviour |
| performance-testing | @core/skills/qa-engineer/performance-testing.md | Design and execute performance tests against a defined baseline and threshold |
| exploratory-testing | @core/skills/qa-engineer/exploratory-testing.md | Run structured exploratory testing to find issues outside the specified scope |

## Composite Skills

Composite skills invoke other skills in sequence. Sub-skills are listed in execution order.

| Skill | File | Sub-skills |
|---|---|---|
| feature-validation | @core/skills/qa-engineer/feature-validation.md | test-planning → test-writing → exploratory-testing → bug-report |
