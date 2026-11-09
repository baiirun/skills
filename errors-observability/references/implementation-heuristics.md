# Errors and Observability Implementation Heuristics

## Error Classification

- Write handlers that can tell retryable, recoverable, user-caused, and programmer
  errors apart. A generic catch block can't.
- When wrapping an error, keep `cause` and add structured metadata. Don't just write
  `new Error("<operation> failed: " + message)`.
- Swallow an error only when the code retries safely, falls back on purpose, or
  surfaces a structured failure instead.
- Attach the operation name and key identifiers: request ID, entity ID, user ID, job
  ID, provider, attempt number.
- Use typed errors, tagged results, or structured error metadata when callers handle
  classes differently.

## Retries and Fallbacks

- Retry only idempotent operations, or operations protected by idempotency keys.
- Bound attempts, use exponential backoff with jitter, and define the final failure.
- Don't retry validation errors, authorization failures, missing required inputs, or
  deterministic business-rule failures.
- Log fallback activation with enough context to judge its impact.
- Choose fail-open or fail-closed on purpose. Auth, permissions, and destructive writes
  fail closed.

## Logging

- Give request and job boundaries one canonical start log and one end log.
- Start logs carry immutable context: request ID, actor, inputs, mode, feature flags,
  target entity.
- End logs carry outcome, duration, status, error class, retry count, and key result
  metrics.
- Emit wide structured events instead of many small log lines.
- Never sample errors. Sample noisy successful hot paths instead.

## Tracing

- Propagate trace or request IDs across process, queue, HTTP, database, and worker
  boundaries.
- Add spans around hot-path I/O: database calls, queues, external APIs, cache, file
  operations.
- Include the trace or request ID in every log line on the traced path.
