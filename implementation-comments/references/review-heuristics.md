# Implementation Comments Review Heuristics

## Useful Comments

- Explain why a branch, guard, retry, cache, fallback, or ordering constraint exists when nearby code cannot make that reason obvious.
- Document local invariants that future edits must preserve, especially around state transitions, concurrency, data shape assumptions, and external system contracts.
- Tie surprising implementation choices back to the relevant spec, feature contract, or invariant when one exists.
- Capture non-obvious tradeoffs such as deliberately duplicated logic, avoided abstractions, compatibility constraints, or provider-specific behavior.
- Describe failure semantics when errors are intentionally swallowed, transformed, retried, or surfaced differently from the default path.

## Comments to Challenge

- Flag comments that restate syntax, assignments, loops, obvious conditionals, or function names.
- Flag stale comments that contradict current code or describe behavior no longer present.
- Flag deferred-work notes such as "fix later", "temporary", or "hack"; remove them or replace them with tracked work outside the source.
- Flag commented-out code unless the disabled path is intentionally preserved and explains when it can be restored or removed.

## Placement and Scope

- Keep comments next to the code they explain; distant explanation becomes stale quickly.
- Prefer one targeted comment over broad file-level narration for a local invariant.
- Avoid comment blocks that hide the implementation or make simple code look complex.
- When several call sites need the same explanation, consider whether the invariant belongs in a type, helper name, parser, assertion, or test instead.

## Prefer Code Clarity

- Prefer renaming variables, extracting a small helper, or simplifying control flow when that removes the need for a comment.
- Do not use comments to excuse unclear code when a small scoped edit can make the behavior self-explanatory.
- Keep comments stable across refactors by describing intent or constraints, not step-by-step implementation choreography.
