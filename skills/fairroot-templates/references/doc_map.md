# fairroot documentation map: Templates

Generated from documentation roots:
- `README.md`
- `templates`
- `examples/simulation`

Use this map after the primary docs in `SKILL.md` when template bootstrap details are ambiguous.

## Start here (ordered)
- `README.md` | project-template install path and first-run commands.
- `templates/README.md` | template catalog and usage intent.
- `templates/project_root_containers/CMakeLists.txt` | root-container template project contract.
- `templates/project_stl_containers/CMakeLists.txt` | STL-container template project contract.
- `templates/project_root_containers/rename.sh` | rename token workflow.
- `templates/project_stl_containers/rename.sh` | rename token workflow.
- `templates/project_root_containers/macro/run_sim.C` | baseline run macro.
- `templates/project_root_containers/macro/eventDisplay.C` | baseline visualization macro.
- `templates/project_stl_containers/macro/run_sim.C` | STL baseline run macro.
- `templates/project_stl_containers/macro/eventDisplay.C` | STL baseline visualization macro.

## Useful validation references
- `tests/examples/simulation/Tutorial1/CMakeLists.txt`
- `tests/examples/simulation/Tutorial1/test_FairTutorialDet1Geo.cxx`

## Validation checkpoints
- Renamed template configures and builds out-of-source.
- Baseline simulation macro writes expected ROOT outputs.
- Event display macro starts with generated geometry and track data.
