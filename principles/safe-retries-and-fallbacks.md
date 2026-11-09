# Safe Retries and Fallbacks

> Apply when adding a retry, a fallback, or a default behavior on failure. Retry only safe, bounded, idempotent operations; fall back only on purpose and visibly; choose fail-open or fail-closed deliberately.

A retry or fallback changes what the system does when something goes wrong. Make that change on purpose.

**Retries:**
- Retry only idempotent operations, or operations protected by idempotency keys (see [make-operations-idempotent](make-operations-idempotent.md)).
- Bound attempts, use exponential backoff with jitter, and define the final failure.
- Leave validation errors, authorization failures, missing required inputs, and deterministic business-rule failures unretried. Retrying them can't change the result.

**Fallbacks:**
- Fall back only for recoverable degradation.
- Log fallback activation with enough context to judge its impact.
- Choose fail-open or fail-closed on purpose. Auth, permissions, and destructive writes fail closed.

**The test:** What happens if this retry runs five times? If this fallback fires all day, would anyone know?
