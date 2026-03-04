---
name: fairroot-templates
description: This skill should be used when users ask about templates in fairroot; it prioritizes documentation references and then source inspection only for unresolved details.
---

# fairroot: Templates

## High-Signal Playbook
### Route conditions
- Use this skill for project bootstrapping from `templates/*`, rename/customization flow, and first simulation run in a copied template.
- Route to `fairroot-build-and-install` for dependency/configure failures.
- Route to `fairroot-simulation-workflows` once template project compiles and runtime flow questions dominate.

### Triage questions
- Root-container or STL-container template (`project_root_containers` vs `project_stl_containers`)?
- Are `FAIRROOTPATH` and `SIMPATH` exported before configuring template project?
- What project name/prefix/detector name should `<project>/rename.sh` apply?
- Are you configuring out-of-source and using the generated `config.sh` in the template build?
- Do you need only simulation scaffold (`<project>/macro/run_sim.C`) or also event display setup?

### Canonical workflow
1. Copy the selected template directory into a new project folder (`README.md`, `templates/README.md`).
2. Run `<project>/rename.sh <ProjectName> <Prefix> <DetectorName>` to rewrite names/paths.
3. Create a build directory and configure with CMake (requires `FAIRROOTPATH`; optionally `SIMPATH`).
4. Build, then source generated `config.sh` in template build tree.
5. Run `<project>/macro/run_sim.C` to produce baseline output; run `<project>/macro/eventDisplay.C` for visualization.
6. Iterate detector/generator/field defaults in template source and rerun.

### Minimal working example
```bash
export SIMPATH=~/fair_install/FairSoft/install
export FAIRROOTPATH=~/fair_install/FairRoot/install
cp -rf templates/project_root_containers MyTest
cd MyTest
./rename.sh MyExperiment MyExp det
mkdir build && cd build
cmake ../MyExperiment
cmake --build . -j"$(nproc)"
. ./config.sh
root -l -q ../macro/run_sim.C
root -l ../macro/eventDisplay.C
```

### Pitfalls and fixes
- `<project>/rename.sh` exits unless exactly 3 arguments are provided; keep `<project> <prefix> <detector>` order.
- `<project>/rename.sh` supports Linux/Darwin path editing only; other platforms error out.
- Template CMake hard-fails when `FAIRROOTPATH` is unset (`templates/project_*/CMakeLists.txt`).
- Out-of-source build is required by template checks; do not configure in project source directory.
- Template `<project>/macro/run_sim.C` enables trajectory storage (`SetStoreTraj(kTRUE)`), which can bloat files; disable for production runs.

### Convergence/validation checks
- Renamed project compiles and generates `build/config.sh`.
- First run creates `test.root`, `params.root`, and `geofile_full.root` from template macro defaults.
- Event display macro initializes and can render MC tracks from produced files.
- Generated class/file names reflect chosen prefix/detector across CMake and sources.

## Template adaptation checklist
- Confirm `<project>/rename.sh` updated both file names and in-file symbols for project/prefix/detector.
- Verify `<project>/macro/run_sim.C` still wires the intended detector modules and field configuration.
- Verify parameter container output is written via `FairParRootFileIo`.
- If customizing detector physics, update `NewDetector::ProcessHits` and rerun baseline outputs.

## Scope
- Handle questions about documentation grouped under the 'templates' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `README.md`
- `templates/README.md`
- `templates/project_root_containers/CMakeLists.txt`
- `templates/project_stl_containers/CMakeLists.txt`
- `templates/project_root_containers/rename.sh`
- `templates/project_stl_containers/rename.sh`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `templates`
- `examples`

## Test references
- `tests`
- `fairroot/tools/tests`

## Optional deeper inspection
- `fairroot`

## Source entry points for unresolved issues
- `templates/project_root_containers/CMakeLists.txt`
- `templates/project_stl_containers/CMakeLists.txt`
- `templates/project_root_containers/rename.sh`
- `templates/project_stl_containers/rename.sh`
- `templates/project_root_containers/macro/run_sim.C`
- `templates/project_root_containers/macro/eventDisplay.C`
- `templates/project_stl_containers/macro/run_sim.C`
- `templates/project_stl_containers/macro/eventDisplay.C`
- `templates/project_root_containers/NewDetector/CMakeLists.txt`
- `templates/project_stl_containers/NewDetector/CMakeLists.txt`
- Prefer targeted source search (for example: `rg -n "rename|MYPROJ|NewDetector|run_sim" templates`).
