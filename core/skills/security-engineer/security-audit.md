# Skill: security-audit

**Type:** atomic

## Purpose

Systematically review a system, codebase, or configuration for security vulnerabilities. Produces a structured finding set with severity ratings, evidence, and remediation guidance — not a general impression of security posture.

## When to Invoke

- A feature, system, or configuration change needs security sign-off before release.
- A threat model has identified areas requiring closer code-level inspection.
- A periodic security review of an existing system is due.
- A security incident has prompted a targeted audit of a specific area.

## Workflow

1. **Define the audit scope.** Specify exactly what is being reviewed: which services, code paths, configuration files, and infrastructure components. Scope creep during an audit reduces depth; a smaller, deeper audit is more useful than a broad, shallow one.

2. **Gather the threat model.** Audit priorities should be derived from the threat model, not from intuition. If no threat model exists, run the threat-modeling skill first.

3. **Review input handling.** For every external input (HTTP requests, file uploads, queue messages, environment variables, third-party API responses):
   - Is the input validated and normalised before use?
   - Is user input ever concatenated into SQL, shell commands, HTML, or file paths?
   - Are allowlists used rather than denylists?

4. **Review authentication and authorisation.** For every protected resource or operation:
   - Is authentication enforced before authorisation?
   - Is authorisation checked before every sensitive action?
   - Are session tokens invalidated on logout and credential change?
   - Are there any routes or operations that skip authentication for "internal" callers?

5. **Review secrets handling.** Search the codebase for hardcoded credentials, API keys, and tokens. Review how secrets are loaded at runtime. Check logs and error messages for credential leakage.

6. **Review cryptography.** Identify every place where data is encrypted, hashed, or signed. Verify that approved algorithms are used and that implementation is via a vetted library — no custom crypto.

7. **Review error handling.** For every error path:
   - Are stack traces or internal details returned to callers?
   - Are errors logged with sensitive data?
   - Does an error in an auth check grant access (fail open)?

8. **Review dependencies.** Check the lockfile against vulnerability advisories. Identify unused dependencies. Note any dependencies pinned to old versions with known CVEs.

9. **Document findings.** For each finding:
   - **Location** — file, line, or component
   - **Description** — what the vulnerability is
   - **Severity** — Critical / High / Medium / Low
   - **Evidence** — the specific code or configuration
   - **Remediation** — specific, actionable fix

## Output

- **Audit scope** — what was reviewed
- **Findings** — each finding with location, description, severity, evidence, and remediation
- **Summary table** — count of findings by severity
- **Verdict** — Clear / Conditional (findings but not blocking) / Blocked (Critical findings)
