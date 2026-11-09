# Implementation Comments Implementation Heuristics

## Comments Worth Writing

- Why a branch, guard, retry, cache, fallback, or ordering constraint exists, when the
  code can't make the reason obvious.
- Local invariants future edits must preserve, especially around state transitions,
  concurrency, data shape assumptions, and external system contracts.
- The spec, feature contract, or invariant behind a surprising choice, linked when one
  exists.
- Non-obvious tradeoffs: deliberately duplicated logic, an avoided abstraction, a
  compatibility constraint, provider-specific behavior.
- Failure semantics when an error is intentionally swallowed, transformed, retried, or
  surfaced differently from the default path.

## Comments Not to Write

- Restatements of syntax, assignments, loops, obvious conditionals, or function names.
- Descriptions of behavior the code no longer has. Update or delete comments when the
  code changes.
- Deferred-work notes such as "fix later", "temporary", or "hack". Track the work
  outside the source.
- Commented-out code, unless the disabled path is kept on purpose and says when it can
  be restored or removed.

## Placement and Scope

- Put the comment next to the code it explains; distant explanations go stale.
- Write one targeted comment for a local invariant instead of file-level narration.
- Keep comment blocks short enough that they don't bury the implementation or make
  simple code look complex.
- If several call sites need the same explanation, move the invariant into a type,
  helper name, parser, assertion, or test instead.

## Code Clarity First

- Rename a variable, extract a small helper, or simplify control flow when that removes
  the need for a comment.
- Don't use a comment to excuse unclear code that a small scoped edit could fix.
- Describe intent or constraints, not step-by-step choreography, so the comment
  survives refactors.
