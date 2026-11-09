---
name: testing-discipline
description: Choosing the few tests worth writing, at the cheapest level that catches the failure. Use when adding tests, fixing a bug, or deciding which tests a change needs.
---

# Testing Discipline

This skill decides how many tests and at which level. `principle-test-behavior` decides
what each test asserts.

Every test must be able to go **red** for a reason you'd care about: a broken
invariant, a mishandled edge case the design exists for, or a regressed bug. Fewer,
sharper tests beat coverage.

## Quick Start

For each behavior change, name the one test that would fail if the behavior broke, and
write that. Example: a fix for malformed imported data starts with a test feeding the
malformed input and asserting the safe failure. Then make it pass.

## Implementation Focus

1. Test what you'd reject an implementation over: core invariants, the edge cases the
   data model is built to handle, and boundaries where later computation would hide a bug.
2. Leave out tests that restate types or signatures, or that could only fail if the
   compiler had already caught it.
3. Choose the cheapest level that catches the failure: unit tests for pure logic and
   parsing, integration tests for behavior across real module or I/O boundaries, and
   end-to-end tests only for a few critical flows.
4. For a bug fix, write the regression test first and watch it go red.

When a property needs many tests to pin down, the structure or contract is unclear.
Call the Skill tool with `skeleton-first` and fix the structure instead of adding tests.

## Principles

- Writing any assertion, choosing mocks, or shaping code for testability: call the
  Skill tool with `principle-test-behavior`.
- A change spanning several steps that each need a check: call the Skill tool with
  `principle-sequence-verifiable-units`.
- Before declaring the work done: call the Skill tool with `principle-prove-it-works`.

## Heuristics

Read `references/implementation-heuristics.md` when choosing a test level or deciding
whether a change needs a test at all.

## Before You Finish

- Each new test goes red only for a reason you'd care about.
- Bug fixes include a test that failed before the fix.
