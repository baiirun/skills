---
name: errors-observability
description: Failure design for services and jobs - error classes, safe retries, deliberate fallbacks, structured logs, and tracing. Use when code calls external systems, retries or falls back, or runs as a request handler or background job.
---

# Errors and Observability

Decide failure behavior before writing the happy path. The logging and tracing guidance
assumes a service or job; apply it where requests, jobs, or traces exist.

## Quick Start

List every way the operation can fail, then give each one a class and a response.
Example: a hydration step that can fail from invalid persisted state, a stale version,
or a dependency timeout gets three distinct error tags. Only the timeout is retried,
and the boundary logs one structured outcome.

## Implementation Focus

1. Classify each expected error as retryable or not, and recoverable or not, before
   writing the handler.
2. Retry only operations that are safe, bounded, idempotent, and use backoff with jitter.
3. Fail fast on non-retryable errors, with structured context.
4. Fall back only for recoverable degradation, and log that the fallback happened.
5. Preserve the original error type, cause, stack, and metadata when wrapping, and add
   the operation and key identifiers.
6. Emit structured start and end logs at request and job boundaries.
7. Log decisions, fallbacks, and unexpected states, not only thrown errors.
8. Propagate trace or request IDs across boundaries and include them in logs.

## Principles

- When an operation can be retried, redelivered, or rerun after a crash, call the
  Skill tool with `principle-make-operations-idempotent`.
- When a guard or catch would silence a symptom, call the Skill tool with
  `principle-fix-root-causes`.
- When errors cross a process or service boundary, call the Skill tool with
  `principle-boundary-discipline`.
- When verifying failure paths, call the Skill tool with `principle-prove-it-works`.

## Heuristics

Read `references/implementation-heuristics.md` when implementing production paths,
asynchronous jobs, external integrations, retry logic, or logging and tracing.

## Before You Finish

- Every catch block retries safely, falls back on purpose, or surfaces a structured error.
- Callers can tell failure classes apart without parsing messages.
- One log line at each boundary is enough to explain what happened.
