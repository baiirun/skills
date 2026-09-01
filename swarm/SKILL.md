---
name: swarm
description: "Fan out N parallel workers, drain them, and return one report. Use for swarm, 'swarm this', or parallel coverage, races, gauntlets, and exploration."
---

# Swarm

Fan out N workers when the active harness supports delegation. They may cover separate slices, race the same brief, or mix both. The parent waits, aggregates, and returns one report. If delegation is unavailable, run the slices sequentially and state that limitation.

## Start

Open a todolist with one entry per phase before launching anything.

1. Frame
2. Fan out
3. Aggregate
4. Report

## Phase A: Frame

1. State the done predicate and the artifact or report the swarm must return.
2. Choose the shape. Partition into slices, race N workers on identical briefs, or mix both. For a race or mixed shape, declare `first pass`, `rank all`, or `best-of` before spawning.
3. Set N from the user or derive it from the shape. N is total workers, not the cloud concurrency limit.
4. Pick the worker model from `swarm-workers` in the optional pstack model configuration when available. Otherwise inherit the parent model. For a model race, name each arm's model up front; if the harness cannot select models, race prompts or approaches instead.
5. Give each worker its own writable output when it writes. Use a worktree, branch, or `/tmpswarm-<slug>/worker-<n>/`.

## Phase B: Fan out

Launch all N workers together through the harness's delegation mechanism. Request background execution when supported. Use remote workers only when their environment has the required repository and credentials; use local workers for local-only resources. When workers edit code, isolate them with separate worktrees or branches and tell each worker its base revision explicitly.

Every brief stands alone. Include the goal, scope, exact slice or race arm, how to verify, and what to report. Reports use `PASS`, `ISSUES`, or `BLOCKED` with evidence.

If a worker drops out, proceed with N-1 and note it.

## Phase C: Aggregate

Read the terminal results. For coverage, every required slice needs a result. For a race, apply the selection rule declared up front. Use first pass, rank all, or best-of. Do not paste raw worker dumps.

Keep a compact result table, one-line evidenced issues, and explicit gaps or dropouts.

## Phase D: Report

Return one consolidated in-chat report with the table, issue one-liners, gaps or dropouts, and the race rule when used.
