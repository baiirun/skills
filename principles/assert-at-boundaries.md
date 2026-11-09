# Assert at Boundaries

> Apply when deciding where runtime checks go. Strong types carry invariants inside the system; assertions guard the boundaries the types can't reach.

Strong types are the ideal. A skeleton's types and the domain model carry the invariants, so a bad value can't be built. Assertions belong where the type system stops.

**Assert at:**
- Raw input entering the system, and values read back from storage or other processes.
- Cross-component invariants a type can't express.
- Preconditions before side effects, and postconditions after transformations whose output leaves the component.
- State-machine-like flows: at entry and at each transition that crosses a component boundary.

**Inside the system, rely on the types.** When an assertion guards a value that never crossed a boundary, the type is too weak. Move the check into the type instead (see [type-system-discipline](type-system-discipline.md)).

**The test:** Has the value this assertion checks crossed a boundary since it was last validated? If not, strengthen the type and delete the assertion.
