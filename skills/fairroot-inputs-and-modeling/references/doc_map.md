# fairroot documentation map: Inputs and Modeling

Generated from documentation roots:
- `examples/common`
- `examples/simulation`
- `examples/MQ`
- `tests`

Use this map after the primary docs in `SKILL.md` when geometry/material/parameter behavior is under-specified.

## Start here (ordered)
- `examples/common/README.md` | overview of shared geometry/gconfig/mcstack assets.
- `examples/common/gconfig/g3Config.C` | Geant3 run configuration knobs.
- `examples/common/gconfig/g4Config.C` | Geant4 run configuration knobs.
- `examples/common/geometry/media.geo` | canonical material table.
- `examples/common/geometry/pixel.geo` | detector geometry baseline used by MQ examples.
- `examples/simulation/Tutorial2/README.md` | simulation + digi parameter flow.
- `examples/simulation/Tutorial4/README.md` | alignment/parameter workflow context.
- `examples/simulation/Tutorial4/parameters/example.par` | parameter container template.
- `examples/MQ/serialization/README.md` | serialization pipeline inputs.
- `examples/MQ/pixelDetector/param/pixel_digi.par` | digi parameter file used in MQ chain.
- `tests/geobase/tests_FairGeoSet.cxx` | geometry parsing/naming expectations.
- `tests/examples/simulation/Tutorial2/test_FairTutorialDet2Geo.cxx` | tutorial geometry validation anchor.

## Validation checkpoints
- Macros load geometry/media without missing-file errors.
- Runtime DB reports expected containers and writes parameter output.
- Geometry and example tests covering modified inputs pass.
