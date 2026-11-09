---
name: correctness-design
description: Parse, don't validate, and make illegal states unrepresentable. Use when designing data types, parsing input at a boundary, naming domain or unit-sensitive values, or writing state machines and transformations.
---

# Correctness Design

Prefer structures that can't hold a bad value over checks that catch one later.

## Quick Start

Start from the boundary where data enters and design the type the rest of the code
will receive. Example: a webhook handler parses and validates the payload once into a
typed event, and everything inward takes that event, never the raw JSON.

## Implementation Focus

1. **Parse, don't validate.** Turn raw input into a typed value once, at the boundary,
   and pass that inward. Inner code relies on the type instead of re-checking.
2. **Make illegal states unrepresentable**: tagged variants, constructors that
   validate, schemas.
3. Name domain concepts, units, ownership, lifecycle, and states precisely enough that
   misuse reads as wrong.
4. Put each invariant next to the data or state it protects.
5. Assert critical inputs, outputs, invariants, and state transitions.
6. Design for the negative space too: invalid input, boundaries, and transitions get a
   defined outcome.

## Principles

- When logic branches on scattered booleans, phases, or repeated shape assumptions,
  call the Skill tool with `principle-model-the-domain`.
- When designing types or signatures in a statically typed language, call the Skill
  tool with `principle-type-system-discipline`.
- When deciding where validation and error handling go, call the Skill tool with
  `principle-boundary-discipline`.
- When deciding where branching and precondition checks live, call the Skill tool with
  `architecture-quality`.

## Heuristics

Read `references/implementation-heuristics.md` when designing input handling, data
models, transformations, or state machines, when naming unit-sensitive or same-typed
values, or when working in code that has produced correctness bugs before.

## Before You Finish

- Raw strings, maps, and nullable fields stop at the boundary where their shape is known.
- Mutually exclusive states are one tagged value, not a combination of optionals or booleans.
- Every transformation has a defined output or structured error for every input.
