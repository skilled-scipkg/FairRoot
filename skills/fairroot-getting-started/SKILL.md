---
name: fairroot-getting-started
description: This skill should be used when users ask about getting started in fairroot; it prioritizes documentation references and then source inspection only for unresolved details.
---

# fairroot: Getting Started

## High-Signal Playbook
### Route conditions
- Use this skill for first-run onboarding, quickest successful demo path, and orientation between MBS/LMD and simulation examples.
- Route to `fairroot-build-and-install` if environment/build setup is incomplete.
- Route to `fairroot-simulation-workflows` after initial success when users ask for deeper simulation pipelines.

### Triage questions
- Is FairRoot already built, and has `config.sh` been sourced in the current shell?
- Does the user want online/MBS-style unpacking or simulation tutorials first?
- Is web histogram monitoring needed (`ActivateHttpServer`) or only batch output?
- Should the next step be MQ LMD sampler flow or simulation macros?
- Is the user preparing a new experiment project (if yes, route to `fairroot-templates`)?

### Canonical workflow
1. Confirm build/install and shell configuration (`. ./config.sh`).
2. Run MBS tutorial unpack macro for the first concrete success path.
3. Optionally enable HTTP histogram server in online run.
4. Run MQ LMD sampler/unpacker/sink starter script for a message-based flow.
5. Move to simulation tutorials or templates once first-run baseline succeeds.

### Minimal working example
```bash
cd <fairroot-build>
. ./config.sh
root -l examples/advanced/MbsTutorial/unpack_mbs.C

cd bin
./startMQExLmd.sh
```

### Pitfalls and fixes
- Running without sourcing `config.sh` breaks environment-driven lookup for examples and libraries.
- `<build>/bin/startMQExLmd.sh` is generated from `examples/MQ/Lmd/startMQExLmd.sh.in`; run from build outputs.
- LMD flow depends on sample data location referenced by the tutorial (`examples/advanced/MbsTutorial`).
- HTTP monitoring is unavailable unless explicitly activated in steering macro (`ActivateHttpServer()`).
- If first-run fails due to dependencies, resolve build/install first before debugging runtime macros.

### Convergence/validation checks
- MBS unpack macro runs without fatal errors and processes input events.
- MQ LMD pipeline starts sampler/unpacker/sink chain and reaches running state.
- When HTTP server is enabled, monitoring endpoint is reachable at `hostname:8080`.
- Follow-up tutorials can be selected from `examples/README.md` after this baseline works.

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `README.md`
- `examples/advanced/MbsTutorial/README.md`
- `examples/MQ/Lmd/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples/advanced/MbsTutorial`
- `examples/MQ/Lmd`

## Test references
- `tests/examples`
- `fairroot/tools/tests`

## Optional deeper inspection
- `fairroot/online`
- `fairroot/mbsapi`
- `fairroot/basemq`

## Source entry points for unresolved issues
- `examples/advanced/MbsTutorial/unpack_mbs.C`
- `examples/advanced/MbsTutorial/FairMBSUnpack.cxx`
- `examples/advanced/MbsTutorial/FairMBSTask.cxx`
- `examples/MQ/Lmd/runLmdSampler.cxx`
- `examples/MQ/Lmd/runMBSMQUnpacker.cxx`
- `examples/MQ/Lmd/runMBSSink.cxx`
- `fairroot/online/source/FairLmdSource.cxx`
- `fairroot/online/source/FairMbsSource.cxx`
- `fairroot/basemq/devices/FairMQLmdSampler.h`
- `fairroot/mbsapi/fLmd.c`
- Prefer targeted source search (for example: `rg -n "Lmd|Mbs|Unpack|Sampler" fairroot examples`).
