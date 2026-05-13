# Knowledge: development-best-practices

**Type:** Internal + External, stable
**Freshness:** Slow-changing — evolves with the industry and team conventions, not with individual features

## What It Contains

Established principles, patterns, and conventions for writing, testing, and maintaining software well. Covers both universal best practices and the team's specific agreed conventions where they diverge from or extend the universal baseline.

Includes:
- Design principles (SOLID, DRY, YAGNI, separation of concerns, least privilege)
- Code design patterns relevant to the team's stack (Gang of Four, domain patterns, functional patterns)
- Testing philosophy and strategy (test pyramid, test naming, what to unit test vs. integrate test vs. e2e test)
- Code review standards (what reviewers check, what blocking vs. non-blocking looks like)
- Refactoring techniques and when to apply them
- API design conventions (REST, GraphQL, versioning, error shapes)
- Error handling philosophy (fail loud, no silent swallowing, structured errors)
- Logging and observability conventions (what to log, what not to log, log levels)
- Branching and commit conventions (branch naming, commit message format, PR size norms)
- Language or framework-specific conventions agreed by the team

## When to Consult

- Before implementing a pattern to confirm the agreed approach
- When reviewing code — to determine whether a practice is a convention violation or just a style difference
- When a design decision has multiple valid options — to check whether the team has already converged on one
- When onboarding to a codebase — to understand the expected norms before contributing
- When writing a spec or ADR — to confirm the proposed approach aligns with team conventions
- When a disagreement about approach arises — to check what the team has agreed rather than relitigating it

## Effective Queries

- "What is the team's convention for error handling in async functions?"
- "Do we prefer composition or inheritance for X type of problem?"
- "What does our test pyramid look like — how many unit vs. integration vs. e2e tests?"
- "What is the agreed commit message format?"
- "What are the code review criteria for a blocking vs. non-blocking comment?"

## What It Does NOT Contain

- Coding standards enforced by linters or type checkers — those are enforced automatically and don't need to be consulted manually
- Security policies — for that, use security-policies
- Architecture decisions for a specific system — for that, use architecture
- Active requirements — for that, use requirements

## Coding Standards

Non-negotiable rules that apply to every coding task, regardless of context.

### Clarity Over Cleverness

- Write code for the next reader, not the runtime.
- Prefer explicit over implicit. Prefer obvious over terse.
- Names should describe purpose, not implementation.

### Minimal Surface Area

- Add only what the task requires. No speculative features, no pre-emptive abstractions.
- A function that does one thing is easier to test, review, and replace.
- Three similar lines is better than a premature abstraction.

### Comments: Only the Why

- Code explains what. Comments explain why — the hidden constraint, the subtle invariant, the workaround for a specific external bug.
- Don't comment what the code already says. Don't leave TODO comments without a ticket or owner.

### Error Handling

- Only handle errors that can actually occur at the call site.
- Don't add fallbacks for impossible states. Trust internal invariants.
- Validate only at system boundaries: user input, external APIs, file I/O.

### Change Discipline

- Touch only what the task requires. Don't improve adjacent code in the same commit.
- Remove imports, variables, and functions that your changes make unused.
- Leave pre-existing dead code alone unless removal is explicitly requested.
- Every changed line should trace directly to the stated requirement.

## Adapter Notes

Provide access via file-system tool for team-specific convention documents stored in the repository (e.g. `CONTRIBUTING.md`, `docs/conventions/`, `docs/engineering-handbook/`).

For universal best practices not yet codified in team docs, web-search against canonical sources (Martin Fowler's refactoring catalogue, language-specific style guides, RFC documents) is appropriate. Prefer team-specific conventions over universal ones when they conflict.
