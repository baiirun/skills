# Architecture Quality Implementation Heuristics

General rules about layers, wrappers, locality, abstraction timing, boundaries, and
dependency direction live in the principle skills named in `SKILL.md`. This file holds
what those principles don't cover.

## Interfaces

- Split an interface instead of adding a boolean flag that switches it between
  unrelated behaviors.
- If adding one provider method would force edits in unrelated consumers, the
  interface is too wide. Split it before adding the method.

## Push Ifs Up

- Keep complex branching in the parent operation, so every case is on one screen and
  redundant, impossible, or dead branches are obvious.
- Write leaf helpers as straight-line work under preconditions the caller already
  established. A helper that checks a precondition and silently returns hides a branch
  from the parent.
- Have callees accept validated values, narrower types, or asserted invariants instead
  of optional or raw values. The caller handles the raw case once.
- When splitting a large function, move non-branching work into helpers first and keep
  the branch structure in the parent.
- Carry a decision across functions as an enum or variant only when the state crosses a
  durable boundary. A variant made in one function only to be matched in the next is a
  branch that belongs in one place.
- Keep branching below the callers when pushing it up would copy policy into many
  callers or expose private details. The goal is control flow you can check in one place.

## Fors Down

- When callers loop over many items applying the same operation, write the operation
  over the collection.
- Push the loop into the operation when that amortizes setup, avoids repeated
  decisions, removes branches from the hot loop, or frees the processing order.
- Consider making the scalar helper a special case of the batch operation.
- Separate control-plane decisions from data-plane work: decide once, then process
  many items in a straight-line loop.
- Keep scalar interfaces for rare one-off calls, and wherever batching would hide error
  handling, ordering guarantees, or per-item invariants.

## Supplying Dependencies

- Inject a dependency when variation, testing, or external I/O requires it, and call it
  directly otherwise.
- Pass dependencies explicitly. A service locator or hidden global lookup hides what a
  unit depends on.
