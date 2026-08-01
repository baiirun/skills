---
name: commit-description-writing
description: Writes durable commit messages with explicit rationale. Use when creating, amending, or squashing commits. This skill requires WHY (problem, root cause/constraint, decision) in addition to WHAT changed.
---

# Commit Description Writing

Write commit messages that read like clear technical prose, not fragmented checklists.

## Non-Negotiables

Every non-trivial commit must include:
1. Problem/context — what issue or need triggered the change
2. Root cause/constraint — why it happened (or what constrained design)
3. Solution/decision — what changed and why this approach
4. Scope/impact — what is affected and what is intentionally unchanged

If these are missing, rewrite.

## Gold Pattern (from strong examples)

Build the message around a causal chain:
1. state the concrete problem/capability,
2. explain the root cause or hard constraint,
3. describe the mechanism that changed,
4. clarify boundaries (what changed vs what stayed the same),
5. add caveats/non-goals only when they are specific and relevant.

This is a writing pattern, not a rigid template.

## Voice and Shape

Aim for readable flow across prose, bullets, and occasional headings.

- Use prose for the core narrative: problem, cause, and decision.
- Use bullets for compact lists (for example, grouped file-area changes or explicit scope boundaries).
- Use headings only when they mark a meaningful topic shift, not as a rigid template.

### Density Rule (No Padding)

Every sentence must add concrete, commit-specific information.

Avoid generic filler like:
- "improves maintainability"
- "reduces complexity"
- "aligns things"

unless tied to explicit mechanism and impact in this commit.

### Diff-Grounded Rule

Do not claim behavior or implementation changes that are not present in the commit diff.

The key requirement is content quality: problem, cause/constraint, decision, and scope should all be easy to find without sounding robotic.

## Subject Line

Use conventional format:

`<type>(<scope>): <high-signal behavior change>`

Examples:
- `fix(editor): remove invalid content holes from leaf node serializers`
- `feat(flight): allow partial stream close without pending chunk errors`
- `chore(flags): remove dormant compiler flags with no active experiments`

Rules:
- Prefer concrete verbs (`remove`, `preserve`, `skip`, `classify`, `harden`)
- Avoid vague terms (`improve`, `cleanup`, `misc fixes`) unless qualified
- Keep concise (target <= 72 chars when practical)

## Context Sufficiency Rule

Do not generate a generic commit from a generic prompt.

If only a weak title exists (`fix: editor`, `chore: upgrades`) and no context is available:
- ask for minimal rationale before drafting, or
- provide a clearly labeled draft with TODO placeholders for Problem/Cause/Decision.

Never present a low-context one-liner as final output.

## Message Patterns by Change Type

### Fix
Explain what was breaking, why it broke, and why this fix is correct.

### Feature/behavior change
Explain motivation, before/after behavior, and compatibility impact.

### Upgrade/chore
Explain why the upgrade/removal was needed, what was touched, and risk boundaries.

### Follow-up
Lead with `Follow up to #<id>`, then explain what gap is closed and current limits.

## Structure Flexibility

Do not enforce a fixed heading style. Choose whatever structure makes the message most readable for the specific change.

A good default for non-trivial commits is:
1. one paragraph on context and why,
2. one section/paragraph on what changed and why,
3. optional short scope/risk/non-goal note when relevant.

For large commits, increase specificity: name major subsystems touched, describe the core reasoning behind each class of change, and bound scope/risk explicitly.

## Value-Only Rule (for optional content)

Only add extra paragraphs/sections when they add concrete value.

Provides value:
- caveats or non-goals that prevent incorrect assumptions
- blast radius or compatibility boundaries that affect rollout
- explicit risk/worst-case notes tied to mechanism
- implicit/tacit knowledge introduced by the change (or required to operate it safely) that would not be obvious from the subject line or quick diff skim

Does not provide value:
- generic filler ("improves maintainability", "reduces risk")
- repeating the subject line in different words
- boilerplate scope statements with no concrete boundary

## Quality Gate

Before finalizing:
- [ ] A reader can answer “why was this needed?” without opening the diff
- [ ] Root cause/constraint is explicit
- [ ] Behavior change is concrete, not adjectival
- [ ] Scope is bounded (what this does not change)
- [ ] Language sounds like precise prose, not template filler

## Anti-Patterns

Bad:
- `fix: editor bug`
- `chore: cleanup`
- `refactor: improve architecture`

Better:
- `fix(editor): remove invalid content holes from TipTap leaf serializers`
- Body explains the ProseMirror invariant and resulting RangeError in plain language

## Output Modes

1. Single final commit message (default)
2. Three subject candidates + recommended one
3. Squash-merge style long-form commit body

Default to mode 1 unless user requests alternatives.
