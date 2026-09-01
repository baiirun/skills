---
name: testing-discipline
description: Review and improve test strategy across focused unit tests, integration coverage, high-value end-to-end flows, coarse I/O mocks, and regression-first bug fixes. Use when adding or reviewing tests, fixing bugs, or judging whether a behavior change is covered.
---

# Testing Discipline

Choose the smallest test level that proves the behavior through the boundary most likely to fail.

## Principles to load

- `principle-prove-it-works` for evidence that the requested behavior holds.
- `principle-sequence-verifiable-units` when implementation order or intermediate verification affects the test plan.

The principles define the need for proof. This skill owns test placement: deciding between unit, integration, and end-to-end coverage; choosing useful fakes or mocks; and keeping assertions stable across refactors.

## Review focus

1. Use focused unit tests for pure logic, parsing, validation, invariants, and edge-heavy transformations.
2. Prefer integration tests for behavior that crosses real module, persistence, routing, serialization, or permission boundaries.
3. Reserve end-to-end tests for critical flows and a small set of valuable edge cases.
4. Mock only coarse, slow, nondeterministic I/O boundaries. Avoid tests coupled to internal call order.
5. Reproduce a bug with a regression test before changing the behavior when practical.
6. Name and assert observable behavior rather than private implementation choreography.

Read `references/review-heuristics.md` when choosing test level or reviewing mocks and regression coverage.

## Output

Order findings by severity. For each finding, name the specialist heuristic or loaded principle, cite the evidence, explain the uncovered behavior or brittleness, and propose the smallest useful test or test refactor.
