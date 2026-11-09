---
name: skeleton-first
description: Before implementing a non-trivial feature or module, design a compiling code skeleton (types, module boundaries, signatures, short contracts, and a few high-value tests) and get user approval (the default) before writing any implementation. Use when a task introduces new data types, more than ~3 functions, a new module, or work that will be handed to subagents. Skip for one-function changes and bug fixes in existing structure.
---

# Skeleton-first

The structure of a program decides how hard it is to get right. If the agent picks the
structure without telling you, nobody reviews the most important decision. So fix the
structure first, as code, and have the user review it.

## Phase 1: Decide the decomposition (no code yet)
1. List the domain concepts and the states they can be in. Choose types that rule out
   illegal states, and specify them strictly: the skeleton is where the shape gets
   pinned down. This overrides the "strengthen only where partiality appears, then
   stop" guidance in `principles/type-system-discipline.md` for skeleton work.
2. Choose a representation in which edge cases follow from the structure. Example: if
   arrays are strided views, most slicing rules fall out without special cases.
   Ask: "under this design, how many special cases disappear?"
3. Split the work into components, each with a narrow interface. Draw the data flow:
   who calls whom, and who owns which state.
4. Name every intermediate value that matters. Put a component boundary wherever an
   error could be hidden by later computation, so it shows up at an interface.

## Phase 2: Write the skeleton as real code
- Put the stubs in the real source files, in the target language, and make them
  compile or typecheck. Use the language's never-returning "not implemented" form
  (Rust `todo!()`, TS `throw new Error("unimplemented")`, Python `...`), never a cast
  or dummy value such as `{} as Foo` or `null!`.
- Include: types/structs/enums, module layout, public and internal signatures,
  allowed dependencies between modules.
- When a schema owns a shape (protobuf, OpenAPI, GraphQL, a database migration),
  derive the skeleton's types from it instead of writing a parallel type by hand.
- Encode every precondition and invariant in the types first: `NonEmpty<Item>`, not
  `Requires: items is non-empty`; `TimeRange { start, duration }`, not
  `Requires: start < end`.
- Give each function a contract in its doc comment, covering only what the types
  can't express (side effects, ordering, performance, cross-component properties):
    Requires: what the caller guarantees
    Ensures:  what the function guarantees on return
    Must not: side effects or mutations that are forbidden
- Write global invariants (properties that span components and that no type can
  carry) once, at module level. Keep them few.
- **Contract budget:** ≤ 5 lines per function. State only decisions you would reject
  an implementation for. Over-detailed contracts lower agent accuracy.
- No implementation details in contracts unless they are requirements (performance,
  memory, ordering).

## Phase 3: A few tests that matter
Call the Skill tool with `testing-and-verifying` and write only the tests it calls for,
aimed at the skeleton's contracts and invariants. Mark them pending or ignored until
their component exists.

## Phase 4: Review gate
Show the user:
- the skeleton diff, including the tests and what each one protects
- a short list of the decisions it encodes and the alternatives rejected
- open questions where the contract is ambiguous

Gate by default: wait for the user's approval before implementing. Skip the gate only
when the user has said to proceed without review for this task, and then state the
skeleton's key decisions in your reply so they can still course-correct. Offer to
commit the skeleton by itself
(`chore: skeleton for <feature>`) so later diffs show implementation separately.

## Phase 5: Implement component by component
- Implement one component at a time and check it against its own contract and tests
  before moving on. Fixing one component alone is cheap; regenerating the whole
  program is not.
- Components with complete contracts can go to parallel subagents. Give each
  subagent only its stub, its contract, and the types it touches.
- If an implementer wants to change a signature, type, or contract, stop and go back
  to Phase 2. Don't edit the skeleton silently.

## Afterward
The signatures and doc contracts stay in the code as the record of what is required.
When requirements change, update the skeleton and its contracts first, then the code.
Don't patch around behavior that was never specified.

## Checklist for a good skeleton
- [ ] Compiles/typechecks with stubs
- [ ] Types make illegal states unrepresentable
- [ ] No contract line states something a type could carry
- [ ] Every component can be pinned down by a ≤5-line contract
- [ ] Correct components imply a correct whole
- [ ] Intermediate state that matters is visible at an interface
- [ ] Each test guards a decision that matters, and none just restates a type
- [ ] Says only what you'd reject an implementation over

## Anti-patterns
- A prose design doc instead of code stubs. Code-like specs beat prose docs even
  when the prose is 4–7× longer.
- Exhaustive contracts "to be safe"
- Many tests compensating for vague interfaces
- Skeleton written after the implementation, to justify it
