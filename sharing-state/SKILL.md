---
name: sharing-state
description: Concurrent writers and operations that rerun. Use when several actors (threads, processes, agents, jobs) may write the same file, branch, key, or state object, or when work must survive crashes and retries.
---

# Sharing State

Before writing the code, read each principle whose condition matches the work. They are short; read them in full rather than from memory of their titles.

| When the work involves | Read |
|---|---|
| Concurrent actors that may write the same file, branch, key, or state object | `principles/separate-before-serializing-shared-state.md` |
| Work that may run twice or resume after a crash | `principles/make-operations-idempotent.md` |
| Choosing data structures that several actors will share | `principles/foundational-thinking.md` |

Done when: every row whose condition matches the work has had its principle read in full, and the code follows it, including its test where it has one.
