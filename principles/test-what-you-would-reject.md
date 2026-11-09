# Test What You Would Reject

> Apply when deciding which tests a change needs and at which level. Write only tests that go red for a reason you'd reject an implementation over, at the cheapest level that catches the failure.

Every test must be able to go **red** for a reason you'd care about: a broken invariant, a mishandled edge case the design exists for, or a regressed bug. Fewer, sharper tests beat coverage. This principle decides how many tests and at which level; [test-behavior](test-behavior.md) decides what each test asserts.

For each behavior change, name the one test that would fail if the behavior broke, and write that.

**Deciding whether to test:**
- Write a test when its failure would show a broken invariant, a mishandled edge case the design exists for, a violated contract at a component boundary, or a regressed bug.
- Leave out tests that restate a type, check that a constructor stores its fields, or could only fail if the compiler or type checker were already failing.
- When many cases share a shape, write one table-driven test instead of many copies.
- When a property needs many tests to pin down, the structure or contract is unclear. Fix the structure (the `skeleton-first` skill) instead of adding tests.

**Choosing the level:**
- Unit tests for pure logic, parsing, validation, invariant checks, and transformations with many edge cases. Assert both accepted and rejected inputs when validation matters.
- Integration tests for behavior that depends on several modules, persistence, routing, serialization, permissions, or boundary adapters. Use real implementations where practical; fake only slow or nondeterministic I/O.
- End-to-end tests for a few critical flows and high-value edge cases. Cover each scenario at one level; an end-to-end test that repeats an integration scenario adds runtime and no new signal.

**Bug fixes:** write the regression test first and watch it go red, then make the smallest change that makes it pass. Aim it at the user-visible failure or the violated invariant, not at the line that was wrong.

**The test:** For each new test, name the decision it guards. If you can't, delete it.
