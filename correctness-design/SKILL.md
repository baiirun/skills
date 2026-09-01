---
name: correctness-design
description: Review and improve domain states, input parsing, semantic naming, validation, invariants, and transformations. Use for domain models, state machines, unit-sensitive values, same-typed parameters, data transformations, or bug-prone logic.
---

# Correctness Design

Review whether the design makes invalid behavior difficult to express and easy to detect.

## Principles to load

- `principle-model-the-domain` for domain concepts, states, transitions, and terminology.
- `principle-type-system-discipline` for validated types and illegal-state prevention.
- `principle-boundary-discipline` for parsing raw input once at the boundary.

The principles supply the shared modeling rules. This skill owns the correctness review: tracing invalid states through real flows, checking semantic naming and units, examining transformations, and judging whether positive and negative cases are covered.

## Review focus

1. Find the first trusted boundary for each raw input and verify that parsing and validation happen there.
2. Trace invalid combinations, ambiguous absence, and partial states through constructors and transitions.
3. Check that names encode domain role, units, ownership, lifecycle, and source or target when those distinctions affect behavior.
4. Keep invariant enforcement next to the state it protects.
5. Check transformations for total handling, preserved identity and context, and safe failure without partial mutation.
6. Cover valid cases, rejected cases, boundaries, and state transitions.

Read `references/review-heuristics.md` for detailed naming and transformation checks.

## Output

Order findings by severity. For each finding, name the specialist heuristic or loaded principle, cite the evidence, show how the invalid state or ambiguity can occur, and propose the smallest change that makes the rule local and enforceable.
