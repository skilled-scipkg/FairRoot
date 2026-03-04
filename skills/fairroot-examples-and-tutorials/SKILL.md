---
name: fairroot-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in fairroot; it prioritizes documentation references and then source inspection only for unresolved details.
---

# fairroot: Examples and Tutorials

## High-Signal Playbook
### Route conditions
- Use this skill when users ask which tutorial/example to run, want a smallest runnable pattern, or need a map from use case to example family.
- Route to `fairroot-simulation-workflows` for detailed run-control debugging.
- Route to `fairroot-templates` when the user wants to bootstrap a new project after reviewing examples.

### Triage questions
- Is the goal simulation basics, MQ transport, online unpacking, or reconstruction/time-based workflows?
- Does the user need a single-host macro flow or multi-process FairMQ topology?
- Is the user asking for event-wise output, parameter-server usage, or serialized transport format comparison?
- Do they need the shortest command path or architecture-level explanation?
- Are they running from the build tree where generated helper scripts exist?

### Canonical workflow
1. Start from `examples/README.md` and choose family (`simulation`, `MQ`, `advanced`).
2. For detector simulation basics, begin with `examples/simulation/Tutorial1` and `Tutorial2`.
3. For MQ reconstruction pipelines, use `examples/MQ/pixelDetector` or `examples/advanced/Tutorial3/MQ`.
4. For online unpacking and monitoring, use `examples/advanced/MbsTutorial` and `examples/MQ/Lmd`.
5. Use generated start scripts/macros from the build tree (`*.sh` scripts generated from `*.in`).
6. Validate selected tutorial path with corresponding `tests/examples/*` suite.

### Minimal working example
```bash
cd <fairroot-build>
. ./config.sh
cd examples/advanced/Tutorial3/macro
root -l -q run_sim.C
root -l -q run_digi.C
root -l -q run_reco.C

# MQ format sweep (generated from start.sh.in)
cd ../MQ
./start.sh binary
```

### Pitfalls and fixes
- Many documented shell starters are generated at build time from `.in` files: use build outputs, not only source tree templates.
- MQ examples require BaseMQ/FairMQ-enabled builds; otherwise devices are unavailable (`CMakeLists.txt`, `examples/MQ/*`).
- DDS instructions assume DDS is installed and configured separately (`examples/MQ/pixelDetector/README.md`).
- Tutorial commands assume a configured shell (`. ./config.sh`) so macros can resolve `VMCWORKDIR` and resources.
- `examples/advanced/Tutorial3/macro/data/dummy.txt` is placeholder data, not a runnable guide.

### Convergence/validation checks
- Minimal selected tutorial should complete with `Macro finished successfully.` in logs.
- Output artifacts expected by the chosen tutorial exist (`*.mc.root`, `*.digi.root`, `*.reco.root`, parameter files).
- `ctest --test-dir <build> -R 'ExSimulation|ExTestDetector|ExPixel|ExPropagator' --output-on-failure` passes for covered paths.
- For MQ runs, sampler/processor/sink topology reaches steady running state and sink output is written.

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/README.md`
- `examples/simulation/README.md`
- `examples/MQ/README.md`
- `examples/advanced/README.md`
- `examples/advanced/Tutorial3/README.md`
- `examples/advanced/Tutorial3/MQ/README.md`
- `examples/advanced/MbsTutorial/README.md`
- `examples/MQ/Lmd/README.md`
- `templates/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`
- `templates`

## Test references
- `tests/examples`
- `fairroot/tools/tests`

## Optional deeper inspection
- `fairroot`

## Source entry points for unresolved issues
- `examples/advanced/Tutorial3/macro/run_sim.C`
- `examples/advanced/Tutorial3/macro/run_digi.C`
- `examples/advanced/Tutorial3/macro/run_reco.C`
- `examples/advanced/Tutorial3/MQ/sampler.cxx`
- `examples/advanced/Tutorial3/MQ/processor.cxx`
- `examples/advanced/Tutorial3/MQ/sink.cxx`
- `examples/MQ/pixelDetector/macros/run_sim.C`
- `examples/MQ/pixelDetector/macros/run_digi.C`
- `examples/MQ/Lmd/runLmdSampler.cxx`
- `examples/MQ/Lmd/runMBSMQUnpacker.cxx`
- `examples/MQ/Lmd/runMBSSink.cxx`
- `templates/project_root_containers/macro/run_sim.C`
- `templates/project_stl_containers/macro/run_sim.C`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" examples fairroot`).
