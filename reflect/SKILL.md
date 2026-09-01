---
name: reflect
description: Spawn three parallel review subagents over the active transcript, surface learnings, and route each to a concrete edit on an existing skill. Use when the user says reflect.
---

# Reflect

Mine the current conversation for durable learnings, then route them into skill edits.

## When to invoke

- The user said "reflect" or "reflect".
- A complex task (5+ tool calls) just landed cleanly and the recipe is worth keeping.
- The agent hit dead ends, found the working path, and the path generalizes.
- The user corrected the agent's approach mid-task.
- A non-trivial workflow emerged that isn't captured anywhere.

Skip when the conversation is trivial, off-topic, or already covered by an existing skill the parent followed correctly. One-offs are not learnings.

## Process

### 1. Locate the active conversation

Use the active harness's current-conversation export, transcript API, or workspace-scoped transcript path when available. Never search unrelated workspaces or global conversation stores. If no transcript mechanism is exposed, write a tight digest of the session and use that instead.

### 2. Run three reviewers

Run the judgment, tooling, and divergent lenses through the harness's delegation mechanism when available. Use `reflect-judgment`, `reflect-tooling`, and `reflect-divergent` from the optional pstack model configuration; otherwise inherit the parent model. Launch them together when concurrency is supported. If delegation is unavailable, run the three templates sequentially.

| Lens | Prompt template |
|---|---|
| Judgment | `references/judgment-reviewer.md` |
| Tooling | `references/tooling-reviewer.md` |
| Divergent | `references/divergent-reviewer.md` |

Pass each template verbatim, substituting the transcript path or digest where marked. Reviewers may use available read-only connectors to verify references, but they must not write files or mutate external systems. The parent applies approved edits.

### 3. Synthesize

Run one synthesizer using `reflect-synthesizer` from the optional pstack configuration or the inherited parent model. Use `references/synthesizer.md` verbatim, with each reviewer's full output inlined where marked. It may use available read-only connectors to spot-check citations, but it must not edit files or external systems. If delegation is unavailable, synthesize in the parent with the same template.

### 4. Structural enforcement check

Sanity-check the synthesizer's Accepted list. For any item that would be enforced more reliably by a lint rule, script, metadata flag, or runtime check, move it from Accepted to Backlog. The synthesizer already applies this criterion; this is a final pass before edits land. See the **encode-lessons-in-structure** principle skill.

### 5. Apply

Before applying any Accepted edit, present the synthesizer's full Accepted/Rejected/Backlog output to the user and wait for explicit approval. The user picks which subset to apply and may redirect routings. Skill changes affect every future agent in the org; do not auto-apply.

Do not file backlog items automatically. Ask before creating or changing anything in an external tracker.

For each approved Accepted item, follow the Routing field exactly:

- Trivial existing-skill edit (a one-line bullet, a tightened sentence, a stale fact corrected): parent does directly.
- Substantive existing-skill edit: use the active harness's skill-authoring guidance when available, then draft, validate, and iterate.
- `tune description: <skill path>`: optimize the description against realistic triggering and non-triggering requests.
- `new skill: <kebab-name>`: follow the standard skill structure and validate it before installation.

If your environment ships a SKILL.md validator, run it on every touched skill before declaring done. Skip this step if it doesn't.

### 6. Summarize for the user

Short list, no preamble:

- Edits applied: `<skill path>`. What changed, one line each.
- New skills created: `<skill path>`. One line each (rare).
- Backlog filed to the devex tracker: `<issue title>` (`<tags>`). One line each.
- Dropped: one line per rejected finding + reason from the synthesizer.
