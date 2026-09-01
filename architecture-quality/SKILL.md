---
name: architecture-quality
description: Review and improve module boundaries, interface depth, dependency direction, control-flow locality, batching, and avoidable indirection. Use when designing or reviewing abstractions, service interfaces, dependency injection, helper extraction, batching, or refactors.
---

# Architecture Quality

Review whether the code places responsibility where a maintainer can understand and change it safely.

## Principles to load

Load these principle skills when they apply:

- `principle-laziness-protocol` for speculative abstractions and changes larger than the evidence supports.
- `principle-minimize-reader-load` for interface depth, pass-through layers, locality, and navigation cost.
- `principle-foundational-thinking` for data shape, ownership, and module structure.
- `principle-boundary-discipline` for framework, transport, persistence, or vendor details crossing the wrong seam.

The principles supply shared rules. This skill owns the architecture review: applying those rules across modules, assessing dependency direction, deciding whether control flow is centralized enough to verify, and identifying useful batch interfaces.

## Review focus

1. Judge abstractions by the complexity they hide at their call sites and the real variation they contain.
2. Define interfaces from consumer needs and keep infrastructure details behind their owning boundary.
3. Keep policy and branching visible in one place when scattering them would make behavior harder to verify.
4. Preserve locality. A helper or layer should own policy, validation, lifecycle, adaptation, or another meaningful responsibility.
5. Prefer batch operations when they remove repeated setup or decisions from a common or hot loop without obscuring per-item failures or ordering.
6. Point dependencies from high-level policy toward narrow ports rather than concrete infrastructure.

Read `references/review-heuristics.md` for a detailed architecture review.

## Output

Order findings by severity. For each finding, name the specialist heuristic or loaded principle, cite the evidence, explain the coupling or maintenance cost, and propose the smallest design change that restores clarity.
