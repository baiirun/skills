---
name: testing-and-verifying
description: Choosing tests, writing assertions, fixing bugs, and proving work is done. Use when adding tests, fixing a bug, sequencing a multi-step change, or before declaring work complete.
---

# Testing and Verifying

Before writing the code, read each principle whose condition matches the work. They are short; read them in full rather than from memory of their titles.

| When the work involves | Read |
|---|---|
| Deciding which tests a change needs and at which level | `principles/test-what-you-would-reject.md` |
| Writing assertions, choosing mocks, or shaping code for testability | `principles/test-behavior.md` |
| Reproducing and fixing a bug | `principles/fix-root-causes.md` |
| A change with several steps, or stacking commits and PRs | `principles/sequence-verifiable-units.md` |
| Before declaring the work done | `principles/prove-it-works.md` |

Done when: every row whose condition matches the work has had its principle read in full, and the code follows it, including its test where it has one.
