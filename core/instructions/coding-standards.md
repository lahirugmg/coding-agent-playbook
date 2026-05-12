# Coding Standards

Shared instruction loaded by agents that read, write, or review code.

## Clarity Over Cleverness

- Write code for the next reader, not the runtime.
- Prefer explicit over implicit. Prefer obvious over terse.
- Names should describe purpose, not implementation.

## Minimal Surface Area

- Add only what the task requires. No speculative features, no pre-emptive abstractions.
- A function that does one thing is easier to test, review, and replace.
- Three similar lines is better than a premature abstraction.

## Comments: Only the Why

- Code explains what. Comments explain why — the hidden constraint, the subtle invariant, the workaround for a specific external bug.
- Don't comment what the code already says. Don't leave TODO comments without a ticket or owner.

## Error Handling

- Only handle errors that can actually occur at the call site.
- Don't add fallbacks for impossible states. Trust internal invariants.
- Validate only at system boundaries: user input, external APIs, file I/O.

## Tests

- Every test must encode WHY the behaviour matters, not just WHAT it does.
- A test that can't fail when business logic changes is not a test.
- Test names should read as specifications: `returns_empty_list_when_no_results`, not `test_1`.
- Don't mock what you can use directly. Prefer integration tests over unit tests when the integration is the risk.

## Conventions

- Match the codebase's existing style unconditionally: naming, formatting, file organisation.
- If two patterns in the codebase contradict, pick the more recent or more tested one, document the choice, and flag the other for cleanup.
- Disagreement with a convention is a separate conversation — never fork conventions silently.

## Change Discipline

- Touch only what the task requires. Don't improve adjacent code in the same commit.
- Remove imports, variables, and functions that YOUR changes make unused.
- Leave pre-existing dead code alone unless removal is explicitly requested.
- Every changed line should trace directly to the stated requirement.
