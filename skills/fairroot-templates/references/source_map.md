# fairroot source map: Templates

Generated from source roots:
- `templates`
- `fairroot`
- `tests`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "rename.sh|MYPROJ|NewDetector|SetStoreTraj|ProcessHits|SetMaterials" templates`
- `rg -n "FairRunSim::|FairRootFileSink::|FairRuntimeDb::" fairroot`

## Suggested source entry points
### Rename and project bootstrap logic
- `templates/project_root_containers/rename.sh`
- `templates/project_stl_containers/rename.sh`
- `templates/project_root_containers/CMakeLists.txt`
- `templates/project_stl_containers/CMakeLists.txt`

### Baseline simulation/event-display macros
- `templates/project_root_containers/macro/run_sim.C`
- `templates/project_root_containers/macro/eventDisplay.C`
- `templates/project_stl_containers/macro/run_sim.C`
- `templates/project_stl_containers/macro/eventDisplay.C`

### Detector and field customization points
- `templates/project_root_containers/NewDetector/NewDetector.cxx` | detector `ProcessHits`, geometry construction, branch registration.
- `templates/project_stl_containers/NewDetector/NewDetector.cxx`
- `templates/project_root_containers/field/MyFieldCreator.cxx` | field factory + runtime DB handoff.
- `templates/project_stl_containers/field/MyFieldCreator.cxx`
- `templates/project_root_containers/MyProjGenerators/Pythia8Generator.cxx`
- `templates/project_stl_containers/MyProjGenerators/Pythia8Generator.cxx`

### Framework-level behavior for generated projects
- `fairroot/base/steer/FairRunSim.cxx`
- `fairroot/base/sink/FairRootFileSink.cxx`
- `fairroot/parbase/FairRuntimeDb.cxx`

### Regression anchors
- `tests/examples/simulation/Tutorial1/test_FairTutorialDet1Geo.cxx`
- `tests/geobase/tests_FairGeoSet.cxx`

## Quick behavior checks
- `./rename.sh <ProjectName> <Prefix> <DetectorName>`
- `root -l -q ../macro/run_sim.C`
- `ctest --test-dir <build> -R 'ExSimulation1|GeoBase' --output-on-failure`
