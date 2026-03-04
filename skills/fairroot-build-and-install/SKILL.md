---
name: fairroot-build-and-install
description: This skill should be used when users ask about build and install in fairroot; it prioritizes documentation references and then source inspection only for unresolved details.
---

# fairroot: Build and Install

## High-Signal Playbook
### Route conditions
- Use this skill for CMake configure/build/install flow, dependency/env setup, and test-target execution.
- Route to `fairroot-templates` for downstream project scaffolding from template directories.
- Route to `fairroot-simulation-workflows` once build/install succeeds and the request shifts to running macros.

### Triage questions
- Are you building FairRoot itself or a copied template project?
- What OS, compiler, and CMake generator are you using?
- Are `SIMPATH` (FairSoft) and, for template projects, `FAIRROOTPATH` exported?
- Do you need `BUILD_EXAMPLES`, `BUILD_TESTING`, `BUILD_BASEMQ`, or `BUILD_DOXYGEN` enabled?
- Is failure at configure time (missing package) or link/runtime test stage?
- Are you building out-of-source (`-S/-B`) and using a clean build directory?

### Canonical workflow
1. Set dependency environment (`SIMPATH`) before configure (`README.md`, `CMakeLists.txt`).
2. Configure out-of-source with explicit install prefix (`README.md`).
3. Build and install with CMake build/install steps (`README.md`).
4. Source generated config script from build tree (`CMakeLists.txt`, `README.md`).
5. Run tests from build tree; for full regression, use a fresh shell without `SIMPATH` as documented (`README.md`).
6. If docs are requested, reconfigure with `-DBUILD_DOXYGEN=ON` (`doxygen/README.md`, `CMakeLists.txt`).

### Minimal working example
```bash
export SIMPATH=~/fair_install/FairSoft/install
cmake -S . -B build \
  -DCMAKE_INSTALL_PREFIX=~/fair_install/FairRoot/install \
  -DBUILD_EXAMPLES=ON -DBUILD_TESTING=ON
cmake --build build -j"$(nproc)"
cmake --install build
. ./build/config.sh
( unset SIMPATH; ctest --test-dir build --output-on-failure )
```

### Pitfalls and fixes
- In-source builds fail policy checks: always use `cmake -S . -B build` (`CMakeLists.txt`, out-of-source checks).
- Template projects fail configure when `FAIRROOTPATH` is unset: export it before `cmake` (`templates/project_root_containers/CMakeLists.txt`).
- `BUILD_BASEMQ=ON` without FairMQ dependency causes configure failure: either install FairMQ or disable BaseMQ (`CMakeLists.txt`).
- Tests can fail from mixed env libraries: run test phase in a fresh shell as documented (`README.md`).
- Doxygen not generated unless explicitly enabled: pass `-DBUILD_DOXYGEN=ON` (`doxygen/README.md`, `CMakeLists.txt`).

### Convergence/validation checks
- `ctest -N --test-dir build` lists expected suites (Base, GeoBase, ExSimulation*, ExRutherford, ExPixel when built).
- `ctest --output-on-failure --test-dir build` passes target suites you enabled.
- Build tree has `config.sh`; install tree has `bin/FairRootConfig.sh` and `bin/fairroot-config` (`CMakeLists.txt`).
- If examples are enabled, `examples/*` targets are present and runnable (`CMakeLists.txt`, `examples/CMakeLists.txt`).

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `README.md`
- `CMakeLists.txt`
- `tests/CMakeLists.txt`
- `tests/examples/CMakeLists.txt`
- `doxygen/README.md`
- `templates/project_root_containers/CMakeLists.txt`
- `templates/project_stl_containers/CMakeLists.txt`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior/regression references for build verification.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`
- `templates`

## Test references
- `tests`
- `fairroot/tools/tests`

## Optional deeper inspection
- `fairroot`
- `cmake/modules`
- `cmake/private`

## Source entry points for unresolved issues
- `CMakeLists.txt`
- `tests/CMakeLists.txt`
- `tests/examples/CMakeLists.txt`
- `tests/examples/simulation/Tutorial1/CMakeLists.txt`
- `tests/examples/simulation/Tutorial2/CMakeLists.txt`
- `tests/examples/simulation/Tutorial4/CMakeLists.txt`
- `fairroot/CMakeLists.txt`
- `fairroot/base/CMakeLists.txt`
- `fairroot/geobase/CMakeLists.txt`
- `fairroot/tools/CMakeLists.txt`
- `cmake/modules/WriteConfigFile.cmake`
- `cmake/modules/FairMacros.cmake`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" fairroot cmake`).
