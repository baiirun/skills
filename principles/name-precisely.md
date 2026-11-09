# Name Precisely

> Apply when naming domain concepts, units, same-typed parameters, nullable values, or related values that appear together. Encode the domain role, units, and qualifiers in names so misuse reads as wrong.

A name is the first contract a reader sees. Name precisely enough that the wrong use of a value looks wrong at the call site.

**The pattern:**
- Name values and operations with the precise domain noun or verb, so a reader knows what the value is and which mental model applies.
- Give each term one meaning. When two concepts could be confused in code, docs, logs, or conversation, give them different names.
- Name the semantic role, not just the type: ownership, lifetime, validity, source, target, authority, durability, or side-effect responsibility.
- Put units and qualifiers in names wherever a unit, bound, or coordinate system matters: `_ms`, `_bytes`, `_offset`, `_index`, `_count`, `_size`, `_limit`, `_start`, `_end`. Order qualifiers most significant first so related names group: `latency_ms_max`, `latency_ms_min`.
- Treat `index`, `count`, `size`, `offset`, `length`, and `limit` as distinct concepts even when they share a primitive type.
- Choose related names that show symmetry at call sites: `source`/`target`, `source_offset`/`target_offset`.
- Write full domain words, keeping abbreviations to conventional tiny scopes such as sort callbacks or matrix math.
- Keep one name per piece of state. Aliases and duplicate variables drift apart.
- Use named options, value objects, or structured parameters when positional arguments of the same type could be swapped.
- Name nullable values so the meaning of `null` is clear at the call site, or replace them with an explicit variant when absence means something.
- Name invariants and states positively, so it's clear which case you're in.

**The test:** Could a reader swap two of these arguments, or mix up two of these values, without the names looking wrong?
