# Group by Reason to Change

> Apply when deciding what goes in one module, file, or folder, when a change touches several places, or when auditing a codebase's structure. Pieces that change together belong together; pieces that change for different reasons must not be tied; pieces with no reason of their own to change go.

Ask one question of every two pieces of code: **should these change together?** The code gets it wrong in exactly three ways.

**Hidden links:** pieces that must change together, where nothing shows it.
- Copies of logic or values. Change one and the rest must follow, but nothing says so.
- A module that reads a global, file, or environment set by another module. The coupling runs through state, so no import reveals it.
- One feature split across folders by layer (`controllers/`, `services/`, `models/`), or related code scattered across unrelated folders. One change needs all of them, and the layout hides it. Colocate by domain, not by layer.
- A call order or convention callers just have to know. Change it and callers break without warning. Make the dependency explicit in the signature or type.

**Needless links:** pieces tied together that change for different reasons.
- Callers that depend on internals. The internals change for their own reasons and the callers break anyway.
- A general function with a parameter only one workflow understands. The function now changes whenever that workflow does (see [consumer-shaped-interfaces](consumer-shaped-interfaces.md)).
- Stable code importing something more volatile (see [depend-on-what-changes-less](depend-on-what-changes-less.md)).

**Surplus:** pieces with no reason of their own to change.
- Pass-through wrappers that only change when the thing they wrap does.
- Extension points, flags, and config for things that never vary.
- Dead code. Nothing uses it, so nothing will ever need it to change.
- Comments and tests that restate the implementation. They change only when it does, so they check nothing and explain nothing (see [comment-the-why](comment-the-why.md), [test-behavior](test-behavior.md)).

**Use history as evidence.** Version control records what actually changes together. Files that always appear in the same commits but live apart are a hidden link; files that live together but never change together are candidates to separate. A commit that touches many folders for one small behavior change is the layout telling you it is wrong.

**The test:** For a typical change in this area, how many places does it land in? One is the goal. For each import, can you say why this piece should care when that one changes?
