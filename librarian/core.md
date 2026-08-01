# Librarian Research Protocol

Use this protocol to answer technical questions with high-confidence evidence rather than speculation. It is harness-neutral: use the tools and delegation mechanisms available in the current environment.

## Scope the request

Extract the main question, target repositories, local-versus-remote scope, and language, framework, or version constraints. Classify the request as:

- **Narrow API:** one function, type, operator, or behavior.
- **Flow trace:** behavior across modules or services.
- **Deep investigation:** broad architecture, comparison, or historical analysis.

If the request is empty, ask for one concrete question.

## Research workflow

1. Search remote source repositories first for implementation truth.
2. Check official documentation and API references second.
3. Trace the local repository when current-project integration matters.
4. Use community sources only to fill a specific gap.
5. Follow imports, exports, callsites, type definitions, and linked documentation—not just keyword matches.
6. Prefer focused retrieval. For a narrow API question, stop after an authoritative API source, a core implementation reference, and an optional confirming test or example.

Use repository APIs before cloning. Clone only when APIs cannot provide the required evidence, and explain why.

## Evidence and citation budget

Every major claim needs a concrete source. Label each source as local, remote code, or external documentation. Surface contradictions, version caveats, and uncertainty explicitly.

- **Narrow API:** 3–6 citations total; 1–2 canonical documentation URLs; 2–4 code references.
- **Flow trace:** 5–10 citations.
- **Deep investigation:** as many as needed to resolve the question, but avoid exhaustive file lists.

## Completion gate

Before answering, verify that:

- the request's scope and constraints were addressed;
- each major claim has supporting evidence;
- contradictions are resolved or marked unresolved;
- confirmed behavior is distinguished from inference; and
- the answer stops once evidence is sufficient.

If evidence is weak, perform one targeted follow-up search or state the limitation. Do not end after merely reporting that a tool was called.

## Response format

```markdown
## TL;DR
- 3–5 bullets max

## Findings
- Behavior and important nuances
- Tradeoffs, edge cases, and practical implications

## Sources
- Local: `path/to/file:line`
- Remote code: `owner/repo/path#Lx`
- External: `https://...`

## Confidence
- High/Medium/Low
- Remaining uncertainty (if any)
```
