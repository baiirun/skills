---
name: errors-observability
description: Review and improve error handling, retries, fallbacks, logging, and tracing. Use when an AI assistant works on code that handles failures, external services, jobs, requests, production operations, background tasks, or any behavior where debuggability and operational safety matter.
---

# Errors Observability

Use this skill to make failure behavior explicit and diagnosable. Treat errors as part of the interface, not incidental control flow.

## Quick Start

Review failure paths by classifying each expected error and checking the emitted context. Example: a hydration step that can fail from invalid persisted state, a stale version, or a dependency timeout should expose distinct error tags and log one structured outcome at the boundary.

## Review Focus

1. Classify errors by retryable vs non-retryable and recoverable vs non-recoverable.
2. Retry only when the operation is safe, bounded, idempotent, and uses backoff with jitter.
3. Fail fast for non-retryable errors with structured context.
4. Use fallbacks only for recoverable degradation, and log the degradation.
5. Preserve context when wrapping or surfacing errors.
6. Emit structured start and end logs for request and job boundaries.
7. Log decisions, fallbacks, and unexpected states, not only thrown errors.
8. Propagate trace or request IDs across boundaries and correlate logs with traces.

## Heuristics

Read `references/review-heuristics.md` when reviewing production paths, asynchronous jobs, external integrations, retry logic, or logging/tracing changes.

## Output Shape

Return findings ordered by severity. For each finding, identify the failure mode, whether it is retryable or recoverable, the missing operational context, and the smallest safe fix.
