# Test behavior

> Apply when designing code for testability or writing and reviewing tests. Create stable behavior boundaries, derive expectations independently, and reject tautological tests and change detectors that only restate the implementation.

A useful test fails when promised behavior breaks and survives when the implementation changes without changing that behavior. Design the code and the test around that standard.

## Make behavior testable

- Separate decisions from effects when the split clarifies the code. Keep domain logic callable without a database, network, clock, random source, or process-wide state.
- Pass nondeterministic or external dependencies through a stable boundary. Tests should be able to supply a clock, identifier source, or coarse I/O fake without replacing internal collaborators one by one.
- Treat hidden mutable state as an implicit test input. A test from one clean starting state proves nothing about another state; remove the hidden state, pass it explicitly, or cover the meaningful transitions.
- Make results observable through the same contract callers use: return values, persisted state, emitted events, protocol messages, or user-visible output.
- Do not expose private methods, add production branches, or split cohesive code into mockable fragments solely for tests. Hard-to-test code often reveals hidden dependencies or mixed responsibilities, but more seams are not automatically better.

## Write tests with an independent reason to pass

- Derive expected results from the requirement, public contract, worked example, or invariant. Do not calculate the expected value with the production algorithm or copy its decision table into the test.
- Assert outcomes at the narrowest stable boundary that proves the behavior. Assert internal calls or ordering only when that interaction is itself part of the contract.
- Use mocks at coarse I/O boundaries. A test where every collaborator is mocked and every assertion repeats the configured responses proves little about whether the pieces work together.
- Keep each test sensitive to a plausible defect. Before keeping it, introduce or imagine a small wrong implementation and identify which assertion would fail.

## Reject false confidence

A **tautological test** restates its setup or the implementation. It passes because the test supplied or recomputed the answer.

A **change-detector test** encodes the current code shape, call sequence, generated output, or broad snapshot without establishing why that exact form is correct. It fails on harmless refactors and can pass when the behavior is wrong. Delete it or rewrite it around an observable contract. Exact snapshots and call-order assertions are valid only when the exact representation or ordering is promised behavior.

Alex Eagle's [Change-Detector Tests Considered Harmful](https://testing.googleblog.com/2015/01/testing-on-toilet-change-detector-tests.html) gives the diagnostic: a test transformed from the same information as the production code behaves like a checksum, not independent evidence.

## The test

Ask both questions:

1. If I replaced the implementation with a reasonable refactor that preserved behavior, would this test still pass unchanged?
2. If I introduced a plausible bug while preserving the current structure, would this test fail?

If either answer is no, move the boundary or rewrite the assertion.
