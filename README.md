# Agent Skills

This repository contains reusable agent skills. Each skill lives in its own directory with a `SKILL.md` entrypoint and optional references or scripts.

The skills use capability-based instructions. They may use delegation, model selection, or connectors when the active agent harness provides those features, and they define fallbacks when it does not.

## How the pieces fit

- **Principles** are plain markdown files in [`principles/`](principles/). Each holds one atomic decision rule with the condition that triggers it. They are not skills, so they cost no always-loaded context.
- **Routing skills** are model-invoked skills, one per kind of problem. Each maps the conditions it covers to the principle files to read, so an agent loads only the rules that apply. Skills that read principles reach them through a `principles` symlink to `../principles`, so `principles/<name>.md` resolves from any harness's skill directory.
- **Workflows** sequence steps for a concrete task: designing a skeleton, writing feature docs, cleaning up comments.
- **`code-quality`** is the user-invoked router: it maps the kind of work to the routing skill, workflow, or single principle that covers it.

## Routing skills

| Skill | Fires for |
|---|---|
| [`designing-structure`](designing-structure/SKILL.md) | Modules, interfaces, abstractions, function structure, a refactor's target shape |
| [`modeling-data`](modeling-data/SKILL.md) | Types, input parsing, naming, runtime checks, data transformations |
| [`handling-failure`](handling-failure/SKILL.md) | Error classes, retries, fallbacks, idempotency, logs, tracing |
| [`testing-and-verifying`](testing-and-verifying/SKILL.md) | Choosing tests, assertions, bug fixes, proving work is done |
| [`changing-existing-code`](changing-existing-code/SKILL.md) | Refactors, migrations, new requirements in existing designs |
| [`sharing-state`](sharing-state/SKILL.md) | Concurrent writers, work that must survive crashes and reruns |
| [`documenting-code`](documenting-code/SKILL.md) | Source comments, recurring rules, feature docs |

## Implementation

- [`code-quality`](code-quality/SKILL.md): User-invoked (`/code-quality`). Routes implementation work to the matching routing skills, workflows, and principles; it prescribes no step order. For reviewing code, use a dedicated review skill or agent.
- [`skeleton-first`](skeleton-first/SKILL.md): Before implementing a non-trivial feature, writes a compiling skeleton of types, module boundaries, signatures, short contracts, and a few high-value tests, then waits for approval. Based on arXiv 2610.38214.
- [`feature-contract-docs`](feature-contract-docs/SKILL.md): Writes durable feature contracts that model purpose, scope, behavior, invariants, interfaces, implementation model, and verification.
- [`no-comments`](no-comments/SKILL.md): Explicit cleanup pass over existing comments and suppressions, using [`principles/comment-the-why.md`](principles/comment-the-why.md) as its policy.
- [`typescript-best-practices`](typescript-best-practices/SKILL.md): TypeScript-specific grounding for the type-system and boundary principles.

## Working style

These stay standalone model-invoked skills because no code-problem router covers them: [`principle-build-the-lever`](principle-build-the-lever/SKILL.md), [`principle-experience-first`](principle-experience-first/SKILL.md), [`principle-guard-the-context-window`](principle-guard-the-context-window/SKILL.md), and [`principle-never-block-on-the-human`](principle-never-block-on-the-human/SKILL.md).

## Refactoring

- [`untangle-codebase`](untangle-codebase/SKILL.md): Runs a whole-codebase refactor in one pass so agents read less per change, break less silently, and debug faster. Invoke explicitly; it does not auto-trigger. Vendored from [caldoai/skills](https://github.com/caldoai/skills/tree/main/skills/untangle-codebase).

## Explanation and writing

- [`how`](how/SKILL.md), [`why`](why/SKILL.md), and [`teach`](teach/SKILL.md): explain how code works, why it is that way, and both together. [`bro`](bro/SKILL.md) restates the last message in plain language.
- [`librarian`](librarian/): Source-backed research across local and remote codebases, with one adapter per harness under `claude/`, `codex/`, and `opencode/`.
- [`show-me`](show-me/SKILL.md): Explains the current topic visually with the smallest fitting view: pseudocode, trees, Mermaid diagrams, diffs, or focused HTML artifacts. Vendored from [humanlayer/skills](https://github.com/humanlayer/skills) at `3c262914`.
- [`technical-writing`](technical-writing/SKILL.md), [`unslop`](unslop/SKILL.md), [`commit-description-writing`](commit-description-writing/SKILL.md), [`pr-description-writing`](pr-description-writing/SKILL.md): prose standards.

`how`, `why`, `teach`, `technical-writing`, `unslop`, `typescript-best-practices`, `no-comments`, and the principles were ported from [Cursor's pstack collection](https://github.com/cursor/plugins/tree/main/pstack/skills), with Cursor-only paths, metadata, and dependencies replaced by harness-neutral fallbacks.

## References

Some skills include deeper guidance under `references/` or helper scripts under `scripts/`. Load only the resources named by the active skill.
