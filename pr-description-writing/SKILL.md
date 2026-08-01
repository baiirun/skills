---
name: pr-description-writing
description: Writes high-context PR descriptions for reviewers and future readers. Use when opening or updating pull requests. This skill enforces explicit WHY (problem, cause/constraint, decision) and clear before/after behavior.
---

# PR Description Writing

Write PR descriptions as readable technical narrative. Prioritize flow and clarity over excessive sectioning.

## Non-Negotiables

Every PR description must still communicate:
1. Why now — underlying issue, pain, or constraint
2. What changed — grouped and concrete
3. Before vs after behavior — not just file edits
4. Scope boundaries — what remains unchanged

If WHY is missing, the description is incomplete.

## Gold Pattern (from strong examples)

Build the description around a causal chain:
1. state the concrete capability/problem being addressed,
2. explain the root cause or hard constraint,
3. describe the implementation mechanism that changed,
4. clarify boundaries (what changes in which context, and what does not),
5. close with non-goals, risks, or compatibility notes only when they are real and specific.

This is a writing pattern, not a rigid template.

## House Style

Aim for readable flow across prose, bullets, and occasional headings.

- Use prose to carry reasoning and narrative continuity.
- Use bullets when listing grouped changes, risks, or decisions is clearer than paragraph form.
- Use headings only when they introduce a genuinely new topic (for example: rationale, behavior impact, compatibility), not to fragment every thought.

### Density Rule (No Padding)

Every sentence must add concrete, PR-specific information.

Avoid generic filler such as:
- "this improves maintainability"
- "this reduces risk"
- "this keeps things aligned"

unless immediately tied to specific mechanisms in the diff.

Prefer:
- concrete cause/effect statements
- explicit behavior changes
- named subsystems/files only when relevant

### Diff-Grounded Rule

Do not claim changes that are not in this PR.

For "what changed" bullets, tie each point to actual modified files or code paths in the PR. Do not blend in adjacent PR context unless explicitly labeled as external context.

Do not include a dedicated **Test Plan** section by default. If validation details matter, include a brief `Validation` note.

## Depth Scaling (Important)

Match depth to PR size and risk.

For larger PRs (roughly >10 files changed, cross-cutting subsystems, or infra/runtime changes), include enough detail to answer:
- which subsystems changed and why each was touched
- the key design/implementation decisions (not just file movement)
- user-visible and operator-visible behavior impact
- risk boundaries and what was intentionally deferred

Avoid shallow summaries like "upgraded dependencies" for broad upgrade PRs; call out notable version jumps and the classes of compatibility edits they required.

## Context Sufficiency Rule

Do not publish an empty or hand-wavy PR body.

If context is insufficient (for example title-only: `fix: editor`):
- ask for missing rationale before finalizing, or
- draft with explicit TODO placeholders for problem, cause, and decision.

Never leave PR body blank when opening/updating.

## Preferred Structure

Use this default shape unless the PR is tiny:

1. Open with one paragraph that explains what is being solved and why. The why must be explicit and evidence-based, not assumed.
2. Add a "what changed and why" section. Use bullets when grouping changes by subsystem makes the review faster.
3. Add further sections only if they provide decision-relevant value.

For larger or architectural PRs, include a dedicated before/after subsection when it clarifies behavior changes.

## Value-Only Rule (for optional sections)

Only add sections like non-goals, risks, blast radius, migration, or dependency context when they add concrete value for a reader.

Provides value:
- clarifies a non-goal that reviewers might otherwise assume is included
- identifies a real risk surface and mitigation
- states migration/rollout requirements or ordering constraints
- explains blast radius across environments/systems
- calls out implicit/tacit knowledge introduced by the change (or required to operate it safely), especially details a reviewer would likely miss from a quick diff scan

Does not provide value:
- generic "risk is low" statements with no mechanism
- repeating obvious facts already clear from the title/diff
- boilerplate compatibility language with no concrete boundary
- sections added just to fill format

## Variant: Upgrade/Chore PRs

Even for upgrades, include rationale in prose:
- why upgrade/removal now (security, compatibility, unblock)
- what was upgraded/removed at a meaningful level
- risk/mitigation and non-impact boundaries

## Reasoning Patterns to Encode

When relevant, include these ideas naturally in prose:
- standards/security compatibility contracts
- targeted compiler/runtime assumptions and worst-case outcomes
- cleanup/removal selection criteria
- phase-specific streaming/render behavior (shell flush vs streamed completion)
- follow-up context (`Follow up to #<id>`) when applicable

## PR Title Guidance

Use conventional format:

`<type>: <pull request title>`

Examples:
- `fix: avoid content-hole serialization in TipTap leaf nodes`
- `feat: allow partial Flight stream closure without pending chunk errors`

Choose type by intent (`feat`, `fix`, `chore`, `refactor`, `proposal`, etc).

## Quality Gate

Before finalizing:
- [ ] WHY is explicit and specific
- [ ] Behavior change is clear in plain language
- [ ] Scope boundaries are explicit
- [ ] Compatibility note is present
- [ ] Description reads naturally and is useful without diff deep-dive
- [ ] No filler sentences that could apply to any PR

## Anti-Patterns

Bad:
- “Improves reliability” with no cause/mechanism
- file list with no narrative
- broad claims without behavior details
- overly rigid boilerplate that feels robotic

Better:
- concise technical narrative with explicit symptom + cause + decision
- concrete before/after behavior
- explicit non-impact or migration guidance

## Output Modes

1. Full PR description (default)
2. Concise PR description (small/safe changes)
3. Detailed squash-merge description

Default to mode 1 unless user asks otherwise.
