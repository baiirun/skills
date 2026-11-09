---
name: modeling-data
description: Types, input parsing, naming, runtime checks, and data transformations. Use when designing types or signatures, parsing raw input, naming values, or writing state machines and code that converts or migrates data.
---

# Modeling Data

Before writing the code, read each principle whose condition matches the work. They are short; read them in full rather than from memory of their titles.

| When the work involves | Read |
|---|---|
| Designing types or function signatures | `principles/type-system-discipline.md` |
| Domain states, transitions, or logic branching on scattered booleans | `principles/model-the-domain.md` |
| Raw input entering the system, or deciding where validation goes | `principles/boundary-discipline.md` |
| Naming domain concepts, units, same-typed parameters, or nullable values | `principles/name-precisely.md` |
| Deciding where runtime checks and assertions go | `principles/assert-at-boundaries.md` |
| Converting, migrating, or updating data | `principles/total-transformations.md` |
| Deciding which values are stored and which are derived | `principles/separate-logic-state-and-effects.md` |

Done when: every row whose condition matches the work has had its principle read in full, and the code follows it, including its test where it has one.
