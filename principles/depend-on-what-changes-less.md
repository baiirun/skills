# Depend on What Changes Less

> Apply when adding an import, choosing which side of a boundary owns a type, or auditing a dependency graph. Every dependency should point toward code that changes less often than the code depending on it.

A dependency is a promise to change when the thing you depend on changes. Only make that promise to code more stable than your own. When stable code imports volatile code, every volatile change ripples into the stable code, and the whole system churns at the rate of its least stable part.

**Rank by volatility, not by layer.** Domain types, invariants, and core decisions change least. Workflows, handlers, and UI change more. Vendor SDKs, framework adapters, and feature-specific glue change most. The names `core`, `utils`, or `shared` do not make a module stable; its change history does.

**The pattern:**
- Point dependencies toward the stable side. Logic may know the domain it decides about; adapters, frameworks, caches, and schedulers may know the logic; the logic must not know them.
- When a stable module needs something from a volatile one, invert it: define the interface where the stable code lives, shaped by what it needs, and let the volatile code implement it.
- Keep `shared` and `utils` modules free of imports from feature code. A shared module that imports a feature is a feature in disguise, and every other importer now depends on that feature.
- Watch for cycles. Two modules that import each other change together by construction; merge them or cut one direction.
- A volatile dependency that many stable modules import is the highest-leverage place to put an interface.

**Check it mechanically.** Script a dependency graph (what imports what) and rerun it as the code changes. Compare edge direction against change frequency from version control. An edge from a rarely-changed file to a frequently-changed one is a defect to fix, not a style preference.

**The test:** For each import, does the imported module change less often than the importer? If not, can the importer instead depend on an interface it owns?
