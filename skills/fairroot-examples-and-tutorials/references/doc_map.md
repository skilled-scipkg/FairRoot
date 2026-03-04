# fairroot documentation map: Examples and Tutorials

Generated from documentation roots:
- `examples`
- `templates`
- `tests`

Use this map after the primary docs in `SKILL.md` to select the shortest valid example path.

## Start here (ordered)
- `examples/README.md` | top-level index for all tutorial families.
- `examples/simulation/README.md` | macro-based detector simulation examples.
- `examples/advanced/README.md` | advanced and time-based workflows.
- `examples/MQ/README.md` | FairMQ example catalog.
- `examples/advanced/Tutorial3/README.md` | detector simulation/digi/reco walkthrough.
- `examples/advanced/Tutorial3/MQ/README.md` | Tutorial3 MQ topology and data-format sweep.
- `examples/advanced/MbsTutorial/README.md` | online unpacking quick start.
- `examples/MQ/pixelDetector/README.md` | end-to-end pixel MQ chain and scripts.
- `examples/MQ/pixelSimSplit/README.md` | split-generator/transport MQ workflow.
- `examples/MQ/Lmd/README.md` | LMD sampler/unpacker/sink quick start.
- `examples/MQ/serialization/README.md` | serialization pipeline startup.
- `examples/simulation/Tutorial1/README.md`
- `examples/simulation/Tutorial2/README.md`
- `examples/simulation/Tutorial4/README.md`
- `templates/README.md` | when user wants to move from examples to a new project.

## Validation checkpoints
- Selected tutorial command path reaches `Macro finished successfully.` or equivalent completion message.
- Expected outputs (`*.mc.root`, `*.digi.root`, `*.reco.root`, `params.root`) are produced for the chosen workflow.
- Matching regression tests in `tests/examples/*` can be listed/executed from the build tree.
