# Skill: deployment

**Type:** atomic

## Purpose

Plan and execute a deployment to a target environment with a defined rollback plan, post-deploy verification, and a clear declaration of success or failure. A deployment without a rollback plan is a gamble.

## When to Invoke

- A change needs to be deployed to staging or production.
- A deployment needs to be planned in advance for a high-risk or high-traffic release.
- A previously failed deployment needs to be assessed and retried or rolled back.

## Workflow

1. **Confirm prerequisites.** Before deploying:
   - [ ] The artifact to be deployed has passed all pipeline stages in a lower environment
   - [ ] The same artifact (same image digest or binary hash) is being promoted — not rebuilt
   - [ ] The deployment window has been communicated to relevant stakeholders
   - [ ] A rollback plan is documented and the rollback has been tested or is known to work
   - [ ] The change log is understood: what is changing, what configuration is changing, what migrations will run

2. **Define the deployment strategy.** Choose the appropriate strategy for the risk level:
   - **Blue/green** — full switch from old version to new; rollback = switch back
   - **Canary** — route a small percentage of traffic to new version; expand or roll back based on metrics
   - **Rolling** — replace instances one at a time; slower but no double capacity required
   - **Feature flag** — code ships but feature is off; activate separately from deployment

3. **Define the rollback trigger.** Specify exactly what will trigger a rollback:
   - Error rate exceeds X% for Y minutes
   - p95 latency exceeds X ms for Y minutes
   - Health check fails on > N instances
   Rollback triggers must be measurable and automatic where possible.

4. **Execute the deployment.** Follow the defined strategy:
   - Apply the change in the target environment
   - Monitor the rollback triggers in real time during the deployment
   - Do not leave the deployment unmonitored during the initial soak period

5. **Run smoke tests.** Immediately after deployment, execute a minimal set of automated checks against the production environment:
   - Key user flows (login, primary action, data read)
   - Health check endpoints
   - A sample of monitoring metrics
   Smoke tests are not regression tests — they are the minimum to confirm the service is alive.

6. **Define the soak period.** The deployment is not complete until metrics are stable for a defined period after the last change. Typical soak: 15–30 minutes for routine changes, 1–4 hours for high-risk changes.

7. **Declare the outcome.** Explicitly state: COMPLETE (all green through soak), ROLLED BACK (trigger hit, rollback executed), or INVESTIGATING (anomaly detected, not yet rolled back).

## Output

- **Pre-deploy checklist** — confirmed prerequisites
- **Deployment log** — what was deployed, when, by whom, with artifact reference
- **Smoke test results** — pass/fail for each check
- **Post-deploy metrics summary** — key metrics during the soak period
- **Outcome declaration** — COMPLETE / ROLLED BACK / INVESTIGATING with rationale
