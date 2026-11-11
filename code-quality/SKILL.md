---
name: code-quality
description: Route implementation work to the code-quality skills and principles that cover it.
disable-model-invocation: true
---

# Code Quality

Find each row whose condition matches the work and load what it names. Load only the matching rows; a one-function fix might match one row, a new feature several. When several match, the order does not matter.

## Skills

Each routing skill maps its own conditions to principle files. Call the Skill tool with the skill named in each matching row.

| When the work involves | Call |
|---|---|
| A new feature or module, more than a few new functions, or work handed to subagents | `skeleton-first` |
| Types, signatures, parsing raw input, naming, runtime checks, or converting data | `modeling-data` |
| Modules, interfaces, abstractions, splitting functions, or a refactor's target shape | `designing-structure` |
| External calls, code that can fail, retries, fallbacks, request handlers, or jobs | `handling-failure` |
| Several actors writing the same state, or work that must survive crashes and reruns | `sharing-state` |
| Refactors, migrations, phased rewrites, or a requirement the design didn't anticipate | `changing-existing-code` |
| Choosing tests, fixing a bug, sequencing a multi-step change, or proving work is done | `testing-and-verifying` |
| Writing or editing source comments, or an instruction repeated a second time | `documenting-code` |
| An explicit cleanup pass over comments and suppressions in a diff | `no-comments` |
| Reading or editing TypeScript | `typescript-best-practices` |

## Principles

When one rule is all the work needs, read the principle directly instead of loading a whole skill. Each file is short; read it in full.

| When the work involves | Read |
|---|---|
| Deciding where runtime checks and assertions go | `principles/assert-at-boundaries.md` |
| Wiring validation, error handling, or framework adapters | `principles/boundary-discipline.md` |
| Code that can fail: external calls, I/O, parsing, jobs, handlers | `principles/classify-failures.md` |
| Source comments, workaround notes, or commented-out code | `principles/comment-the-why.md` |
| Adding or changing an interface, extracting a helper, or supplying a dependency | `principles/consumer-shaped-interfaces.md` |
| Adding an import, deciding which side owns a type, or auditing a dependency graph | `principles/depend-on-what-changes-less.md` |
| Writing the same instruction a second time, or a recurring correction | `principles/encode-lessons-in-structure.md` |
| A novel interaction or architectural decision with no precedent | `principles/exhaust-the-design-space.md` |
| Debugging | `principles/fix-root-causes.md` |
| Choosing core types and data structures before writing logic | `principles/foundational-thinking.md` |
| Deciding what shares a module, file, or folder, or a change that lands in several places | `principles/group-by-reason-to-change.md` |
| A growing diff, or the urge to add layers, abstractions, or signal threading | `principles/laziness-protocol.md` |
| Commands, lifecycle steps, or loops that run amid crashes, restarts, and retries | `principles/make-operations-idempotent.md` |
| A new internal API while old callers still exist | `principles/migrate-callers-then-delete-legacy-apis.md` |
| Code that is hard to trace: layers, wrappers, hidden state | `principles/minimize-reader-load.md` |
| Stateful logic, heavy branching, or a shape assumption repeated across files | `principles/model-the-domain.md` |
| Naming domain concepts, units, same-typed parameters, or nullable values | `principles/name-precisely.md` |
| Request handlers, jobs, workers, or calls across services | `principles/observable-boundaries.md` |
| A planned rewrite or migration with explicit phases | `principles/outcome-oriented-execution.md` |
| Finishing a task, before declaring it done | `principles/prove-it-works.md` |
| Placing branches, splitting functions, or an operation over many items | `principles/push-ifs-up-fors-down.md` |
| Wiring callbacks, handlers, hooks, or middleware, or when order depends on registration | `principles/centralize-control-flow.md` |
| Integrating a new requirement into an existing design | `principles/redesign-from-first-principles.md` |
| Adding a retry, a fallback, or default behavior on failure | `principles/safe-retries-and-fallbacks.md` |
| Concurrent actors that might write the same file, branch, key, or state | `principles/separate-before-serializing-shared-state.md` |
| Business decisions mixed with mutable state, I/O, caching, or scheduling | `principles/separate-logic-state-and-effects.md` |
| Multi-step work, or stacking commits and PRs | `principles/sequence-verifiable-units.md` |
| An `if` for one value, a one-caller parameter, a swallowed error, a sleep, or a disabled test | `principles/special-cases-are-requirements.md` |
| Sequencing an addition, refactor, or rewrite | `principles/subtract-before-you-add.md` |
| Designing for testability, or writing and reviewing tests | `principles/test-behavior.md` |
| Deciding which tests a change needs and at which level | `principles/test-what-you-would-reject.md` |
| Converting, migrating, or updating data | `principles/total-transformations.md` |
| Designing types or function signatures | `principles/type-system-discipline.md` |
