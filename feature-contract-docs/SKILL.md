---
name: feature-contract-docs
description: Write and review durable feature documentation covering purpose, scope, behavior, invariants, interfaces, implementation ownership, tradeoffs, and verification. Use for feature docs, capability docs, implementation notes, or ADR-like records that must preserve behavior across code changes.
---

# Feature Contract Docs

This is an artifact skill. It produces or reviews durable feature documentation; it is not a general review principle.

Inspect the implementation, tests, existing docs, and available product or issue context before writing. Describe the contract and ownership model, not a file tour or progress log.

## Principles to load

- `principle-experience-first` for the user or operator outcome the feature exists to provide.
- `principle-model-the-domain` for stable concepts, states, and terminology.
- `principle-prove-it-works` for executable or observable verification.

## Required shape

1. Purpose: the user or system need.
2. Scope: what the contract covers and the non-goals needed to prevent ambiguity.
3. Behavior contract: testable MUST, SHOULD, and MUST NOT statements.
4. Interfaces: user and API surfaces, events, persisted entities, configuration, and external systems.
5. Implementation model: responsibility, ownership, collaboration, and the reasons behind the shape.
6. Verification: how a human or agent can prove the contract still holds.
7. Notes: optional non-normative context kept separate from the contract.

## Review focus

- Tie major implementation choices to a purpose, invariant, requirement, or external constraint.
- Separate source-of-truth state from derived, cached, and display-only state.
- Name stable semantic interfaces instead of fragile file paths.
- Record tradeoffs only when they explain the current shape or prevent a likely mistake.
- Keep deferred work in the project's tracking system.

Read `references/review-heuristics.md` for document placement and contract-quality checks.

## Output

When writing, use the required shape with concise sections. When reviewing, order findings by severity and cite the missing or stale contract knowledge, its consequence, and the smallest documentation fix.
