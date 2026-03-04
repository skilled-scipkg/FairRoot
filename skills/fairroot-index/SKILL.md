---
name: fairroot-index
description: This skill should be used when users ask how to use fairroot and the correct generated documentation skill must be selected before going deeper into source code.
---

# fairroot Skills Index

## Route the request
- `fairroot-build-and-install`: configure/build/install failures, dependency detection, CMake options, and test execution.
- `fairroot-simulation-workflows`: macro/device execution flow, simulation->digitization->reconstruction, output files, and event display.
- `fairroot-inputs-and-modeling`: geometry/media/gconfig/parameter-container setup and model input consumption.
- `fairroot-examples-and-tutorials`: selecting runnable examples by use case and obtaining shortest tutorial command paths.
- `fairroot-getting-started`: first-run orientation (MBS/LMD quickstart) and initial success path.
- `fairroot-templates`: bootstrapping a new project from `templates/*`, rename/build flow, and template customization.
- `fairroot-doxygen`: Doxygen generation and docs publishing questions only.

## Fast triage questions
- Is the user blocked in configure/build/install, or already running macros/devices?
- Is the issue about detector/input definitions (geometry, media, params), or runtime orchestration?
- Does the user need a minimal runnable example or tutorial choice?
- Is the user creating a new project from templates?
- Is this specifically about docs generation (`-DBUILD_DOXYGEN=ON`)?

## Documentation-first workflow
1. Route to the single best topic skill above.
2. Start with that skill's primary documentation references.
3. If needed, inspect the full inventory in that skill's `references/doc_map.md`.
4. Escalate to that skill's `references/source_map.md` only when docs are insufficient.
5. Use targeted source search after step 4: `rg -n "<symbol_or_keyword>" fairroot`.
6. Return with exact file-path citations.

## Troubleshooting routing
- Configure/link/package errors -> `fairroot-build-and-install`.
- Macro runtime failures, output mismatch, event display issues -> `fairroot-simulation-workflows`.
- Wrong geometry/material/parameter behavior -> `fairroot-inputs-and-modeling`.
- "Which example should I run?" -> `fairroot-examples-and-tutorials`.
- "How do I start from scratch?" -> `fairroot-getting-started`, then `fairroot-templates`.

## Documentation-first inputs
- `README.md`
- `doxygen/README.md`
- `examples`
- `templates`
- `tests`
- `fairroot/tools/tests`

## Source directories for deeper inspection
- `fairroot`
