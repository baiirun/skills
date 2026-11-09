---
name: architecture-quality
description: Deep modules, late abstraction, locality of behavior, and push ifs up, fors down. Use when creating or changing abstractions, module boundaries, or interfaces, or when extracting helpers.
---

# Architecture Quality

## Quick Start

Before extracting a helper or adding an interface, write the call site first and ask
whether the new piece makes it clearer. Example: instead of a `UserServiceManager` with
one implementation and broad methods, call the concrete code directly until a second
implementation or a volatile dependency gives the interface a reason to exist.

## Implementation Focus

1. **Push ifs up, fors down.** Make each decision once, in the parent operation, and
   hand leaf helpers the result so they do straight-line work. Give hot paths batch
   interfaces: decide once, then loop.
2. Define each interface from what its consumer calls, and expose nothing else.
3. Build **deep modules**: a small interface with real behavior behind it. A layer that
   only forwards calls is shallow; call through it directly.

## Principles

These own the general rules. Call them when their trigger appears:

- Abstracting early, growing the diff, or threading a new signal through layers: call
  the Skill tool with `principle-laziness-protocol`.
- Layers to trace, wrappers, locality, or hidden state: call the Skill tool with
  `principle-minimize-reader-load`.
- Choosing core types and module structure before logic: call the Skill tool with
  `principle-foundational-thinking`.
- Framework, transport, persistence, or vendor types near business logic: call the
  Skill tool with `principle-boundary-discipline`.
- Decisions that depend on mutable state, I/O, caching, or scheduling, or dependency
  direction between them: call the Skill tool with
  `principle-separate-logic-state-and-effects`.

## Heuristics

Read `references/implementation-heuristics.md` when splitting a large function, placing
branches and precondition checks, shaping an interface over many items, or deciding
how a dependency is supplied.

## Before You Finish

- Each decision about a piece of state is made in one place, and helpers receive the result.
- Every new abstraction has a second user, a volatile dependency, or a boundary to adapt.
- Every function does more than forward its arguments.
