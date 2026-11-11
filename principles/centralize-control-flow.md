# Centralize Control Flow

> Apply when wiring callbacks, event handlers, middleware, lifecycle hooks, or promise chains, or when the order of operations depends on which handler runs first. Put the sequence in one function that calls the pieces by name.

The order things happen should be a fact written in one place, not an emergent property of registration order, dispatch order, or which callback fires.

**Why:** A reader answering "what happens after X?" should find one function and read it top to bottom. When the sequence is spread across handlers subscribed to the same event, hooks on the same lifecycle, or `.then` chains with branching inside, the reader has to find every subscriber, work out the framework's dispatch order, and assemble the flow in their head. That assembly is wrong often enough to cause bugs and slow enough to cost every reader.

**The pattern:**
- Write one function that calls `a()`, then `b()`, then `c()` instead of three handlers subscribed to the same event. Registration order is hidden control flow.
- When a framework forces handlers, make each handler a one-line call into a named sequencing function, so the flow still has one home.
- Keep the state machine, if there is one, in one module (see [model-the-domain](model-the-domain.md)). Scattered `if (phase === ...)` checks across handlers are a state machine that has been exploded.
- Replace `onSuccess`/`onError` callback pairs and branching inside `.then` with a single sequential function using `await` and ordinary `if`. The branches become visible and the order becomes literal.
- Treat middleware chains and plugin hooks as a sequence to own, not to accumulate. If behavior depends on middleware order, write the order down as a list in one place.
- Inside the sequencing function, apply [push-ifs-up-fors-down](push-ifs-up-fors-down.md): decisions in the parent, straight-line work in the leaves.

**The test:** Can you point to the one function where the order of operations for this flow is written? If the answer is "it depends on what's registered," the flow is decentralized.
