---
name: automate-me
description: Create or refresh a personal working-style skill from the user's stated preferences and, when available, recent workspace-scoped conversations.
---

# Automate me

Turn the user's recurring working conventions into one concise `-mode` skill. Preserve an existing mode skill unless the user explicitly wants to start over.

## Find the target

Search the project-local and user-level skill directories exposed by the active harness for matching `*-mode/SKILL.md` files. If the harness does not expose its skill locations, ask the user where the skill should live. Never search unrelated workspaces or private conversation stores.

For an existing skill, use its last modification time as the start of the evidence window. Preserve rules the user has not contradicted.

## Gather evidence

Use the active harness's workspace-scoped conversation history when it is available and authorized. Divide a large history into independent slices only when the harness supports delegation. Look for repeated evidence about:

- response length, tone, and format;
- autonomy and approval boundaries;
- investigation and verification habits;
- code and prose conventions;
- delegation and parallelism;
- git, review, and shipping practices;
- how the user creates and maintains skills.

Require repeated evidence before turning an observed behavior into a rule. Treat a single occurrence as a prompt for confirmation, not a preference.

Ask one or two focused questions about missing or conflicting areas. Use structured choices when the harness supports them; plain chat is fine otherwise.

## Draft

Use the active harness's skill-authoring guidance when available. Otherwise follow the standard skill shape: a folder named after the skill, a `SKILL.md` with `name` and `description` frontmatter, and only the supporting files the workflow needs.

Place the skill in the existing location when updating. For a new skill, use the project-local or user-level skill directory chosen by the user. Keep invocation policy in harness-specific metadata only when the user requests it and the target harness supports it; keep the `SKILL.md` itself portable.

Organize only the sections supported by evidence. Useful categories include response style, autonomy, investigation, delegation, code and prose discipline, verification, and delivery process. Do not copy another person's mode skill.

Apply the `unslop` skill to the draft. Show the draft, incorporate feedback, validate its frontmatter and references with whatever skill validator is available, then save it. Do not commit, push, or open a pull request unless the user asks.

## Guardrails

- Keep conversation access scoped to the active workspace.
- Do not encode secrets, private transcript text, or identifying details as examples.
- Do not restate generic agent behavior.
- Reference other installed skills by name instead of copying them.
- Prefer a short operational rule over a long rationale.
- If no conversation history is available, build the skill from the user's answers instead of blocking.
