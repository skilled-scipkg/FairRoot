---
name: fairroot-simulation-workflows
description: This skill should be used when users ask about simulation workflows in fairroot; it prioritizes documentation references and then source inspection only for unresolved details.
---

# fairroot: Simulation Workflows

## High-Signal Playbook
### Route conditions
- Use this skill for end-to-end execution flow: simulation, digitization, reconstruction, MQ device chains, outputs, and event display.
- Route to `fairroot-inputs-and-modeling` when the blocker is geometry/material/parameter definitions.
- Route to `fairroot-build-and-install` when binaries/macros fail due to missing build/dependency setup.

### Triage questions
- Which workflow family: `examples/simulation`, `examples/MQ`, or `examples/advanced/Tutorial3`?
- Which transport engine (`TGeant3` or `TGeant4`) and is MT mode enabled?
- Are you running from a configured build shell (`. ./config.sh`) so `VMCWORKDIR` is valid?
- Do you need event-wise flow or split/streamed FairMQ flow?
- Which output artifact is failing: `.mc.root`, `.digi.root`, `.reco.root`, or parameter file?
- Do you need event display or only batch validation?

### Canonical workflow
1. Source build environment and enter the tutorial macro directory (`README.md`, tutorial READMEs).
2. Run simulation macro first (`examples/simulation/Tutorial1/macros/run_tutorial1.C`, `examples/simulation/Tutorial2/macros/run_tutorial2.C`, `examples/simulation/Tutorial4/macros/run_tutorial4.C`, or `examples/MQ/pixelDetector/macros/run_sim.C`).
3. Run digitization/reco macros when needed (`examples/simulation/Tutorial2/macros/create_digis.C`, `examples/MQ/pixelDetector/macros/run_digi.C`, `examples/simulation/Tutorial4/macros/run_reco.C`).
4. For MQ split transport, run generator/transporter with documented topology options (`examples/MQ/pixelSimSplit/README.md`).
5. Inspect output ROOT files and parameter files printed by macros.
6. Open event display macros when visual checks are needed (`examples/simulation/Tutorial1/macros/eventDisplay.C` and related tutorial macro directories).
7. Confirm behavior with tests in `tests/examples/simulation/*` and `tests/examples/MQ/pixelDetector`.

### Minimal working example
```bash
cd <fairroot-build>
. ./config.sh
cd examples/simulation/Tutorial1/macros
root -l -q 'run_tutorial1.C(10, "TGeant3")'
root -l eventDisplay.C

cd ../../Tutorial2/macros
root -l -q 'run_tutorial2.C(10, "TGeant4", true)'
root -l -q create_digis.C
```

### Pitfalls and fixes
- Missing `VMCWORKDIR` causes geometry/config lookup failures: source `config.sh` first (`CMakeLists.txt`, tutorial macros).
- MQ examples that rely on generated scripts must be run from build outputs, not only source tree `.in` templates (`start.sh.in`, `startMQExLmd.sh.in`).
- `pixelDetector` MQ topologies require pre-generated sim+digi files per README preparations (`examples/MQ/pixelDetector/README.md`).
- DDS mode requires external DDS installation and FairRoot configured with DDS path (`examples/MQ/pixelDetector/README.md`).
- Tutorial1 MT mode writes split outputs (`_t1.root`, `_t2.root`), so downstream checks must read both (`examples/simulation/Tutorial1/macros/run_tutorial1.C`).

### Convergence/validation checks
- Tutorial macros should print `Macro finished successfully.` and expected output/parameter file names.
- `examples/simulation/Tutorial1/macros/run_tutorial1.C` internal checks pass: events/tracks/points and expected branch/leaf counts.
- `examples/MQ/pixelDetector/macros/run_sim.C` checks point statistics (`NumberOfPoints`) and minimum event count.
- `ctest --test-dir <build> -R 'ExSimulation|ExRutherford|ExPixel' --output-on-failure` passes.

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/simulation/README.md`
- `examples/simulation/Tutorial1/README.md`
- `examples/simulation/Tutorial2/README.md`
- `examples/simulation/Tutorial4/README.md`
- `examples/MQ/pixelDetector/README.md`
- `examples/MQ/pixelSimSplit/README.md`
- `tests/examples/simulation/Tutorial1/CMakeLists.txt`
- `tests/examples/simulation/Tutorial2/CMakeLists.txt`
- `tests/examples/simulation/Tutorial4/CMakeLists.txt`
- `tests/examples/simulation/rutherford/CMakeLists.txt`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorial macros/examples as executable patterns.
- Use tests as minimal validation references.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples/simulation`
- `examples/MQ`
- `examples/advanced/Tutorial3`

## Test references
- `tests/examples/simulation`
- `tests/examples/MQ/pixelDetector`
- `fairroot/tools/tests`

## Optional deeper inspection
- `fairroot/base`
- `fairroot/parbase`
- `fairroot/generators`
- `fairroot/eventdisplay`

## Source entry points for unresolved issues
- `examples/simulation/Tutorial1/macros/run_tutorial1.C`
- `examples/simulation/Tutorial2/macros/run_tutorial2.C`
- `examples/simulation/Tutorial2/macros/create_digis.C`
- `examples/simulation/Tutorial4/macros/run_tutorial4.C`
- `examples/simulation/Tutorial4/macros/run_reco.C`
- `examples/MQ/pixelDetector/macros/run_sim.C`
- `examples/MQ/pixelDetector/macros/run_digi.C`
- `examples/MQ/pixelDetector/macros/run_reco.C`
- `fairroot/base/steer/FairRunSim.cxx`
- `fairroot/base/steer/FairRunAna.cxx`
- `fairroot/base/sink/FairRootFileSink.cxx`
- `fairroot/parbase/FairRuntimeDb.cxx`
- `fairroot/generators/FairBoxGenerator.cxx`
- `fairroot/eventdisplay/FairEventManager.cxx`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" fairroot examples`).
