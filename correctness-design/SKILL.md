---
name: correctness-design
description: Review and improve correctness by parsing inputs at boundaries, making illegal states unrepresentable, naming domain concepts precisely, placing validation near data, preserving invariants, and using assertions around important state transitions. Use when an AI assistant works on domain models, input parsing, state machines, validation, data transformations, same-typed parameters, unit-sensitive values, or bug-prone logic.
---

# Correctness Design

Use this skill to make incorrect states hard to express and easy to detect. Prefer validated structures over repeated defensive checks.

## Quick Start

Review raw inputs at the first boundary they enter. Example: a webhook handler should parse and validate the payload once, then pass a typed event inward instead of passing raw JSON through multiple layers.

## Review Focus

1. Parse raw inputs at the boundary once, then pass structured values inward.
2. Model invalid combinations out of existence with types, constructors, or schemas.
3. Name domain concepts, units, ownership, lifecycle, and state transitions precisely enough that misuse is visible.
4. Keep invariants close to the data or state they protect.
5. Avoid shotgun parsing and repeated validation across call sites.
6. Use assertions for critical inputs, outputs, invariants, and state transitions.
7. Cover positive and negative spaces: valid cases, invalid cases, boundaries, and transitions.

## Heuristics

Read `references/review-heuristics.md` when reviewing input handling, data models, transformations, state machines, unit-sensitive values, same-typed parameters, domain terminology, or code that previously produced correctness bugs.

## Output Shape

Return findings ordered by severity. For each finding, name the specific heuristic that produced the finding, identify the invalid state, semantic naming, or invariant risk, cite the concrete evidence, show how it can occur, and propose the smallest change that makes the invariant local and enforceable.
