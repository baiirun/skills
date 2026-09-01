### Opening a PR

Invoked at the end of every other playbook.

**Worktree.** Work from a git worktree off the target branch. Give each concurrent writer its own worktree. Never reset or overwrite a dirty worktree. Preserve unrelated changes and move the requested work into a fresh worktree when necessary.

**Commits.** Commit liberally; rebase into small, ordered commits before opening PRs. Each commit is a future PR: landable, ordered to tell the story. Amend when the fix belongs in a just-made commit; new commit when separable.

**PRs.** Inspect the diff for generated filler and accidental complexity before commit. Run `no-comments` before review. Write the PR title, description, and commit body with `technical-writing`, then apply `unslop`. Open or update the PR only when the user asked for that external action.

**Titles.** Use Conventional Commits in the form `type(scope): subject`. Use `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, or `perf` as the type. Use the changed area, such as `pstack` or `poteto-mode`, as the scope. Keep the subject short and imperative. Apply the same `technical-writing` and `unslop` pass as the body. Name a real symbol when one carries the change. For example, `fix(pstack): retarget opening-a-pr babysit trigger`. Do not add a trailing period.

**Descriptions.** Use these sections in order. Drop a section when it is empty.

- `## Why`. State the intent and why this approach fits.
- `## Scope`. State facts from the diff. Name real symbols and paths. Name both sides of a rename or retarget. State what is in and out when the boundary matters.
- `## Tradeoffs`. State real choices only. Skip this section when there are none.
- `## Blast Radius`. State who and what the change touches. Explain why the change is safe or risky. If main is red without the fix, name the continuing cost.
- `## Verification`. State how you ran each check and its rigor. Name the real path, such as `control-cli`, `control-ui`, or the targeted tests. State the outcome of each check, not only the command name.

After these sections, attach videos or screenshots when they prove a claim. Do not use `## Summary` or `## Test plan` boilerplate. A commit body does not restate its subject.

**Size and stacks.** Prefer five narrow PRs to one large PR. Stack follow-ups with Graphite (`gt`), and keep the ordered stack visible to reviewers. Branch from main only for independent work. Rebase on `main` before substantial stack work.

**Readiness.** Respect the user's requested draft or ready state. If unspecified, infer from whether the work and verification are complete. Verify the live PR state through the hosting service before reporting it.

**Babysit.** Opening a PR does not start a babysit. Post the URL and keep building. Finish the phase or stack first. Run a separate babysit pass only when the user asks for one after the whole stack exists. A babysit for each new PR stalls the build and spends checks on commits that later waves restart. Push back when feedback drifts from intent.

A delegated worker that opens a PR runs `interrogate`, a diff-cleanup pass, and `no-comments`. It returns the URL and does not babysit. Return to the parent.
