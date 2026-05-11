# Code Quality Skills

This repository contains focused Codex skills for reviewing and improving code quality. Use `code-quality` as the coordinator when the task spans multiple dimensions; use a specialist skill directly when the concern is narrow.

## Coordinator

- [`code-quality`](code-quality/SKILL.md): Routes broad code-quality work to the relevant specialist skills and deduplicates findings.

## Specialist Skills

- [`architecture-quality`](architecture-quality/SKILL.md): Reviews abstractions, interfaces, dependency direction, indirection, and locality of behavior.
- [`correctness-design`](correctness-design/SKILL.md): Reviews boundary parsing, illegal states, validation placement, invariants, assertions, and state transitions.
- [`errors-observability`](errors-observability/SKILL.md): Reviews error classification, retries, fallbacks, structured logging, tracing, and operational debuggability.
- [`feature-contract-docs`](feature-contract-docs/SKILL.md): Writes and reviews durable feature contracts that model purpose, scope, behavior, invariants, interfaces, implementation model, and verification.
- [`implementation-comments`](implementation-comments/SKILL.md): Reviews local source comments for useful WHY, invariants, spec requirements, tradeoffs, constraints, and stale or misleading commentary.
- [`testing-discipline`](testing-discipline/SKILL.md): Reviews test strategy, regression coverage, integration boundaries, end-to-end scope, and mocking discipline.

## References

Several skills include deeper heuristics under their `references/` directories. Load those only when the specialist skill says they are relevant to the review or implementation task.
