# Testing Discipline Implementation Heuristics

## Deciding Whether to Test

- Write a test when its failure would show a broken invariant, a mishandled edge case
  the design exists for, a violated contract at a component boundary, or a regressed bug.
- Don't write a test that restates a type, checks that a constructor stores its fields,
  or would only fail if the compiler or type checker were already failing.
- Don't write a test that pins the current implementation's private steps. It breaks on
  every refactor and catches nothing.
- When many cases share a shape, write one table-driven test instead of many copies.

## Unit Tests

- Use unit tests for pure logic, parsing, validation, invariant checks, and
  transformations with many edge cases.
- Assert both accepted and rejected inputs when validation matters.

## Integration Tests

- Use integration tests for behavior that depends on several modules, persistence,
  routing, serialization, permissions, or boundary adapters.
- Use real implementations where practical. Fake only slow or nondeterministic I/O.
- Assert observable behavior: outputs, persisted state, emitted events, user-visible errors.

## End-to-End Tests

- Reserve end-to-end tests for a few critical flows and high-value edge cases.
- Don't repeat integration scenarios at the end-to-end level.
- Assert outcomes, not timing or styling, unless the feature is visual.

## Mocks

- Mock coarse I/O boundaries: network providers, payment gateways, clocks, queues,
  filesystem access.
- Don't mock internal collaborators just to assert call order.
- Use fakes or fixtures when they make the behavior clearer than a mock would.

## Regression Bugs

- First write a test that fails for the reported bug.
- Make the smallest change that makes it pass.
- Aim the test at the user-visible failure or the violated invariant, not at the
  line that was wrong.
