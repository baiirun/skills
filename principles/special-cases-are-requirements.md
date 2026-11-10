# Special Cases Are Requirements

> Apply when you find or are about to write an `if` for one value, a parameter for one caller, a swallowed exception, a retry or sleep, or a disabled test. Each is a requirement the design never accounted for. Collect them and redesign for the requirement instead of patching the case.

A special case is code that exists for one situation instead of following from how the system works. It is not a defect in the code; it is evidence of a requirement the design does not model. Treat each one as a message about what the system needs to be.

**Recognize them:**
- An `if` for one value, caller, tenant, or environment.
- A parameter or flag only one caller passes.
- A swallowed exception, or a catch that returns a default.
- A retry, sleep, or wait that hopes something else has finished.
- A disabled, skipped, or always-passing test.
- A global or flag one module sets so another module behaves differently.

**Collect before fixing.** Do not fix special cases one at a time. List every one you can find in the area, with its location, then ask what requirement each is standing in for. A sleep before focusing an input and a global `skipRefocus` flag are the same requirement: dialogs must return focus to where it was. A switch per action in the keymap, a second list in the command palette, and a per-action undo case are one requirement: actions are data, and every surface runs from the same list.

**Look for the one fix behind several problems.** The right redesign usually resolves a cluster of special cases at once, and it often looks nothing like any of them. Work out what the system would look like if it had known this requirement from the start (see [redesign-from-first-principles](redesign-from-first-principles.md)), then remove the cases the redesign makes unnecessary. Keep only the special cases the system still genuinely needs, and make each one say why.

**Measure progress by what is left.** The number of special cases remaining is the best indicator of how well the design matches its requirements. A new feature that adds one more branch to an existing chain, or a second boolean that must stay in sync with the first, means a requirement was patched in rather than modeled (see [model-the-domain](model-the-domain.md)).

**The test:** Can you name the requirement this special case stands in for? Would a design built around that requirement still need the case?
