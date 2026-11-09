# Feature Contract Docs Writing Heuristics

## Contract Quality

- Write the purpose as why the feature exists, not which files or screens changed.
- Add non-goals wherever a future agent might otherwise extend the feature the wrong way.
- Write behavior statements that are testable and normative: "MUST", "SHOULD",
  "MUST NOT", not vague prose.
- Write invariants as relationships that must stay true across refactors, not as
  transient implementation steps.

## Implementation Model

- Explain why responsibilities live where they do, especially source-of-truth
  boundaries, ownership, derivation, caching, retries, authorization, and persistence.
- Name stable semantic boundaries: APIs, events, persisted entities, configs,
  external systems.
- Skip file-by-file tours unless the file name is itself the stable interface.
- Record a tradeoff only when it explains a current constraint or prevents an
  accidental rewrite.

## Documentation Placement

- Use a feature contract for durable capability behavior and invariants.
- Use an ADR for a high-leverage decision whose alternatives and consequences matter
  beyond one feature.
- Use an inline comment only for local why that the code and the contract can't carry.
- Use tracked work for deferred tasks, not source reminders.

## Verification

- Write verification that proves the contract: positive flows, forbidden behavior,
  important boundaries, failure states.
- Prefer checks a future human or agent can run after changing the implementation.
- When behavior depends on external systems, say what must be mocked, simulated,
  or observed.
