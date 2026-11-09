# Comment the Why

> Apply when writing or editing source comments, workaround notes, deferred-work notes, or commented-out code. A comment earns its place by stating a reason the code can't show; prefer a rename or extraction when that does the job.

A comment tells the reader something the code can't: why it's shaped this way, which invariant or spec requirement it protects, or which external constraint forces it. Comment once the code is close to final, so comments describe the final shape.

For each spot a reader might stop and ask "why?", first try to make the code answer it with a rename or small extraction. If it still can't, write one comment with the reason. A retry loop that deliberately skips a provider error says why that error is terminal, not that the loop iterates attempts.

**Worth writing:**
- Why a branch, guard, retry, cache, fallback, or ordering constraint exists, when the code can't make the reason obvious.
- Local invariants future edits must preserve, especially around state transitions, concurrency, data shape assumptions, and external system contracts.
- The spec, feature contract, or invariant behind a surprising choice, linked when one exists.
- Non-obvious tradeoffs: deliberately duplicated logic, an avoided abstraction, a compatibility constraint, provider-specific behavior.
- Failure semantics when an error is intentionally swallowed, transformed, retried, or surfaced differently from the default path.

**Placement:**
- Put the comment next to the code it explains; distant explanations go stale.
- Write one targeted comment for a local invariant instead of file-level narration.
- When several call sites need the same explanation, move the invariant into a type, helper name, parser, assertion, or test instead (see [encode-lessons-in-structure](encode-lessons-in-structure.md)).
- Describe intent or constraints, not step-by-step choreography, so the comment survives refactors.

**Keep the source clean:**
- When you change code, update or delete the comments that describe it.
- Track deferred work outside the source, in the project's tracker.
- Delete commented-out code, unless it's an intentionally disabled path that says why and when it can be restored or removed.

**The test:** Does every comment state a why the code can't show? Would a rename make any of them unnecessary?
