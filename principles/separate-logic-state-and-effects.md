# Separate logic, state, and effects

> Apply when code mixes business decisions with mutable state, I/O, caching, scheduling, or physical storage choices. Keep authoritative facts explicit, derive other values, isolate effects, and require optimizations to change cost without changing meaning.

Store authoritative facts, derive everything else, and keep operational machinery out of the logic that decides what the system means. An optimization may change cost, never meaning.

## Classify the parts

- **Authoritative state** is input the requirements say the system must remember. Name its owner and the operations allowed to change it.
- **Derived data** is a function of authoritative state. Recompute it by default. If performance requires storing it, treat it as a rebuildable cache or projection, not a second writable source of truth.
- **Logic** is a deterministic decision, query, invariant, or state transition over explicit inputs. It may return new state and effects to perform, but it does not read hidden mutable state or perform I/O itself.
- **Effects** translate between the system and the outside world: parse input, load state, invoke logic, persist results, publish events, or render output. Keep this shell thin.
- **Operational state and control** include caches, indexes, denormalized storage, retries, scheduling, evaluation order, and parallelism. Keep them behind the core dependency boundary.

## Apply the separation

- Pass only the state a decision uses. A pure function that accepts one giant `AppState` has recreated global state with an explicit parameter.
- Encode ordering only when promised behavior or correctness requires it. Do not turn incidental statement order into a dependency or test contract.
- Enforce an invariant once at the authority that owns the affected state. Do not duplicate it across handlers, jobs, UI code, and persistence adapters.
- Make performance state disposable. Removing a cache, index, materialized view, denormalization, or eager scheduler may make the system slower, but it must not change the answer.
- Point dependencies inward. Logic knows the domain state it reads; caches, persistence, frameworks, and schedulers may know the logic, but the logic does not know them.

Do not turn these distinctions into ceremonial layers. State and the behavior that protects its invariants can live in one cohesive module or type. The rule concerns authority, dependencies, and effects, not file count.

Derived state can be retained when recomputation is too expensive or when carrying it makes a time-dependent process substantially clearer. Keep one authoritative source, document how the derived state is rebuilt or reconciled, and prevent callers from updating both independently.

## The tests

Ask:

1. Why is this value stored, and what is its authoritative source?
2. Can every derived value be rebuilt from authoritative facts?
3. If the performance machinery disappeared, would the system remain correct?
4. Can I understand the decision from its explicit inputs without inspecting a database, clock, cache, or process-wide object?
5. If two operations changed order, should promised behavior change? If not, remove the accidental ordering.

This principle adapts the state, logic, and control separation from Moseley and Marks's [Out of the Tar Pit](https://dl.acm.org/doi/10.1145/1167515.1167513) without requiring its proposed Functional Relational Programming architecture.
