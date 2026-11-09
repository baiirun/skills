---
name: feature-contract-docs
description: Feature docs written as contracts (purpose, scope, MUST and MUST NOT rules, interfaces, implementation model, verification). Use when creating or updating feature docs, capability docs, or ADR-like records.
---

# Feature Contract Docs

The document should let a future agent understand why the feature exists, what
contract it must preserve, and how the implementation relates to that contract.

## Quick Start

Before writing, read the implementation, tests, existing docs, and any issue or spec.
Then write the feature as a contract, not an implementation tour or a progress log. If
the feature went through `skeleton-first`, its contracts and invariants are the
starting point.

## Required Shape

1. Purpose: why this feature exists and what user or system need it serves.
2. Scope: what the contract covers, with explicit non-goals where they prevent ambiguity.
3. Behavior Contract: normative MUST, SHOULD, and MUST NOT statements for flows and
   invariants.
4. Interfaces: user and API surfaces, events and messages, persisted entities,
   configuration, external systems.
5. Implementation Model: where responsibility lives, how the main pieces collaborate,
   and why the design is shaped this way.
6. Verification: how a human or agent can prove the contract still holds.
7. Notes: optional non-normative context, kept separate from the contract.

## Writing Focus

1. Tie every major implementation choice to a purpose, invariant, spec requirement, or
   external constraint.
2. State forbidden behavior and illegal states as MUST NOT statements.
3. Separate source-of-truth facts from derived, cached, or display-only state.
4. Name stable semantic interfaces instead of touring files.
5. Record tradeoffs and rejected alternatives only when they explain the current shape.
6. Put deferred work in non-goals or tracked work.
7. Tie verification to observable contract behavior, not incidental implementation details.

## Principles

- When writing the purpose and scope, call the Skill tool with
  `principle-experience-first`.
- When naming the feature's concepts and states, call the Skill tool with
  `principle-model-the-domain`.
- When writing the verification section, call the Skill tool with
  `principle-prove-it-works`.

## Heuristics

Read `references/implementation-heuristics.md` when writing a feature contract,
deciding between a feature contract and an ADR, or deciding whether an implementation
change needs a doc update.

## Before You Finish

- Every MUST and MUST NOT is something a test or a person could check.
- The doc would survive renaming every file it mentions.
- Changed behavior in this change is reflected in the contract.
