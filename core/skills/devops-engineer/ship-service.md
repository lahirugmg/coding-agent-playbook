# Skill: ship-service

**Type:** composite
**Sub-skills:** pipeline-design → containerization → infrastructure-as-code → deployment

## Purpose

End-to-end workflow for making a service production-ready from an infrastructure perspective. Covers the CI/CD pipeline, container definition, cloud infrastructure, and the deployment itself — with rollback coverage at every step.

## When to Invoke

- A new service needs to be made deployable for the first time.
- An existing service is being significantly restructured and its delivery infrastructure needs to match.
- A service is being promoted from staging to production for the first time.

## Workflow

### Step 1 — Pipeline Design (@pipeline-design)

Before touching any infrastructure:

1. Read the codebase to understand the build, test, and packaging requirements.
2. Run the pipeline-design skill: design the CI/CD stages, triggers, environments, and artifact flow.
3. Define the promotion model: how a passing build in CI becomes a candidate for production.

**Gate:** Pipeline design is reviewed by at least one engineer familiar with the codebase. Do not write infrastructure code without an agreed pipeline design.

### Step 2 — Containerization (@containerization)

With the pipeline design agreed:

1. Run the containerization skill: write or review the Dockerfile, compose files, and any container orchestration config.
2. Image must be minimal, non-root, and pinned to a specific base image digest.
3. Verify the image builds and the service starts correctly inside the container before proceeding.

**Gate:** Container image builds cleanly, service starts, and a basic health check passes inside the container.

### Step 3 — Infrastructure as Code (@infrastructure-as-code)

With the container ready:

1. Run the infrastructure-as-code skill: write the cloud infrastructure definitions (Terraform, CloudFormation, or equivalent) for compute, networking, storage, and secrets management.
2. All infrastructure must be in version control. No manual console changes.
3. Run `plan` or `diff` and review before applying. Infrastructure drift must be zero before deployment.

**Gate:** IaC has been reviewed, planned, and applied successfully to the staging environment.

### Step 4 — Deployment (@deployment)

With infrastructure in place:

1. Run the deployment skill: execute the deployment to production with a defined rollback plan.
2. Monitor health checks, error rates, and latency for a defined soak period post-deploy.
3. Declare the deployment complete only when all health checks are green and the soak period has passed.

**Gate:** Post-deploy metrics are within normal bounds for the full soak period. Rollback plan is documented and tested.

## Output

A service delivery package containing:

- **Pipeline definition** — CI/CD config committed to version control
- **Container artifacts** — Dockerfile, compose files, image verified and tagged
- **Infrastructure code** — all cloud resources defined in IaC, applied to staging and production
- **Deployment record** — what was deployed, when, by whom, with rollback procedure
- **Post-deploy health summary** — metrics confirming the service is healthy

This package is the handoff artifact for the SRE to establish ongoing observability and runbooks.
