---
name: fairroot-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in fairroot; it prioritizes documentation references and then source inspection only for unresolved details.
---

# fairroot: Inputs and Modeling

## High-Signal Playbook
### Route conditions
- Use this skill for geometry/material definitions, gconfig steering, parameter-container files, and serialization/input model choices.
- Route to `fairroot-simulation-workflows` when the question is primarily about run orchestration instead of model definition.
- Route to `fairroot-build-and-install` if model issues are actually missing dependency/build artifacts.

### Triage questions
- Which geometry source is used: ASCII (`*.geo`) or ROOT geometry (`tutorial4.root`)?
- Which transport config is active (`g3Config.C`, `g4Config.C`, or post-init variants)?
- Which parameter files are authoritative (`*.params.root`, `*.par` ASCII, or both)?
- Which detector/task consumes the parameters (digitizer, reco task, misalignment handler)?
- Are defaults accepted, or are threshold/noise/material/cut values being tuned?
- Is validation needed at geometry-shape level or end-to-end event output level?

### Canonical workflow
1. Identify input artifacts in docs: geometry/media under `examples/common/geometry`, config macros under `examples/common/gconfig`, parameter files in tutorial directories.
2. Ensure macros set `GEOMPATH` and `CONFIG_DIR` from `VMCWORKDIR` before run.
3. Confirm detector geometry hooks (`SetGeometryFileName`) and material file (`SetMaterials("media.geo")`).
4. Wire parameter IO through runtime DB (`FairParRootFileIo` + `FairParAsciiFileIo`) in the run macro.
5. Run the minimal macro chain and inspect produced `.root` + parameter outputs.
6. Validate geometry naming/shape conventions with `tests/geobase` and relevant example test suites.

### Minimal working example
```bash
cd <fairroot-build>
. ./config.sh
cd examples/simulation/Tutorial2/macros
root -l -q 'run_tutorial2.C(10, "TGeant4", true)'
root -l -q create_digis.C

# Optional parameter tuning entrypoint:
# examples/MQ/pixelDetector/param/pixel_digi.par
```

### Pitfalls and fixes
- Missing `GEOMPATH` or `CONFIG_DIR` breaks geometry/config lookup: run from configured shell and keep macro env setup intact.
- Parameter values may be silently wrong when ASCII parameter input is not connected as second runtime DB input (`examples/simulation/Tutorial2/macros/create_digis.C`, `examples/MQ/pixelDetector/macros/run_digi.C`).
- Material/geometry file-name mismatches (`media.geo`, `pixel.geo`, `tutorial4.root`) cause runtime setup failures.
- Misalignment parameter files require strict container layout and vector lengths (`examples/simulation/Tutorial4/parameters/example.par`).
- Changing modeling constants without updating validation can mask regressions; re-run geometry-focused tests.

### Convergence/validation checks
- Runtime DB prints expected containers and saves output parameter file.
- Output files exist and can be opened with expected trees/branches.
- `ctest --test-dir <build> -R 'GeoBase|ExSimulation|ExPixel' --output-on-failure` passes.
- Geometry naming checks (`checkGeoSetNamingConventions`) pass in relevant example tests.

## Scope
- Handle questions about inputs, system setup, models, and physical parameterization.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/common/README.md`
- `examples/MQ/serialization/README.md`
- `examples/common/gconfig/g3Config.C`
- `examples/common/gconfig/g4Config.C`
- `examples/common/geometry/media.geo`
- `examples/MQ/pixelDetector/param/pixel_digi.par`
- `examples/simulation/Tutorial4/parameters/example.par`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples/common`
- `examples/simulation/Tutorial2`
- `examples/simulation/Tutorial4`
- `examples/MQ/serialization`
- `examples/MQ/pixelDetector`

## Test references
- `tests/geobase`
- `tests/examples/simulation`
- `tests/examples/MQ/pixelDetector`

## Optional deeper inspection
- `fairroot/geobase`
- `fairroot/parbase`
- `fairroot/base/field`

## Source entry points for unresolved issues
- `examples/common/gconfig/g3Config.C`
- `examples/common/gconfig/g4Config.C`
- `examples/common/geometry/media.geo`
- `examples/MQ/pixelDetector/param/pixel_digi.par`
- `examples/simulation/Tutorial4/parameters/example.par`
- `examples/simulation/Tutorial2/macros/create_digis.C`
- `examples/MQ/pixelDetector/macros/run_digi.C`
- `fairroot/geobase/FairGeoLoader.cxx`
- `fairroot/geobase/FairGeoInterface.cxx`
- `fairroot/parbase/FairRuntimeDb.cxx`
- `fairroot/parbase/FairParAsciiFileIo.cxx`
- `fairroot/parbase/FairParRootFileIo.cxx`
- `fairroot/base/field/FairFieldFactory.cxx`
- `fairroot/base/field/FairField.cxx`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" fairroot examples/common`).
