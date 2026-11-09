# Agent Skills

This repository contains reusable agent skills. Each skill lives in its own directory with a `SKILL.md` entrypoint and optional references or scripts.

The skills use capability-based instructions. They may use delegation, model selection, conversation history, connectors, or recurring monitoring when the active agent harness provides those features, and they define fallbacks when it does not.

## Skill roles

Skills in this repository have four roles:

- Coordinators route work without repeating specialist policy. [`code-quality`](code-quality/SKILL.md) coordinates broad, read-only code reviews.
- Specialists apply several principles to one kind of judgment or artifact. The code-quality specialists cover architecture, correctness, failures, tests, source comments, and feature contracts.
- `principle-*` skills contain atomic decision rules that other skills can compose. They do not own broad review workflows or output formats.
- Workflows sequence actions, tools, and verification for a concrete task.

Use a specialist directly for narrow work. Use a coordinator only when the request crosses several specialist concerns.

## Code quality specialists

- [`architecture-quality`](architecture-quality/SKILL.md)
- [`correctness-design`](correctness-design/SKILL.md)
- [`errors-observability`](errors-observability/SKILL.md)
- [`feature-contract-docs`](feature-contract-docs/SKILL.md)
- [`implementation-comments`](implementation-comments/SKILL.md)
- [`testing-discipline`](testing-discipline/SKILL.md)

[`implementation-comments`](implementation-comments/SKILL.md) owns the general source-comment policy. [`no-comments`](no-comments/SKILL.md) is the explicit editing workflow for aggressive comment and suppression cleanup.

## Pstack workflows

The pstack skills cover architecture, investigation, adversarial review, verification, orchestration, technical writing, and working-style automation. The `principle-*` skills hold the focused design and execution rules used by those workflows.

These skills were ported from [Cursor's pstack collection](https://github.com/cursor/plugins/tree/main/pstack/skills). Cursor-only paths, metadata, tool arguments, model identifiers, review-bot behavior, and plugin dependencies were replaced with harness-neutral capability checks and fallbacks.

`tdd` and `make-bot-ui` are intentionally excluded.

## Design

- [`skeleton-first`](skeleton-first/SKILL.md): Before implementing a non-trivial feature, writes a compiling skeleton of types, module boundaries, signatures, short contracts, and a few high-value tests, then waits for approval. Based on arXiv 2610.38214.

## Refactoring

- [`untangle-codebase`](untangle-codebase/SKILL.md): Runs a whole-codebase refactor in one pass so agents read less per change, break less silently, and debug faster. Invoke explicitly; it does not auto-trigger. Vendored from [caldoai/skills](https://github.com/caldoai/skills/tree/main/skills/untangle-codebase).

## Explanation

- [`show-me`](show-me/SKILL.md): Explains the current topic visually with the smallest fitting view: pseudocode, trees, Mermaid diagrams, diffs, or focused HTML artifacts. Vendored from [humanlayer/skills](https://github.com/humanlayer/skills) at `3c262914`.

## References

Some skills include deeper guidance under `references/`, executable helpers under `scripts/`, or workflow-specific playbooks. Load only the resources named by the active skill.
