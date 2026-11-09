---
name: implementation-comments
description: Why-comments in source code, and clearer code where a rename or extraction does the job. Use when writing or editing code comments, workaround notes, or commented-out code.
---

# Implementation Comments

This skill owns the repository's general policy for source comments. Comment once the
code is close to final. A comment earns its place by telling the reader something the
code can't: why it's shaped this way, which invariant or spec requirement it protects,
or which external constraint forces it.

For an explicit, aggressive cleanup pass that removes comments and suppressions, the
user runs `no-comments`, which uses this skill for policy.

## Quick Start

For each spot a reader might stop and ask "why?", first try to make the code answer it
with a rename or small extraction. If it still can't, write one comment with the
reason. Example: a retry loop that deliberately skips a provider error says why that
error is terminal, not that the loop iterates attempts.

## Implementation Focus

1. Write comments that explain local intent, constraints, invariants, spec
   requirements, tradeoffs, and surprising behavior.
2. Put each comment right next to the behavior or invariant it explains.
3. When you change code, update or delete the comments that describe it.
4. Rename or extract before commenting, when that removes the confusion.
5. Track deferred work outside the source, in the project's tracker.
6. Delete commented-out code, unless it's an intentionally disabled path with a stated
   reason.

## Principles

- When a comment narrates code or adds reading cost, call the Skill tool with
  `principle-minimize-reader-load`.
- When a type, assertion, test, name, or lint rule could enforce what the comment
  says, call the Skill tool with `principle-encode-lessons-in-structure`.

## Heuristics

Read `references/implementation-heuristics.md` when commenting complex code, deciding
whether to clarify code instead of commenting, or writing workaround notes.

## Before You Finish

- Every comment states a why the code can't show.
- Deferred work is tracked outside the source, and no commented-out block was added.
