---
name: designing-structure
description: Module, interface, and function structure. Use when creating or changing modules, interfaces, or abstractions, splitting functions, or deciding a refactor's target shape.
---

# Designing Structure

Before writing the code, read each principle whose condition matches the work. They are short; read them in full rather than from memory of their titles.

| When the work involves | Read |
|---|---|
| Choosing core types and module layout before logic | `principles/foundational-thinking.md` |
| Logic that branches a lot or repeats a shape assumption | `principles/model-the-domain.md` |
| Placing branches, splitting functions, or writing an operation over many items | `principles/push-ifs-up-fors-down.md` |
| Adding or changing an interface, extracting a helper, or supplying a dependency | `principles/consumer-shaped-interfaces.md` |
| Code that is hard to trace: layers, wrappers, hidden state | `principles/minimize-reader-load.md` |
| Abstracting early, a growing diff, or threading a new signal through layers | `principles/laziness-protocol.md` |
| Business decisions mixed with mutable state, I/O, caching, or scheduling | `principles/separate-logic-state-and-effects.md` |
| Framework, transport, persistence, or vendor types near business logic | `principles/boundary-discipline.md` |
| A novel decision with no precedent in the codebase | `principles/exhaust-the-design-space.md` |

For a new feature, a new module, or more than a few functions, call the Skill tool with `skeleton-first` and fix the structure as stubs before implementing.

Done when: every row whose condition matches the work has had its principle read in full, and the code follows it, including its test where it has one.
