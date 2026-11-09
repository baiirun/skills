---
name: correctness-design
description: Parse, don't validate, and make illegal states unrepresentable. Use when designing data types, parsing input at a boundary, naming domain or unit-sensitive values, or writing state machines and transformations.
---

# Correctness Design

Strong types are the ideal. The skeleton's types and the domain model carry the
invariants, so a bad value can't be built. Assertions guard the boundaries the types
can't reach.

## Quick Start

Start from the boundary where data enters and design the type the rest of the code
will receive. Example: a webhook handler parses and validates the payload once into a
typed event, and everything inward takes that event, never the raw JSON.

## Implementation Focus

1. **Parse, don't validate.** Turn raw input into a typed value once, at the boundary,
   and pass that inward.
2. **Make illegal states unrepresentable.** Model variants as one tagged type.
3. Name domain concepts, units, ownership, lifecycle, and states precisely enough that
   misuse reads as wrong.
4. Assert at boundaries: where raw input enters, before side effects, and at state
   transitions that cross components. Inside, rely on the types.
5. Give every input a defined outcome: invalid input, edge values, and transitions
   included.
6. Write total transformations, and build the new value before replacing the old one so
   a failure leaves nothing half-changed.

## Principles

These own the general rules. Call them when their trigger appears:

- Domain states, transitions, or logic that branches on scattered booleans: call the
  Skill tool with `principle-model-the-domain`.
- Designing types or signatures: call the Skill tool with
  `principle-type-system-discipline`.
- Deciding where parsing, validation, and error handling go: call the Skill tool with
  `principle-boundary-discipline`.
- Deciding which values are stored and which are derived: call the Skill tool with
  `principle-separate-logic-state-and-effects`.

## Heuristics

Read `references/implementation-heuristics.md` when naming unit-sensitive, same-typed,
or nullable values, or when writing transformations and state transitions.

## Before You Finish

- Raw strings, maps, and nullable fields stop at the boundary where their shape is known.
- Mutually exclusive states are one tagged value, not a combination of optionals or booleans.
- Every transformation has a defined output or structured error for every input.
