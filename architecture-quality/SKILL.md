---
name: architecture-quality
description: Review and improve software architecture with emphasis on narrow interfaces, avoiding premature abstraction, preserving locality of behavior, centralizing control flow, reducing indirection, batch-oriented hot paths, and using dependency inversion. Use when an AI assistant is designing or reviewing abstractions, module boundaries, dependency injection, service interfaces, helper extraction, batching, or refactors.
---

# Architecture Quality

Use this skill to keep code understandable, loosely coupled, and locally reasoned about. Prefer existing codebase patterns unless they directly conflict with the quality goal.

## Quick Start

Review new abstractions by asking whether they reduce real complexity at the call site. Example: a new `UserServiceManager` with one implementation and broad methods should be challenged unless it hides volatile behavior or matches an established local pattern.

## Review Focus

1. Avoid premature abstraction. Let repeated usage and real variation justify new abstractions.
2. Keep interfaces narrow. Expose only the behavior the consumer needs.
3. Reduce indirection. Flatten designs that require unnecessary jumps to understand behavior, including pass-through wrappers that add no policy, type narrowing, lifecycle ownership, or meaningful context.
4. Preserve locality of behavior. Keep behavior close to the unit where a maintainer looks for it.
5. Centralize branching and precondition checks where they make control flow easier to verify.
6. Prefer batch-oriented interfaces when callers repeatedly apply the same operation over many items or a hot path.
7. Apply dependency inversion from the consumer's needs. Pass dependencies in and depend on small interfaces.
8. Separate data from behavior when it makes composition clearer without scattering invariants.

## Heuristics

Read `references/review-heuristics.md` when performing a detailed review, designing a new abstraction, or deciding whether to split or merge modules.

## Output Shape

Return findings ordered by severity. For each finding, name the specific heuristic that produced the finding, identify the coupling or locality issue, cite the concrete evidence, explain the maintenance risk, and propose the smallest design change that restores clarity.
