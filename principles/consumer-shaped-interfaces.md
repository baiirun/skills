# Consumer-Shaped Interfaces

> Apply when adding or changing an interface, extracting a helper, or deciding how a dependency is supplied. Write the call site first, expose only what the consumer calls, build deep modules, and pass dependencies explicitly.

An interface exists for its caller. Define it from what the consumer calls, not from everything the provider can do, and make it **deep**: a small surface with real behavior behind it.

**Start from the call site.** Before extracting a helper or adding an interface, write the call that would use it and ask whether the new piece makes that call clearer. A `UserServiceManager` with one implementation and broad methods should stay concrete until a second implementation or a volatile dependency gives the interface a reason to exist.

**The pattern:**
- Expose only what the consumer needs.
- Split an interface instead of adding a boolean flag that switches it between unrelated behaviors.
- Keep one caller's vocabulary out of a general function. A parameter only one workflow understands ties the function to that workflow's changes; move the decision to the caller.
- If adding one provider method would force edits in unrelated consumers, the interface is too wide. Split it before adding the method.
- A layer that only forwards calls is shallow; call through it directly. Add a layer only when it owns policy, narrows a type, manages a lifecycle, or adapts a boundary.

**Dependencies:**
- Inject a dependency when variation, testing, or external I/O requires it, and call it directly otherwise.
- Pass dependencies explicitly, as small interfaces shaped by the consumer. A service locator or hidden global lookup hides what a unit depends on.

**The test:** Does every method on this interface have a caller today? Could a caller use it without learning how it works inside?
