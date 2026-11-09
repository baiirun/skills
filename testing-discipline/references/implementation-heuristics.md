# Testing Discipline Implementation Heuristics

What a test asserts, how it uses mocks, and how it avoids tautological or
change-detector tests live in `principle-test-behavior`. This file covers how many
tests to write and at which level.

## Deciding Whether to Test

- Write a test when its failure would show a broken invariant, a mishandled edge case
  the design exists for, a violated contract at a component boundary, or a regressed bug.
- Leave out tests that restate a type, check that a constructor stores its fields, or
  could only fail if the compiler or type checker were already failing.
- When many cases share a shape, write one table-driven test instead of many copies.

## Unit Tests

- Use unit tests for pure logic, parsing, validation, invariant checks, and
  transformations with many edge cases.
- Assert both accepted and rejected inputs when validation matters.

## Integration Tests

- Use integration tests for behavior that depends on several modules, persistence,
  routing, serialization, permissions, or boundary adapters.
- Use real implementations where practical. Fake only slow or nondeterministic I/O.

## End-to-End Tests

- Reserve end-to-end tests for a few critical flows and high-value edge cases.
- Cover each scenario at one level. An end-to-end test that repeats an integration
  scenario adds runtime and no new signal.

## Regression Bugs

- First write a test that fails for the reported bug.
- Make the smallest change that makes it pass.
- Aim the test at the user-visible failure or the violated invariant, not at the
  line that was wrong.
