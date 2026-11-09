# Correctness Design Implementation Heuristics

## Boundary Parsing

- Convert untrusted or raw input into validated domain values where it enters the system.
- Boundaries include HTTP handlers, CLI args, env vars, config files, database rows,
  queue payloads, webhooks, files, user input, and third-party API responses.
- When the shape is knowable at the boundary, don't pass raw strings, dictionaries,
  JSON blobs, or nullable fields deeper.
- Use constructors, parsers, schemas, or value objects that return validated types.

## Illegal States

- Replace optional fields that encode mutually exclusive states with one tagged value.
- Use discriminated unions, enums with payloads, or explicit state objects where the
  language supports them.
- Replace boolean combinations that allow nonsensical states with a single state value.
- Make default states explicit when missing data means something.

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
- Write full domain words instead of abbreviations, except in conventional tiny scopes
  such as sort callbacks or matrix math.
- Don't create aliases or duplicate variables for the same state; copies drift.
- Use named options, value objects, or structured parameters when positional arguments
  of the same type could be swapped.
- Name nullable values so the meaning of `null` is clear at the call site, or replace
  them with an explicit variant when absence means something.
- Name invariants and states positively. Negated names and double negatives hide which
  space you're in.

## Invariants

- Enforce each invariant next to the state it protects, once.
- Write functions whose parameters already satisfy their preconditions. Handle raw,
  optional, or invalid states at the boundary, where they can be parsed, branched on,
  asserted, or rejected once.
- Assert important postconditions after transformations and important preconditions
  before side effects.
- For state-machine-like flows, assert both at the boundaries and at each transition.

## Transformations

- Write total transformations: every input state yields a defined output or a
  structured error.
- Don't mutate in place in a way that leaves data invalid if a later step fails. Build
  the new value, then swap.
- Carry identifiers and source context through transformation chains so errors can say
  what failed and where.
