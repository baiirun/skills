---
name: handling-failure
description: Failure design: error classes, retries, fallbacks, idempotency, logs, and tracing. Use when code calls external systems, can fail, retries or falls back, or runs as a request handler or job.
---

# Handling Failure

Before writing the code, read each principle whose condition matches the work. They are short; read them in full rather than from memory of their titles.

| When the work involves | Read |
|---|---|
| Any code that can fail | `principles/classify-failures.md` |
| Adding a retry, a fallback, or default behavior on failure | `principles/safe-retries-and-fallbacks.md` |
| An operation that can be retried, redelivered, or rerun after a crash | `principles/make-operations-idempotent.md` |
| Request handlers, jobs, workers, or calls across services | `principles/observable-boundaries.md` |
| Errors crossing a process or service boundary | `principles/boundary-discipline.md` |
| A guard or catch that would silence a symptom | `principles/fix-root-causes.md` |

Done when: every row whose condition matches the work has had its principle read in full, and the code follows it, including its test where it has one.
