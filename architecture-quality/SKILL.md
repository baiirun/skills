---
name: architecture-quality
description: Review and improve software architecture with emphasis on narrow interfaces, avoiding premature abstraction, preserving locality of behavior, reducing indirection, and using dependency inversion. Use when Codex is designing or reviewing abstractions, module boundaries, dependency injection, service interfaces, or refactors.
---

# Architecture Quality

Use this skill to keep code understandable, loosely coupled, and locally reasoned about. Prefer existing codebase patterns unless they directly conflict with the quality goal.

## Review Focus

1. Avoid premature abstraction. Let repeated usage and real variation justify new abstractions.
2. Keep interfaces narrow. Expose only the behavior the consumer needs.
3. Reduce indirection. Flatten designs that require unnecessary jumps to understand behavior.
4. Preserve locality of behavior. Keep behavior close to the unit where a maintainer looks for it.
5. Apply dependency inversion from the consumer's needs. Pass dependencies in and depend on small interfaces.
6. Separate data from behavior when it makes composition clearer without scattering invariants.

## Heuristics

Read `references/review-heuristics.md` when performing a detailed review, designing a new abstraction, or deciding whether to split or merge modules.

## Output Shape

Return findings ordered by severity. For each finding, identify the coupling or locality issue, explain the maintenance risk, and propose the smallest design change that restores clarity.
