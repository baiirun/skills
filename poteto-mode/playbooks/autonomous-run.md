### Autonomous run

**You own the exit condition. Define done, then drive to it without stopping.** Use for "going to bed", "run until done", or a request to keep monitoring until a condition holds.

1. State the exit condition as a checkable predicate before the first iteration (tests green, repro fixed, all N PRs merged, pixel-diff zero). A vague goal stalls; a predicate lets you stop.
2. Pick the wake mechanism exposed by the active harness. Prefer event-based watching for CI, merges, and ref changes, with a time-based heartbeat as fallback. Without an event source, use a fixed interval sized to when the result is worth checking again.
3. Each iteration makes the smallest change the evidence justifies, verifies it against the predicate, commits if it advanced, discards changes that didn't help. Belt-and-suspenders that "might help" gets reverted, not left to ride.
   Sequence the work via the **sequence-verifiable-units** principle skill, verifying each unit before the next instead of batching checks at the end.
4. Address in-scope broken skills, related bugs, flaky verifiers, review noise, tooling failures, and fixable drift. Put unrelated fixes in their own proposal or PR only when the user authorizes that expanded scope. Ask only for irreversible actions, external writes, genuine product choices, or a real dead end. Keep the predicate as the main drive.
5. Checkpoint every iteration via the **show-me-your-work** skill, a row for what changed and whether the predicate moved. A run with no trail can't be audited or resumed.
6. Stop when the predicate is met. A plateau is not a stop, so keep going and pivot your approach to push past it. Surface a genuine dead end rather than spinning, and never relax the predicate to declare victory.

**Reply:** the exit condition, iterations run, what landed, what was discarded, final predicate state.
