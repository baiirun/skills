---
name: code-quality
description: Walk a feature build through data model, structure, failures, tests, comments, and docs.
disable-model-invocation: true
---

# Code Quality

Run every step in this same context. The decisions in one step constrain the next.

## Quick Start

Walk the steps below and run only those the change touches. Example: adding a file
importer to a desktop app touches the data model and boundaries (step 2), module shape
(step 3), and a few tests for malformed input (step 6). Step 4's service logging and
tracing guidance doesn't apply.

## Implementation Order

1. **Design the structure.** For a new feature, module, or more than a few functions,
   call the Skill tool with `skeleton-first`.
   Done when: the user has approved the skeleton.
2. **Model the data.** Call the Skill tool with `modeling-data`.
   Done when:
   - every place raw input enters has one function that parses it into a typed value, and
   - every state the feature can be in is one variant of one type.
3. **Shape the modules.** Call the Skill tool with `designing-structure`.
   Done when:
   - every new public function is already called by real code in this change
     (nothing exposed for later), and
   - each decision about the feature's state is made in one place, with helpers
     receiving the result instead of re-checking it.
4. **Decide failure semantics.** When the code calls external systems, runs as a
   service or job, retries, or falls back, call the Skill tool with
   `handling-failure`. When several actors write shared state or work must survive
   reruns, also call the Skill tool with `sharing-state`.
   Done when: every expected failure has a class (retryable or not, recoverable or not)
   and a chosen response, before the happy path is written.
5. **Write the code**, keeping the decisions above. When one turns out wrong, change it
   on purpose and return to the step that made it.
   Done when: it builds, the changed feature path has been run (see
   `principles/prove-it-works.md`), and each decision from steps 1–4 is still visible in
   the code or was changed on purpose.
6. **Add the tests that matter.** Call the Skill tool with `testing-and-verifying`.
   Done when:
   - each invariant from step 2 has a test that fails if the invariant breaks,
   - every other test guards a bug fix or an edge case the design exists for, and
   - all tests pass.
7. **Comment the non-obvious why.** Once the code is stable, call the Skill tool with
   `documenting-code`.
   Done when: every comment added states a reason the code itself can't show.
8. **Record the contract.** When the change adds or alters durable feature behavior,
   call the Skill tool with `feature-contract-docs`.
   Done when: every behavior this change added or altered appears in the contract.

A one-function fix usually needs only steps 5 and 6.
