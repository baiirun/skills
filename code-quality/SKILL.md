---
name: code-quality
description: Coordinate a read-only review across architecture, correctness, errors and observability, testing, implementation comments, and feature contract documentation. Use for broad code-quality reviews. This skill reports findings and does not edit code.
---

# Code Quality

Coordinate the specialist review skills. Do not duplicate their policy here.

## Contract

- Review only. Do not edit files, format code, stage changes, commit, or implement fixes.
- Select only the specialists relevant to the changed behavior.
- Use independent reviewers concurrently when the harness supports them. Otherwise run the same specialist passes sequentially.
- If a relevant specialist cannot be loaded, name the missing coverage instead of silently replacing it with a generic review.

## Specialists

- `architecture-quality`: interfaces, dependency direction, indirection, locality, control flow, and batching.
- `correctness-design`: domain states, parsing, validation, invariants, naming, and transformations.
- `errors-observability`: error classification, retries, fallbacks, logs, traces, and operational diagnosis.
- `testing-discipline`: test level, regression coverage, mocks, and behavior-focused assertions.
- `implementation-comments`: missing, stale, redundant, or misleading source comments.
- `feature-contract-docs`: missing or stale durable feature contracts. Select this only when the change introduces or alters a feature-level contract that future maintainers need.

## Workflow

1. Inspect the requested scope and identify the changed behaviors and boundaries.
2. Select the relevant specialist skills. Load and apply each selected skill in full.
3. Ask each specialist for actionable findings with file and line evidence, severity, the rule that was violated, and the smallest practical fix.
4. Merge findings only when they describe the same affected behavior. Preserve every contributing specialist and rule.
5. Return findings only. A later implementation request may apply the fixes.

## Output

Lead with findings ordered by severity. Each finding must include:

- affected file and line;
- severity;
- contributing specialist and rule;
- concrete evidence and consequence;
- smallest practical fix.

If there are no findings, say so and name any review coverage or verification gaps.
