# fairroot documentation map: Build and Install

Generated from documentation roots:
- `README.md`
- `cmake`
- `doxygen`
- `templates`
- `tests`

Use this map after the primary docs in `SKILL.md` when configure/build behavior is still unclear.

## Start here (ordered)
- `README.md` | canonical install flow (`SIMPATH`, configure/build/install, test shell reset).
- `CMakeLists.txt` | top-level options (`BUILD_EXAMPLES`, `BUILD_TESTING`, `BUILD_BASEMQ`, `BUILD_DOXYGEN`) and install artifacts.
- `cmake/README.md` | CMake module layout and generated script flow.
- `templates/README.md` | downstream project bootstrap contract.
- `doxygen/README.md` | doxygen toggle and output location.
- `tests/CMakeLists.txt` | global test groups configured for this build.
- `tests/examples/CMakeLists.txt` | simulation/example test registration.
- `tests/geobase/CMakeLists.txt` | geometry validation test registration.
- `fairroot/tools/tests/CMakeLists.txt` | utility library test coverage.

## Template build docs
- `templates/project_root_containers/CMakeLists.txt`
- `templates/project_stl_containers/CMakeLists.txt`
- `templates/project_root_containers/rename.sh`
- `templates/project_stl_containers/rename.sh`

## Validation checkpoints
- Configure succeeds with expected options in the CMake summary.
- `ctest -N --test-dir <build>` lists expected suites (`ExSimulation*`, `ExPixel`, `GeoBase`).
- Generated environment scripts exist in the build tree after configure.
