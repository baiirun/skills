# Testing Discipline Review Heuristics

## Unit Tests

- Use unit tests for pure logic, parsing, validation, invariant checks, and edge-case-heavy transformations.
- Keep unit tests focused on stable behavior, not private helper choreography.
- Prefer table-driven cases when many boundaries or variants must be covered.
- Assert both accepted and rejected inputs when validation matters.

## Integration Tests

- Prefer integration tests for behavior that depends on multiple modules, persistence, routing, serialization, permissions, or external boundary adapters.
- Use real implementations when practical and fake only slow or nondeterministic I/O.
- Verify observable behavior: outputs, persisted state, emitted events, and user-visible errors.

## End-to-End Tests

- Keep E2E tests limited to critical flows and high-value edge cases.
- Avoid duplicating every integration scenario at the E2E layer.
- Ensure E2E assertions verify outcomes, not incidental timing or styling unless the feature is visual.

## Mocks

- Mock coarse I/O boundaries such as network providers, payment gateways, clocks, queues, and filesystem access.
- Avoid mocking internal collaborators just to force call-order assertions.
- Prefer fakes or fixtures when they make behavior clearer than mocks.

## Regression Bugs

- First write or identify a test that fails for the reported bug.
- Fix the smallest behavior necessary to make the regression pass.
- Keep the regression focused on the user-visible failure or violated invariant.
