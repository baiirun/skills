---
name: implementation-comments
description: Write and review source comments that explain non-obvious local intent, invariants, requirements, tradeoffs, failure semantics, or external constraints. Use when adding or reviewing inline comments, block comments, workaround notes, deferred-work comments, or commented-out code.
---

# Implementation Comments

This skill owns the repository's general policy for source comments. A comment should preserve a local reason the code cannot express clearly by itself.

Use `no-comments` only when the user explicitly asks for an aggressive cleanup pass that removes comments and suppressions and implements small root-cause fixes. That workflow loads this skill for policy.

## Principles to load

- `principle-minimize-reader-load` for narration, duplication, and comments that increase reading cost.
- `principle-encode-lessons-in-structure` when a type, assertion, test, name, or lint rule can enforce the lesson.

## Review focus

1. Keep comments that explain local intent, an invariant, a requirement, a tradeoff, surprising failure behavior, or an external constraint.
2. Remove comments that translate nearby syntax into prose.
3. Keep the explanation beside the behavior it governs and narrow its scope.
4. Rewrite or remove stale, vague, and misleading comments.
5. Prefer a small code clarification when it can express the same fact without commentary.
6. Move deferred work to the project's tracking system.
7. Delete commented-out code unless it represents an intentionally disabled path with a current reason and removal condition.

Read `references/review-heuristics.md` for detailed authoring and review guidance.

## Output

For authored comments, write only the necessary local explanation. For reviews, order findings by severity and propose the smallest action: keep, remove, rewrite, relocate, link to a durable contract, or encode the rule in code or tests.
