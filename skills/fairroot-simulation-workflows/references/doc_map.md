# fairroot documentation map: Simulation Workflows

Generated from documentation roots:
- `examples/simulation`
- `examples/MQ`
- `examples/advanced`
- `tests/examples`

Use this map after the primary docs in `SKILL.md` to pick the right simulation/digi/reco execution path.

## Start here (ordered)
- `examples/simulation/README.md`
- `examples/simulation/Tutorial1/README.md`
- `examples/simulation/Tutorial2/README.md`
- `examples/simulation/Tutorial4/README.md`
- `examples/MQ/pixelDetector/README.md`
- `examples/MQ/pixelSimSplit/README.md`
- `examples/advanced/Tutorial3/README.md`
- `examples/advanced/Tutorial3/MQ/README.md`

## Validation-oriented docs
- `tests/examples/simulation/Tutorial1/CMakeLists.txt`
- `tests/examples/simulation/Tutorial2/CMakeLists.txt`
- `tests/examples/simulation/Tutorial4/CMakeLists.txt`
- `tests/examples/MQ/pixelDetector/CMakeLists.txt`

## Validation checkpoints
- Macro chain completes without fatal errors and writes expected output files.
- Event display macros open and attach to produced files.
- Matching simulation/MQ test suites can run from the same build configuration.
