---
name: no-comments
description: Perform an explicit, aggressive cleanup of comments and suppressions in a diff. Remove narration and dead constraints, preserve proven non-obvious rationale, and encode enforceable rules in code or tests.
---

# No Comments

Use this workflow only when the user explicitly asks for a comment-removal or no-comments pass.

## Policy to load

Read `principles/comment-the-why.md` first. It owns the policy for which comments deserve to exist. Also read:

- `principles/encode-lessons-in-structure.md` when code, types, assertions, tests, or lint can replace prose.
- `principles/fix-root-causes.md` when a suppression or warning comment points to a small underlying defect.

## Scope

Use the files or diff named by the caller. If none is named, use the current working-tree diff against the repository's base branch. Do not widen the scope to similar comments elsewhere.

## Workflow

1. Inventory comments, commented-out code, lint suppressions, and type-checker suppressions in scope.
2. Classify each item using `comment-the-why`: keep, remove, rewrite, track elsewhere, or encode.
3. Review the classification independently when the harness supports another reviewer. Otherwise pause and perform a second pass with only the policy and diff in view.
4. Apply the smallest accepted edits. Implement a root-cause fix only when it is local, clearly correct, and inside the requested scope.
5. Preserve comments about constraints outside the repository only when the constraint and consequence are concrete. Offer an enforceable replacement when one is practical.
6. Run the narrow checks affected by the edits and inspect the final diff.

## Output

Report comments removed, comments rewritten, suppressions removed or retained, rules encoded in code or tests, checks run, and any constraints that remain unenforced.
