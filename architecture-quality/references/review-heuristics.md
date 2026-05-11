# Architecture Quality Review Heuristics

## Abstractions

- Flag abstractions with one implementation unless they hide real complexity, isolate volatile behavior, or match a clear existing pattern.
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
- Keep invariants close to the data or state they protect.

## Dependency Direction

- High-level policy should not depend on low-level infrastructure details.
- Dependencies should be injected when variation, testing, or external I/O boundaries require it.
- Avoid service locators or hidden global lookups when a direct dependency would make behavior explicit.
