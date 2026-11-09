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

1. Abstract late. Write it concretely first; extract when repeated usage or real
   variation shows the shape.
2. Make interfaces narrow. Expose only what the consumer needs, defined from the
   consumer's side.
3. Build **deep modules**: a small interface with real behavior behind it. A layer
   that only forwards calls is shallow; call through it directly. Add a layer only
   when it owns policy, narrows a type, manages a lifecycle, or adapts a boundary.
4. Keep behavior where a maintainer will look for it: same function, then same file,
   then a nearby module.
5. **Push ifs up, fors down.** Make each decision once, in the parent operation, and
   hand leaf helpers the result so they do straight-line work. Give hot paths batch
   interfaces: decide once, then loop.
6. Pass dependencies in, as small interfaces shaped by the consumer.

## Principles

- When the change grows larger than the problem, or a new layer or threaded signal
  appears, call the Skill tool with `principle-laziness-protocol`.
- When answering "where does X come from?" needs several hops or hidden state, call
  the Skill tool with `principle-minimize-reader-load`.
- Before writing logic on new core types, call the Skill tool with
  `principle-foundational-thinking`.
- When framework, transport, persistence, or vendor types approach business logic,
  call the Skill tool with `principle-boundary-discipline`.
- When decisions depend on mutable state, I/O, caching, or scheduling, call the Skill
  tool with `principle-separate-logic-state-and-effects`.

## Heuristics

Read `references/implementation-heuristics.md` when designing a new abstraction,
splitting a large function, deciding whether to split or merge modules, or shaping an
interface over many items.

## Before You Finish

- Every new abstraction has a second user, a volatile dependency, or a boundary to adapt.
- Every function does more than forward its arguments.
- One user action can be followed without hopping through registration layers.
