---
name: code-quality
description: Coordinate code quality review and implementation guidance across architecture, errors and observability, correctness, and testing. Use when an AI assistant needs to evaluate or improve code design quality, run a broad code-quality pass, or orchestrate specialist reviewers with $architecture-quality, $errors-observability, $correctness-design, and $testing-discipline.
---

# Code Quality

Use this skill as the coordinator for code-quality work. Keep this skill lightweight: route to the specialist skills instead of duplicating their guidance.

## Quick Start

For a broad review, inspect the changed code and route findings through the relevant specialist dimensions. Example: "Review this diff for code quality" should check whether architecture, errors and observability, correctness, or testing concerns apply, then return a deduplicated findings list.

## Specialist Skills

- Use `$architecture-quality` for abstractions, interfaces, dependency direction, indirection, and locality of behavior.
- Use `$errors-observability` for error classification, retries, fallbacks, logging, tracing, and operational debuggability.
- Use `$correctness-design` for boundary parsing, invariants, illegal states, validation placement, and assertions.
- Use `$testing-discipline` for test strategy, regression tests, integration coverage, end-to-end boundaries, and mocking discipline.

## Workflow

1. Determine which quality dimensions apply to the task or diff.
2. Load only the specialist skill bodies needed for those dimensions.
3. If delegation is available and the user asks for specialized or parallel review, run one focused reviewer per relevant dimension.
4. Ask each specialist to return prioritized findings with concrete file and line references when reviewing code.
5. Deduplicate findings across specialists, keep the highest severity, and convert them into a concise action list.
6. When implementing fixes, keep edits scoped to the quality issue and preserve existing codebase patterns.

## Specialist Reviewer Prompts

Use these prompts when delegation is allowed and useful:

```text
Use $architecture-quality to review this diff for abstraction boundaries, interface shape, dependency direction, and locality of behavior. Return only actionable findings with file/line references and severity.
```

```text
Use $errors-observability to review this diff for error classification, retry behavior, fallback semantics, structured logging, tracing, and debuggability. Return only actionable findings with file/line references and severity.
```

```text
Use $correctness-design to review this diff for boundary parsing, invalid states, validation placement, invariants, assertions, and state transitions. Return only actionable findings with file/line references and severity.
```

```text
Use $testing-discipline to review this diff for missing regression coverage, unit/integration balance, end-to-end scope, and inappropriate mocks. Return only actionable findings with file/line references and severity.
```

## Output Shape

Lead with findings. For each finding, include the affected file and line, severity, why it matters, and the smallest practical fix. If there are no findings, state that clearly and call out residual risk or test gaps.
