# Total Transformations

> Apply when writing code that converts, migrates, or updates data. Every input gets a defined output or a structured error, failures leave nothing half-changed, and errors can say what failed and where.

A transformation is correct only if it is correct for every input it can receive, including the invalid ones, the edge values, and the ones that fail halfway.

**The pattern:**
- Write total transformations: every input state yields a defined output or a structured error.
- Give invalid input, edge values, and state transitions a defined outcome, not an accident.
- Build the new value, then swap, so a failure partway through leaves the old data valid.
- Carry identifiers and source context through transformation chains so errors can say what failed and where.

**The test:** Pick the strangest valid input and one invalid input. Does each have a defined result? If the process dies at the midpoint, is the stored data still valid?
