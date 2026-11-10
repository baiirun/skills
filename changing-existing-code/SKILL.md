---
name: changing-existing-code
description: Refactors, migrations, and new requirements in existing designs. Use when refactoring, migrating callers, rewriting in phases, or adding a requirement the current design didn't anticipate.
---

# Changing Existing Code

Before writing the code, read each principle whose condition matches the work. They are short; read them in full rather than from memory of their titles.

| When the work involves | Read |
|---|---|
| Sequencing an addition, refactor, or rewrite | `principles/subtract-before-you-add.md` |
| Integrating a new requirement into an existing design | `principles/redesign-from-first-principles.md` |
| An `if` for one value, a one-caller parameter, a swallowed error, a sleep, or a disabled test | `principles/special-cases-are-requirements.md` |
| A change that lands in several places, or code that must change together but lives apart | `principles/group-by-reason-to-change.md` |
| Introducing a new internal API while old callers still exist | `principles/migrate-callers-then-delete-legacy-apis.md` |
| A planned rewrite or migration with phase boundaries | `principles/outcome-oriented-execution.md` |
| A growing diff, or the urge to add layers or thread a signal | `principles/laziness-protocol.md` |
| A sweep or run of similar edits | `principles/sequence-verifiable-units.md` |

When the target shape crosses a function boundary, call the Skill tool with `skeleton-first` to fix it as stubs before moving code. For a whole-codebase cleanup, tell the user to run `/untangle-codebase`.

Done when: every row whose condition matches the work has had its principle read in full, and the code follows it, including its test where it has one.
