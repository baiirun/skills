# Feature Contract Docs Review Heuristics

## Contract Quality

- Purpose should explain why the feature exists, not just what files or screens changed.
- Scope should include non-goals when a future agent might otherwise extend the feature incorrectly.
- Behavior contract statements should be testable and normative. Prefer "MUST", "SHOULD", and "MUST NOT" over vague prose.
- Invariants should describe relationships that must stay true across refactors, not transient implementation steps.

## Implementation Model

- Explain why responsibilities live where they do, especially source-of-truth boundaries, ownership, derivation, caching, retries, authorization, and persistence.
- Name stable semantic boundaries such as APIs, events, persisted entities, configs, and external systems.
- Avoid file-by-file tours unless the file name is itself the stable interface.
- Capture tradeoffs only when they explain current constraints or prevent future accidental rewrites.

## Documentation Placement

- Use feature contracts for durable capability behavior and invariants.
- Use ADRs for high-leverage decisions whose alternatives and consequences matter beyond one feature.
- Use inline comments only for local why that cannot be expressed clearly in code or the feature contract.
- Use tracked work for deferred tasks; do not leave source reminders as documentation.

## Verification

- Verification should prove the contract, including positive flows, forbidden behavior, important boundaries, and failure states.
- Prefer checks that a future human or agent can execute after changing the implementation.
- If behavior depends on external systems, document what must be mocked, simulated, or observed.
