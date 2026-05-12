# Architecture Quality Review Heuristics

## Abstractions

- Flag abstractions with one implementation unless they hide real complexity, isolate volatile behavior, or match a clear existing pattern.
- Flag exported functions that only forward arguments to another function when they do not narrow the interface, enforce a precondition, choose policy, adapt a boundary, or provide a durable public contract. A renamed alias alone is not enough.
- Flag boolean flags that make one interface perform multiple unrelated behaviors.
- Prefer call-site clarity over theoretical reuse. If a helper hides the important decision, keep the decision local.
- Do not apply DRY when the duplication is cheaper than the coupling created by the shared abstraction.

## Interfaces

- Define interfaces from the consumer's needs, not the provider's full capability set.
- Prefer small interfaces passed through constructors, parameters, or context over concrete imports from distant modules.
- Flag interfaces that leak persistence, transport, framework, or vendor details into business logic.
- Flag changes where adding one provider method forces edits across unrelated consumers.

## Locality

- Prefer behavior in the same function, then same file, then nearby module. The farther away behavior moves, the stronger the justification should be.
- Flag designs where understanding one user action requires following multiple registration layers, callbacks, or side-effectful imports.
- Flag wrapper functions whose body is only `return callee(...)`, `return await callee(...)`, or the same call wrapped in generic error decoration; keep the call direct unless the wrapper owns behavior a reader would otherwise miss.
- Keep invariants close to the data or state they protect.
- Keep complex branching in the parent operation when that lets a reviewer see all cases on one screen and spot redundant, impossible, or dead branches.
- Prefer leaf helpers that do straight-line work under already-established preconditions instead of helpers that silently check a precondition and return without doing anything.
- Push precondition checks to callers when the callee can accept a validated value, narrower type, or asserted invariant instead of an optional/raw value.
- When splitting a large function, move non-branching work into helpers before moving the branch structure itself.
- Challenge enum or variant objects that only reify a branch selected in one function and immediately matched in another; if the state does not cross a durable boundary, keep the branch local.
- Do not push branching upward when it would duplicate policy across many callers or expose private implementation details; the goal is centralized, verifiable control flow.

## Batching

- Prefer operations over batches or collections when callers commonly loop over many items and apply the same operation to each item.
- Push loops down into the operation when batching can amortize setup cost, avoid repeated decision-making, remove branches from hot loops, or make processing order flexible.
- Consider whether a scalar helper should be the special case of a batch operation rather than the primary interface.
- Separate control-plane decisions from data-plane work where it makes the hot path simpler: decide once, then process many items in a straight-line loop.
- Do not introduce batch abstractions for rare one-off calls or when batching would obscure error handling, ordering guarantees, or per-item invariants.

## Dependency Direction

- High-level policy should not depend on low-level infrastructure details.
- Dependencies should be injected when variation, testing, or external I/O boundaries require it.
- Avoid service locators or hidden global lookups when a direct dependency would make behavior explicit.
