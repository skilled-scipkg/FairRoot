---
name: fairroot-doxygen
description: This skill should be used when users ask about doxygen in fairroot; it prioritizes documentation references and then source inspection only for unresolved details.
---

# fairroot: Doxygen

## High-Signal Playbook
### Route conditions
- Use this skill for generating or troubleshooting local FairRoot API docs from source.
- Route to `fairroot-build-and-install` if the issue is broader configure/dependency failure.
- Route to `fairroot-simulation-workflows` if the user asks to run/validate simulations rather than docs.

### Triage questions
- Was CMake configured with `-DBUILD_DOXYGEN=ON`?
- Is Doxygen actually found during configure (`Doxygen_FOUND` path)?
- Is the user building from the configured build tree where `DoxygenDoc` target exists?
- Is the failure in Doxygen input config (`doxyfile`) or in the wrapper script (`doc_makeall.sh`)?

### Canonical workflow
1. Configure with doxygen enabled.
2. Build the dedicated documentation target.
3. Confirm HTML index output exists.
4. If generation fails, inspect `doxygen/CMakeLists.txt`, `doxyfile.in`, and top-level option gating.

### Minimal working example
```bash
cmake -S . -B build -DBUILD_DOXYGEN=ON
cmake --build build --target DoxygenDoc -j"$(nproc)"
ls build/doxygen/doc/html/index.html
```

### Pitfalls and fixes
- `BUILD_DOXYGEN=ON` without Doxygen installed yields warning-only behavior and no docs target output.
- Running from the wrong directory misses generated `doc_makeall.sh` in the build tree.
- Editing `doxyfile.in` without reconfiguring leaves stale generated settings.

### Convergence/validation checks
- Configure log reports Doxygen enabled.
- Build creates documentation output under `<build>/doxygen/doc/html`.
- `index.html` is present and opens with populated class/module pages.

## Scope
- Handle questions about doxygen generation and docs packaging for FairRoot.
- Keep responses concise and path-specific; escalate to source only when docs are insufficient.

## Primary documentation references
- `doxygen/README.md`
- `doxygen/CMakeLists.txt`
- `doxygen/doxyfile.in`
- `doxygen/doc_makeall.sh.in`
- `CMakeLists.txt`
- `cmake/private/FairRootSummary.cmake`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `CMakeLists.txt`
- `doxygen/CMakeLists.txt`
- `doxygen/doxyfile.in`
- `doxygen/doc_makeall.sh.in`
- `doxygen/fairDoxy.conf`
- `cmake/private/FairRootSummary.cmake`
- `cmake/modules/FairMacros.cmake`
- Prefer targeted source search (for example: `rg -n "BUILD_DOXYGEN|DoxygenDoc|doxyfile" CMakeLists.txt doxygen cmake`).
