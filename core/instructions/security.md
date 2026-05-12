# Security

Shared instruction loaded by agents that produce or review code, infrastructure, or system design.

## Validate at Boundaries, Trust Internally

- Validate all input at system entry points: HTTP requests, CLI args, file uploads, webhook payloads, queue messages.
- Once validated and normalised, trust the data internally — don't re-validate at every layer.
- Never trust data that crosses a trust boundary (user-supplied, third-party API, deserialized from storage).

## Injection Prevention

- Never concatenate user input into SQL, shell commands, HTML, or template strings.
- Use parameterised queries for all database access.
- Use allowlists, not denylists, for input validation.
- Treat file paths from external sources as untrusted — canonicalise and check against an allowed root.

## Secrets Management

- No secrets in source code, commit history, logs, or error messages.
- Load secrets from environment variables or a secret manager at runtime.
- Never log credentials, tokens, or PII — even at debug level.
- Rotate secrets that may have been exposed; don't just overwrite.

## Authentication and Authorisation

- Authenticate before authorising. Never skip authentication in "internal" routes.
- Apply the principle of least privilege: request only the permissions the task requires.
- Invalidate sessions on logout and password change.
- Use constant-time comparison for credential checks to prevent timing attacks.

## Dependency Hygiene

- Prefer well-maintained dependencies with active security patching.
- Pin dependency versions in production builds. Use a lockfile.
- Review changelogs and security advisories before updating.
- Remove unused dependencies — every package is an attack surface.

## Cryptography

- Don't implement cryptographic primitives yourself. Use vetted library functions.
- Use established algorithms: AES-GCM for symmetric encryption, RSA-OAEP or ECDH for asymmetric, bcrypt/argon2 for password hashing.
- Never use MD5 or SHA-1 for security-sensitive hashing.
- Generate random values with a cryptographically secure RNG.

## Fail Secure

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
