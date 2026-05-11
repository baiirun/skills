---
name: testing-discipline
description: Review and improve test strategy with focused unit tests, integration coverage, small high-value end-to-end suites, coarse I/O mocks, and regression-first bug fixes. Use when Codex adds or reviews tests, fixes bugs, changes behavior, or evaluates whether implementation risk is covered.
---

# Testing Discipline

Use this skill to match test coverage to implementation risk. Tests should protect behavior and invariants without making refactors brittle.

## Review Focus

1. Write focused unit tests for important logic and invariants.
2. Prefer integration tests as the default safety net for behavior across real boundaries.
3. Keep end-to-end coverage small, curated, and reserved for critical paths and high-value edge cases.
4. Avoid mocks unless necessary; when needed, mock only coarse I/O boundaries.
5. Reproduce bugs with regression tests before fixing them.
6. Verify test names and assertions describe stable behavior rather than implementation details.

## Heuristics

Read `references/review-heuristics.md` when choosing test level, reviewing mocks, fixing bugs, or deciding whether coverage is sufficient for a behavior change.

## Output Shape

Return findings ordered by severity. For each finding, identify the untested behavior or brittle test design, explain the risk, and propose the smallest useful test or test refactor.
