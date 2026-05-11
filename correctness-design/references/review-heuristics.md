# Correctness Design Review Heuristics

## Boundary Parsing

- Convert untrusted or raw inputs into validated domain values at the system boundary.
- Boundaries include HTTP handlers, CLI args, env vars, config files, database rows, queue payloads, webhooks, files, and third-party API responses.
- Do not pass raw strings, dictionaries, JSON blobs, or nullable fields deep into code when the shape is knowable at the boundary.
- Prefer constructors, parsers, schemas, or value objects that return validated types.

## Illegal States

- Flag data models where combinations of optional fields encode mutually exclusive states.
- Prefer discriminated unions, tagged variants, enums with payloads, or explicit state objects where the language supports them.
- Avoid boolean combinations that allow nonsensical states.
- Make default states explicit when missing data has semantic meaning.

## Semantic Naming

- Flag names that do not encode the domain noun or verb precisely enough for a reader to know what the value is, what operation is happening, or what mental model applies.
- Do not overload one term with multiple context-dependent meanings; split names when two concepts can be confused in code, docs, logs, or team communication.
- Prefer names that expose semantic roles instead of repeating only the type: ownership, lifetime, allocation strategy, validity, source, target, authority, durability, retry state, or side-effect responsibility.
- Include units and qualifiers in names for values where a unit, bound, ordering, or coordinate system matters, such as `_ms`, `_bytes`, `_min`, `_max`, `_offset`, `_index`, `_count`, `_size`, `_limit`, `_start`, or `_end`.
- Order qualifiers from most significant to least significant so related names group together and scan consistently, such as `latency_ms_max` with `latency_ms_min`.
- Treat nearby primitive values with different semantics as distinct concepts even when the language cannot enforce it; `index`, `count`, `size`, `offset`, `length`, and `limit` should not be used interchangeably.
- Avoid abbreviations that hide meaning. Prefer full domain words except for conventional tiny scopes such as sort callbacks, matrix math, or project-standard acronyms.
- Prefer long, descriptive names for scripts, CLI flags, and other input-facing options when short forms would make intent or safety unclear.
- Follow the project's identifier and file naming conventions, including separator style, because consistent word boundaries make names easier to scan and compare.
- Preserve project capitalization and acronym conventions when they carry domain meaning; inconsistent acronyms create false distinctions.
- Choose related names that make symmetry visible at call sites and in calculations, such as `source`/`target` and `source_offset`/`target_offset` instead of mismatched short forms.
- Prefer noun names for durable domain concepts that must also appear in documentation, logs, metrics, derived identifiers, or conversation.
- Name helper functions or callbacks so their relationship to the parent operation is clear when that call history matters for correctness.
- Avoid unnecessary aliases or duplicate variables for the same state; extra names increase the chance that copied or cached state diverges.
- Use named options, value objects, or structured parameters when positional arguments can be swapped, especially for same-typed values or nullable arguments.
- Name nullable values so the meaning of `null` is clear at the call site, or replace the nullable value with an explicit variant when absence has domain meaning.
- Prefer positive names for invariants and states; negated names and double negatives make positive and negative spaces harder to verify.

## Invariants

- Keep invariant enforcement next to the state it protects.
- Avoid scattered validation checks that can diverge over time.
- Prefer functions whose parameters already satisfy required preconditions; push raw optional or invalid states to the boundary where they can be parsed, branched, asserted, or rejected once.
- Flag helpers that silently return or no-op when a precondition is missing if the caller could instead make the valid and invalid paths explicit.
- Challenge intermediate enum or variant states that merely duplicate a branch condition and are immediately matched later; model variants only when the state is durable or crosses a real boundary.
- Assert important postconditions after transformations and important preconditions before side effects.
- Include both boundary assertions and transition assertions for state-machine-like flows.

## Transformations

- Prefer total transformations where possible: every input state has a defined output or a structured error.
- Avoid partial mutation that can leave data in an invalid intermediate state after failure.
- Preserve identifiers and source context through transformation chains for error reporting and debugging.
