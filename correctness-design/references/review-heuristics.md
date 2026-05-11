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

## Invariants

- Keep invariant enforcement next to the state it protects.
- Avoid scattered validation checks that can diverge over time.
- Assert important postconditions after transformations and important preconditions before side effects.
- Include both boundary assertions and transition assertions for state-machine-like flows.

## Transformations

- Prefer total transformations where possible: every input state has a defined output or a structured error.
- Avoid partial mutation that can leave data in an invalid intermediate state after failure.
- Preserve identifiers and source context through transformation chains for error reporting and debugging.
