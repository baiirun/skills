# Classify Failures

> Apply when writing code that can fail: external calls, I/O, parsing, jobs, or request handlers. Decide each failure's class and response before writing the happy path, and keep error context intact.

Errors are part of the interface, not incidental control flow. List every way an operation can fail, then give each one a class and a response before writing the happy path.

A hydration step that can fail from invalid persisted state, a stale version, or a dependency timeout gets three distinct error tags. Only the timeout is retried.

**Classify each expected failure:**
- Retryable or not, and recoverable or not.
- User-caused, programmer error, or environment.

**The pattern:**
- Fail fast on non-retryable errors, with structured context.
- Write handlers that can tell failure classes apart. A generic catch block can't.
- Use typed errors, tagged results, or structured error metadata when callers handle classes differently.
- When wrapping an error, keep its type, cause, and stack, and add the operation name and key identifiers: request ID, entity ID, user ID, job ID, provider, attempt number. A message like `"<operation> failed: " + message` discards all of that.
- Swallow an error only when the code retries safely, falls back on purpose, or surfaces a structured failure instead.

**The test:** Can a caller tell every failure class apart without parsing a message string? Does every catch block retry, fall back, or surface?
