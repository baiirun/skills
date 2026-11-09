# Architecture Quality Implementation Heuristics

## Abstractions

- Give an abstraction one implementation only when it hides real complexity, isolates
  volatile behavior, or matches an established local pattern.
- Export a function that forwards to another only when it narrows the interface,
  enforces a precondition, chooses policy, adapts a boundary, or is a durable public
  contract. A rename alone is not a reason.
- Split an interface instead of adding a boolean flag that switches it between
  unrelated behaviors.
- Keep the important decision at the call site. If a helper would hide it, don't extract.
- Duplicate code when sharing it would cost more coupling than the copies cost upkeep.

## Interfaces

- Write the interface from what the consumer calls, not from everything the provider
  can do.
- Pass small interfaces through constructors, parameters, or context instead of
  importing concrete modules from far away.
- Keep persistence, transport, framework, and vendor types out of business logic
  signatures.
- If adding one provider method would force edits in unrelated consumers, the
  interface is too wide. Split it before adding the method.

## Locality

- Put behavior in the same function first, then the same file, then a nearby module.
  The farther it moves, the stronger the reason should be.
- Wire a user action so it can be followed without registration layers, callbacks, or
  side-effecting imports.
- Don't write wrappers whose body is only `return callee(...)`, `return await callee(...)`,
  or the same call with generic error decoration. Call the callee.
- Put invariant enforcement next to the data or state it protects.
- Keep complex branching in the parent operation, so every case is on one screen and
  redundant, impossible, or dead branches are obvious.
- Write leaf helpers as straight-line work under preconditions the caller already
  established. Don't write helpers that check a precondition and silently return.
- Have callees accept validated values, narrower types, or asserted invariants instead
  of optional or raw values. The caller handles the raw case once.
- When splitting a large function, move non-branching work into helpers first and keep
  the branch structure in the parent.
- Don't create an enum or variant whose only job is to carry a branch decided in one
  function to a match in another. Keep the branch local unless the state crosses a
  durable boundary.
- Don't push branching up if it would copy policy into many callers or expose private
  details. The goal is control flow you can check in one place.

## Batching

- When callers loop over many items applying the same operation, write the operation
  over the collection.
- Push the loop into the operation when that amortizes setup, avoids repeated
  decisions, removes branches from the hot loop, or frees the processing order.
- Consider making the scalar helper a special case of the batch operation.
- Separate control-plane decisions from data-plane work: decide once, then process
  many items in a straight-line loop.
- Skip batching for rare one-off calls, or when it would hide error handling, ordering
  guarantees, or per-item invariants.

## Dependency Direction

- Make high-level policy independent of low-level infrastructure details.
- Inject a dependency when variation, testing, or external I/O requires it, and not
  otherwise.
- Use a direct dependency instead of a service locator or hidden global lookup.
