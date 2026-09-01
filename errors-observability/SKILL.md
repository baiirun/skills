---
name: errors-observability
description: Review and improve error classification, retries, fallbacks, logging, tracing, and operational diagnosis. Use for external services, jobs, requests, background work, and other failure-sensitive production paths.
---

# Errors and Observability

Review whether failures are safe to handle and possible to diagnose from production evidence.

## Principles to load

- `principle-fix-root-causes` for symptom guards and error handling that hides the underlying defect.
- `principle-make-operations-idempotent` for retries and repeated delivery.
- `principle-boundary-discipline` for preserving error meaning across process and service boundaries.
- `principle-prove-it-works` for failure-path verification and operational evidence.

The principles supply shared rules. This skill owns failure classification, retry and fallback policy, structured event design, trace propagation, and the practical question of whether an operator can diagnose the outcome.

## Review focus

1. Classify expected failures by retryability, recoverability, and responsibility.
2. Retry only safe, bounded operations with backoff, jitter, and a clear terminal outcome.
3. Use fallbacks only for deliberate recoverable degradation and record when they activate.
4. Preserve type, cause, stack, identifiers, and structured context when errors cross a boundary.
5. Emit useful structured outcomes at request and job boundaries, including duration, attempts, and result.
6. Propagate request or trace identity through queues, services, workers, and external calls.

Read `references/review-heuristics.md` for detailed operational checks.

## Output

Order findings by severity. For each finding, name the specialist heuristic or loaded principle, identify the failure mode, cite the evidence, state the retry or recovery semantics, describe the missing diagnostic context, and propose the smallest safe fix.
