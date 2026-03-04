# fairroot documentation map: Doxygen

Generated from documentation roots:
- `doxygen`
- `cmake`
- `README.md`

Use this map after the primary docs in `SKILL.md` when docs generation behavior is ambiguous.

## Start here (ordered)
- `doxygen/README.md` | public-facing doxygen build instructions.
- `CMakeLists.txt` | top-level `BUILD_DOXYGEN` gate and `add_subdirectory(doxygen)` behavior.
- `doxygen/CMakeLists.txt` | `DoxygenDoc` target creation and configured script files.
- `doxygen/doxyfile.in` | Doxygen input/output configuration template.
- `doxygen/doc_makeall.sh.in` | wrapper script called by `DoxygenDoc` target.
- `cmake/private/FairRootSummary.cmake` | configure-time status text for Doxygen enable/disable.

## Validation checkpoints
- Configure step reports Doxygen enablement state.
- `DoxygenDoc` target is present in build system output.
- HTML index exists under `<build>/doxygen/doc/html/index.html` after target build.
