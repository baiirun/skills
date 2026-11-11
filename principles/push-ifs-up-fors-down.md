# Push Ifs Up, Fors Down

> Apply when writing or splitting functions that branch on state, extracting helpers, or writing an operation that callers run over many items. Make each decision once in the parent and hand leaf helpers the result; give hot paths batch interfaces.

**Ifs up.** Make each decision once, in the parent operation, so every case is on one screen and redundant, impossible, or dead branches are obvious. Leaf helpers do straight-line work under preconditions the caller already established.

**Fors down.** When callers loop over many items applying the same operation, put the loop inside the operation. Decide once, then process many items in a straight-line loop.

**Ifs up:**
- Keep complex branching in the parent operation.
- Write leaf helpers that assume their preconditions. A helper that checks a precondition and silently returns hides a branch from the parent.
- Have callees accept validated values, narrower types, or asserted invariants instead of optional or raw values. The caller handles the raw case once.
- When splitting a large function, move non-branching work into helpers first and keep the branch structure in the parent.
- Carry a decision across functions as an enum or variant only when the state crosses a durable boundary. A variant made in one function only to be matched in the next is a branch that belongs in one place.
- Keep branching below the callers when pushing it up would copy policy into many callers or expose private details. The goal is control flow you can check in one place.
- When the branching is spread across callbacks, handlers, or hooks rather than across functions, see [centralize-control-flow](centralize-control-flow.md).

**Fors down:**
- Write the operation over the collection when callers commonly loop over it.
- Push the loop down when that amortizes setup, avoids repeated decisions, removes branches from the hot loop, or frees the processing order.
- Consider making the scalar helper a special case of the batch operation.
- Separate control-plane decisions from data-plane work.
- Keep scalar interfaces for rare one-off calls, and wherever batching would hide error handling, ordering guarantees, or per-item invariants.

**The test:** Can you see every case of this decision in one function? Does the hot loop contain a decision that could have been made once before it?
