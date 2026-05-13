# Knowledge: security-guidelines

**Type:** Internal, stable
**Freshness:** Slow-changing — updated when common vulnerability classes evolve or team practices change

## What It Contains

Developer-facing guidance for writing secure code. Covers the techniques and rules that prevent the most common classes of vulnerability at the point of implementation and review.

Includes:
- Input validation and boundary enforcement
- Injection prevention (SQL, shell, HTML, path traversal)
- Secrets management practices
- Authentication and authorisation patterns
- Dependency hygiene for security
- Cryptographic algorithm selection
- Fail-secure error handling
- A code review checklist for catching security issues

## When to Consult

- Before implementing any feature that accepts external input
- When writing code that touches authentication, authorisation, or session management
- When handling secrets, credentials, or PII
- When reviewing code for security issues
- When selecting a cryptographic approach
- When adding or updating a dependency

## Effective Queries

- "How should I validate and sanitise this form input before using it in a query?"
- "What is the correct way to handle and store API keys in this service?"
- "What algorithms are appropriate for password hashing?"
- "What should I check when reviewing a PR for injection vulnerabilities?"
- "How should errors be handled at an authentication boundary?"

## What It Does NOT Contain

- Organisation-specific security policies, compliance frameworks, or approved algorithm lists — for that, use security-policies
- Vulnerability findings for a specific system — those come from a security audit skill
- CVE information about specific packages — for that, use dependency-registry

## Rules

### Validate at Boundaries, Trust Internally

- Validate all input at system entry points: HTTP requests, CLI args, file uploads, webhook payloads, queue messages.
- Once validated and normalised, trust the data internally — don't re-validate at every layer.
- Never trust data that crosses a trust boundary (user-supplied, third-party API, deserialised from storage).

### Injection Prevention

- Never concatenate user input into SQL, shell commands, HTML, or template strings.
- Use parameterised queries for all database access.
- Use allowlists, not denylists, for input validation.
- Treat file paths from external sources as untrusted — canonicalise and check against an allowed root.

### Secrets Management

- No secrets in source code, commit history, logs, or error messages.
- Load secrets from environment variables or a secret manager at runtime.
- Never log credentials, tokens, or PII — even at debug level.
- Rotate secrets that may have been exposed; don't just overwrite.

### Authentication and Authorisation

- Authenticate before authorising. Never skip authentication in "internal" routes.
- Apply the principle of least privilege: request only the permissions the task requires.
- Invalidate sessions on logout and password change.
- Use constant-time comparison for credential checks to prevent timing attacks.

### Dependency Hygiene

- Prefer well-maintained dependencies with active security patching.
- Pin dependency versions in production builds. Use a lockfile.
- Review changelogs and security advisories before updating.
- Remove unused dependencies — every package is an attack surface.

### Cryptography

- Don't implement cryptographic primitives yourself. Use vetted library functions.
- Use established algorithms: AES-GCM for symmetric encryption, RSA-OAEP or ECDH for asymmetric, bcrypt/argon2 for password hashing.
- Never use MD5 or SHA-1 for security-sensitive hashing.
- Generate random values with a cryptographically secure RNG.

### Fail Secure

- On unexpected error, deny by default — don't allow access when the authorisation check fails.
- Catch and handle exceptions at security-critical paths; an unhandled exception that exposes a stack trace is a vulnerability.
- Return generic error messages to external callers; log detail internally.

## Code Review Checklist

When reviewing code for security:
- [ ] No user input reaches a sink (SQL, shell, HTML, path) without sanitisation
- [ ] No secrets in code or configs committed to version control
- [ ] Authorisation checked before every sensitive action
- [ ] Errors handled without leaking internal detail to callers
- [ ] Dependencies are pinned and reviewed

## Adapter Notes

Provide access via file-system tool for any team-maintained secure coding guides stored in the repository (e.g. `docs/security/`, `SECURITY.md`).

For general secure coding guidance not yet codified in team docs, web-search against canonical sources (OWASP cheat sheets, language-specific security guides, CWE descriptions) is appropriate. Always prefer team-specific guidance over general references when they exist.
