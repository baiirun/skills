# Observable Boundaries

> Apply when writing request handlers, jobs, workers, or calls across process and service boundaries. Emit one structured start and end event per boundary, log decisions as well as errors, and propagate trace IDs. Service- and job-oriented.

An operator should be able to explain what happened at a boundary from its logs alone.

**Logging:**
- Give request and job boundaries one canonical start log and one end log.
- Start logs carry immutable context: request ID, actor, inputs, mode, feature flags, target entity.
- End logs carry outcome, duration, status, error class, retry count, and key result metrics.
- Log decisions, fallbacks, and unexpected states, not only thrown errors.
- Emit wide structured events instead of many small log lines.
- Never sample errors. Sample noisy successful hot paths instead.

**Tracing:**
- Propagate trace or request IDs across process, queue, HTTP, database, and worker boundaries.
- Add spans around hot-path I/O: database calls, queues, external APIs, cache, file operations.
- Include the trace or request ID in every log line on the traced path.

**The test:** From one boundary's end log, can you tell what was asked, what happened, how long it took, and which trace to open?
