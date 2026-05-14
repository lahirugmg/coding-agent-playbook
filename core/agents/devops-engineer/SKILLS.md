# DevOps Engineer — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows. Every workflow follows three phases: **Pre-work** (design pipeline and infrastructure before building), **Execution** (build and optimise the delivery system), **Post-work** (deploy and verify the service is healthy in production).

## Pre-work Skills

| Skill | File | When to use |
|---|---|---|
| pipeline-design | @core/skills/devops-engineer/pipeline-design.md | Design or refactor a CI/CD pipeline for a project or service |
| infrastructure-as-code | @core/skills/devops-engineer/infrastructure-as-code.md | Write or review infrastructure definitions in Terraform, CloudFormation, or similar |

## Execution Skills

| Skill | File | When to use |
|---|---|---|
| containerization | @core/skills/devops-engineer/containerization.md | Containerise an application or review existing container definitions |
| build-optimization | @core/skills/devops-engineer/build-optimization.md | Identify and address bottlenecks in build or pipeline execution time |

## Post-work Skills

| Skill | File | When to use |
|---|---|---|
| deployment | @core/skills/devops-engineer/deployment.md | Execute a deployment with rollback coverage and post-deploy verification |

## Composite Workflows

Composite skills chain pre-work, execution, and post-work into a single invocable workflow.

| Skill | File | Phase chain |
|---|---|---|
| ship-service | @core/skills/devops-engineer/ship-service.md | pipeline-design → infrastructure-as-code (pre-work) → containerization → build-optimization (execution) → deployment (post-work) |
