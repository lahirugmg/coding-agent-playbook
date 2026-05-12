# Skill: code-review

**Type:** atomic
**Scope:** Review human-authored code changes against coding standards, correctness, and security.

## When to Invoke

- A pull request or diff is ready for review before merge.
- Asked to review a specific file, function, or change set.

## Inputs

- The diff or file(s) to review.
- The stated purpose of the change (ticket, PR description, or verbal summary).

## Procedure

1. **Understand intent first.** Read the PR description or ask for one before reading code. Reviewing without knowing the goal produces noise.

2. **Correctness** — does the code do what it claims?
   - Trace the happy path end-to-end.
   - Identify edge cases the code doesn't handle. Note whether they are in scope.
   - Check for off-by-one errors, null/undefined access, incorrect assumptions about input ranges.

3. **Standards compliance** — does the code match the codebase's conventions?
   - Naming, formatting, file organisation.
   - No speculative abstractions or features beyond the stated scope.
   - Comments only where the why is non-obvious.

4. **Security** — does the code introduce vulnerabilities?
   - User input reaching a sink without sanitisation.
   - Secrets, PII, or internal detail leaking to logs or error responses.
   - Authorisation checks missing or bypassable.

5. **Tests** — do they verify intent?
   - Every changed behaviour should have a corresponding test.
   - Tests should fail when the business logic they protect is removed.
   - Missing tests are a blocking concern, not a suggestion.

6. **Surgical check** — does the diff touch only what the task requires?
   - Flag unrelated changes. They should be split out, not bundled.

## Output

A structured review with three sections:

**Blocking** — must be resolved before merge. Each item: file:line, what's wrong, why it matters, suggested fix.

**Non-blocking** — improvements worth considering but not required. One line each.

**Confirmed** — two or three things done well. Keeps the signal-to-noise ratio honest.

If there are no blocking issues, say so explicitly.
