---
name: setup-pstack
description: Configure optional per-role model preferences for pstack. Use for "setup pstack", "configure pstack models", or changing pstack's model choices.
---

# Setup pstack

Create or update an optional pstack model configuration without assuming a particular agent harness.

## Configuration location

Use the first applicable location:

1. The path in `PSTACK_MODEL_CONFIG`.
2. `.pstack/models.yaml` in the current project when the user wants project-local settings.
3. `${XDG_CONFIG_HOME:-$HOME/.config}/pstack/models.yaml` for user-level settings.

Do not write configuration until the user chooses project-local or user-level scope.

## Workflow

1. Ask the active harness which model identifiers are available for delegated work, if it exposes that information. If model selection is unsupported, use `inherit-parent` for every role.
2. Read an existing configuration from the chosen location.
3. Show the current role mapping. Mark identifiers that the active harness cannot resolve.
4. Ask the user to confirm changes. Lists control the number of parallel reviewers or candidates.
5. Validate every explicit identifier against the active harness. `inherit-parent` is always valid.
6. Write YAML in this shape:

```yaml
refactoring: inherit-parent
bug-fix: inherit-parent
perf-issue: inherit-parent
hillclimb: inherit-parent
judgment: inherit-parent
prose: inherit-parent
hardest-tasks: inherit-parent
how-explorer: inherit-parent
how-explainer: inherit-parent
how-critics:
  - inherit-parent
why-investigators: inherit-parent
why-synthesizer: inherit-parent
reflect-tooling: inherit-parent
reflect-judgment: inherit-parent
reflect-divergent: inherit-parent
reflect-synthesizer: inherit-parent
arena-runners:
  - inherit-parent
  - inherit-parent
arena-cross-judge-pool:
  - inherit-parent
swarm-workers: inherit-parent
interrogate-reviewers:
  - inherit-parent
  - inherit-parent
```

Skills must treat this file as an optional preference layer. If the file, a role, model selection, or delegation is unavailable, inherit the parent model and continue with the capabilities the harness provides.

After writing, report the exact path and note that availability is checked again at execution time.
