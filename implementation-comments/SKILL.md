---
name: implementation-comments
description: Add and review local source-code comments that explain why nearby implementation code exists or is written a certain way, especially non-obvious invariants, spec requirements, tradeoffs, failure semantics, and constraints. Use when an AI assistant writes, edits, or reviews inline comments, block comments, workaround notes, deferred-work comments, or commented-out code inside source files.
---

# Implementation Comments

Use this skill to make source comments earn their place. Comments should explain why nearby code is shaped a certain way, which invariant or spec requirement it protects, or what external constraint is not obvious from the implementation.

## Quick Start

Add a comment only where the reader would otherwise miss the local why. Example: a retry loop that deliberately skips a specific provider error should say why the feature contract treats that error as terminal, not describe that the loop iterates attempts.

## Review Focus

1. Explain local intent, constraints, invariants, spec requirements, tradeoffs, and surprising behavior.
2. Avoid comments that merely translate nearby code into prose.
3. Keep comments close to the behavior or invariant they explain.
4. Replace stale, vague, or misleading comments instead of adding more commentary.
5. Prefer clearer code over explanatory comments when a small rename or extraction removes the confusion.
6. Remove deferred-work comments; create tracked work instead of leaving reminders in source.
7. Delete commented-out code unless it documents an intentional disabled path with a clear reason.

## Heuristics

Read `references/review-heuristics.md` when performing a detailed comment review, adding comments to complex implementation code, or deciding whether code should be clarified instead of commented.

## Output Shape

Return findings ordered by severity. For each finding, identify the confusing or misleading source comment behavior, explain the maintenance risk, and propose the smallest change: remove, rewrite, relocate, link to the relevant feature contract, or replace the comment with clearer code.
