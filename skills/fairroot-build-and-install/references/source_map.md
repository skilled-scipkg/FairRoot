# fairroot source map: Build and Install

Generated from source roots:
- `cmake`
- `doxygen`
- `fairroot`
- `templates`
- `tests`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "BUILD_(EXAMPLES|TESTING|BASEMQ|DOXYGEN)|SIMPATH|FAIRROOTPATH" CMakeLists.txt templates cmake`
- `rg -n "CHECK_OUT_OF_SOURCE_BUILD|CHECK_INSTALL_DIRECTORY|WRITE_CONFIG_FILE" cmake`
- `rg -n "fairroot_add_catch2_test_suite|add_subdirectory" tests`

## Suggested source entry points
### Configure and option gating
- `CMakeLists.txt` | symbols: `Option(BUILD_DOXYGEN)`, `Option(BUILD_EXAMPLES)`, `find_package2(...)`.
- `fairroot/CMakeLists.txt` | sub-library registration order.
- `examples/CMakeLists.txt` | example family toggles under `BUILD_EXAMPLES`.
- `tests/CMakeLists.txt` | test tree activation under `BUILD_TESTING`.

### Config script generation and environment handoff
- `cmake/modules/WriteConfigFile.cmake` | symbols: `WRITE_CONFIG_FILE`, `CONVERT_LIST_TO_STRING`.
- `cmake/scripts/config.sh.in` | runtime shell exports.
- `cmake/scripts/config.csh.in` | csh shell exports.
- `cmake/scripts/fairroot-config.in` | install-side config helper script.

### Build policy and failure guards
- `cmake/modules/FairMacros.cmake` | symbols: `CHECK_OUT_OF_SOURCE_BUILD`, `CHECK_INSTALL_DIRECTORY`, `SetBasicVariables`.
- `cmake/private/FairRootSummary.cmake` | final summary of enabled components.
- `cmake/modules/FindFairRoot.cmake` | consumer-side package discovery behavior.

### Template project configure/build behavior
- `templates/project_root_containers/CMakeLists.txt` | required `FAIRROOTPATH`, linked FairRoot components.
- `templates/project_stl_containers/CMakeLists.txt` | required `FAIRROOTPATH`, linked FairRoot components.
- `templates/project_root_containers/rename.sh` | token rewrite logic for project/prefix/detector names.
- `templates/project_stl_containers/rename.sh` | token rewrite logic for STL template.

### Test registration for regression checks
- `tests/examples/simulation/Tutorial1/CMakeLists.txt` | suite `ExSimulation1` registration.
- `tests/examples/simulation/Tutorial2/CMakeLists.txt` | suite `ExSimulation2` registration.
- `tests/examples/MQ/pixelDetector/CMakeLists.txt` | suite `ExPixel` registration.
- `tests/geobase/CMakeLists.txt` | geometry check suite registration.

## Quick behavior checks
- `cmake -S . -B <build> -DBUILD_EXAMPLES=ON -DBUILD_TESTING=ON`
- `cmake --build <build> -j"$(nproc)"`
- `ctest --test-dir <build> --output-on-failure`
