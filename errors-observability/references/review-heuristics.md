# Errors and Observability Review Heuristics

## Error Classification

- Flag generic catch blocks that cannot distinguish retryable, recoverable, user-caused, and programmer errors.
- Flag swallowed errors unless the code retries safely, falls back intentionally, or surfaces a structured failure.
- Preserve operation names and key identifiers such as request ID, entity ID, user ID, job ID, provider, and attempt number.
- Prefer typed errors, tagged results, or structured error metadata when downstream handling depends on classification.

## Retries and Fallbacks

- Retry only idempotent operations or operations protected by idempotency keys.
- Require bounded attempts, exponential backoff, jitter, and clear final failure handling.
- Do not retry validation errors, authorization failures, missing required inputs, or deterministic business-rule failures.
- Log fallback activation with enough context to diagnose impact.
- Choose fail-open or fail-closed deliberately. Auth, permissions, and destructive writes should fail closed.

## Logging

- Request and job boundaries should have canonical start and end logs.
- Start logs should include immutable context: request ID, actor, inputs, mode, feature flags, and target entity.
- End logs should include outcome, duration, status, error class, retry count, and important result metrics.
- Prefer wide structured events over many tiny log lines.
- Do not sample out errors. Sample noisy successful hot paths instead.

## Tracing

- Propagate trace or request IDs across process, queue, HTTP, database, and worker boundaries.
- Add spans around hot-path I/O: database calls, queues, external APIs, cache, and file operations.
- Ensure logs include the trace or request ID used by tracing.
