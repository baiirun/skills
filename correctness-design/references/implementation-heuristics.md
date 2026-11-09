# Correctness Design Implementation Heuristics

Boundary parsing, illegal states, total functions, branded primitives, and derived
state live in the principle skills named in `SKILL.md`. This file holds what those
principles don't cover.

## Semantic Naming

- Name values and operations with the precise domain noun or verb, so a reader knows
  what the value is and which mental model applies.
- Give each term one meaning. When two concepts could be confused in code, docs, logs,
  or conversation, give them different names.
- Name the semantic role, not just the type: ownership, lifetime, validity, source,
  target, authority, durability, or side-effect responsibility.
- Put units and qualifiers in names wherever a unit, bound, or coordinate system
  matters: `_ms`, `_bytes`, `_offset`, `_index`, `_count`, `_size`, `_limit`,
  `_start`, `_end`. Order qualifiers most significant first so related names group:
  `latency_ms_max`, `latency_ms_min`.
- Treat `index`, `count`, `size`, `offset`, `length`, and `limit` as distinct concepts
  even when they share a primitive type.
- Choose related names that show symmetry at call sites: `source`/`target`,
  `source_offset`/`target_offset`.
- Write full domain words, keeping abbreviations to conventional tiny scopes such as
  sort callbacks or matrix math.
- Keep one name per piece of state. Aliases and duplicate variables drift apart.
- Use named options, value objects, or structured parameters when positional arguments
  of the same type could be swapped.
- Name nullable values so the meaning of `null` is clear at the call site, or replace
  them with an explicit variant when absence means something.
- Name invariants and states positively, so it's clear which case you're in.

## Assertions at Boundaries

- Assert where the type system stops: raw input entering, values read back from
  storage or other processes, and cross-component invariants a type can't express.
- Assert preconditions before side effects, and postconditions after transformations
  whose output leaves the component.
- For state-machine-like flows, assert at entry and at each transition that crosses a
  component boundary.
- When an assertion guards a value inside the system, move the check into the type
  instead.

## Transformations

- Write total transformations: every input state yields a defined output or a
  structured error.
- Build the new value, then swap, so a failure partway through leaves the old data valid.
- Carry identifiers and source context through transformation chains so errors can say
  what failed and where.
