# Agent Skills

This repository contains reusable agent skills. Each skill lives in its own directory with a `SKILL.md` entrypoint and optional references or scripts.

The skills use capability-based instructions. They may use delegation, model selection, conversation history, connectors, or recurring monitoring when the active agent harness provides those features, and they define fallbacks when it does not.

## Skill roles

Skills in this repository have four roles:

- Coordinators sequence work without repeating specialist policy. [`code-quality`](code-quality/SKILL.md) walks an implementation through the code-quality specialists.
- Specialists apply several principles to one kind of design decision or artifact. The code-quality specialists cover architecture, correctness, failures, tests, source comments, and feature contracts.
- `principle-*` skills contain atomic decision rules that other skills can compose. They do not own broad workflows or output formats.
- Workflows sequence actions, tools, and verification for a concrete task.

Use a specialist directly for narrow work. Use a coordinator only when the work crosses several specialist concerns.

## Code quality

The code-quality skills guide implementation, not review. For reviewing code, use a dedicated review skill or agent.

- [`code-quality`](code-quality/SKILL.md): User-invoked (`/code-quality`). Walks an implementation through data model, structure, failure semantics, tests, comments, and docs, calling each specialist at the step where it applies.
- [`architecture-quality`](architecture-quality/SKILL.md): Designs abstractions, interfaces, dependency direction, control-flow placement, batching, and locality of behavior.
- [`correctness-design`](correctness-design/SKILL.md): Designs boundary parsing, illegal-state-free data models, naming, invariants, assertions, and total transformations.
- [`errors-observability`](errors-observability/SKILL.md): Designs service and job failure behavior: error classes, retries, fallbacks, structured logging, and tracing.
- [`feature-contract-docs`](feature-contract-docs/SKILL.md): Writes durable feature contracts that model purpose, scope, behavior, invariants, interfaces, implementation model, and verification.
- [`implementation-comments`](implementation-comments/SKILL.md): Writes source comments that carry non-obvious why, and prefers clearer code where a rename or extraction suffices.
- [`testing-discipline`](testing-discipline/SKILL.md): Chooses the few tests worth writing, their level, mock boundaries, and regression-first bug fixes.

[`implementation-comments`](implementation-comments/SKILL.md) owns the general source-comment policy. [`no-comments`](no-comments/SKILL.md) is the explicit editing workflow for aggressive comment and suppression cleanup.

## Design

- [`skeleton-first`](skeleton-first/SKILL.md): Before implementing a non-trivial feature, writes a compiling skeleton of types, module boundaries, signatures, short contracts, and a few high-value tests, then waits for approval. Based on arXiv 2610.38214.

## Refactoring

- [`untangle-codebase`](untangle-codebase/SKILL.md): Runs a whole-codebase refactor in one pass so agents read less per change, break less silently, and debug faster. Invoke explicitly; it does not auto-trigger. Vendored from [caldoai/skills](https://github.com/caldoai/skills/tree/main/skills/untangle-codebase).

## Explanation

- [`show-me`](show-me/SKILL.md): Explains the current topic visually with the smallest fitting view: pseudocode, trees, Mermaid diagrams, diffs, or focused HTML artifacts. Vendored from [humanlayer/skills](https://github.com/humanlayer/skills) at `3c262914`.

## Pstack skills

The `how`, `why`, `teach`, `technical-writing`, `unslop`, `typescript-best-practices`, `no-comments`, and `principle-*` skills hold the remaining pstack investigation, writing, and design rules.

These skills were ported from [Cursor's pstack collection](https://github.com/cursor/plugins/tree/main/pstack/skills). Cursor-only paths, metadata, tool arguments, model identifiers, review-bot behavior, and plugin dependencies were replaced with harness-neutral capability checks and fallbacks.

`tdd` and `make-bot-ui` are intentionally excluded.

## References

Some skills include deeper guidance under `references/`, executable helpers under `scripts/`, or workflow-specific playbooks. The code-quality specialists keep theirs in `references/implementation-heuristics.md`. Load only the resources named by the active skill.
