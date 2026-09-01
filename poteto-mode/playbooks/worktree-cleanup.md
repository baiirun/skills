### Worktree and simulator cleanup

**You own the disk and the safety gate.** Prune merged or abandoned git worktrees and stale iOS simulators to reclaim space. Deletion is irreversible, so every step guards against deleting something in use or holding uncommitted work.

1. Snapshot and audit. Record `df -h /`, then run `scripts/worktree-audit.sh`. It reads paths from `git worktree list`, including worktrees stored in tool-managed directories. It classifies each by size, age, merge state, uncommitted work, PR state, and, when `PSTACK_TRANSCRIPTS_DIR` points to a workspace-scoped transcript export, the newest chat that touched it.
2. The bucket is advice, not permission. The pinned and active chats are the real artifact (principle-prove-it-works). Get that set from the user or sidebar and cross-check every candidate. The lever has marked `safe` a worktree the user had pinned, so the pinned set wins.
3. Verify usage before deleting. For every `verify-recent-chat` row, or anything you doubt, use delegated workers when available to inspect the workspace-scoped transcripts. Otherwise inspect them directly. Pinned or ongoing worktrees remain in use even when their names are not visible in the main workspace list.
4. Pause on irreversible loss. `wip:N` is N tracked uncommitted edits. Show the diff and get a decision first, since removing a clean worktree is recoverable from its branch but uncommitted work is gone. `scratch:N` is untracked throwaway, safe to drop, but name the files. Per Autonomy, clean and merged and not-in-use proceeds; `wip` and in-use pause.
5. Ask for explicit confirmation of the exact paths before deletion. Remove each confirmed clean worktree with `git worktree remove <path>`, using `--force` only when the user approved discarding the named untracked or ignored files. Move leftover directories to trash when practical, then run `git worktree prune`. Confirm with `df -h /` and re-list.
6. Simulators and other reclaimers. Simulators are usually the next-biggest win. Inspect before deleting. Other candidates include Xcode `DerivedData` and `iOS DeviceSupport`, harness caches, and package-manager caches. Clear only confirmed disposable data within the user's requested scope.

This is the one playbook that deletes user state with no code review to catch a slip, so the gates above are the review.

**Reply:** `df -h /` before and after with space reclaimed, the worktrees pruned, and a one-line reason for each held back (in-use by which chat, or uncommitted work).
