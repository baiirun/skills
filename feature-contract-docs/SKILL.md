---
name: feature-contract-docs
description: Write and review durable feature documentation that models why a feature exists, its scope and non-goals, behavior contract, invariants, interfaces, implementation model, tradeoffs, and verification. Use when an AI assistant creates or updates feature docs, capability docs, implementation notes, ADR-like records, or documentation that should preserve product and system behavior across complex codebases.
---

# Feature Contract Docs

Use this skill to preserve implementation knowledge at the feature level. The document should let a future agent understand why the feature exists, what contract it must preserve, and how the implementation relates to that contract.

## Quick Start

Before writing, inspect the implementation, tests, existing docs, and issue or spec context. Then document the feature as a contract: purpose, scope, invariants, interfaces, implementation model, and verification. Do not write an implementation tour or progress log.

## Required Shape

1. Purpose: why this feature exists and what user or system need it serves.
2. Scope: what the contract covers, with explicit non-goals when they prevent ambiguity.
3. Behavior Contract: normative MUST, SHOULD, and MUST NOT statements for flows and invariants.
4. Interfaces: user/API surfaces, events/messages, persisted entities, configuration, and external systems.
5. Implementation Model: where responsibility lives, how the main pieces collaborate, and why the design is shaped this way.
6. Verification: how a human or agent can prove the contract still holds.
7. Notes: optional non-normative context, kept separate from the contract.

## Review Focus

1. Anchor every major implementation choice to a purpose, invariant, spec requirement, or external constraint.
2. Make illegal states and forbidden behavior explicit with MUST NOT statements.
3. Separate source-of-truth facts from derived, cached, or display-only state.
4. Name stable semantic interfaces instead of fragile file tours.
5. Capture important tradeoffs and rejected alternatives only when they explain current implementation shape.
6. Keep deferred work out of source comments; use explicit non-goals or tracked work instead.
7. Keep verification tied to observable contract behavior, not incidental implementation details.

## Heuristics

Read `references/review-heuristics.md` when writing or reviewing a feature contract, deciding whether a doc should be a feature contract or ADR, or checking whether implementation changes require documentation updates.

## Output Shape

When writing docs, produce the required shape using concise sections. When reviewing docs, return findings ordered by severity; for each finding, name the specific heuristic that produced the finding, identify the missing or stale contract knowledge, cite the concrete evidence, explain the risk for future implementation work, and propose the smallest documentation or code-linking fix.
