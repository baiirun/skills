---
name: code-quality
description: Coordinate read-only code-quality reviews across architecture, errors and observability, correctness, testing, implementation comments, and feature contract docs. Use when an AI assistant needs to review code quality, run a broad code-quality pass, or orchestrate specialist subagent reviewers with architecture-quality, errors-observability, correctness-design, testing-discipline, implementation-comments, and feature-contract-docs. This skill must not edit files or implement fixes.
---

# Code Quality

Use this skill as the coordinator for read-only code-quality review work. Keep this skill lightweight: route to the specialist skills in dedicated subagents instead of duplicating their guidance.

## Review Contract

- This is a code review skill, not an implementation or fix skill.
- Do not edit files, run formatters that write files, stage changes, commit, or implement fixes.
- Treat invocation of `code-quality` as an explicit request to run specialist review subagents.
- A `code-quality` review is not complete unless each selected specialist subagent confirms it loaded and applied its assigned specialist skill.
- Do not substitute a generic code review for the specialist heuristics. Findings must come from the relevant specialist dimensions below.
- If specialist subagents cannot be spawned or a specialist skill cannot be loaded, stop and report that `code-quality` could not be completed instead of silently continuing as a normal code review.

## Quick Start

For a broad review, inspect the changed code, choose the relevant specialist dimensions, and run each selected specialist skill as a focused read-only subagent. Example: "Review this diff for code quality" should check whether architecture, errors and observability, correctness, testing, implementation comment, or feature contract documentation concerns apply, run the relevant specialist subagents, then return a deduplicated findings list. Do not make code changes.

## Specialist Skills

- Use `architecture-quality` for abstractions, interfaces, dependency direction, indirection, control-flow locality, batching, and locality of behavior.
- Use `errors-observability` for error classification, retries, fallbacks, logging, tracing, and operational debuggability.
- Use `correctness-design` for boundary parsing, invariants, illegal states, semantic naming, validation placement, preconditions, and assertions.
- Use `testing-discipline` for test strategy, regression tests, integration coverage, end-to-end boundaries, and mocking discipline.
- Use `implementation-comments` for local source comments that explain non-obvious why, invariants, spec requirements, tradeoffs, failure semantics, constraints, deferred-work notes, and commented-out code.
- Use `feature-contract-docs` for durable feature documentation that models purpose, scope, behavior contracts, invariants, interfaces, implementation model, tradeoffs, and verification.

## Workflow

1. Determine which quality dimensions apply to the task or diff.
2. Run one focused read-only subagent per relevant specialist skill. Subagents must load and apply their assigned specialist skill themselves.
3. Ask each specialist subagent to confirm the specialist skill it used, then return prioritized findings with concrete file and line references.
4. If subagents are unavailable, stop and report that `code-quality` could not be completed.
5. Deduplicate findings across specialists, keep the highest severity, and convert them into a concise action list.
6. Return review findings only. Do not implement fixes unless the user separately asks for a follow-up implementation pass.

## Specialist Subagent Prompts

Use these prompts when spawning the specialist subagents:

```text
You are a read-only specialist code reviewer. Do not edit files, run write commands, stage changes, commit, or implement fixes. Load and use the architecture-quality skill to review this diff for abstraction boundaries, interface shape, dependency direction, control-flow locality, batching opportunities, and locality of behavior. Confirm that you used architecture-quality. Return only actionable findings with file/line references and severity.
```

```text
You are a read-only specialist code reviewer. Do not edit files, run write commands, stage changes, commit, or implement fixes. Load and use the errors-observability skill to review this diff for error classification, retry behavior, fallback semantics, structured logging, tracing, and debuggability. Confirm that you used errors-observability. Return only actionable findings with file/line references and severity.
```

```text
You are a read-only specialist code reviewer. Do not edit files, run write commands, stage changes, commit, or implement fixes. Load and use the correctness-design skill to review this diff for boundary parsing, invalid states, semantic naming, validation placement, preconditions, invariants, assertions, and state transitions. Confirm that you used correctness-design. Return only actionable findings with file/line references and severity.
```

```text
You are a read-only specialist code reviewer. Do not edit files, run write commands, stage changes, commit, or implement fixes. Load and use the testing-discipline skill to review this diff for missing regression coverage, unit/integration balance, end-to-end scope, and inappropriate mocks. Confirm that you used testing-discipline. Return only actionable findings with file/line references and severity.
```

```text
You are a read-only specialist code reviewer. Do not edit files, run write commands, stage changes, commit, or implement fixes. Load and use the implementation-comments skill to review this diff for redundant, stale, missing, or misleading implementation comments; deferred-work notes that should be tracked outside source; commented-out code; and places where clearer code should replace comments. Confirm that you used implementation-comments. Return only actionable findings with file/line references and severity.
```

```text
You are a read-only specialist code reviewer. Do not edit files, run write commands, stage changes, commit, or implement fixes. Load and use the feature-contract-docs skill to review this diff for missing or stale feature-level documentation: purpose, scope, behavior contract, invariants, interfaces, implementation model, tradeoffs, and verification. Confirm that you used feature-contract-docs. Return only actionable findings with file/line references and severity.
```

## Output Shape

Lead with findings. For each finding, include the affected file and line, severity, why it matters, and the smallest practical fix. If there are no findings, state that clearly and call out residual risk or test gaps.
